# index.html

## User interface

Ruuvi Gateway sets up a WiFi hotspot and a webserver that provides the user interface for configuration over HTTP. The user interface can be accessed in any major browser. To connect to the user interface connect to hotspot "**Configure Ruuvi Gateway XXXX**" (it does not require a password). Once connected, open your browser and enter **http://10.10.0.1** . After the initial configuration is complete, you will be able to access the gateway from the LAN in the same way.

### Greeting window

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Internet connection settings

#### Internet connection A) WiFi

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

In case WiFi is hidden, you can enter WiFi SSID manually - this option is available under "Advanced settings":

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### Internet connection B) Ethernet

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

By default DHCP is enabled, so you don't need to configure anything else:

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

But you can always set the network settings manually, if necessary:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

In the next step, Ruuvi Gateway will ask you to connect the Ethernet cable (but that's okay if it's already connected):

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_025.png>)

if the Ethernet cable has not been connected in 30 seconds, an error message will be displayed. In this case, you can go back and try again.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### Software update

In this step Ruuvi Gateway checks for software updates:

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

If a newer version is available, the gateway will offer to update the firmware:

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

You can also install earlier or beta versions of the software by providing the URL to the required firmware. If you have built your own firmware, you can run HTTP server and provide the URL to your firmware binaries (See [gw-install-custom-firmware.md](../ruuvi-gateway-firmware/gw-install-custom-firmware.md "mention")).

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

Here is an example of the software update process:

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

After the software update is completed, Ruuvi Gateway will be restarted in a few seconds, and the following page will be displayed:

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### Automatic configuration download

Ruuvi Gateway can automatically download its configuration from a remote server, you can enable this feature on this page:

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

You need to specify the base URL from where gw\_cfg.json with the Gateway settings can be downloaded. After pressing the Download button, a new configuration will be downloaded, which completes the configuration process. After that, Ruuvi Gateway will periodically check for configuration updates and download them. The polling period is set in the configuration file gw\_cfg.json ([gateway-configuration.md](../data-formats/gateway-configuration.md "mention")), which is downloaded from the server.

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

It is also possible to use basic HTTP authentication:

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Or Bearer authentication (using a token):

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### Automatic updates

On this page, you can configure automatic software updates. By default, updates are automatically installed 2 weeks after release.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Under the "Advanced Settings", you can configure a schedule for installing updates - select weekdays and preferred timeslot:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

If you would like to participate in beta testing the new releases, then you can choose the following option (in this case new versions will be installed immediately after the release):

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Also, you can disable automatic software updating by switching to "Manual updates only" mode:

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

### Access Settings from LAN

On this page, you can set access rules to Ruuvi Gateway from the local network. By default, the access is password protected using the default password (unique device ID which is printed on the bottom of Ruuvi Gateway).

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

It is also possible to access Ruuvi Gateway from LAN using bearer authentication with an API key (token). You can enable read-only access (to retrieve data via the /history endpoint) or read-write access (to read any data or change the configuration):

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

### Cloud Options

By default, Ruuvi Gateway sends accumulated messages from Bluetooth sensors [http-time-stamped-data-from-bluetooth-sensors.md](../data-formats/http-time-stamped-data-from-bluetooth-sensors.md "mention") and some statistics [http-gateway-status.md](../data-formats/http-gateway-status.md "mention") to Ruuvi Cloud:

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

But you can change the cloud options under the "Advanced Settings":

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

#### Backend A) HTTP(S)

You can enable or disable sending data to Ruuvi Cloud:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Or configure to send data to your own server via HTTP/HTTPS (sending to both Ruuvi Cloud and your own server is not supported yet):

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

#### Backend B) MQTT

Also, you can enable relaying data to MQTT server:

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

#### Backend C) Statistics

In the Statistics section, you can configure the sending of statistics to Ruuvi Cloud or your own server, or disable the sending of statistics:

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Time Synchronization Options

In case the standard set of NTP servers is not accessible, then you can provide addresses of other NTP servers or use DHCP to get a list of NTP servers automatically. If Ruuvi Gateway does not have access to the Internet and NTP, then you can disable time synchronization, but in this case, relayed messages will not contain timestamps.

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### Bluetooth Scanning Settings

By default, Ruuvi Gateway scans only for Ruuvi sensors (filtered by BLE SIG member ID 0x0499)

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Scan PHY Modulations to scan with. Coded PHY is also known as BLE Long Range. Most of the existing devices send only on 1 MBit/s PHY. Modulations are scanned in sequence, so scanning both PHYs leads to at least 50 % packet loss on other PHY.

Scan extended payloads Both coded PHY and 1 MBit/s PHY may have a primary advertisement which tells that there is going to be extended data on a secondary channel. If enabled, the secondary payload is scanned. Coded PHY supports only Coded extended payload, 1 Mbit/s PHY supports scanning at 2 Mbit/s and 1 Mbit/s PHY extended payloads.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Scan channel Each enabled BLE channel is scanned in sequence for at least 7000 ms per channel, for a total of 21000 ms if all 3 channels are enabled. At least one channel must be enabled.

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

### Configuration completion

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>







****
