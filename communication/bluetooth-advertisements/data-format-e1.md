---
description: 'Lifecycle: In Production'
---

# Data format E1 (Extended v1)

Related Ruuvi Devices: Ruuvi Air, Ruuvi Gateway

This data format uses Bluetooth 5 advertisement extension to provide more data than Bluetooth 4 advertisements can. Any Bluetooth 5.0 and upwards capable device should be able to receive this data format. It extends on data format 6; if the same device receives both in data format 6 and E1, the format 6 packet should be discarded.

The data is decoded from "Manufacturer Specific Data" -field, for more details please check [Bluetooth Advertisements section](https://docs.ruuvi.com/communication/bluetooth-advertisements). Manufacturer ID is **`0x0499`** , which is transmitted as **`0x9904`** in raw data. The actual data payload is:

| Offset        |   Allowed values   | Description                                                                                                   |
| ------------- | :----------------: | ------------------------------------------------------------------------------------------------------------- |
| 0             |        `E1`        | Data format (8bit)                                                                                            |
| 1-2           | `-32767 ... 32767` | Temperature in 0.005 degrees                                                                                  |
| 3-4           |   `0 ... 40 000`   | Humidity (16bit unsigned) in 0.0025% (0-163.83% range, though realistically 0-100%)                           |
| 5-6           |    `0 ... 65534`   | Pressure (16bit unsigned) in 1 Pa units, with offset of -50 000 Pa                                            |
| 7-8           |    `0 ... 10000`   | PM 1.0, ug/m^3. Resolution 0.1/bit, range 0 ... 1000. 16bit unsigned                                          |
| 9-10          |    `0 ... 10000`   | PM 2.5, ug/m^3. Resolution 0.1/bit, range 0 ... 1000. 16bit unsigned                                          |
| 11-12         |    `0 ... 10000`   | PM 4.0, ug/m^3. Resolution 0.1/bit, range 0 ... 1000. 16bit unsigned                                          |
| 13-14         |    `0 ... 10000`   | PM 10.0, ug/m^3. Resolution 0.1/bit, range 0 ... 1000. 16bit unsigned                                         |
| 15-16         |    `0 ... 40000`   | CO2 concentration, ppm. Resolution 1/bit, range 0 ... 40000. 16bit unsigned                                   |
| 17, +FLAGS b6 |     `0 ... 500`    | VOC index, unitless. Resolution 1 / bit, range 0 ... 500. 9 bit unsigned, least significant bit in Flags byte |
| 18, +FLAGS b7 |     `0 ... 500`    | NOX index, unitless. Resolution 1 / bit, range 0 ... 500. 9 bit unsigned, least significant bit in Flags byte |
| 19-21         | `0 ... 14 428 400` | Luminosity, Lux. Resolution 0.01/bit, range 0 ... 144 284                                                     |
| 22            |        `255`       | Reserved                                                                                                      |
| 23            |        `255`       | Reserved                                                                                                      |
| 24            |        `255`       | Reserved                                                                                                      |
| 25-27         | `0 ... 16 777 214` | Measurement sequence counter. Each new sample increments counter by 1. 24bit unsigned                         |
| 28            |    `0bVVXXXXXV`    | Flags. Value of each bit is described below                                                                   |
| 29-33         |   `0xFFFFFFFFFF`   | Reserved                                                                                                      |
| 34-39         |   `Any valid mac`  | 48bit MAC address.                                                                                            |

_Not available_ is signified by largest presentable number for unsigned values, smallest presentable number for signed values and all bits set for mac. All fields are MSB first. All signed values are 2-complement, i.e. `0xFC18` is read as `-1000` and `0x03E8` is read as `1000`. If original data overflows the data format, data is clipped to closest value that can be represented. For example temperature 170.00 C becomes 163.835 C

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

#### **PM 1.0/2.5/4.0/10.0**

Values supported: 0 to 6553.4 (ug/m^3), however the sensor on Ruuvi supports only 1000 ug/m^3. Values are uint16\_t, MSB first. All channels are identical. Resolution is 0.1 per bit

Note: Each measurement means "particle smaller than this", i.e. 10.0 includes 4.0 includes 2.5 includes 1.0, so measured value for larger particles is always larger.

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

Luminosity represents the light level in the environment of the sensor. The light level is compensated with human eye sensitivity curve. Value is 24-bit unsigned fixed-point number with resolution of 0.01

Please note that the highest valid value is 16 777 214, and 16 777 215 is reserved for the "not available".

_Example_

| Value      | Measurement             |
| ---------- | ----------------------- |
| `0x0000`   | 0 lux                   |
| `0x03E8`   | 10.00 lux               |
| 16 777 215 | Invalid / not available |

#### **Measurement sequence number**

Measurement sequence number gets incremented by one for every measurement. It can be used to gauge signal quality and packet loss as well as to deduplicated data entries. You should note that the measurement sequence refers to data rather than transmission, so you might receive many transmissions with the same measurement sequence number. Please note that the highest valid value is 16 777 214, and 16 777 215 is reserved for the "not available".

_Example_

| Value        | Measurement             |
| ------------ | ----------------------- |
| `00`         | 0 counts                |
| `1000`       | 1000 counts             |
| `16 777 215` | Invalid / not available |

#### **Flags**

Flags byte contains additional information and is interpreted bit-by-bit. "X" Means "don't care, 1 or 0". "V" Means the value of bit. Bits 1...5 are reserved. Bit 0 is least significant, bit 7 is most significant.

| Value         | Significance                                                                                |
| ------------- | ------------------------------------------------------------------------------------------- |
| `0bXXXX XXXV` | 1 -> Calibration in progress, sensor data not fully accurate yet. 0 -> Calibration complete |
| `0bXVXX XXXX` | VOC bit 9, 1-> set, 0 -> not set                                                            |
| `0bVXXX XXXX` | NOX bit 9, 1-> set, 0 -> not set                                                            |

#### **MAC address**

MAC address is static, statistically unique random identifier of the device. The address is 48 bits, with 2 most significant bits always set.

### Test vectors

These test vectors are based on [ruuvi.endpoints.c](https://github.com/ruuvi/ruuvi.endpoints.c) project. The tests are bidirectional, decode-encode results in original raw data. Encode-decode must result in same values with given precision, but floating point rounding differences may occur.

#### Case: valid data

Raw binary data: `0xE1170C5668C79E0065007004BD11CA00C90A0213E0ACXXXXXXDECDEE01XXXXXXXXXXCBB8334C884F` XX : Reserved

| Field                | Value                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Data format          | `E1`                                                                                                                |
| Temperature          | `29.500` C                                                                                                          |
| Pressure             | `101102` Pa                                                                                                         |
| Humidity             | `55.300` RH-%                                                                                                       |
| PM 1.0               | `10.1` ug/m^3                                                                                                       |
| PM 2.5               | `11.2` ug/m^3                                                                                                       |
| PM 4.0               | `121.3` ug/m^3                                                                                                      |
| PM 10.0              | `455.4` ug/m^3                                                                                                      |
| CO2                  | `201` ppm                                                                                                           |
| VOC                  | `20`                                                                                                                |
| NOX                  | `4`                                                                                                                 |
| Luminosity           | `13 027.00` Lux                                                                                                     |
| Measurement Sequence | `14 601 710`                                                                                                        |
| Flags                | <p>Calibration in progress: <code>True</code></p><p>VOC b9: <code>false</code></p><p>NOX b9: <code>false</code></p> |
| MAC                  | `CB B8 33 4C 88 4F`                                                                                                 |

#### Case: maximum values

Raw binary data: `0xE17FFF9C40FFFE27102710271027109C40FAFADC28F0XXXXXXFFFFFE3FXXXXXXXXXXCBB8334C884F` XX : Reserved

| Field                | Value                                                                                                               |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Data format          | `E1`                                                                                                                |
| Temperature          | `163.835` C                                                                                                         |
| Pressure             | `115534` Pa                                                                                                         |
| Humidity             | `100.000` RH-%                                                                                                      |
| PM 1.0               | `1000.0` ug/m^3                                                                                                     |
| PM 2.5               | `1000.0` ug/m^3                                                                                                     |
| PM 4.0               | `1000.0` ug/m^3                                                                                                     |
| PM 10.0              | `1000.0` ug/m^3                                                                                                     |
| CO2                  | `40000` ppm                                                                                                         |
| VOC                  | `500`                                                                                                               |
| NOX                  | `500`                                                                                                               |
| Luminosity           | `144284.00` Lux                                                                                                     |
| Measurement Sequence | `16 777 214`                                                                                                        |
| Flags                | <p>Calibration in progress: <code>True</code></p><p>VOC b9: <code>false</code></p><p>NOX b9: <code>false</code></p> |
| MAC                  | `CB B8 33 4C 88 4F`                                                                                                 |

Case: minimum values

Raw binary data: `0xE1800100000000000000000000000000000000000000XXXXXX0000000XXXXXXXXXXXCBB8334C884F` XX : Reserved

| Field                | Value                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Data format          | `E1`                                                                                                                 |
| Temperature          | `-163.835` C                                                                                                         |
| Pressure             | `50000` Pa                                                                                                           |
| Humidity             | `000.000` RH-%                                                                                                       |
| PM 1.0               | `0000.0` ug/m^3                                                                                                      |
| PM 2.5               | `0000.0` ug/m^3                                                                                                      |
| PM 4.0               | `0000.0` ug/m^3                                                                                                      |
| PM 10.0              | `0000.0` ug/m^3                                                                                                      |
| CO2                  | `00000` ppm                                                                                                          |
| VOC                  | `000`                                                                                                                |
| NOX                  | `000`                                                                                                                |
| Luminosity           | `00000.00` Lux                                                                                                       |
| Measurement Sequence | `00 000 000`                                                                                                         |
| Flags                | <p>Calibration in progress: <code>false</code></p><p>VOC b9: <code>false</code></p><p>NOX b9: <code>false</code></p> |
| MAC                  | `CB B8 33 4C 88 4F`                                                                                                  |

#### Case: Invalid values

Raw binary data: `0xE18000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFXXXXXXFFFFFFFEXXXXXXXXXXFFFFFFFFFFFF` XX : Reserved

| Field                | Value                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Data format          | `E1`                                                                                                               |
| Temperature          | `NaN` C                                                                                                            |
| Pressure             | `NaN` Pa                                                                                                           |
| Humidity             | `NaN` RH-%                                                                                                         |
| PM 1.0               | `NaN` ug/m^3                                                                                                       |
| PM 2.5               | `NaN` ug/m^3                                                                                                       |
| PM 4.0               | `NaN` ug/m^3                                                                                                       |
| PM 10.0              | `NaN` ug/m^3                                                                                                       |
| CO2                  | `NaN` ppm                                                                                                          |
| VOC                  | `NaN`                                                                                                              |
| NOX                  | `NaN`                                                                                                              |
| Luminosity           | `NaN` Lux                                                                                                          |
| Measurement Sequence | `NaN`                                                                                                              |
| Flags                | <p>Calibration in progress: <code>false</code></p><p>VOC b9: <code>true</code></p><p>NOX b9: <code>true</code></p> |
| MAC                  | `FF FF FF FF FF FF`                                                                                                |
