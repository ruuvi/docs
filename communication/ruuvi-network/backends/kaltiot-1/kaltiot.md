---
description: >-
  Lifecycle: Alpha. This list is imported from
  https://beacontracker.kalt.io/static/docs/REST-API.html .
---

# Kaltiot Smart Tracker Public REST API

The following headers are required:

```text
ApiKey: xxx
Content-Type: application/json
```

The API key is the same as the one you use for Kaltiot Smart IoT REST API.

Alternatively, you can also specify `ApiKey` as a query parameter.

**Error status codes**

* 400 Bad Request is returned when the request is invalid. Response body will contain error messages.
* 401 Unauthorized is returned when the ApiKey is invalid.
* 404 Not Found is returned when the resource does not exist.
* 501 Not Implemented is returned when the server does not support the functionality required to fulfill the request. Response body may contain error messages.

**Example response to a bad request**

```text
{
  "errors": {
    "page": ["is not an integer"],
    "trackable_id": ["is too short (min. 3 characters)"]
  }
}
```

## GET /beacons <a id="get-/beacons"></a>

Returns a paginated list of registered beacons.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| complete | boolean | Return full info \(as from GET /beacons/:id\) instead of just ids. |
| movable | string | Filter results depending on if the device is movable. Accepted values: `yes`, `no`, `ignore`. Defaults to `ignore`. |
| is\_phone | string | Filter results depending on if the device is a phone. Accepted values: `yes`, `no`, `ignore`. Defaults to `ignore`. |
| page | integer | Page of items to fetch. Starts at 0. |
| per\_page | integer | Number of items to fetch per page. Default 20. |
| trackable\_id | string | Wildcard filter for trackable id. Use `*` to match all beacons with any non-empty trackable id. |
| location\_name | string | Match all beacons whose location name contains this string. |
| ids | string | Filter results by full ids. Comma-separated. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beacons'
```

**Example response**

```text
{
  "beacons": [
    "001122334455",
    "112233445566",
    ...
  ],
  "pages": 30
}
```

## GET /beacons/:id <a id="get-/beacons/:id"></a>

Returns information on a beacon.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beacons/1234-abcd'
```

**Example response**

```text
{
  "id": "1234-abcd",
  "trackable_id": "box",
  "group_id": "packages",

  "customer_id": "updater",
  "timestamp": 1234567890, 

  "latitude": 12.34,
  "longitude": 56.78,
  "accuracy": 1234,
  "location_name": "container 555", 
  "area_name": "something", 

  "movable": true,
  "meta": {},

  "prob_of_movement": 30,
  "gps_used": false,
  "reloc_ts": 1234567890, 
  "is_phone": false,
  "floor": 1,
}
```

## PATCH /beacons/:id <a id="patch-/beacons/:id"></a>

Update information on a beacon. Only fields in the request body are updated.

If any of the following fields are specified, `timestamp` will be updated and customer\_id will be set to null to indicate a location update through the REST API: `latitude`, `longitude`, `accuracy`, `location_name`.

NOTE: `movable` can only be set to `false` if `trackable_id` is not empty.

**Request fields**

| Field | Type | Description |
| :--- | :--- | :--- |
| trackable\_id | string | Optional. |
| movable | boolean | Optional. |
| prob\_of\_movement | integer | Probability of movement. Optional. |
| meta | object | Optional. |
| latitude | string | Optional. |
| longitude | string | Optional. |
| accuracy | string | Optional. |
| location\_name | string | Optional. |
| group\_id | string | Optional. |
| floor | string | Optional. |

**Response status codes**

Returns 204 No Content on success.

**Example request**

```text
curl -iX PATCH \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d \
'{ "trackable_id": "office" }' \
 'https://beacontracker.kalt.io/api/beacons/1234-abcd'
```

## DELETE /beacons/:id <a id="delete-/beacons/:id"></a>

Delete a beacon.

**Response status codes**

Returns 204 No Content on success.

**Example request**

```text
curl -iX DELETE \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beacons/1234-abcd'
```

## GET /beacons/floor/:floor <a id="get-/beacons/floor/:floor"></a>

