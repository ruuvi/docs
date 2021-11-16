---
description: 'Lifecycle: Obsolete. Last updated 2020-09-25'
---

# WhereOS

{% swagger baseUrl="https://whereos.ruuvi.com" path="/stream/post" method="post" summary="Gateway data" %}
{% swagger-description %}
Post Gateway data to this endpoint.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
"application/json"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="applicationid" type="string" %}
"387c6e87-f916-4c95-b067-b1d87726dde"
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pipelinename" type="string" %}
"write"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="data" type="object" %}
JSON data object with gateway data
{% endswagger-parameter %}

{% swagger-response status="200" description="Data successfully posted" %}
```
```
{% endswagger-response %}
{% endswagger %}

Sample URL; `https://whereos.ruuvi.com/stream/post?applicationid=387c6e87-f916-4c95-b067-b1d87726dde6&pipelinename=write `

Sample post data is at [Gateways-page](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LsPjfnhNj3v37AZtF-d%2F-M3jUH1sYjkphMsp0YBV%2F-M3j\_O0aAXI37-CWYbsi%2Fgwdata.json?alt=media\&token=07a07df8-2d6e-43da-b696-4197c8a21104).

{% swagger baseUrl="https://whereos.ruuvi.com" path="/api/ruuvi/coordinates/$COORDINATES" method="get" summary="Tags at a location" %}
{% swagger-description %}
**Important: This method is only for convenience of developers and may be removed in production.**
{% endswagger-description %}

{% swagger-parameter in="path" name="coordinates" type="string" %}
Coordinate string configured to Gateway. This might be a office name, gateway ID or a lat,long string. Query must match exactly the configuration. 
{% endswagger-parameter %}

{% swagger-parameter in="query" name="p_aggregation" type="string" %}
Downsample data to interval, default 15m. Valid values are number + s | m | h, e.g. "15m" 
{% endswagger-parameter %}

