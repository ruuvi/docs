# Bluetooth advertisements

**Introduction**

If you're not already familiar with Bluetooth Low-Energy \(BLE\) advertisements in general, please read the [Argenox primer](https://www.argenox.com/library/bluetooth-low-energy/ble-advertising-primer/).

The default way of getting data from RuuviTags is to listen to Bluetooth Low-Energy advertisement packets. The data is in manufacturer specific format. 

Additionally, connectable Ruuvi devices have a scan responce which contains device name "Ruuvi XXXX" and UUID of the Nordic UART Service. However if you're looking to only read the advertised data, you can ignore the scan responses. 

**Advertisement intervals**

The data is broadcast and not acknowledged by the listeners, therefore there is no guarantee that any single data packet will be heard by a nearby phone or gateway. The chance to receive the data depends on the signal strength and noise on the 2.4 GHz band, typically 25 ... 90 % of advertisements can be received in good conditions. 

The delay between updates is random, a gateway may miss 10 advertisements in a row even in good conditions. This latency is dependend on the broadcast interval, faster broadcasting means more chances to catch the data. On the other hand faster broadcasting will drain the battery faster, so there is a performance / battery runtime tradeoff. 

As of Ruuvi Firmware version 3.28.1 the default advertisement rate is 1285 ms + random delay of 0 ... 10 ms per advertisement. Test versions of firmware advertise at a rate of 211 ms + 0 ... 10 ms and long life versions at a rate of 8995 ms + 0 ... 10 ms. These intervals match Apple guidelines for bluetooth accessories. Android doesn't similar guidelines. 

**Advertisement data**

The advertisement begins with mandatory flags highlighted in blue. The the actual manufacturer specific data begins with a header highlighted in dark green which contains:

* Length \(not counting length byte\): **0x**1B = 27 bytes
* Type: **0x**FF = Manufacturer specific data
* Manufacturer ID, least significant byte first: **0x**0499 = Ruuvi Innovations Ltd
* Payload data: **0x**050F274035C454005000C8FC20A456F030E5C9445429E38D

Grayed out data is the scan response. Scan response is relevent when establishing the Bluetooth Connection to Ruuvi devices, but we can ignore it here.

![Advertised data and scan response](../../.gitbook/assets/image%20%285%29.png)

Interpretation of different payloads is described in the sub-sections of this page.

\*\*\*\*

