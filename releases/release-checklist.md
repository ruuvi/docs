---
description: 'Lifecycle: Alpha. Last updated 2020-07-23'
---

# Release checklist

## ESP32

### Hotspot

| Test | How to check | Pass / Fail | Checked by, date |
| :--- | :--- | :--- | :--- |
| Hotspot is active on first boot. | Check that there is hotspot "Ruuvi Gateway ABCD" Check that it is connectable with password "12345678" |  |  |
| Hotspot is deactivated on internet connection. | Connect gateway with Ethernet cable observe that hotspot is turned off. |  |  |
| Hotspot remains deactivated after internet connection. | Disconnect Ethernet cable, reboot. |  |  |
| Hotspot is reactivated on short button press. | Press button, connect to WiFi |  |  |

### Button

| Test | How to check | Pass / Fail | Checked by, date |
| :--- | :--- | :--- | :--- |
| LED indicates button press. | Check LED on button press |  |  |
| LED indicates state Hotspot Active after short press.  | Check LED after button press |  |  |
| On press &lt; 5s configuration hotspot is activated, settings in flash remain | Configure custom settings. Press button briefly. Connect to hotspot, verify configured settings are shown. |  |  |
| On press &gt; 5s configuration hotspot is activated, settings in flash remain | Configure custom settings. Hold button for 5+ s. Connect to hotspot, verify default settings are shown. |  |  |

### LED

| Test | How to check | Pass / Fail | Checked by date |
| :--- | :--- | :--- | :--- |
| Hotspot active indication is activated. | Boot up unconfigured gateway.  |  |  |
| Button press indication is activated on button press in configuration mode. | Press button when not connected to Internet |  |  |
| Connection ok indication is activated.  | Connect Gateway with Ethernet Cable.  |  |  |
| Button press indication is activated on button press in connected more. | Connect Gateway with Ethernet Cable, press button |  |  |
| Disconnection indication is activated. | Connect and disconnect Gateway with Ethernet Cable. |  |  |
| Button press indication is activated on button press in disconnected mode. | Connect and disconnect Gateway with Ethernet Cable, press button. |  |  |

