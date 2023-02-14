# Configuration update via API

You can configure the gateway so that you can update the configuration on it programmatically using bearer authentication.

On the "Access Settings" page, enable full access using bearer authentication and set the API-key:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Example of a command to download the configuration and save it to the ruuvi.json file:

```shell
    curl -v http://<RUUVI_GW_IP>/ruuvi.json 
      -H "Authorization: Bearer 1SDrQH1FkH+pON0GsSjt2gYeMSP02uYqfuu7LWdaBvY=" 
      --output ruuvi.json
```

Example of a command to upload the configuration from the "./ruuvi.json" file:

```shell
    curl -v http://<RUUVI_GW_IP>/ruuvi.json 
      -H "Authorization: Bearer 1SDrQH1FkH+pON0GsSjt2gYeMSP02uYqfuu7LWdaBvY=" 
      -d @./ruuvi.json 
```

**Note**: The network settings must be uploaded separately from the main Gateway configuration.

Example of "ruuvi.json" with the network settings (See [gateway-configuration.md](../data-formats/gateway-configuration.md "mention")):

```json
{
  "wifi_sta_config": {
    "ssid": "",
    "password": ""
  },
  "wifi_ap_config": {
    "password": "",
    "channel": 1
  },
  "use_eth": true,
  "eth_dhcp": true,
  "eth_static_ip": "",
  "eth_netmask": "",
  "eth_gw": "",
  "eth_dns1": "",
  "eth_dns2": ""
}
```

The network configuration must contain the **use\_eth** key and the main Gateway configuration must not contain it.