Returns beacons in given floor.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beacons/floor/1'
```

**Example response**

```text
{"beacons":[
  {
  "id": "1234-abcd",
  "trackable_id": "box",
  "group_id": "packages",

  "customer_id": "updater",
  "timestamp": 1234567890, 

  "latitude": 12.34,
  "longitude": 56.78,
  "accuracy": 1234,
  "location_name": "container 555", 
  "area_name": "something", 

  "movable": true,
  "meta": {},

  "prob_of_movement": 30,
  "gps_used": false,
  "reloc_ts": 1234567890, 
  "is_phone": false,
  "floor":1,
  }
]}
```

## GET /beacons/floor\_numbers <a id="get-/beacons/floor_numbers"></a>

Returns configured floor numbers.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beacons/floor_numbers'
```

**Example response**

```text
{
  "floor_numbers":[1,2,3],
  "pages":1
}
```

## GET /beaconconfig <a id="get-/beaconconfig"></a>

Returns beacon configuration for organization, to be written into the beacon.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/beaconconfig?type=logger'
```

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| type | string | `logger` or `scanner`. Defaults to `logger`. Optional. |

**Example response**

```text
{
  config: {
    samplingInterval : 1,
    sensors : 2,
    accelerationThreshold : 3,
    skipDuplicates : 4,
    flushDelay : 100,
    flushAdInterval: 10
  }
}
```

## POST /beaconconfig <a id="post-/beaconconfig"></a>

Sets beacon configuration for organization. The whole configuration is overwritten \(both logger and scanner\).

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX POST \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d '{ "logger": { "samplingInterval": 1, "sensors": 2, "accelerationThreshold": 3, "skipDuplicates": 4, "flushDelay": 100, "flushAdInterval": 10 }, "scanner": { "samplingInterval": 1, "sensors": 2, "accelerationThreshold": 3, "skipDuplicates": 4, "flushDelay": 100, "flushAdInterval": 10 } }' \
 'https://beacontracker.kalt.io/api/beaconconfig'
```

**Example response**

```text
{
  result: "Ok"
}
```

## GET /history <a id="get-/history"></a>

Returns location history for beacons.

* If both `to` and `from` are unspecified, returns data for the last 5 minutes.
* If `to` is specified but `from` isn't, returns all data up to the time indicated by `to`.
* If `from` is specified but `to` isn't, returns all data from the time indicated by `from`.
* Time window of 14 days or more is not supported.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ids | string | Comma-separated list of beacon ids. **Required**. |
| from | number | UTC timestamp, milliseconds. Optional. |
| to | number | UTC timestamp, milliseconds. Optional. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/history?ids=abcd-1234'
```

**Example response**

```text
[{
  id: "abcd-1234",
  history: [{ timestamp: 0, relocTs: 0, locationName: "location0", areaName: "area0", latitude: 1, longitude: 4, accuracy: 1, gpsUsed: false, updatedBy: { id: "dcba-5678", trackableId: "phone dcba-5678"}},
            { timestamp: 1, relocTs: 1, locationName: "location1", areaName: "area1", latitude: 2, longitude: 5, accuracy: 1, gpsUsed: false, updatedBy: { id: "dcba-5678", trackableId: "phone dcba-5678"}},
            { timestamp: 2, relocTs: 2, locationName: "location2", areaName: "area2", latitude: 3, longitude: 6, accuracy: 1, gpsUsed: false, updatedBy: { id: "dcba-5678", trackableId: "phone dcba-5678"}}]
}]
```

## GET /history/sensor/:sensor\_type <a id="get-/history/sensor/:sensor_type"></a>

Returns sensor history for beacons.

* Supported sensor types: `temperature`, `humidity`, `pressure`, `motion_detected`, `collision_x`, `collision_y`, `collision_z`, `hexdump`.
* If both `to` and `from` are unspecified, returns data for the last 5 minutes.
* If `to` is specified but `from` isn't, returns all data up to the time indicated by `to`.
* If `from` is specified but `to` isn't, returns all data from the time indicated by `from`.
* Time window of 14 days or more is not supported.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ids | string | Comma-separated list of beacon ids. **Required**. |
| from | number | UTC timestamp, milliseconds. Optional. |
| to | number | UTC timestamp, milliseconds. Optional. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/history/sensor/temperature?ids=abcd-1234'
```

**Example response**

```text
[{
  id: "abcd-1234",
  history: [{ timestamp: 0, value: 4 },
            { timestamp: 1, value: 5 },
            { timestamp: 2, value: 6 }]
}]
```

Returns rssi history for beacons.

