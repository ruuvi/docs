# Polling mode

It is possible to poll the accumulated data from the  Ruuvi Gateway via HTTP.

On the "Access Settings" page, enable bearer authentication and set the bearer token:

![](<../.gitbook/assets/Screenshot from 2022-06-10 10-20-23.png>)

After that it is possible to poll data using "/history" endpoint:

```
curl -H "Authorization: Bearer 0i0XJhGjpiMdEBRxI+hEXtJoGoL1jM7DFv6c6netsjU=" http://192.168.1.108/history
```

The accumulated data will be returned in JSON format: [http-time-stamped-data-from-bluetooth-sensors.md](../data-formats/http-time-stamped-data-from-bluetooth-sensors.md "mention")or [http-data-from-bluetooth-sensors-without-timestamps.md](../data-formats/http-data-from-bluetooth-sensors-without-timestamps.md "mention")

Example of time-stamped data:

```
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