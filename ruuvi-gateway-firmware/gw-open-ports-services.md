---
description: 'Lifecycle: in production'
---

# GW open ports / services

Ruuvi Gateway uses the following network services and ports.

### DHCP
- **67/udp inbound** — DHCP **server** in **configuration hotspot mode** (unconfigured / after Configure button).
- **68/udp outbound** — DHCP **client** when Ethernet/Wi‑Fi uses DHCP.

### DNS
- **5353/udp bi‑directional** — mDNS on LAN (gateway discoverable via its *.local name).
- **53/udp, 53/tcp outbound** — Unicast DNS to configured resolvers (required to resolve Ruuvi Cloud and any user‑configured endpoints).

### HTTP(S)
- **80/tcp inbound** — Web UI & local APIs over LAN (`/`, `/history`, `/metrics`, `/ruuvi.json`).
  - Sensitive configuration fields are encrypted during **hotspot provisioning**. Local HTTP is plaintext; place the device on a trusted LAN or use a reverse proxy/TLS terminator if HTTPS on LAN is required.
- **443/tcp outbound** — HTTPS to cloud/update services: `network.ruuvi.com`, `fwupdate.ruuvi.com`. Allowing `*.ruuvi.com` is recommended.

### MQTT(S) (optional)
- **1883/tcp outbound** — MQTT to user‑configured broker (disabled by default).
- **8883/tcp outbound** — MQTT over TLS to user‑configured broker (disabled by default).

### NTP
- **123/udp outbound** — Time sync. DHCP‑provided NTP servers are supported.
  - Common defaults: `time.ruuvi.com`, `time.google.com`, `time.cloudflare.com`, `pool.ntp.org` (may vary by firmware).
