---
description: 'Lifecycle: Proposal'
---

# Data format 8 (Encrypted environmental)

Related Ruuvi Devices: RuuviTag

This is a proposed encrypted data format which is not yet implemented in Ruuvi devices outside of a few proof-of-concept projects

The encryption uses nRF52-builtin AES128 encryption in Elctronic Codebook (ECB) mode. Data to be encrypted is temprature, humidity, pressure, voltage, TX power, measurement count and movement counts. The measurement sequence counter protects against replay attacks.

Data format has an unencrypted header, 16 bytes of AES-128 encrypted data, 1 byte crc8 and 6 bytes long MAC address for iOS devices.

| Offset |      Allowed values      | Description                                                                                                                                                                                                                                                                                        |
| ------ | :----------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0      |            `8`           | Data format.                                                                                                                                                                                                                                                                                       |
| 1-2    |    `-32767 ... 32767`    | Temperature in 0.005 degrees.                                                                                                                                                                                                                                                                      |
| 3-4    |      `0 ... 40 000`      | Humidity (16bit unsigned) in 0.0025% (0-163.83% range, though realistically 0-100%).                                                                                                                                                                                                               |
| 5-6    |       `0 ... 65534`      | Pressure (16bit unsigned) in 1 Pa units, with offset of -50 000 Pa.                                                                                                                                                                                                                                |
| 7-8    | `0 ... 2046`, `0 ... 30` | Power info (11+5bit unsigned), first 11 bits is the battery voltage above 1.6V, in millivolts (1.6V to 3.646V range). Last 5 bits unsigned are the TX power above -40dBm, in 2dBm steps. (-40dBm to +20dBm range).                                                                                 |
| 9-10   |       `0 ... 65534`      | Movement counter (16 bit unsigned), incremented by motion detection interrupts from accelerometer                                                                                                                                                                                                  |
| 11-12  |       `0 ... 65534`      | Measurement sequence number (16 bit unsigned), each time a measurement is taken, this is incremented by one, used for measurement de-duplication. Depending on the transmit interval, multiple packets with the same measurements can be sent, and there may be measurements that never were sent. |
| 13-16  |           `Any`          | Reserved for future use.                                                                                                                                                                                                                                                                           |
| 17     |        `0 ... 255`       | CRC8, used to check for correct decryption.                                                                                                                                                                                                                                                        |
| 18-23  |      `Any valid MAC`     | 48bit MAC address.                                                                                                                                                                                                                                                                                 |

The encryption key is formed according to the application, usually a static key shared in application + unique key derived from 8-byte tag ID.&#x20;

## Invalid values

If a value cannot be determined for any reason, a special invalid value is sent. For unsigned values the invalid value is largest presentable number, for example `0xFFFF` and for signed values the invalud value is smallest presentable number, for example `0x8000`. Invalid values should be treated as NULL, NAN, NONE or similar by the parser.

## Example

| Data        | Value                                                                                                    |
| ----------- | -------------------------------------------------------------------------------------------------------- |
| Temperature | 24.58 C                                                                                                  |
| Humidity    | 40.54 RH-%                                                                                               |
| Pressure    | 100453 Pa                                                                                                |
| Battery     | 2.765 V                                                                                                  |
| TX Power    | +4 dBm                                                                                                   |
| Movement    | 15                                                                                                       |
| Measurement | 6353                                                                                                     |
| Reserved    | 0                                                                                                        |
| Checksum    | [174](https://crccalc.com/?crc=13343F58C51548E6000F18D100000000\&method=crc8\&datatype=hex\&outtype=hex) |
| MAC         | 0xAABBCCDDEEFF                                                                                           |

| Keys     | Binary                                                  |
| -------- | ------------------------------------------------------- |
| ID       | 0x0011223344556677                                      |
| Password | 0x5275757669636f6d5275757669546167 _"RuuvicomRuuviTag"_ |

Unencrypted binary:

| DF | T    | H    | P    | B+TX | C    | M    | R        | CH | MAC          |
| -- | ---- | ---- | ---- | ---- | ---- | ---- | -------- | -- | ------------ |
| 08 | 1334 | 3F58 | C515 | 48E6 | 000F | 18D1 | 000000E0 | 1C | AABBCCDDEEDD |

Encryption key:

| Component | Binary                                          |
| --------- | ----------------------------------------------- |
| ID        | 00 11 22 33 44 55 66 77                         |
| password  | 52 75 75 76 69 63 6f 6d 52 75 75 76 69 54 61 67 |
| Result    | 52 64 57 45 2d 36 09 1a 52 75 75 76 69 54 61 67 |

Encrypted data: [`0x43825B56324FE019C4BD4D6D3CECAC6E`](http://extranet.cryptomathic.com/aescalc/index?key=526457452D36091A5275757669546167\&iv=00000000000000000000000000000000\&input=13343F58C51548E6000F18D100000000\&mode=ecb\&action=Encrypt\&output=9E49ED7745032DF5D2CC6E2A3047207B)

Complete message:

| DF | T    | H    | P    | B+TX | C    | M    | R        | CH | MAC          |
| -- | ---- | ---- | ---- | ---- | ---- | ---- | -------- | -- | ------------ |
| 08 | 4382 | 5B56 | 324F | E019 | C4BD | 4D6D | 3CECAC6E | 1C | AABBCCDDEEDD |

## Implementing the data format

Contact us at support@ruuvi.com if you want to implement this data format for your use case.&#x20;



