# Automatic configuration download

Ruuvi Gateway can automatically download its configuration from a remote server, you can enable this feature on this page:

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

You need to specify the base URL from where gw\_cfg.json with the Gateway settings can be downloaded.

If you specify a folder name as the base URL (any URL that does not end with '.json'), it will first attempt to read the configuration file for the Gateway from \<GW\_MAC>.json (e.g. AABBCCDDEEFF.json). If this file fails, it will attempt to read the overall configuration from gw\_cfg.json.

The configuration file can also be generated dynamically by the server, which requires the server to analyse the HTTP header 'ruuvi\_gw\_mac', which contains the MAC address in the format XX:XX:XX:XX:XX:XX.

After entering the base URL, press the Check button to validate the URL and check that the configuration file exists. Next, after pressing the Download button, the new configuration will be downloaded, which completes the configuration process. After that, Ruuvi Gateway will periodically check for configuration updates and download them. The polling period is set in the configuration file ([gateway-configuration.md](../../data-formats/gateway-configuration.md "mention")), which is downloaded from the server.

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

The gateway configuration file on the remote server must contain at least the following attributes:

* **remote\_cfg\_use:** true
* **remote\_cfg\_url**: URL
* **remote\_cfg\_refresh\_interval\_minutes**: a period of checking for an updated configuration (in minutes)
* **remote\_cfg\_auth\_type**: authentication type ('**no**' if authentication is not required)

Example of minimal gw\_cfg.json:

```json
{
  "remote_cfg_use": true, 
  "remote_cfg_url": "http://192.168.1.101:7000/", 
  "remote_cfg_refresh_interval_minutes": 10,
  "remote_cfg_auth_type": "no" 
}
```

All configuration attributes not specified in the configuration file will retain their previous value after the new configuration is loaded from the remote server.

Configuration downloads with basic HTTP authentication are also supported:

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Example of corresponding minimal gw\_cfg.json:

```json
{
  "remote_cfg_use": true, 
  "remote_cfg_url": "http://192.168.1.101:7000/", 
  "remote_cfg_refresh_interval_minutes": 10,
  "remote_cfg_auth_type": "basic",
  "remote_cfg_auth_basic_user": "user1",
  "remote_cfg_auth_basic_pass": "password1"
}
```

Or Bearer authentication (using a token):

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Example of corresponding minimal gw\_cfg.json:

```json
{
  "remote_cfg_use": true, 
  "remote_cfg_url": "http://192.168.1.101:7000/", 
  "remote_cfg_refresh_interval_minutes": 10,
  "remote_cfg_auth_type": "bearer",
  "remote_cfg_auth_bearer_token": "my_secret_token_123"
}
```
