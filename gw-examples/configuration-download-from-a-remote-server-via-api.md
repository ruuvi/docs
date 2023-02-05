# Configuration download from a remote server via API

You can trigger a forced configuration download programmatically, using bearer authentication, but you must first configure the Gateway to use [automatic-configuration-download.md](../ruuvi-gateway-firmware/gateway-web-ui/automatic-configuration-download.md "mention").

Configuration on the remote server must contain the field **lan\_auth\_api\_key\_rw**:

```json
{
  "remote_cfg_use": true, 
  "remote_cfg_url": "http://192.168.1.101:7000/", 
  "remote_cfg_refresh_interval_minutes": 10,
  "remote_cfg_auth_type": "no",
  "lan_auth_api_key_rw": "1SDrQH1FkH+pON0GsSjt2gYeMSP02uYqfuu7LWdaBvY="
}
```

Example of a command to trigger a configuration download from the preconfigured remote server:

```
curl -v http://<RUUVI_GW_IP>/gw_cfg_download 
    -H "Authorization: Bearer 1SDrQH1FkH+pON0GsSjt2gYeMSP02uYqfuu7LWdaBvY=" -d ''
```
