# Read logged history - Ruuvi Air

Related Ruuvi Devices: Ruuvi Air

## Overview

Ruuvi Air supports reading logged sensor history data over a Bluetooth Low Energy (BLE) connection using the Nordic UART Service (NUS). This allows mobile applications to retrieve historical air quality measurements stored on the device.

The protocol is similar to [RuuviTag log reading](log-read.md), but uses a different data format (E1) that includes additional air quality measurements such as PM2.5, CO₂, VOC, NOx, luminosity, and sound levels.

## Log read flow

1. The mobile app connects to Ruuvi Air over BLE
2. The app negotiates a larger MTU (247+ bytes recommended)
3. The app subscribes to NUS TX characteristic notifications
4. The app sends a log read command to the NUS RX characteristic
5. Ruuvi Air responds with multiple packets containing logged records
6. When all records are sent, Ruuvi Air sends an end-of-transmission marker

### Request format

The log read request is an 11-byte message with the following structure:

| Byte offset | Field | Description |
|-------------|-------|-------------|
| 0 | Destination | `0x3B` (Air Quality endpoint) |
| 1 | Source | `0x3B` (Air Quality endpoint) |
| 2 | Operation | `0x21` (Multi-record log read) or `0x11` (Single-record log read) |
| 3-6 | Current time | Current Unix timestamp (big-endian, seconds since epoch) |
| 7-10 | Start time | Start Unix timestamp to read from (big-endian, seconds since epoch) |

The multi-record read (`0x21`) is recommended as it packs multiple records per BLE packet for faster transfer.

### Example request

Reading all air quality data from timestamp `1733760000` (2024-12-09 16:00:00 UTC) with current time `1733763600` (2024-12-09 17:00:00 UTC):

```
0x3B 3B 21 67 57 01 B0 67 56 F2 00
```

- `0x3B 3B`: Destination and Source = Air Quality
- `0x21`: Multi-record log read operation
- `0x6757 01B0`: Current time = 1733763600
- `0x6756 F200`: Start time = 1733760000

## Response format

### Multi-record response packet

When using multi-record read (`0x21`), each response packet contains multiple records:

| Byte offset | Field | Description |
|-------------|-------|-------------|
| 0 | Destination | Source index from request |
| 1 | Source | `0x3B` (Air Quality endpoint) |
| 2 | Operation | `0x20` (Multi-record log write) |
| 3 | Num records | Number of records in this packet |
| 4 | Record length | Length of each record (38 bytes) |
| 5+ | Records | Packed record data |

### Record data format (38 bytes per record)

Each record contains a timestamp followed by E1 data format payload:

| Byte offset | Field | Type | Description |
|-------------|-------|------|-------------|
| 0-3 | Timestamp | uint32_t BE | Unix timestamp in seconds |
| 4 | Data format | uint8_t | `0xE1` |
| 5-6 | Temperature | int16_t BE | Temperature × 200 (°C) |
| 7-8 | Humidity | uint16_t BE | Humidity × 400 (%) |
| 9-10 | Pressure | uint16_t BE | (Pressure - 50000) Pa |
| 11-12 | PM1.0 | uint16_t BE | PM1.0 × 10 (µg/m³) |
| 13-14 | PM2.5 | uint16_t BE | PM2.5 × 10 (µg/m³) |
| 15-16 | PM4.0 | uint16_t BE | PM4.0 × 10 (µg/m³) |
| 17-18 | PM10.0 | uint16_t BE | PM10.0 × 10 (µg/m³) |
| 19-20 | CO₂ | uint16_t BE | CO₂ (ppm) |
| 21 | VOC | uint8_t | VOC index (0-500), bit 9 in flags |
| 22 | NOx | uint8_t | NOx index (0-500), bit 9 in flags |
| 23-25 | Reserved | uint24_t BE | Reserved  |
| 26 | Reserved | uint8_t | Reserved  |
| 27 | Reserved | uint8_t | Reserved  |
| 28 | Reserved | uint8_t | Reserved  |
| 29-31 | Sequence cnt | uint24_t BE | Measurement sequence counter |
| 32 | Flags | uint8_t | Extended bits for 9-bit values |
| 33-37 | Reserved | - | Reserved for future use |

