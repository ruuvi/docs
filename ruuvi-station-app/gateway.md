---
description: >-
  With this feature you can let the app act as a gateway, forwarding RuuviTag
  measurements to a http endpoint using POST requests.
---

# Gateway

### Setup

The app will act as a gateway when:

1. Background scanning is enabled
2. A valid URL has been set in app settings

If the 2 points are fulfilled the app will POST background scanning results to the URL. The app only sends measurements for tags added in the app.

### Data format

Every POST can contain one or few tag scan results after **"tags"**. 

`"tags":[{tagdata1},{tagdata2}, ... ,{tagdataN}]`

#### `Tag fields description`

| `Field name` | Data format | Unit/Format | Description |
| :--- | :--- | :--- | :--- |
| accelX | Double | G | Acceleration along X axis, including gravity |
| accelY | Double | G | Acceleration along Y axis, including gravity |
| accelZ | Double | G | Acceleration along Z axis, including gravity |
| createDate | String | yyyy-MM-dd'T'HH:mm:ssZ | Date when tag added to Ruuvi Station |
| dataFormat | Int |  | Data format from tag firmware |
| defaultBackground | Int |  | Id of curent background used in Ruuvi Station for this tag |
| favorite | boolean |  | Always true for tags added to Ruuvi Station |
| humidity | Double | Percentage | Current relative humidity |
| id | String |  | MAC address of tag |
| measurementSequenceNumber | Int |  | Value gets incremented by one for every measurement from 0 to 2^16 |
| movementCounter | Int |  | How many times tag has detected movement from 0 to 2^8 |
| name | String |  | Name of tag specified by user \(can be absent\) |
| pressure | Int | Pa | Current pressure |
| rssi | Int | dBm | Received signal strength indication |
| temperature | Double | Celsius | Current temperature |
| txPower | Int | dBm | Transmission power of tags |
| updateAt | String | yyyy-MM-dd'T'HH:mm:ssZ | Date of current measurments |
| voltage | Double | V | Battery voltage from tag |

#### Common POST fields 

| `Field name` | Data format | Unit/Format | Description |
| :--- | :--- | :--- | :--- |
| batteryLevel | Int | Percentage | Current battery charge percentage |
| deviceId | String |  | Configurable in app settings, default is UUID generated on first start |
| eventId | String |  | UUID for this request |
| accuracy | Double | meters | horizontal accuracy of this location, radial |
| latitude | Double | degrees | latitude |
| longitude | Double | degrees | longitude |
| time | String | yyyy-MM-dd'T'HH:mm:ssZ | Gateway request send date |

#### Example

```text
{
  "tags": [
    {
      "accelX": 0.012,
      "accelY": -0.004,
      "accelZ": 1.008,
      "createDate": "2020-08-11T18:51:58+0300",
      "dataFormat": 5,
      "defaultBackground": 2,
      "favorite": true,
      "humidity": 32.8425,
      "id": "E5:F1:98:34:C0:0F",
      "measurementSequenceNumber": 62865,
      "movementCounter": 21,
      "name": "Kitchen"
      "pressure": 98702,
      "rssi": -43,
      "temperature": 25.58,
      "txPower": 4,
      "updateAt": "2020-08-18T19:57:48+0300",
      "voltage": 3.013
    }
  ],
  "batteryLevel": 35,
  "deviceId": "yxftd9pnitd-156xhref9g69a",
  "eventId": "c07e3f9f-f6bb-4792-be6f-a9be95cdff38",
  "location": {
    "accuracy": 35.369,
    "latitude": 55.8256671,
    "longitude": 37.5962931
  },
  "time": "2020-08-18T19:57:48+0300"
}
```

###  [Ruuvi Station](https://ruuvi.com/manuals/station/app-settings/) gateway API Server

Open source gateway server can be found at: [https://github.com/ruuvi/ruuvi-station-influx-gateway](https://github.com/ruuvi/ruuvi-station-influx-gateway)

