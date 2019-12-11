# Heartbeat transmissions

While the GATT connection is established and central has registered to NUS notifications, the sensor will send a heartbeat of current sensor data at the advertisement broadvast interval.

The sensor data is in format 5, however due to GATT transmission payloads being limited to 20 bytes without MTU negotiation the data format is cut at 18 bytes, i.e. MAC address of the tag is not sent. 

The heartbeat transmissions may be omitted when GATT connection is busy, for example during log reads. 

The heartbeats are same data payloads as what is sent over BLE advertisements, and the interval is same as advertisement update interval. 

If the heartbeat can't fit into the 20 bytes of payload of GATT transmission, it will be cut into last data element which fits in whole. For example the Ruuvi Dataformat 5 has 24 bytes of which 6 last bytes are MAC address of the tag.  As the MAC address \(gray\) cannot fit into the payload, it is cut out leaving 18 bytes which are transmitted \(green\).

![Heartbeat data cut to 18 bytes](../../../.gitbook/assets/image%20%288%29.png)

For details on how to parse the data please review the section Data Format 5 / RAWv2.