* If both `to` and `from` are unspecified, returns data for the last 5 minutes.
* If `to` is specified but `from` isn't, returns all data up to the time indicated by `to`.
* If `from` is specified but `to` isn't, returns all data from the time indicated by `from`.
* Time window of 14 days or more is not supported.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ids | string | Comma-separated list of beacon ids. **Required**. |
| from | number | UTC timestamp, milliseconds. Optional. |
| to | number | UTC timestamp, milliseconds. Optional. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/history/rssi?ids=abcd-1234'
```

**Example response**

```text
[{
  id: "abcd-1234",
  history: [{ key: "cdef-5678", timestamp: 0, rssi: -20, scancount: 1, txpower: 4 },
            { key: "cdef-5678", timestamp: 1, rssi: -21, scancount: 1, txpower: 4 },
            { key: "cdef-5678", timestamp: 2, rssi: -22, scancount: 1, txpower: 4 }]
}]
```

## GET /assets <a id="get-/assets"></a>

Returns location history for beacons. Calculates new area names based on geofence areas. Subsequental locations that have same area name are filtered out.

* If both `to` and `from` are unspecified, returns data for the last 5 minutes.
* If `to` is specified but `from` isn't, returns all data up to the time indicated by `to`.
* If `from` is specified but `to` isn't, returns all data from the time indicated by `from`.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ids | string | Comma-separated list of beacon ids. **Required**. |
| from | number | UTC timestamp, milliseconds. Optional. |
| to | number | UTC timestamp, milliseconds. Optional. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/assets?ids=abcd-1234'
```

**Example response**

```text
[{
  id: "abcd-1234",
  history: [{ areaName: "home", latitude: 1, longitude: 4, accuracy: 1, timestamp: 0 },
            { areaName: "office", latitude: 2, longitude: 5, accuracy: 1, timestamp: 1 },
            { areaName: "home", latitude: 3, longitude: 6, accuracy: 1, timestamp: 2 }]
}]
```

## GET /usage <a id="get-/usage"></a>

Returns usage report for beacons.

* If both `to` and `from` are unspecified, returns data for the last 24 hours.
* If `to` is specified but `from` isn't, returns 24 hours data up to the time indicated by `to`.
* If `from` is specified but `to` isn't, returns all data from the time indicated by `from`.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ids | string | Comma-separated list of beacon ids. **Required**. |
| from | number | UTC timestamp, milliseconds. Optional. |
| to | number | UTC timestamp, milliseconds. Optional. |
| resolution | string | Results groupping resolution. Either 1d or 1h. Optional, default is 1h. |
| format | string | Output format. Either json or csv. Optional, default is json. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/usage?ids=abcd-1234'
```

**Example response**

```text
[{
  id: "abcd-1234", usage: {
    1495527321000: { total: 3, percentage: { A: 67, B: 33 },
      locations: { A: 2, B: 1 } },
  },
}]
```

## GET /key <a id="get-/key"></a>

Request API key.

**Response status codes**

Returns 200 OK on success.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| application | string | Application id to request API key. **Required**. |
| rid | string | Resource identifier where API key is sent to. **Required**. |

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
 'https://beacontracker.kalt.io/api/key?application=myapp&rid=myrid'
```

## GET /terms/:rid <a id="get-/terms/:rid"></a>

Returns non-accepted terms and conditions for rid.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/terms/abcd-1234'
```

**Example response**

Returns non-accepted terms and conditions, where: 1 = policy 2 = terms and conditions 3 = ok to locate

```text
[1, 2, 3]
```

## GET /terms/:rid/short <a id="get-/terms/:rid/short"></a>

Returns terms and conditions short version texts.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/terms/abcd-1234/short'
```

**Example response**

```text
{"1":"short policy","2":"short terms","3":"short ok to locate"}
```

## GET /terms/:rid/long <a id="get-/terms/:rid/long"></a>

Returns terms and conditions long version texts.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/terms/abcd-1234/long'
```

**Example response**

```text
{"1":"long policy","2":"long terms","3":"long ok to locate"}
```

## PUT /terms/:rid <a id="put-/terms/:rid"></a>

Saves accepted terms and conditions.

**Response status codes**

Returns 200 OK on success.

**Example request**

Body must be JSON array where is accepted terms: 1 = policy 2 = terms and conditions 3 = ok to locate

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d "[1,2,3]"
 'https://beacontracker.kalt.io/api/terms/abcd-1234'
```

## GET /geofence <a id="get-/geofence"></a>

