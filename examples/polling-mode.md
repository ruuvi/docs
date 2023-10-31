# Polling mode

It is possible to poll the accumulated data from the  Ruuvi Gateway via HTTP.

On the "Access Settings" page, enable bearer authentication and set the bearer token:

<figure><img src="../.gitbook/assets/Screenshot from 2023-06-27 22-30-41.png" alt=""><figcaption></figcaption></figure>

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
    "timestamp": 1698727580,
    "gw_mac": "F4:D9:16:FE:4F:AD",
    "tags": {
      "E3:75:CF:37:4E:23": {
        "rssi": -51,
        "timestamp": 1698727579,
        "data": "0201061BFF990405164D77BDC74A03FCFF34FFFC87D6DA63CAE375CF374E23",
        "dataFormat": 5,
        "temperature": 28.545,
        "humidity": 76.6325,
        "pressure": 101018,
        "accelX": 1.020,
        "accelY": -0.204,
        "accelZ": -0.004,
        "movementCounter": 218,
        "voltage": 2.686,
        "txPower": -32,
        "measurementSequenceNumber": 25546,
        "id": "E3:75:CF:37:4E:23"
      },
      "F4:1F:0C:28:CB:D6": {
        "rssi": -66,
        "timestamp": 1698727579,
        "data": "0201061BFF99040514F564D7C7B40008FFF403E8B2767A669BF41F0C28CBD6",
        "dataFormat": 5,
        "temperature": 26.825,
        "humidity": 64.5375,
        "pressure": 101124,
        "accelX": 0.008,
        "accelY": -0.012,
        "accelZ": 1.000,
        "movementCounter": 122,
        "voltage": 3.027,
        "txPower": -32,
        "measurementSequenceNumber": 26267,
        "id": "F4:1F:0C:28:CB:D6"
      },
      "C6:A5:B9:E0:AD:06": {
        "rssi": -60,
        "timestamp": 1698727579,
        "data": "0201061BFF99040517C166ACC78C00540004041C8756086435C6A5B9E0AD06",
        "dataFormat": 5,
        "temperature": 30.405,
        "humidity": 65.7100,
        "pressure": 101084,
        "accelX": 0.084,
        "accelY": 0.004,
        "accelZ": 1.052,
        "movementCounter": 8,
        "voltage": 2.682,
        "txPower": -32,
        "measurementSequenceNumber": 25653,
        "id": "C6:A5:B9:E0:AD:06"
      }
    }
  }
}
```

Also, it is possible to request only raw data without decoding:

```bash
curl -v http://<RUUVI_GW_IP>/history?decode=false 
    -H "Authorization: Bearer vum0G0DwdUBiNreYdSdqB785SX+l9VsnDQyDclwDP/Q="
```

Example of time-stamped data without decoding:

```json
{
  "data": {
    "coordinates": "",
    "timestamp": 1698727580,
    "gw_mac": "F4:D9:16:FE:4F:AD",
    "tags": {
      "E3:75:CF:37:4E:23": {
        "rssi": -51,
        "timestamp": 1698727579,
        "data": "0201061BFF990405164D77BDC74A03FCFF34FFFC87D6DA63CAE375CF374E23"
      },
      "F4:1F:0C:28:CB:D6": {
        "rssi": -66,
        "timestamp": 1698727579,
        "data": "0201061BFF99040514F564D7C7B40008FFF403E8B2767A669BF41F0C28CBD6"
      },
      "C6:A5:B9:E0:AD:06": {
        "rssi": -60,
        "timestamp": 1698727579,
        "data": "0201061BFF99040517C166ACC78C00540004041C8756086435C6A5B9E0AD06"
      }
    }
  }
}
```
