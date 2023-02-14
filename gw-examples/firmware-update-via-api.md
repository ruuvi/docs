# Firmware update via API

You can run a firmware update from a specified URL programmatically, using bearer authentication.

On the "Access Settings" page, enable full access using bearer authentication and set the API-key:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Example of a command to run a firmware update from the URL: "https://my\_server.com:7000/gw\_firmware/"

```shell
    curl -v http://<RUUVI_GW_IP>/fw_update.json 
      -H "Authorization: Bearer 1SDrQH1FkH+pON0GsSjt2gYeMSP02uYqfuu7LWdaBvY=" 
      -H 'Content-Type: application/json' 
      -d '{"url":"https://my_server.com:7000/gw_firmware/"}'
```