{% swagger-response status="200" description="Data of tags near the gateway. Array of JSON objects." %}
```
[
    {
        "rssi": -76,
        "data": "1eff060001092002afab33763d0e9a55a8b1200d435b42957653586b1030ff",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "021a4c93870b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -74,
        "data": "1eff06000109200286d615eb083513e0ce4a3b81930b88f2d8631cc9a1fe02",
        "coordinates": "Saase",
        "rssi_max": -74,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "043162b09154",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -93,
        "data": "1eff060001092002110dcf5b845c805296e70d12315246e10781cb8d5b2c34",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "163a0d8989f0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -76,
        "data": "1eff0600010920024a6044b7bdd6d0a3b7bd4e6c5bafffbfe4130b9f36ecd9",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "25e3be4243eb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -73,
        "data": "1eff0600010920021ac6a6e220cde100891c6b3051bf21ac9881cc454c2f8d",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "2a53a6f48c6d",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -81,
        "data": "1eff060001092002bc046312d771835b84075ec934fc2557a04f7ce80a1ca8",
        "coordinates": "Saase",
        "rssi_max": -81,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "313221640799",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -91,
        "data": "1eff060001092002c944cfb8ebf4a35cbcf3cdd3b417fbf8eb579319c1e535",
        "coordinates": "Saase",
        "rssi_max": -91,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "38abeb5cd42a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -71,
        "data": "1eff06000109200227b923cfb7dbb03ae54fb05babe3211c69868a2d4e8a93",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "3abe5ac51bec",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -71
    },
    {
        "rssi": -94,
        "data": "1eff0600010920022e2a2785d6fe1a517f3620b95a9455562a546905532b3d",
        "coordinates": "Saase",
        "rssi_max": -94,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "3d365ca36d7b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -94
    },
    {
        "rssi": -88,
        "data": "02011a020a0c0bff4c001006031adc95c73d",
        "coordinates": "Saase",
        "rssi_max": -88,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "414bcb2b15f6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -88
    },
    {
        "rssi": -84,
        "data": "1eff060001092002e2a86bce0bb3cf4d2275c524493a07ae05388f2b8263e8",
        "coordinates": "Saase",
        "rssi_max": -84,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "425c37b4fcfd",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -84
    },
    {
        "rssi": -72,
        "data": "0201060aff4c001005511c383eec",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "4433162032fa",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -72
    },
    {
        "rssi": -67,
        "data": "0201060aff4c001005511c7c3db2",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "49e10536723a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -68,
        "data": "0201060aff4c001005511c73bb52",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "4b05103a0017",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -68
    },
    {
        "rssi": -93,
        "data": "02011a020a0c0aff4c00100503183ffbdc",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "4ca1dabb17d3",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -67,
        "data": "0201060aff4c001005511c31f20c",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "4d1c544d2617",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -76,
        "data": "0201060aff4c001005511c2f3d2a",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "4ee986c308b1",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -68,
        "data": "0201060aff4c001005511c85bb36",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "4f4ca2fb5ce8",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -69
    },
    {
        "rssi": -90,
        "data": "02011a020a080aff4c001005611c0ff8f3",
        "coordinates": "Saase",
        "rssi_max": -90,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "5062da9e14c4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    },
    {
        "rssi": -67,
        "data": "0201060aff4c001005511cbf7974",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "50c2e1714264",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -76,
        "data": "0201060aff4c001005511c8c8b7a",
        "coordinates": "Saase",
        "rssi_max": -75,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "52791d7c929c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -76,
        "data": "0201060aff4c001005511ce0eaa4",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "537f10ce08d3",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -93,
        "data": "1eff4c0007190102202b328f0100009a045209f81fda1f1ff2c58303f6a8ee",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "53beab204c61",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -74,
        "data": "0201060aff4c001005511c81c19e",
        "coordinates": "Saase",
        "rssi_max": -74,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "544c594e3bf0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -72,
        "data": "0201060aff4c001005511c2bef96",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "572d2af8b7dd",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -72
    },
    {
        "rssi": -67,
        "data": "0201060aff4c001005511caab6d5",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "57b705c836ed",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -78,
        "data": "0201060aff4c001005511c9af199",
        "coordinates": "Saase",
        "rssi_max": -78,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "595de0640ed1",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -93,
        "data": "02011a020a0c0aff4c00100503180b1e8b",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "5966f9117ee4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -94,
        "data": "02011a020a0c0aff4c0010050318bc5b06",
        "coordinates": "Saase",
        "rssi_max": -94,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "5c6ab292fcf4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -94
    },
    {
        "rssi": -71,
        "data": "0201060aff4c001005511ca3dd7e",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "5e3d263d3382",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -71
    },
    {
        "rssi": -89,
        "data": "1eff060001092002e2a86bce0bb3cf4d2275c524493a07ae05388f2b8263e8",
        "coordinates": "Saase",
        "rssi_max": -88,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "5fa010e46cdb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -70,
        "data": "0201060aff4c001005511c901ae3",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "60e8f6e69548",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -70
    },
    {
        "rssi": -68,
        "data": "0201060aff4c001005511c678f9f",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "617f01986fef",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -70
    },
    {
        "rssi": -65,
        "data": "0201060aff4c001005511ca6b61e",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "63df6c90c83e",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -66
    },
    {
        "rssi": -66,
        "data": "0201060aff4c001005511c334bb7",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "6776004a1cac",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -66
    },
    {
        "rssi": -66,
        "data": "0201060aff4c001005511c6eb246",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "6a42fb5abe6a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -66
    },
    {
        "rssi": -91,
        "data": "02011a020a0c0aff4c0010054b1c71b0b1",
        "coordinates": "Saase",
        "rssi_max": -91,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "6a509fb28472",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -74,
        "data": "0201060aff4c001005511c36b455",
        "coordinates": "Saase",
        "rssi_max": -74,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "6b6f47de57c5",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -75,
        "data": "0201060aff4c0010051118d7c285",
        "coordinates": "Saase",
        "rssi_max": -75,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "6cdef06f0441",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -67,
        "data": "0201060aff4c001005511c9782ee",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "6e28fdeb4472",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -81,
        "data": "0201060aff4c001005511cb90c26",
        "coordinates": "Saase",
        "rssi_max": -81,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "7375151daf3d",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -92,
        "data": "1eff060001092002a27280ce88c01c61a12f000b962fed16c9d3ab511aa1e4",
        "coordinates": "Saase",
        "rssi_max": -92,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "7411ee60cab0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -92
    },
    {
        "rssi": -71,
        "data": "0201060aff4c001005511ccb00ce",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "77f06b334306",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -72
    },
    {
        "rssi": -93,
        "data": "02011a020a0c0aff4c00100511184b2d8a",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "79f8ff3929b7",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -76,
        "data": "0201060aff4c001005511c71c386",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "7b2538b6414e",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -89,
        "data": "1eff060001092002a27280ce88c01c61a12f000b962fed16c9d3ab511aa1e4",
        "coordinates": "Saase",
        "rssi_max": -89,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "7c33671af646",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    },
    {
        "rssi": -89,
        "data": "02011a020a0c0bff4c0010060a1ede81fa25",
        "coordinates": "Saase",
        "rssi_max": -89,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "7c5b8b96fade",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -82,
        "data": "1eff060001092002fe8fe9a32f2810ace729f582ef586b2614b5525d64b844",
        "coordinates": "Saase",
        "rssi_max": -82,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "7d4f3ede1af6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -82
    },
    {
        "rssi": -66,
        "data": "0201060aff4c001005511c7677e8",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "7d778abc6c0f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -68
    },
    {
        "rssi": -76,
        "data": "0201060aff4c001005511c5e07a6",
        "coordinates": "Saase",
        "rssi_max": -76,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "7dcbf3422680",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -93,
        "data": "02011a020a0c0aff4c0010050318c74865",
        "coordinates": "Saase",
        "rssi_max": -93,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "7f36bc4552b1",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -67,
        "data": "020118031900020b094a424c20466c697020330aff570053002300011e52",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "b8d50bc9e1fb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -62,
        "data": "020118031900020b094a424c20466c697020330aff570053002300011e52",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "b8d50bc9e1fb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -65
    },
    {
        "rssi": -62,
        "data": "020118031900020b094a424c20466c697020330aff570053002300011e52",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "b8d50bc9e1fb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -62
    },
    {
        "rssi": -65,
        "data": "0201041bff990405107e2ddcc9cf0000ff1803f89ff66f1463c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -88
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510852df0ca490000ff2403f8a2166f2a33c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510782dd5cc0b0004ff1c03eba2166f6beac04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -76,
        "data": "02011e0aff7500010002000103020319c000",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c0f54292e3e2",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -77,
        "data": "02011e0aff7500010002000103020319c000",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c0f54292e3e2",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510802df3c99affdc002c03e092b6bcdc3cc3583413b9f4",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c3583413b9f4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510862df3ca16ffd0002c03dc9336bc0808c3583413b9f4",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c3583413b9f4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510782de3cbd5ffd8003003e49396bc8b59c3583413b9f4",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c3583413b9f4",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -61,
        "data": "0201041bff9904051117341cc9b2fff0ff0cfc106276efbb23c3a73b33d4c9",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c3a73b33d4c9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -82
    },
    {
        "rssi": -61,
        "data": "0201041bff990405111e3411ca2effecff0cfc106196efe6edc3a73b33d4c9",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c3a73b33d4c9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -61,
        "data": "0201041bff990405111233f0cbeeffe8ff0cfc0862d6ef6a58c3a73b33d4c9",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c3a73b33d4c9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -70
    },
    {
        "rssi": -69,
        "data": "02010611ff990403371508c9a1fff80106fc390c01",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c3c08a49792b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -80
    },
    {
        "rssi": -72,
        "data": "02010611ff99040337150bca21fffb0106fc3d0c07",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c3c08a49792b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -84
    },
    {
        "rssi": -75,
        "data": "02010611ff990403371506cbe2fffc010afc410bf5",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c3c08a49792b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510f42badc934ffd00174fc38ad16cad355c4a34245023f",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c4a34245023f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510f72ba3c9b2ffcc0178fc3cad16caff20c4a34245023f",
        "coordinates": "Saase",
        "rssi_max": -60,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c4a34245023f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -63,
        "data": "0201041bff99040510ee2b95cb74ffcc0170fc38abd6ca8272c4a34245023f",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c4a34245023f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510c832d8c8f2fcd001a4fe40afb674bd00c602662b09c8",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c602662b09c8",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -63,
        "data": "0201041bff99040510cd32dfc96dfcd801a8fe48ae7674e8b7c602662b09c8",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c602662b09c8",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -80
    },
    {
        "rssi": -63,
        "data": "0201041bff99040510c532c4cb2cfcd401a4fe40aed6746c2ac602662b09c8",
        "coordinates": "Saase",
        "rssi_max": -61,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c602662b09c8",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510f9352bc8e0011cff6cfc2498f66514bac9445429e38d",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "c9445429e38d",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510fa350cc95d0118ff68fc249816652aaac9445429e38d",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c9445429e38d",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510f634cfcb22011cff70fc2498f6656c49c9445429e38d",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c9445429e38d",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -74,
        "data": "0201061bff9904fa864594a6b636d2b51fe808d5abc57b99cb31380df7a600",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "cb31380df7a6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -83,
        "data": "0201061bff9904fa3cd5484f76679b19933bc35fdff334ddcb31380df7a600",
        "coordinates": "Saase",
        "rssi_max": -74,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "cb31380df7a6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -78,
        "data": "0201061bff9904fa2f0bee817c554bc1f985afa3732d81aecb31380df7a600",
        "coordinates": "Saase",
        "rssi_max": -74,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "cb31380df7a6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -84
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510dc2e9cc9e6040cffb800889096edce1fcc184dd582b0",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "cc184dd582b0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510e22e88ca650414ffbc008490f6edf9bfcc184dd582b0",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "cc184dd582b0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510d82e60cc26040cffbc00849176ed7d25cc184dd582b0",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "cc184dd582b0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -70,
        "data": "02010415ff9904033e1533c911ffedff70fc380a6900000000",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "cccde2217036",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -75,
        "data": "02010415ff99040341151dc99bffe9ff60fc340a6300000000",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "cccde2217036",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -76,
        "data": "02010415ff9904033a1452cb5bffe5ff5cfc380a6900000000",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "cccde2217036",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -71,
        "data": "0201041bff990405109b2e5fc983fe700084fc68715608f481cd4d957ebb38",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "cd4d957ebb38",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -83
    },
    {
        "rssi": -71,
        "data": "0201041bff990405109c2e68ca00fe80007cfc6072b6082041cd4d957ebb38",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "cd4d957ebb38",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -83
    },
    {
        "rssi": -72,
        "data": "0201041bff99040510932e55cbbdfe780084fc60715608a3becd4d957ebb38",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "cd4d957ebb38",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -83
    },
    {
        "rssi": -77,
        "data": "0201041bff990405119429e2c96bfff4ffe4fc309b9606001ace19501d50a5",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "ce19501d50a5",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -72,
        "data": "0201041bff99040511bd2b84c9e8fff8ffe0fc2c9a36062be6ce19501d50a5",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "ce19501d50a5",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -70,
        "data": "0201041bff99040510ec2ac0cbaefff0ffe4fc2898f607af53ce19501d50a5",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "ce19501d50a5",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -86
    },
    {
        "rssi": -67,
        "data": "0201061bff9904fadde3cb1a0bbe7d48e42db0a7588f21afd04afd84bb3b00",
        "coordinates": "Saase",
        "rssi_max": -61,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "d04afd84bb3b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -67,
        "data": "0201061bff9904fa569262624dd3967702fbfad6e4e3d543d04afd84bb3b00",
        "coordinates": "Saase",
        "rssi_max": -60,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "d04afd84bb3b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -66,
        "data": "0201061bff9904fa88ed21d35486cffc0526474850494c94d04afd84bb3b00",
        "coordinates": "Saase",
        "rssi_max": -61,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "d04afd84bb3b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510d8308ec96803d8016cffc0a45611bfa9d0c5b00f4637",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "d0c5b00f4637",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -72,
        "data": "0201041bff99040510dd3076c9e603d4016cffc8a45611eb4dd0c5b00f4637",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "d0c5b00f4637",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510d3304ccba603dc0168ffc0a5b6116eb7d0c5b00f4637",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "d0c5b00f4637",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -76,
        "data": "0201041bff99040510ce2f88c92efff4006cfc08b03668d1d5d2ce151e309c",
        "coordinates": "Saase",
        "rssi_max": -69,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "d2ce151e309c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -79,
        "data": "0201041bff99040510d12f74c9acfff00060fc08b11668fd79d2ce151e309c",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "d2ce151e309c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -82,
        "data": "0201041bff99040510cc2f44cb6affec0068fc08afb66880cfd2ce151e309c",
        "coordinates": "Saase",
        "rssi_max": -78,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "d2ce151e309c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -65,
        "data": "0201061bff990405106a27d1c926ffbcfc7001b0b176387ba5d6570696959b",
        "coordinates": "Saase",
        "rssi_max": -58,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "d6570696959b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -63,
        "data": "0201061bff990405107027c0c99fffb8fc7001b0b23638a79ad6570696959b",
        "coordinates": "Saase",
        "rssi_max": -56,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "d6570696959b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -64,
        "data": "0201061bff990405106627a5cb62ffb4fc7801b8b176382b6ad6570696959b",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "d6570696959b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -77,
        "data": "0201041bff99040510903141ca1600c80128fc58979605f48eda3eed2b0eb9",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "da3eed2b0eb9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -70,
        "data": "0201041bff9904051092312fca9000d0011cfc509816052046da3eed2b0eb9",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "da3eed2b0eb9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -82
    },
    {
        "rssi": -71,
        "data": "0201041bff990405108b3101cc5500cc0120fc48979605a3afda3eed2b0eb9",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "da3eed2b0eb9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -73,
        "data": "0201041bff99040512df39f1c58cfffcfffcfffc45d600af6adab3673134bf",
        "coordinates": "Saase",
        "rssi_max": -73,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "dab3673134bf",
        "gwmac": "30aea4cc1e2c",
        "rssi_min": -73
    },
    {
        "rssi": -60,
        "data": "0201041bff990405108b2e1bc9a7ffa8fc3801d0933645977ddab59bdfa9bb",
        "coordinates": "Saase",
        "rssi_max": -49,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "dab59bdfa9bb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -53,
        "data": "0201041bff99040510b33132ca27ff9cfc3401c096b646a338dab59bdfa9bb",
        "coordinates": "Saase",
        "rssi_max": -43,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "dab59bdfa9bb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -63
    },
    {
        "rssi": -53,
        "data": "0201041bff99040510243320cbeeff9cfc3801d0963646c738dab59bdfa9bb",
        "coordinates": "Saase",
        "rssi_max": -51,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "dab59bdfa9bb",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -56
    },
    {
        "rssi": -83,
        "data": "0201061bff99040510682c7dc93bffa400a80420b17681a9f7dac5854c6ecc",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "dac5854c6ecc",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -76,
        "data": "0201061bff990405106c2c66c9b8ffa400ac0414aff681d5dcdac5854c6ecc",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "dac5854c6ecc",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -77,
        "data": "0201061bff990405105e2c48cb76ffa000ac041caf368159bbdac5854c6ecc",
        "coordinates": "Saase",
        "rssi_max": -75,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "dac5854c6ecc",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -74,
        "data": "0201041bff990405106232a8c8d0fc4cfe7c0064ad960ab2c0dcd65e5fb24b",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "dcd65e5fb24b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -86
    },
    {
        "rssi": -66,
        "data": "0201041bff9904051070329ac949fc48fe78006cae760ac8a3dcd65e5fb24b",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "dcd65e5fb24b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -80
    },
    {
        "rssi": -68,
        "data": "0201041bff9904051057329fcb0efc4cfe7c006cacb60a0a56dcd65e5fb24b",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "dcd65e5fb24b",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -79,
        "data": "0201041bff990405111c3405c90e02e8fd24ffd4aa16c9b974dce178f91f85",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "dce178f91f85",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -84,
        "data": "0201041bff990405111f3405c99002ecfd28ffd8aa16c9e538dce178f91f85",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "dce178f91f85",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -81,
        "data": "0201041bff990405111833efcb4f02f0fd24ffe0aaf6c968a1dce178f91f85",
        "coordinates": "Saase",
        "rssi_max": -78,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "dce178f91f85",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510ccffffffff00e4ff7cfc20ae76d1ad19df06dcba793a",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "df06dcba793a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -69,
        "data": "0201041bff9904051068ffffffff00dcff84fc1cacb6d1d8c5df06dcba793a",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "df06dcba793a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -67,
        "data": "0201041bff9904051036ffffffff00d4ff7cfc1cad16d15c07df06dcba793a",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "df06dcba793a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -86
    },
    {
        "rssi": -74,
        "data": "0201041bff99040510be2f0dc8f90038fe24fc9cb896ffa890e362b15a7860",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "e362b15a7860",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    },
    {
        "rssi": -78,
        "data": "0201041bff99040510c02f19c9770038fe1cfc9cb736ffd44be362b15a7860",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "e362b15a7860",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -92
    },
    {
        "rssi": -75,
        "data": "0201041bff99040510b92f06cb3c0034fe1cfc9cb896ff5786e362b15a7860",
        "coordinates": "Saase",
        "rssi_max": -73,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "e362b15a7860",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -74,
        "data": "0201041bff99040510ca2e69c91bfe04fc900088aaf606ed9ce576fdf21a2f",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "e576fdf21a2f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -86
    },
    {
        "rssi": -74,
        "data": "0201041bff99040510d02e6bc996fe08fc90008cabd6061960e576fdf21a2f",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "e576fdf21a2f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -75,
        "data": "0201041bff99040510c52e53cb5cfe00fc94008cab56069cb6e576fdf21a2f",
        "coordinates": "Saase",
        "rssi_max": -73,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "e576fdf21a2f",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -66,
        "data": "0201061bff990405108e2b27c988ffbcfbfcffc4b0b66379f3e7aeab82fda9",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "e7aeab82fda9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201061bff99040510942b2dca06ffb4fbfcffc0b0b663a5f7e7aeab82fda9",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "e7aeab82fda9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -65,
        "data": "0201061bff99040510882b07cbcbffb8fbf8ffbcb1766329d3e7aeab82fda9",
        "coordinates": "Saase",
        "rssi_max": -60,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "e7aeab82fda9",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -76,
        "data": "0201041bff99040511113570c963fcb0021cffaca376731498e9d54bfe15e7",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "e9d54bfe15e7",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -72,
        "data": "0201041bff99040511193572c9e2fcb00214ffb0a296732a6ae9d54bfe15e7",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "e9d54bfe15e7",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -75,
        "data": "0201041bff990405110f355acbaafcb00214ffa4a376736c1be9d54bfe15e7",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "e9d54bfe15e7",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -75,
        "data": "0201041bff990405127a381ec9860058ffe404109636000293ea17e9643a7a",
        "coordinates": "Saase",
        "rssi_max": -69,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "ea17e9643a7a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -80,
        "data": "0201041bff99040513ff2d3dcaf20038001c04089794020010ea17e9643a7a",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "ea17e9643a7a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -95
    },
    {
        "rssi": -79,
        "data": "0201041bff99040511db2a51cb790034001c0414a12e054b0dea17e9643a7a",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "ea17e9643a7a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -96
    },
    {
        "rssi": -73,
        "data": "02010611ff990403341438c94fff0400f5fc560bdd",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "ec032bee090a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -88
    },
    {
        "rssi": -71,
        "data": "02010611ff99040334143ac9cbff0400f1fc570be9",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "ec032bee090a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -73,
        "data": "02010611ff990403331436cb8cff0300f4fc5a0bdd",
        "coordinates": "Saase",
        "rssi_max": -71,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "ec032bee090a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510dd3502c9290004ffbcfc00a376009251ed4dfae75678",
        "coordinates": "Saase",
        "rssi_max": -60,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "ed4dfae75678",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -85
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510de34f3c9a70000ffbcfc04a376009ca8ed4dfae75678",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "ed4dfae75678",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510d434ddcb690000ffbcfc00a45600bc78ed4dfae75678",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "ed4dfae75678",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -54,
        "data": "0201041bff990405100d2a74c99800ccfd00026ca936bdbe69f286691bb05a",
        "coordinates": "Saase",
        "rssi_max": -49,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f286691bb05a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -67
    },
    {
        "rssi": -58,
        "data": "0201041bff99040510342ea9ca1700f8fd080254a7d6bfea18f286691bb05a",
        "coordinates": "Saase",
        "rssi_max": -53,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f286691bb05a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -70
    },
    {
        "rssi": -57,
        "data": "0201041bff9904050fb12ee9cbdf00f0fd100274a8b6bf6d8bf286691bb05a",
        "coordinates": "Saase",
        "rssi_max": -47,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f286691bb05a",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -62
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510a03aadc96eff44009cfbe8b11607b15bf54f92067795",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f54f92067795",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510aa3a9fc9eeff440098fbe8b11607c740f54f92067795",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f54f92067795",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -66,
        "data": "0201041bff990405109c3a94cbb4ff4000a4fbe8b0960708e6f54f92067795",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f54f92067795",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -72,
        "data": "0201061bff9904faa3797e356145e87334001a1d13a9f6c4f5662ffbc8af00",
        "coordinates": "Saase",
        "rssi_max": -69,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f5662ffbc8af",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -91
    },
    {
        "rssi": -72,
        "data": "0201061bff9904fa7a654351c2f761ef134eff55eb3fcab5f5662ffbc8af00",
        "coordinates": "Saase",
        "rssi_max": -70,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f5662ffbc8af",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -70,
        "data": "0201061bff9904fa257f3c836f3966d42b0cdfba09b916a1f5662ffbc8af00",
        "coordinates": "Saase",
        "rssi_max": -69,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f5662ffbc8af",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -67,
        "data": "0201041bff9904051482ffffffff80008000800068f600547ff63a84a8e412",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f63a84a8e412",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -87
    },
    {
        "rssi": -67,
        "data": "0201041bff9904051482ffffffff800080008000a0d600806ff63a84a8e412",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f63a84a8e412",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -67,
        "data": "0201041bff9904051450ffffffff800080008000a0d6000330f63a84a8e412",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f63a84a8e412",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff9904050f0affffffff80008000800068f60054a5f63a84a8e452",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f63a84a8e452",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff9904050ed8ffffffff8000800080009e9600800df63a84a8e452",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f63a84a8e452",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -67,
        "data": "0201041bff9904050ea6ffffffff800080008000a1360002eef63a84a8e452",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f63a84a8e452",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510c53371c9ab80008000800068f6005476f63a84a8e480",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f63a84a8e480",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -81
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510cd3369ca27800080008000a13600802ef63a84a8e480",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f63a84a8e480",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510bb3369cbe9800080008000a1360002fff63a84a8e480",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f63a84a8e480",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510d238bbffff80008000800068f60054a4f63a84a8e4c3",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f63a84a8e4c3",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -83
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510dc38afffff8000800080009e96008014f63a84a8e4c3",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f63a84a8e4c3",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -79
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510c638abffff800080008000a1360002f1f63a84a8e4c3",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f63a84a8e4c3",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -80,
        "data": "0201041bff990405108b2d7ac9fbffe0ffe003fca8b6008f23f772e194d3e6",
        "coordinates": "Saase",
        "rssi_max": -69,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "f772e194d3e6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -93
    },
    {
        "rssi": -70,
        "data": "0201041bff99040510922d7dca77ffecffdc0400a936009978f772e194d3e6",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "f772e194d3e6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -71,
        "data": "0201041bff99040510842d7ccc3bffecffdc0400aa1600b949f772e194d3e6",
        "coordinates": "Saase",
        "rssi_max": -68,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "f772e194d3e6",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -82
    },
    {
        "rssi": -65,
        "data": "0201061bff990405104a297fc95801580050fc3cb6b61f79fbfb974e97de5c",
        "coordinates": "Saase",
        "rssi_max": -59,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "fb974e97de5c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -83
    },
    {
        "rssi": -64,
        "data": "0201061bff99040510542980c9d901580050fc3cb5361fa5fbfb974e97de5c",
        "coordinates": "Saase",
        "rssi_max": -60,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "fb974e97de5c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -64,
        "data": "0201061bff9904051044297fcb9c0154004cfc38b6b61f29c7fb974e97de5c",
        "coordinates": "Saase",
        "rssi_max": -57,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "fb974e97de5c",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -66,
        "data": "0201041bff99040510be315ac93701800154fc70917653cd0cfc4806679b7e",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "fc4806679b7e",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -80
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510bf3143c9b501800150fc70917653f8d6fc4806679b7e",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "fc4806679b7e",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510b93119cb760180014cfc6890f6537c48fc4806679b7e",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "fc4806679b7e",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -76,
        "data": "0201041bff99040510bb2ecdc9caff54ff1403c46a56725360fe79570aefd0",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "fe79570aefd0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -94
    },
    {
        "rssi": -78,
        "data": "0201041bff99040510c12ec5ca45ff50ff1403c8673672d895fe79570aefd0",
        "coordinates": "Saase",
        "rssi_max": -66,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "fe79570aefd0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -97
    },
    {
        "rssi": -80,
        "data": "0201041bff99040510b32e9dcc08ff50ff1403c0697672689cfe79570aefd0",
        "coordinates": "Saase",
        "rssi_max": -72,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "fe79570aefd0",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -89
    },
    {
        "rssi": -90,
        "data": "0201061bff9904fa24c95fc7b4cc11dea63021292bea8b2ffee50c99fefe00",
        "coordinates": "Saase",
        "rssi_max": -85,
        "time": "2020-03-30T00:00:00.000Z",
        "id": "fee50c99fefe",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -94
    },
    {
        "rssi": -93,
        "data": "0201061bff9904faf2f51d93890710176f7e926975f8ee59fee50c99fefe00",
        "coordinates": "Saase",
        "rssi_max": -91,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "fee50c99fefe",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -95
    },
    {
        "rssi": -90,
        "data": "0201061bff9904fa6794b5fd3bd5c546aa192baf5ac73057fee50c99fefe00",
        "coordinates": "Saase",
        "rssi_max": -90,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "fee50c99fefe",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -90
    }
]
```
{% endswagger-response %}
{% endswagger %}

