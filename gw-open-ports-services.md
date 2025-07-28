---
description: 'Lifecycle: in production'
---

# GW open ports / services

Ruuvi Gateway has these Internet services / ports open:

### DHCP

67: DHCP server in configuration hotspot mode

68: DHCP client

### DNS

5353: Multicast DNS

### HTTP(S)

Outgoing 443, domains network.ruuvi.com, fwupdate.ruuvi.com, \*.ruuvi.com wildcard is recommended.

Incoming 80 for configuration over LAN. Sensitive information is encrypted on application level.&#x20;

### MQTT(S) (Optional)

Ports and domains depend on user configuration, not used by default.

### NTP

Ruuvi Gateway supports automatic NTP discovery through DHCP.

123: domains time.ruuvi.com, time.google.com, time.cloudflare.com, pool.ntp.org

