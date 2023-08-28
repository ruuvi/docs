# Bluetooth Scanning Settings

To access **Bluetooth Scanning Settings**, you must first enable access to configure advanced settings on the **Cloud Options** page under **Advanced Settings**:

<figure><img src="../../.gitbook/assets/Screenshot from 2023-06-27 21-32-36.png" alt=""><figcaption></figcaption></figure>

By default, Ruuvi Gateway scans only for Ruuvi sensors (filtered by BLE SIG member ID 0x0499)

<figure><img src="../../.gitbook/assets/Screenshot from 2023-06-27 21-51-12.png" alt=""><figcaption></figcaption></figure>

Also, you can enable Bluetooth long range (also known as Coded PHY). It is a new mode introduced in Bluetooth Version 5.0 to extend the range of Bluetooth devices from 30-100 feet to ranges of 1 kilometer and beyond.

**Note**: Most existing devices only transmit on 1 Mbps PHY. 1 Mbps and Coded PHYs modulations are scanned sequentially, so scanning both PHYs will result in at least 50% packet loss on one of the PHYs.

<figure><img src="../../.gitbook/assets/Screenshot from 2023-06-27 21-52-48.png" alt=""><figcaption></figcaption></figure>

If you want to relay data from more than just Ruuvi sensors, you need to select the "**All (including third party beacons)**" option and adjust the scanned PHYs, Bluetooth channels used and the ability to use extended payload (BLE extended advertising):&#x20;

<figure><img src="../../.gitbook/assets/Screenshot from 2023-06-27 21-54-14.png" alt=""><figcaption></figcaption></figure>

**Scan extended payloads**. Both Coded PHY and 1 Mbps PHY may have a primary advertisement that tells that there is going to be extended data on a secondary channel. If "**Use extended payload**" is enabled, the secondary payload will be scanned.&#x20;

Coded PHY supports only Coded extended payload, 1 Mbps PHY supports scanning at 2 Mbps and 1 Mbps PHY extended payloads.

**Use channel**. Each enabled BLE channel is scanned sequentially for a minimum of 7000 ms per channel, for a total of 21000 ms if all 3 channels are enabled. At least one channel must be active.

It is possible to filter out the relayed Bluetooth sensors. You can use **whitelist mode** if you only want to share data for specific sensors, or **blacklist mode** if you want to share data from all sensors except the specified list.

<figure><img src="../../.gitbook/assets/Screenshot from 2023-06-27 22-08-56.png" alt=""><figcaption></figcaption></figure>

If you don't see some sensors, try to press on **Refresh list**. If a sensor is offline, you can add it manually by entering its MAC address and pressing on the **Add** button.
