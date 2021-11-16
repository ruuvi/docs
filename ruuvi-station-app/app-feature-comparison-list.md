# App Feature Comparison list

This document is to compare features that are in the current development to highlight differences between iOS and Android platforms. Identical features will be removed from this list.\
\
Updated 15.1.2021\
\
Item listed in italic: naming difference\
”-” : missing feature/item

### &#x20;Adding A New Sensor <a href="hardbreak-adding-a-new-sensor" id="hardbreak-adding-a-new-sensor"></a>

This screen is very different in both apps: Android version provides a highly simplified functionality.\
\


| **Item**          | **iOS**                                                                                                                                                                      | **Android**                                                               |   |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | - |
| Virtual Sensors   | <p>More info popup <img src="https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/atlassian/info_32.png" alt=":info:"><br>Pick from the map<br>Your location</p> | <p>-<br>-<br>-</p>                                                        |   |
| Nearby sensors    | <p>Connectable sensor icon<br>dBm + signal strength icon<br>Name: <em>Ruuvi xxxx</em><br>Buy sensors link</p>                                                                | <p>-<br>dBm + signal strength icon<br>Name: <em>MAC address</em><br>-</p> |   |
| Adding new sensor | Adds new sensor card, opens sensor card                                                                                                                                      | Adds new sensor card, opens sensor settings                               |   |

### Sensor Card <a href="sensor-card" id="sensor-card"></a>

This screen is highly similar in both apps, only minor differences remain

| **Item**                           | **iOS**                                                                                                                                                  | **Android**                                                                                                                          |   |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | - |
| Elements on page (new sensor card) | <p>-(connectable sensors)<br>Graphs<br>Sensor Settings<br>Sensor Name<br>Temperature<br>Humidity<br>Air Pressure<br>RSSI<br>Connected<br>Updated ago</p> | <p>Alert icon<br>Graphs<br>Sensor Settings<br>Sensor Name<br>Temperature<br>Humidity<br>Air Pressure<br>RSSI<br>-<br>Updated ago</p> |   |
| Graphs                             | <p>Graph Temp<br>Graph Humidity<br>Graph Air Pressure<br>Clear button<br>Sync button<br>Export</p>                                                       | <p>Graph Temp<br>Graph Humidity<br>Graph Air Pressure<br>Clear button<br>Sync button<br>-</p>                                        |   |

### Sensor Settings <a href="sensor-settings" id="sensor-settings"></a>

Contains various differences, mainly related to custom alerts and sensor info. Connectable sensors are coming to Android soon.

| **Item** | **iOS** | **Android** |   |
| -------- | ------- | ----------- | - |

| **Item**   | **iOS**                                                                                                                                                                                                                                                                                                            | **Android**                                                                                                                                  |   |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- | - |
| Name       | <p><em>Ruuvi xxxx</em><br>20 chars</p>                                                                                                                                                                                                                                                                             | <p><em>MAC Address</em><br>32 chars</p>                                                                                                      |   |
| Connection | <p>Keep Connection<br>Connected</p>                                                                                                                                                                                                                                                                                | <p>-<br>-</p>                                                                                                                                |   |
| Alerts     | <p>More info popup <img src="https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/atlassian/info_32.png" alt=":info:"><br>On/Off<br>Temperature<br><em>Air Humidity</em><br>Air Pressure<br><em>Connection</em><br>Movement<br>Custom alert descriptions<br>Alert types (changeable from settings)</p> | <p>-<br>On/Off<br>Temperature<br><em>Relative Air Humidity</em><br>Air Pressure<br><em>Signal strength (RSSI)</em><br>Movement<br>-<br>-</p> |   |
| More info  | <p>More info popup <img src="https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/atlassian/info_32.png" alt=":info:"><br>UUID<br>Data Format<br>Data Received Via<br>Tx Power<br>Movement Counter<br>Measurement Seq Number</p>                                                                       | <p>-<br>-<br>-<br>-<br>-<br>-<br>-</p>                                                                                                       |   |
| Remove     | _Remove_                                                                                                                                                                                                                                                                                                           | _Remove Sensor_                                                                                                                              |   |
| Other      | -                                                                                                                                                                                                                                                                                                                  | Export sensor data button                                                                                                                    |   |

### General non-specific <a href="general-non-specific" id="general-non-specific"></a>

| **Item**          | **iOS**                                                  | **Android**                             |   |
| ----------------- | -------------------------------------------------------- | --------------------------------------- | - |
| In-app guides     | Add second sensor first time shows swipe guide animation | <p>-<br><br></p>                        |   |
| App optimizations | -                                                        | User disables app/battery optimizations |   |

### Settings <a href="settings" id="settings"></a>

Layouts are quite different: iOS uses multi-level menu approach where as Android provides a single-level menu. Many naming differences remain.

| **Item**    | **iOS** | **Android**         |   |
| ----------- | ------- | ------------------- | - |
| Dashboard   | -       | Dashboard feature   |   |
| App Gateway | -       | Gateway URL feature |   |
