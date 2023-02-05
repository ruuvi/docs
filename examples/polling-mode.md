# Polling mode

It is possible to poll the accumulated data from the  Ruuvi Gateway via HTTP.

On the "Access Settings" page, enable bearer authentication and set the bearer token:

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

After that it is possible to poll data using the "/history" endpoint:

```shell
curl -v http://<RUUVI_GW_IP>/history 
    -H "Authorization: Bearer vum0G0DwdUBiNreYdSdqB785SX+l9VsnDQyDclwDP/Q="
```

The accumulated data will be returned in JSON format: [http-time-stamped-data-from-bluetooth-sensors.md](../data-formats/http-time-stamped-data-from-bluetooth-sensors.md "mention")or [http-data-from-bluetooth-sensors-without-timestamps.md](../data-formats/http-data-from-bluetooth-sensors-without-timestamps.md "mention")

Example of time-stamped data:

```json
{
  "data": {
    "coordinates": "",
    "timestamp": "1654830992",
    "gw_mac": "C8:25:2D:8E:9C:2C",
    "tags": {
      "F4:1F:0C:28:CB:D6": {
        "rssi": -36,
        "timestamp": "1654830991",
        "data": "0201061BFF99040514785B20C743FFC0FFC003E8AC3682473FF41F0C28CBD6"
      },
      "E3:75:CF:37:4E:23": {
        "rssi": -67,
        "timestamp": "1654830991",
        "data": "0201061BFF99040514F05CE3C6DDFED8FC38FFFCAB761D6269E375CF374E23"
      },
      "C6:A5:B9:E0:AD:06": {
        "rssi": -72,
        "timestamp": "1654830991",
        "data": "0201061BFF99040513E6606CC72600D0FF88040CA9F64361E4C6A5B9E0AD06"
      }
    }
  }
}
```