### Flags byte interpretation

The flags byte contains the 9th bit for values that need more than 8 bits of precision:

| Bit | Field |
|-----|-------|
| 6 | VOC bit 9 |
| 7 | NOx bit 9 |

### Decoding formulas

| Field | Formula | Unit | Range |
|-------|---------|------|-------|
| Temperature | raw / 200.0 | °C | -163.84 to +163.83 |
| Humidity | raw / 400.0 | % | 0 to 100 |
| Pressure | raw + 50000 | Pa | 50000 to 115534 |
| PM values | raw / 10.0 | µg/m³ | 0 to 1000 |
| CO₂ | raw | ppm | 0 to 65534 |
| VOC/NOx | (byte \| (flag_bit9 << 8)) | index | 0 to 500 |

### Invalid values

When a sensor value is unavailable or invalid, the following special values are used:

| Field | Invalid value |
|-------|---------------|
| Temperature | `0x8000` |
| Humidity | `0xFFFF` |
| Pressure | `0xFFFF` |
| PM values | `0xFFFF` |
| CO₂ | `0xFFFF` |
| VOC/NOx | `0x1FF` (511) |
| Sequence | `0xFFFFFF` |
| MAC | `0xFFFFFFFFFFFF` |

### End of transmission

When all records have been sent, Ruuvi Air sends a final packet with:
- `num_records = 0`
- `record_length = 38`

Example end marker:
```
0x3B 3B 20 00 26 FF FF FF FF ...
```

This indicates no more records are available.

## Example communication

| Device | Data | Description |
|--------|------|-------------|
| Central | `0x3B 3B 21 67 57 01 B0 67 56 F2 00` | "Read air quality log. Current time: 2024-12-09 17:00, start from: 2024-12-09 16:00" |
| Peripheral | `0x3B 3B 20 06 26 ...` | "6 records of 38 bytes each in this packet" |
| ... | ... | Additional packets with records |
| Peripheral | `0x3B 3B 20 00 26` | "No more records (end of log)" |

## Implementation notes

### MTU considerations

Negotiating a larger MTU (247+ bytes) is recommended for optimal throughput. A minimum MTU of ~46 bytes is required to fit a single 38-byte record with headers. With a larger MTU, BLE Data Length Extension (DLE) enables up to 244 bytes per notification. With 38 bytes per record and a 5-byte packet header, up to 6 records can be packed in a single BLE packet:

```
(244 - 5) / 38 = 6 records per packet
```

### Time synchronization

The protocol uses a time offset calculation to handle clock drift between the device and the mobile app:
1. The app sends its current Unix time in the request
2. The device calculates the offset: `offset = app_time - device_time`
3. Timestamps in responses are adjusted by this offset

This ensures the returned timestamps are relative to the app's clock rather than the device's internal clock.

### Record interval

Ruuvi Air logs measurements once per second. A full day of history contains approximately 86,400 records.

## Code references

- **Firmware**: [ruuvi.air.main/src/nus.c](https://github.com/ruuvi/ruuvi.air.main/blob/main/src/nus.c)
- **Android**: [NordicGattManager.kt](https://github.com/ruuvi/com.ruuvi.bluetooth.default/blob/main/default_bluetooth_library/src/main/java/com/ruuvi/station/bluetooth/gatt/NordicGattManager.kt)
- **iOS**: [BTServices.swift](https://github.com/ruuvi/BTKit/blob/main/Sources/BTKit/Devices/BTServices.swift)
- **Data format**: [ruuvi.endpoints.c](https://github.com/ruuvi/ruuvi.endpoints.c)

## Related documentation

- [Read logged history - RuuviTag](log-read.md)
- [Data format E1](../../bluetooth-advertisements/data-format-e1.md)
