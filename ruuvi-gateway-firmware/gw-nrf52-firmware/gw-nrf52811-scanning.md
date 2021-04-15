---
description: 'Lifecycle: Beta. Last updated 2021-04-15'
---

# GW nRF52811 scanning

nRF52811 scans continuously with 7000 ms scan window and 7000 ms scan window. This allows Ruuvi Gateway to reliably detect slow RuuviTag advertising which is once per 6425 ms. 

Each scan is done on one enabled channel at a time, and once every selected channel is scanned next PHY is scanned. For example if the default setting of scanning all primary advertising channels 37, 38 and 39 on long range and 1 MBit / s modulation is enabled, one complete scan takes 3 channels \* 2 PHYs \* 7000 ms for a total of 42 seconds. 

Some Bluetooth devices can also advertise on secondary channels, the secondary advertisement works by first advertising information of secondary advertisement on primary channel and then sending secondary advertisement on any channel and modulation. If the primary advertisement was on long range PHY only long range secondary advertisements are scanned, if primary advertisement was on 1 MBit / s PHY secondary advertisement can be either 1 MBit / s or 2 MBit / s. 

By default nRF52811 will report only Ruuvi manufacturer specific data, but it's possible to configure the scan to report all seen beacons. 

Gateway can be configured via UART to enable/disable channels and PHYs with ruuvi\_endpoint\_ca\_uart commands.