Get all virtual beacons. Virtual beacon is a circular geo-fence that gives name to geographic area.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/geofence'
```

**Example response**

```text
[
    {
      "name": "company_site_1",
      "latitude": 12.34, 
      "longitude": 56.78, 
      "radius": 120, 
      "gpsEnabled": true,
    },
    {
      "name": "company_site_2",
      "latitude": 12.34, 
      "longitude": 56.78, 
      "radius": 120, 
      "gpsEnabled": true,
    },
    ...
]
```

## GET /geofence/:name <a id="get-/geofence/:name"></a>

Get virtual beacon with name.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/geofence/company_site_!'
```

**Example response**

```text
{
  "name": "company_site_1",
  "latitude": 12.34, 
  "longitude": 56.78, 
  "radius": 120, 
  "gpsEnabled": true,
}
```

## POST /geofence <a id="post-/geofence"></a>

Creates a new virtual beacon or update the existing one.

**Response status codes**

Returns 201 OK on success. `Location` field in the response header will point to the created virtual beacon

**Example request**

```text
curl -iX POST \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
    -d \
   '{ "latitude": 12.34, "longitude": 56.78, "name": "area3", "radius": 90, "gpsEnabled": true }'
 'https://beacontracker.kalt.io/api/geofence'
```

**Example response**

```text
{result: "Ok"}
```

## DELETE /geofence/:name <a id="delete-/geofence/:name"></a>

Deletes virtaul beacon.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX DELETE \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
    -d \
 'https://beacontracker.kalt.io/api/geofence/area3'
```

**Example response**

```text
{result: "Ok"}
```

## GET /floorplans <a id="get-/floorplans"></a>

Get a paginated list of floorplans. Filtered either suitable for mobile screens \(default\) or suitable for desktop.

**Query parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| page | integer | Page of items to fetch. Starts at 0. |
| per\_page | integer | Number of items to fetch per page. Default 20. |
| mobile | string | Filter floorplans suitable for mobile screen. Accepted values: `yes`, `no`, `ignore`. Any other value \(or if not defined\) will be interpreted as `yes`. |

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans'
```

**Example response**

```text
{
  "floorplans": [
    {
      "id": 1,
      "latitude": 12.34, 
      "longitude": 56.78, 
      "width": 12.34, 
      "height": 56.78, 
      "bearing": 90.12, 
      "name": "someplace",
      "timestamp": 1234567890,
      "mobile": true,
      "floor": 1,
    },
    {
      "id": 2,
      "latitude": 12.34,
      "longitude": 56.78,
      "width": 12.34,
      "height": 56.78,
      "bearing": 90.12,
      "name": "someplace",
      "timestamp": 1234567890,
      "mobile": false,
      "floor": 2
    },
    ...
  ],
  pages: 30
}
```

## GET /floorplans/:id <a id="get-/floorplans/:id"></a>

Get information on a floorplan.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans/1'
```

**Example response**

```text
{
  "id": 1,
  "latitude": 12.34,
  "longitude": 56.78,
  "width": 12.34,
  "height": 56.78,
  "bearing": 90.12,
  "name": "someplace",
  "floor": 1,
  "timestamp": 1234567890
}
```

## GET /floorplans/:id/data <a id="get-/floorplans/:id/data"></a>

Get the image data of a floorplan.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -X GET \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans/1/data'
```

**Example response**

```text
HTTP/1.1 200 OK
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 08 Jun 2016 12:12:42 GMT
Connection: keep-alive
Transfer-Encoding: chunked

<data here>
```

## GET /floorplans/:id/data\_rotated <a id="get-/floorplans/:id/data_rotated"></a>

Get the image data of a floorplan, pre-rotated by the bearing associated with the floorplan.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -X GET \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans/1/data_rotated'
```

**Example response**

```text
HTTP/1.1 200 OK
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 08 Jun 2016 12:12:42 GMT
Connection: keep-alive
Transfer-Encoding: chunked

<data here>
```

## POST /floorplans <a id="post-/floorplans"></a>

Creates a new floorplan. `Location` field in the response header will point to the created floorplan. By default creates floorplan suitable for mobile devices. To create floorplan suitable for desktop \(large image\) add parameter "mobile": false.

**Response status codes**

Returns 201 Created on success. `Location: /api/floorplans/:id` header contains the path to the created resource.

**Example request**

```text
curl -iX POST \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d \
'{ "latitude": 12.34, "longitude": 56.78, "width": 12.34, "height": 56.78, "bearing": 90.12, "floor": 1, }' \
 'https://beacontracker.kalt.io/api/floorplans'
