---
description: 'Lifecycle: In Production'
---

# Data format 6

Related Ruuvi Devices: Ruuvi Air, Ruuvi Gateway

This data format uses Bluetooth 4 advertisement extension to be compatible with Bluetooth 4 devices. Any Bluetooth 5.0 and upwards capable device should discard this data format and listen to data format E1 packets instead.

The data is decoded from "Manufacturer Specific Data" -field, for more details please check [Bluetooth Advertisements section](https://docs.ruuvi.com/communication/bluetooth-advertisements). Manufacturer ID is **`0x0499`** , which is transmitted as **`0x9904`** in raw data. The actual data payload is:

| Offset        |   Allowed values   | Description                                                                                                                  |
| ------------- | :----------------: | ---------------------------------------------------------------------------------------------------------------------------- |
| 0             |         `6`        | Data format (8bit)                                                                                                           |
| 1-2           | `-32767 ... 32767` | Temperature in 0.005 degrees                                                                                                 |
| 3-4           |   `0 ... 40 000`   | Humidity (16bit unsigned) in 0.0025% (0-163.83% range, though realistically 0-100%)                                          |
| 5-6           |    `0 ... 65534`   | Pressure (16bit unsigned) in 1 Pa units, with offset of -50 000 Pa                                                           |
| 7-8           |    `0 ... 10000`   | PM 2.5, ug/m^3. Resolution 0.1/bit, range 0 ... 1000. 16bit unsigned                                                         |
| 9-10          |    `0 ... 40000`   | CO2 concentration, ppm. Resolution 1/bit, range 0 ... 40000. 16bit unsigned                                                  |
| 11 +FLAGS b6  |     `0 ... 500`    | VOC index, unitless. Resolution 1 / bit, range 0 ... 500. 9 bit unsigned, least significant bit in Flags byte                |
| 12, +FLAGS b7 |     `0 ... 500`    | NOX index, unitless. Resolution 1 / bit, range 0 ... 500. 9 bit unsigned, least significant bit in Flags byte                |
| 13            |     `0 ... 254`    | Luminosity, Lux. Logarithmic, range 0 ... 65535. See below for details                                                       |
| 14            |        `255`       | Reserved                                                                                                                     |
| 15            |      `0...255`     | Measurement sequence. A device sending also in E1 data format will have identical least significant byte for the same sample |
| 16            |    `0bVVXX XXXV`   | Flags. See below for details                                                                                                 |
| 17-19         |   `Any valid mac`  | Lowest 3 bytes of device MAC address                                                                                         |

_Not available_ is signified by largest presentable number for unsigned values, smallest presentable number for signed values and all bits set for mac. All fields are MSB first 2-complement, i.e. `0xFC18` is read as `-1000` and `0x03E8` is read as `1000`. If original data overflows the data format, data is clipped to closest value that can be represented. For example temperature 170.00 C becomes 163.835 C

### Data field descriptions

#### Temperature

Values supported: -163.835 °C to +163.835 °C in 0.005 °C increments.

_Example_

| Value    | Measurement             |
| -------- | ----------------------- |
| `0x0000` | 0 °C                    |
| `0x01C3` | +2.255 °C               |
| `0xFE3D` | -2.255 °C               |
| `0x8000` | Invalid / not available |

#### **Humidity**

Values supported: 0.0 % to 100 % in 0.0025 % increments. Higher values than 100 % are possible, but they generally indicate a faulty or miscalibrated sensor.

_Example_

| Value   | Measurement             |
| ------- | ----------------------- |
| `0`     | 0%                      |
| `10010` | 25.025%                 |
| `40000` | 100.0%                  |
| `65535` | Invalid / not available |

#### **Atmospheric Pressure**

Values supported: 50000 Pa to 115534 Pa in 1 Pa increments.

_Example_

| Value   | Measurement                            |
| ------- | -------------------------------------- |
| `00000` | 50000 Pa                               |
| `51325` | 101325 Pa (average sea-level pressure) |
| `65534` | 115534 Pa                              |
| `65535` | Invalid / not available                |

#### **PM 2.5**

Values supported: 0 to 6553.4 (ug/m^3), however the sensor on Ruuvi supports only 1000 ug/m^3. Value is uint16\_t, MSB first. Resolution is 0.1 per bit

_Example_

| Value    | Measurement             |
| -------- | ----------------------- |
| `0x0000` | 0 ug/m^3                |
| `0x03E8` | 100.0 ug/m^3            |
| `0xFFFF` | Invalid / not available |

#### CO2

Values supported: 0 to 65534 (ppm), however the sensor on Ruuvi supports only 40000 ppm and in natural environment CO2 is always at least around 400 ppm. Resolution is 1 per bit. Values are uint16\_t, MSB first.

| Value    | Measurement             |
| -------- | ----------------------- |
| `0x0000` | 0 ppm                   |
| `0x03E8` | 1000 ppm                |
| `0xFFFF` | Invalid / not available |

#### VOC, NOX

Volatile Organic Compounds and Nitrogen Oxides are unitless indexes which learn the installation environment and track changes over time. For VOC the index average is 100, i.e. values under 100 mean the air quality is improving and values over 100 mean the air quality is getting worse.

Nox index has base value of 1, values higher than 1 meaning there's more nitrogen oxides in the air than usual.

Both values use 9 bits, least significant bit is in Flags byte.

| Value   | Measurement             |
| ------- | ----------------------- |
| `0x000` | 0                       |
| `0x0E8` | 232                     |
| `0x1FF` | Invalid / not available |

#### **Luminosity**

Luminosity represents the light level in the environment of the sensor. The light level is compensated with human eye sensitivity curve. Value is 8-bit unsigned logarithmic number. Values should be rounded at most to 0.01 precision.

Please note that the highest valid code is 254, and 255 is reserved for the "not available".

Decoding and encoding:

```
MAX_VALUE := 65535
MAX_CODE  := 254
DELTA     := ln(MAX_VALUE + 1) / MAX_CODE
CODE      := round(ln(value + 1) / DELTA)
VALUE     := exp(CODE * delta) -1
```

_Example_

| Value  | Measurement             |
| ------ | ----------------------- |
| `0x00` | 0 lux                   |
| `0x01` | `0.04` lux              |
| `0x10` | `1.01` lux              |
| `0x80` | `244.06` lux            |
| `0xFE` | `65535.00` lux          |
| `0xFF` | Invalid / not available |

#### **Measurement sequence number**

Measurement sequence number gets incremented by one for every measurement. It can be used to gauge signal quality and packet loss as well as to deduplicated data entries. You should note that the measurement sequence refers to data rather than transmission, so you might receive many transmissions with the same measurement sequence number.

Please note that the highest valid value is 255, there is no "invalid / not available" value as this counter tracks the E1 format counter.

_Example_

| Value  | Measurement |
| ------ | ----------- |
| `0x00` | 0 counts    |
| `0x10` | 10 counts   |
| `0xFF` | 255 counts  |

#### **Flags**

Flags byte contains additional information and is interpreted bit-by-bit. "X" Means "don't care, 1 or 0". "V" Means the value of bit. Bits 1...5 are reserved. Bit 0 is least significant, bit 7 is most significant.

| Value         | Significance                                                                                |
| ------------- | ------------------------------------------------------------------------------------------- |
| `0bXXXX XXXV` | 1 -> Calibration in progress, sensor data not fully accurate yet. 0 -> Calibration complete |
| `0bXVXX XXXX` | VOC bit 9, 1-> set, 0 -> not set                                                            |
| `0bVXXX XXXX` | NOX bit 9, 1-> set, 0 -> not set                                                            |

#### **MAC address**

MAC address is static, statistically unique random identifier of the device. The address is 48 bits, but this data format carries only 24 least significant bits.

Please note that the Bluetooth advertisement itself carries the full MAC address of the sensor, and most host devices can and should parse the MAC address directly from the Bluetooth metadata. However, iOS devices do not reveal the full MAC address to the application, but instead convert the MAC address to an UUID which is not guaranteed to stay static. Hence iOS devices should use these 24 bits as a static identifier of the device.

### Test vectors

These test vectors are based on [ruuvi.endpoints.c](https://github.com/ruuvi/ruuvi.endpoints.c) project. The tests are bidirectional, decode-encode results in original raw data. Encode-decode must result in same values with given precision, but floating point rounding differences may occur.

#### Case: valid data

Raw binary data: `0x06170C5668C79E007000C90501D9XXCD004C884F` XX : Reserved

| Field                | Value                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Data format          | `06`                                                                                                                 |
| Temperature          | `29.500` C                                                                                                           |
| Pressure             | `101102` Pa                                                                                                          |
| Humidity             | `55.300` RH-%                                                                                                        |
| PM 2.5               | `11.2` ug/m^3                                                                                                        |
| CO2                  | `201` ppm                                                                                                            |
| VOC                  | `10`                                                                                                                 |
| NOX                  | 2                                                                                                                    |
| Luminosity           | `13 026.67` Lux                                                                                                      |
| Measurement Sequence | `205`                                                                                                                |
| Flags                | <p>Calibration in progress: <code>False</code></p><p>VOC b9: <code>False</code></p><p>NOX b9: <code>False</code></p> |
| MAC                  | `4C 88 4F`                                                                                                           |

#### Case: maximum values

Raw binary data: `0x067FFF9C40FFFE27109C40FAFAFEXXFF074C8F4F` XX : Reserved

| Field                | Value                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Data format          | `06`                                                                                                                |
| Temperature          | `163.835` C                                                                                                         |
| Pressure             | `115534` Pa                                                                                                         |
| Humidity             | `100.000` RH-%                                                                                                      |
| PM 2.5               | `1000.0` ug/m^3                                                                                                     |
| CO2                  | `40000` ppm                                                                                                         |
| VOC                  | `500`                                                                                                               |
| NOX                  | `500`                                                                                                               |
| Luminosity           | `65535.00` Lux                                                                                                      |
| Measurement Sequence | `255`                                                                                                               |
| Flags                | <p>Calibration in progress: <code>True</code></p><p>VOC b9: <code>False</code></p><p>NOX b9: <code>False</code></p> |
| MAC                  | `4C 88 4F`                                                                                                          |

Case: minimum values

Raw binary data: `0x0680010000000000000000000000XX00004C884F` XX : Reserved

| Field                | Value                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Data format          | `06`                                                                                                                 |
| Temperature          | `-163.835` C                                                                                                         |
| Pressure             | `50000` Pa                                                                                                           |
| Humidity             | `000.000` RH-%                                                                                                       |
| PM 2.5               | `0000.0` ug/m^3                                                                                                      |
| CO2                  | `00000` ppm                                                                                                          |
| VOC                  | `000`                                                                                                                |
| NOX                  | `000`                                                                                                                |
| Luminosity           | `00000.00` Lux                                                                                                       |
| Measurement Sequence | `000`                                                                                                                |
| Flags                | <p>Calibration in progress: <code>false</code></p><p>VOC b9: <code>false</code></p><p>NOX b9: <code>false</code></p> |
| MAC                  | `4C 88 4F`                                                                                                           |

#### Case: Invalid values

Raw binary data: `0x068000FFFFFFFFFFFFFFFFFFFFFFXXFFFFFFFFFF` XX : Reserved

| Field                | Value                                                                                                             |
| -------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Data format          | `06`                                                                                                              |
| Temperature          | `NaN` C                                                                                                           |
| Pressure             | `NaN` Pa                                                                                                          |
| Humidity             | `NaN` RH-%                                                                                                        |
| PM 2.5               | `NaN` ug/m^3                                                                                                      |
| CO2                  | `NaN` ppm                                                                                                         |
| VOC                  | `NaN`                                                                                                             |
| NOX                  | `NaN`                                                                                                             |
| Luminosity           | `NaN` Lux                                                                                                         |
| Measurement Sequence | `255`                                                                                                             |
| Flags                | <p>Calibration in progress: <code>true</code></p><p>VOC b9: <code>true</code></p><p>NOX b9: <code>true</code></p> |
| MAC                  | `FF FF FF`                                                                                                        |
