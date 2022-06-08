---
description: 'Lifecycle: Beta. Last update 202<1-06-15. GW ESP32 Configuration'
---

# index.html

## User interface

Ruuvi Gateway sets up a WiFi hotspot and a webserver that provides the user interface for configuration over HTTP. The user interface can be accessed in any major browser. To connect to the user interface connect to hotspot "**RuuviGatewayXXXX**" (it does not require a password). Once connected, open your browser and enter **http://10.10.0.1** . After the initial configuration is complete, you will be able to access the gateway from the LAN in the same way.

### Greeting window

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_021.png>)

### Internet connection settings

#### Internet connection A) WiFi

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_055 (2).png>)

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_027.png>)

In case if WiFi is hidden, you can enter WiFi SSID manually - this option is available under "Advanced settings":

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_028.png>)

#### Internet connection B) Ethernet

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_022.png>)

By default DHCP is enabled, so you don't need to configure anything else:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_023.png>)

But you can always set the network settings manually, if necessary:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_024.png>)

In the next step, Ruuvi Gateway will ask you to connect the Ethernet cable (but that's okay if it's already connected):

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_025.png>)

if the Ethernet cable has not been connected in 30 seconds, an error message will be displayed. In this case, you can go back and try again.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_026.png>)

### Software update

In this step Ruuvi Gateway check for software updates:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_029.png>)

You can also install previous or beta versions of the software by providing the URL containing the required firmware. If you built your custom firmware, you can run HTTP-sever and provide the URL to your firmware binaries.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_030.png>)

Here is an example of the software update process:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_031.png>)

After the software update is completed, Ruuvi Gateway will be restarted in a few seconds, and the following page will be displayed:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_032.png>)

### Automatic configuration download

Ruuvi Gateway can automatically download its configuration from a remote server, you can enable this feature on this page:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_034.png>)

You need to specify the base URL from where gw\_cfg.json with the Gateway settings can be downloaded. After pressing the Download button, a new configuration will be downloaded, which completes the configuration process. After that, Ruuvi Gateway will periodically check for configuration updates and download them. The check period is set in the configuration file gw\_cfg.json ([gateway-configuration.md](../data-formats/gateway-configuration.md "mention")), which is downloaded from the server.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_035.png>)

It is also possible to use basic HTTP authentication:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_036.png>)

Or Bearer authentication (using a token):

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_037.png>)

### Automatic updates

On this page, you can configure automatic software updates. By default, updates are automatically installed 2 weeks after release.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_038.png>)

Under the "Advanced Settings", you can configure a schedule for installing updates - select weekdays and preferred timeslot:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_039.png>)

If you would like to participate in beta testing the new releases, then you can choose the following option (in this case new versions will be installed immediately after the release):

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_040.png>)

Also, you can disable automatic software updating by switching to "Manual updates only" mode:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_041.png>)

### Access Settings from LAN

On this page, you can set access rules to Ruuvi Gateway from the local network. By default, the access is password protected using the default password (unique device ID which is printed on the bottom of Ruuvi Gateway).

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_042.png>)

It is also possible to access Ruuvi Gateway from LAN using bearer authentication with an API key (token):

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_043.png>)

### Cloud Options

By default, Ruuvi Gateway sends accumulated messages from Bluetooth sensors ([http-time-stamped-data-from-bluetooth-sensors.md](../data-formats/http-time-stamped-data-from-bluetooth-sensors.md "mention")) and some statistics ([http-gateway-status.md](../data-formats/http-gateway-status.md "mention")) to Ruuvi Cloud:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_044.png>)

But you can change the cloud options under the "Advanced Settings":

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_045.png>)

#### Backend A) HTTP(S)

You can enable or disable sending data via HTTP/HTTPS and specify the address of your own server:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_046.png>)

#### Backend B) MQTT

Also, you can enable relaying data to MQTT server:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_047.png>)

#### Backend C) Statistics

It is also possible to disable sending statistics or changing the server address:

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_048.png>)

### Time Synchronization Options

In case the standard set of NTP servers is not accessible, then you can provide addresses of other NTP servers or use DHCP to get a list of NTP servers automatically. If Ruuvi Gateway does not have access to the Internet and NTP, then you can disable time synchronization, but in this case, relayed messages will not contain timestamps.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_049.png>)

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_050.png>)

### Bluetooth Scanning Settings

By default, Ruuvi Gateway scans only for Ruuvi sensors (filtered by BLE SIG member ID 0x0499)

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_051.png>)

Scan PHY Modulations to scan with. Coded PHY is also known as BLE Long Range. Most of existing devices send only on 1 MBit / s PHY. Modulations are scanned in sequence, so scanning both PHYs leads to at least 50 % packet loss on other PHY.

Scan extended payloads Both coded PHY and 1 MBit / s phy may have a primary advertisement which tells that there is going to be extended data on a secondary channel. If enabled, the secondary payload is scanned. Coded PHY supports only Coded extended payload, 1 Mbit / s PHY supports scanning at 2 Mbit / s and 1 Mbit / s PHY extended payloads.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_052.png>)

Scan channel Each enabled BLE channel is scanned in sequence for at least 7000 ms per channel, for a total of 21000 ms if all 3 channels are enabled. At least one channel must be enabled.

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_053.png>)

### Configuration completion

![](<../.gitbook/assets/Ruuvi Gateway Configuration Wizard - Google Chrome\_054.png>)







****