Sample URL: `https://whereos.ruuvi.com/api/ruuvi/coordinates/Saase?p_aggregation=12h`

{% swagger baseUrl="https://whereos.ruuvi.com" path="/api/ruuvi/tag/$TAG" method="get" summary="History of a tag" %}
{% swagger-description %}
Get history data of one tag by MAC address.
{% endswagger-description %}

{% swagger-parameter in="path" name="tag" type="string" %}
MAC address of tag, lower case, no colons.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="p_aggregation" type="string" %}
 Downsample data to interval, default 15m. Valid values are number + s | m | h, e.g. "15m"
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
[
    {
        "rssi": -66,
        "data": "0201041bff990405107f2ddcc9f80000ff1c03f3a2166f19d7c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T09:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -88
    },
    {
        "rssi": -65,
        "data": "0201041bff990405107f2dd4ca0afff8ff1c03eba2f66f1f43c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T10:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510822de2ca440004ff1c03f0a2f66f24cfc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T11:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -76
    },
    {
        "rssi": -63,
        "data": "0201041bff99040510852df0ca490000ff2403f8a2166f2a33c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T12:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -71
    },
    {
        "rssi": -63,
        "data": "0201041bff99040510862df8ca470000ff1c03f3a1366f3012c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T13:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -70
    },
    {
        "rssi": -63,
        "data": "0201041bff990405108a2dfcca450000ff1c03f3a2f66f3525c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T14:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -65
    },
    {
        "rssi": -63,
        "data": "0201041bff990405108d2dffca710004ff1c03f3a2166f3aa6c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T15:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -65
    },
    {
        "rssi": -64,
        "data": "0201041bff990405108f2e07cabc0000ff1c03f8a2f66f402ec04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-30T16:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -67,
        "data": "0201041bff990405108a2dffcb000000ff1803eba2f66f4593c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T17:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -75
    },
    {
        "rssi": -68,
        "data": "0201041bff990405108a2dfccb570000ff1803f0a2f66f4b0fc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T18:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -78
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510882df8cb9afffcff2403f3a2f66f5084c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T19:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -67,
        "data": "0201041bff99040510842df4cbb6fffcff2003f0a2f66f55fcc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -67,
        "time": "2020-03-30T20:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -77
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510802deccbfa0004ff1803f8a2166f5b78c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-30T21:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -64,
        "data": "0201041bff990405107f2de8cc090004ff2003f8a2f66f60f3c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T22:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -64,
        "data": "0201041bff990405107d2de0cc070000ff1c03eba1b66f666dc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-30T23:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510782dd5cc0b0004ff1c03eba2166f6beac04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T00:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510702dc3cbfa0004ff1c03f3a1366f7168c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T01:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -65
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510692db6cc0efffcff2003f8a1b66f76d6c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T02:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -74
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510632daacbec0000ff1c03f3a2166f7c59c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T03:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -66
    },
    {
        "rssi": -64,
        "data": "0201041bff990405105c2d9ecbcafffcff2003f8a2f66f8205c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T04:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510552d93cbc70000ff2003f3a2f66f873cc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T05:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510522d87cba80000ff2003f8a2166f8cb6c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T06:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510512d83cb770000ff2003eba2966f9235c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -64,
        "time": "2020-03-31T07:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -64,
        "data": "0201041bff99040510512d7fcb300000ff1c03f0a1b66f97a9c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -63,
        "time": "2020-03-31T08:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510502d7dcaebfffcff2003f8a2966f9d2cc04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -62,
        "time": "2020-03-31T09:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -73
    },
    {
        "rssi": -65,
        "data": "0201041bff99040510502d7dca5d0000ff1c03f3a2966fa299c04db14ab635",
        "coordinates": "Saase",
        "rssi_max": -65,
        "time": "2020-03-31T10:00:00.000Z",
        "id": "c04db14ab635",
        "gwmac": "30aea4cc1e2f",
        "rssi_min": -65
    }
]
```
{% endswagger-response %}
{% endswagger %}

Sample URL: `https://whereos.ruuvi.com/api/ruuvi/tag/c04db14ab635?p_aggregation=1h`