```

Example floorplan for desktop only:

```text
curl -iX POST \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d \
'{ "latitude": 12.34, "longitude": 56.78, "width": 12.34, "height": 56.78, "bearing": 90.12, "mobile": false, "floor": 1, }' \
 'https://beacontracker.kalt.io/api/floorplans'
```

## PATCH /floorplans/:id <a id="patch-/floorplans/:id"></a>

Update floorplan information.

**Response status codes**

Returns the modified floorplan on success. The timestamp will also be updated.

**Example request**

```text
curl -iX PATCH \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d \
'{ "bearing": 55.666 }' \
 'https://beacontracker.kalt.io/api/floorplans/1'
```

**Example response**

```text
{
  "id": 1,
  "latitude": 12.34,
  "longitude": 56.78,
  "width": 12.34,
  "height": 56.78,
  "bearing": 55.666,
  "name": "someplace",
  "floor": 1,
  "timestamp": 1234567890
}
```

## PUT /floorplans/:id/data <a id="put-/floorplans/:id/data"></a>

Set the binary data of a floorplan.

**Response status codes**

Returns 204 No Content on success.

**Example request**

```text
curl -iX PUT \
   -H "Content-Type:multipart/form-data" \
   -H "ApiKey:xxx" \
   -F "data=@example.jpg" \
 'https://beacontracker.kalt.io/api/floorplans/1/data'
```

## DELETE /floorplans/:id <a id="delete-/floorplans/:id"></a>

Delete a floorplan.

**Response status codes**

Returns 204 No Content on success. Even if floorplan doesn't exist.

**Example request**

```text
curl -iX DELETE \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans/1'
```

## DELETE /floorplans/:id/data <a id="delete-/floorplans/:id/data"></a>

Delete the binary data of a floorplan.

**Response status codes**

Returns 204 No Content on success.

**Example request**

```text
curl -iX DELETE \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/floorplans/1'
```

## PUT /apps/:id <a id="put-/apps/:id"></a>

Enable or disable an app. Enabling means the service will start listening for notifications for this app.

**Request fields**

| Field | Type | Description |
| :--- | :--- | :--- |
| enabled | boolean | Self-explanatory. |

**Response status codes**

Returns 204 No Content on success.

**Example request**

```text
curl -iX PUT \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
   -d '{ "enabled": true }' \
 'https://beacontracker.kalt.io/api/apps/some_app'
```

## GET /packages/:file <a id="get-/packages/:file"></a>

Download a package.

**Response status codes**

Returns 200 OK on success.

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/packages/example_v1.2.3.apk?bewit=asdf'
```

Get url for a chart showing the distribution of locations for a beacon in a specified time span.

**Request fields**

| Field | Type | Description |
| :--- | :--- | :--- |
| id | string | Beacon id. **Required**. |
| from | number | UTC timestamp, milliseconds. **Required**. |
| to | number | UTC timestamp, milliseconds. **Required**. |

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/metabase/locations?ids=1,2,3&from=4444&to=5555'
```

**Example response**

```text
"https://reporting.torqhub.io/embed/question/abcdef"
```

## GET /securitydomain <a id="get-/securitydomain"></a>

Get security domain for the application. If security domain is defined, application uses email verification to authenticate application user.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/securitydomain'
```

**Example response**

```text
  {
    "securitydomain": "kaltiot.com"
  }
```

## POST /securitydomain <a id="post-/securitydomain"></a>

Request backend to send email verification to given email address.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX POST \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
    -d \
   '{ "rid": "myrid", "email": "user.email", "code": "client generated code" }'
 'https://beacontracker.kalt.io/api/securitydomain'
```

**Example response**

```text
  {
    result: "Ok"
  }
```

## GET /time <a id="get-/time"></a>

Get backend timestamp.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/time'
```

**Example response**

```text
  {
    "time": 1525353332779
  }
```

## GET /appid <a id="get-/appid"></a>

Get Application ID.

**Response status codes**

Returns 200 OK on success.

**Example request**

```text
curl -iX GET \
   -H "Content-Type:application/json" \
   -H "ApiKey:xxx" \
 'https://beacontracker.kalt.io/api/appid'
```

**Example response**

```text
  {
    "appId": "example_app.kaltiot"
  }
```

