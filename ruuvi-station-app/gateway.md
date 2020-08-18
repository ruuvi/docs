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

If the 2 points are fulfilled the app will POST background scanning results to the URL.

URL set in app settings will get all the tags in one POST.  \(The app only sends measurements for tags added in the app.\)

### Data format

Every POST can contain one or few tag scan results after **"tags"**. 

`"tags":[{tagdata1},{tagdata2}, ... ,{tagdataN}]`

```text
{
    "tags": [
    {
      "accelX": Double // Acceleration along X axis, including gravity. Unit G
      "accelY": Double // Acceleration along Y axis, including gravity. Unit G
      "accelZ": Double // Acceleration along Z axis, including gravity. Unit G
      "createDate": String // Date when tag added to Ruuvi Station in format "yyyy-MM-dd'T'HH:mm:ssZ"
      "dataFormat": Int // Data format from tag firmware
      "defaultBackground": Int // Id of curent background used in Ruuvi Station
      "favorite": boolean // always true for tags added to Ruuvi Station
      "humidity": Double // current humidity
      "id": String // MAC address of tag
      "measurementSequenceNumber": Int // ???
      "movementCounter": Int // ???
      "name": String // Name of tag specified by user (can be absent)
      "pressure": Int // Current pressure in Pa
      "rssi": Int // Received signal strength indication in dBm
      "temperature": Double // Temperature in C,
      "txPower": Int // ???,
      "updateAt": String // Date of current measurments in format "yyyy-MM-dd'T'HH:mm:ssZ",
      "voltage": Voltage from tag in V
    }
  ],
  "batteryLevel": Int // current battery charge percentage,
  "deviceId": String // configurable in app settings, default is UUID generated on first start
  "eventId": String // UUID for this request
  "location": {
    "accuracy": Float // horizontal accuracy of this location, radial, in meters
    "latitude": Double // latitude, in degrees
    "longitude": Double // longitude, in degrees
  },
  "time": String // Date in format "yyyy-MM-dd'T'HH:mm:ssZ"
}
```

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

