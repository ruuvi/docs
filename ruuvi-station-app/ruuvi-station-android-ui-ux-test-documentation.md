# Ruuvi Station Android UI/UX test documentation

Temperature, humidity, pressure: setting allows adjusting unit and resolution**Installation, app info**

UI/UX checklist

Ruuvi Station app adds Ruuvi Station icon on Android OS and iOS home screen. Icon design features a round Ruuvi “eye”.

| App icon shows number of alerts triggered with red counter badge                                     |
| ---------------------------------------------------------------------------------------------------- |
| App configuration available in OS settings: app permissions, language, notifications, sound settings |

QA checklist

App size after installation Android OS: 72 MB iOS: 121.5 MB

| <p>Android OS: notifications, nearby devices</p><p>iOS: Bluetooth, notifications</p> |
| ------------------------------------------------------------------------------------ |
| Android OS: Icon counter badge shows number of triggered alerts                      |
| Icon counter badge is hidden by default                                              |

### **Onboarding**   <a href="#onboarding-hardbreak" id="onboarding-hardbreak"></a>

9 app tour screens shown with ability to swipe left-right between screens followed by 2 login screens.

UI/UX checklist

Screens:

| 2 Dashboard                                          |
| ---------------------------------------------------- |
| 3 Personalise                                        |
| 4 History                                            |
| 5 Alerts                                             |
| 6 Share Sensors (A Ruuvi Gateway router is required) |
| 7 Widgets (A Ruuvi Gateway router is required)       |
| 8 Ruuvi Web App (A Ruuvi Gateway router is required) |
| 9 Almost there! (continue to sign in)                |
|                                                      |
| 1 Benefits                                           |
| 2 Sign in or create a free Ruuvi account             |



QA Checklist

| Matches design                                                                    |
| --------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                            |
| Portrait, landscape modes                                                         |
| Swipe to left/right works                                                         |
| Skip button works                                                                 |
| User is able to minimise Benefits screen to go back to last screen of onboarding  |
| User is able to skip sign in by choosing Continue and No thanks, skip             |
| User is able to go back to Benefits screen from Sign in using back button         |
| App requests following permissions: Bluetooth, Notifications, Location (Android)  |
| Permissions requested on empty dashboard: Notifications, Nearby Devices (Android) |
| Notification permission granted                                                   |
| Notification permission dismissed, will nag for permission again until granted    |
| Notification permission denied, will not ask again                                |
| Bluetooth permission granted                                                      |
| Bluetooth permission denied, will not ask again                                   |
| Nearby devices permission granted                                                 |
| Nearby devices permission denied, will nag for permission again until granted     |

### **Main menu** <a href="#main-menu" id="main-menu"></a>

Main menu gives access to main top level features in app.\
\


UI/UX checklist

Main menu is accessible through top left corner of the app indicated by drawer icon.&#x20;

Tap on drawer icon reveals menu from left side of screen.

Menu tree:&#x20;

| **Top**                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|                                                                                                                                                                                |
| **Menu**                                                                                                                                                                       |
| <p>Add a New Sensor </p><p>App Settings </p><p>About / Help</p><p>Send Feedback</p><p>What to measure with Ruuvi?</p><p>Buy Ruuvi Sensors</p><p>Sign in / My Ruuvi Account</p> |

QA checklist

| Matches design                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Elements scale on various screen sizes                                                                                                                             |
| Portrait, landscape modes                                                                                                                                          |
| Menu is shown on the dashboard view after onboarding is completed (first launch)                                                                                   |
| Menu can be hidden by swipe right on the menu                                                                                                                      |
| Menu is always shown on dashboard view                                                                                                                             |
| When dashboard view enabled swipe from left side of screen only works on dashboard not on cards scene                                                              |
| Add a New Sensor brings to Add a New Sensor view                                                                                                                   |
| App Settings brings to App Settings view                                                                                                                           |
| About / Help brings to About / Help screen                                                                                                                         |
| About / Help screen shows changelog, app version, added sensors, locally stored measurements and database size at the bottom of the screen                         |
| What to measure with Ruuvi opens default mobile browser with URL ruuvi.com/ideas , includes language UTM                                                           |
| Buy Ruuvi Sensors opens default mobile browser with URL[ ruuvi.com](http://ruuvi.com/)/products​, includes language UTM                                            |
| Sign in / My Ruuvi Account is either forwarding user to sign in flow or shows a subpage with signed in user email address and ability to delete account or log out |

### **Add a New Sensor** <a href="#nearby-ruuvi-sensors" id="nearby-ruuvi-sensors"></a>

User is shown a real time list of nearby Bluetooth sensors.



UI/UX checklist

| Tap on any listed tag will create a new Sensor Card and add it to the alphabetical location in cards |
| ---------------------------------------------------------------------------------------------------- |
| Sensors in/out of range are updated using foreground scan interval                                   |
| User has ability to scan Ruuvi sensor with NFC on device that supports NFC scanning                  |
| Ta on Add with NFC (iOS) will enable NFC scanning of sensors on iOS                                  |
| Menu item (main menu): Add a New Sensor                                                              |

QA Checklist

| Matches design                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                           |
| Portrait, landscape modes                                                                                        |
| Sensor shows: Default name (Ruuvi + last 4 of MAC address), dBm value, signal strength using volume indicator    |
| Sensors list sorted according to signal strength (nearest at the top)                                            |
| List entries separated by line                                                                                   |
| If Bluetooth disabled app requests for permission and shows Bluetooth is disabled status                         |
| Arrow at top left: if no existing sensor cards will show NO SENSORS ADDED, PRESS HERE TO ADD SENSORS placeholder |
| If no NFC capability on device the NFC option is hidden                                                          |
| If no existing sensor cards dashboard will show placeholder                                                      |
| Arrow at top left: if sensor cards exist will show previous viewed sensor card                                   |

### **Sensor Cards** <a href="#sensor-card" id="sensor-card"></a>

\
Sensor Card will be created when the user taps on the sensor in Add a New Sensor screen or when the user adds sensor by scanning it with NFC.&#x20;

Alternatively sensor cards can be synchronized from Ruuvi Cloud cloud service when a user is signed in to the application.

Sensor Card shows information regarding a Ruuvi sensor, this can be either real time Bluetooth sensor data or synchronized cloud sensor data.

Ruuvi Station mobile has three different kinds of sensor cards:



| Image view (dashboard)  |
| ----------------------- |
| Simple view (dashboard) |
| Full image view         |

\


UI/UX checklist

Image view (dashboard) card elements:



|                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Top**                                                                                                                                                 |
| <p>Sensor name<br>Alert indicator<br>Three Dots Menu</p>                                                                                                |
| **Main**                                                                                                                                                |
| <p>Sensor background image <br>Temperature<br>Humidity <br>Air Pressure <br>Movements <br>Data Source <br>Last updated <br>Battery status indicator</p> |

Temperature, Humidity, Air Pressure units and their resolution can be set in App Settings.

\
QA Checklist

| Matches design                                                                                          |
| ------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                  |
| Portrait, landscape modes                                                                               |
| Alert indicator not visible when disabled                                                               |
| Alert indicator blinking when alert triggered                                                           |
| Alert indicator bell when alert enabled                                                                 |
| Tap on sensor card opens Full image view or History view according to selected Card action in View menu |
| Sensor name shown as non-capitalized, in single line                                                    |
| Sensor name shows Ruuvi + 4 last of MAC address as default                                              |
| Long tag name adapts to fit screen                                                                      |
| Can use emoticon as name                                                                                |
| Name will not link URL or code                                                                          |
| Value separator uses localization: ie comma for EU, dot for US                                          |
| Temperature uses units set in App Settings/Temperature unit                                             |
| Temperature uses resolution set in App Settings/Temperature                                             |
| Humidity uses units set in App Settings/Humidity unit                                                   |
| Humidity uses resolution set in App Settings/Humidity                                                   |
| Pressure uses units set in App Settings/Pressure unit                                                   |
| Pressure uses resolution set in App Settings/Pressure                                                   |
| Updated ago shows values in h/m/s/ or date + h/m/s                                                      |
| Updated ago uses foreground interval for Bluetooth sensor when app in foreground                        |
| Data source shows Bluetooth icon or Gateway icon depending on where last datapoint was received         |
| Adding/removing sensor reflects on Sensor Card list                                                     |
| Renaming sensor reflects on Sensor Card                                                                 |
| Sensors organize to alphabetical order automatically by default                                         |

Simple view (dashboard) card elements:

|                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------- |
| **Top**                                                                                                                     |
| <p>Sensor name<br>Alert indicator<br>Three Dots Menu</p>                                                                    |
| **Main**                                                                                                                    |
| <p>Temperature<br>Humidity <br>Air Pressure <br>Movements <br>Data Source <br>Last updated <br>Battery status indicator</p> |

Temperature, Humidity, Air Pressure units and their resolution can be set in App Settings.

QA Checklist

| Matches design                                                                                          |
| ------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                  |
| Portrait, landscape modes                                                                               |
| Alert indicator not visible when disabled                                                               |
| Alert indicator blinking when alert triggered                                                           |
| Alert indicator bell when alert enabled                                                                 |
| Tap on sensor card opens Full image view or History view according to selected Card action in View menu |
| Sensor name shown as non-capitalized, in single line                                                    |
| Sensor name shows Ruuvi + 4 last of MAC address as default                                              |
| Long tag name adapts to fit screen                                                                      |
| Can use emoticon as name                                                                                |
| Name will not link URL or code                                                                          |
| Value separator uses localization: ie comma for EU, dot for US                                          |
| Temperature uses units set in App Settings/Temperature unit                                             |
| Temperature uses resolution set in App Settings/Temperature                                             |
| Humidity uses units set in App Settings/Humidity unit                                                   |
| Humidity uses resolution set in App Settings/Humidity                                                   |
| Pressure uses units set in App Settings/Pressure unit                                                   |
| Pressure uses resolution set in App Settings/Pressure                                                   |
| Updated ago shows values in h/m/s/ or date + h/m/s                                                      |
| Updated ago uses foreground interval for Bluetooth sensor when app in foreground                        |
| Data source shows Bluetooth icon or Gateway icon depending on where last datapoint was received         |
| Adding/removing sensor reflects on Sensor Card list                                                     |
| Renaming sensor reflects on Sensor Card                                                                 |
| Sensors organize to alphabetical order automatically by default                                         |

Full image view card elements:

|                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Top**                                                                                                                                            |
| <p>Ruuvi logo <br>Alert indicator <br>Charts icon <br>Sensor Card settings icon</p>                                                                |
| **Main**                                                                                                                                           |
| <p>Sensor Name <br>Temperature <br>Humidity <br>Air Pressure <br>Data source <br>Last updated<br>Battery status indicator <br>Background image</p> |

Temperature, Humidity, Air Pressure units can be set in App Settings.

QA Checklist

| Matches design                                                                                          |
| ------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                  |
| Portrait, landscape modes                                                                               |
| Alert indicator greyed when disabled                                                                    |
| Alert indicator blinking when alert triggered                                                           |
| Alert indicator bell when alert enabled                                                                 |
| Tap on sensor card opens Full image view or History view according to selected Card action in View menu |
| Sensor name shown as non-capitalized, in single line                                                    |
| Sensor name shows Ruuvi + 4 last of MAC address as default                                              |
| Long tag name adapts to fit screen                                                                      |
| Can use emoticon as name                                                                                |
| Name will not link URL or code                                                                          |
| Value separator uses localization: ie comma for EU, dot for US                                          |
| Temperature uses units set in App Settings/Temperature unit                                             |
| Temperature uses resolution set in App Settings/Temperature                                             |
| Humidity uses units set in App Settings/Humidity unit                                                   |
| Humidity uses resolution set in App Settings/Humidity                                                   |
| Pressure uses units set in App Settings/Pressure unit                                                   |
| Pressure uses resolution set in App Settings/Pressure                                                   |
| Updated ago shows values in h/m/s/ or date + h/m/s                                                      |
| Updated ago uses foreground interval for Bluetooth sensor when app in foreground                        |
| Data source shows Bluetooth icon or Gateway icon depending on where last datapoint was received         |
| Adding/removing sensor reflects on Sensor Card list                                                     |
| Renaming sensor reflects on Sensor Card                                                                 |
| Sensors organize to alphabetical order automatically by default                                         |



### **Dashboard** <a href="#dashboard" id="dashboard"></a>

Dashboard is the default home screen in the app.

If user doesn't yet have any sensors added, app will show an empty placeholder that will suggest user to add sensors. If user has previously signed in to the app but logged out app will show an empty placeholder that will suggest user to sign in or to add sensors.\
\


UI/UX checklist

Dashboard elements:\
\


| **Top**                                                      |
| ------------------------------------------------------------ |
| <p>Main Menu</p><p>Ruuvi logo</p><p>View Menu</p>            |
| **Main (no sensor cards)**                                   |
| <p>Add a Sensor<br>Sign in</p>                               |
| **Main (sensor cards)**                                      |
| <p>Sensor card (image card)<br>Sensor card (simple card)</p> |

Tap on any sensor card  on dashboard will open either Full image view or History view. View action can be selected in View Menu.

QA checklist

| Matches design                                                                    |
| --------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                            |
| Portrait, landscape modes                                                         |
| Main menu in Sensor Card view has been replaced with Back button                  |
| Back button in Sensor Card view will bring back to Dashboard                      |
| Scrollable                                                                        |
| If user has no sensors added a placeholder is shown                               |
| Placeholder when user not signed in previously shows Add a sensor button          |
| Placeholder when user signed in previously shows Sign in and Add a sensor buttons |
| Changing temperature units in App Settings reflects on dashboard                  |
| Changing temperature resolution in App Settings reflects on dashboard             |
| Changing humidity units in App Settings reflects on dashboard                     |
| Changing humidity resolution in App Settings reflects on dashboard                |
| Changing pressure units in App Settings reflects on dashboard                     |
| Changing pressure resolution in App Settings reflects on dashboard                |
| Adding/removing sensor reflects on dashboard                                      |
| Renaming sensor in Sensor Settings reflects on dashboard                          |
| Sensors organize to alphabetical order automatically by default                   |

### **Sensor Settings** <a href="#sensor-settings" id="sensor-settings"></a>

\
Sensor Settings contains settings and information regarding a single sensor.

\
UI/UX checklist\
\
Sensor Settings are accessed via three dots menu on Dashboard or gear icon on the Full Sensor Card. Sensor card settings show sensor information.

Sensor Settings elements:&#x20;

| **Top**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Back to Sensor Card view (arrow icon)<br>Background image</p>                                                                                                                                                                                                                                                                                                                                                                                                     |
| **Main**                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <p>Background image (Android)<br>Name<br>Owner<br>Owner’s Ruuvi Plan (when signed in and shared sensor)<br>Share (when signed in and sensor owner)<br>Bluetooth Connection (iOS only)<br>Alerts<br>Temperature</p><p>Air Humidity</p><p>Air Pressure</p><p>Signal Strength</p><p>Movement</p><p>Connection (iOS)</p><p>Cloud Connection (when signed in)<br>Offset Correction</p><p>Temperature</p><p>Humidity</p><p>Pressure<br>More info<br>Firmware<br>Remove</p> |

QA Checklist

| Matches design                                                                                                                                                                                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                                                                                                                          |
| Portrait, landscape modes                                                                                                                                                                                       |
| Back icon exists to Sensor Card                                                                                                                                                                                 |
| Default Ruuvi background image is set on sensor card creation                                                                                                                                                   |
| Permissions to use camera/access gallery is requested when first time accessing camera icon on background image subpage                                                                                         |
| User can choose from a collection of default images                                                                                                                                                             |
| User can take photo using device camera                                                                                                                                                                         |
| User can choose image from device internal/external location                                                                                                                                                    |
| Supported image file formats: jpg, png, typical image formats supported by device. When no support error displayed                                                                                              |
| Image automatically scaled to fit various screen sizes, portrait/landscape                                                                                                                                      |
| Default sensor name is Ruuvi + last 4 of MAC address                                                                                                                                                            |
| Sensor Name supports max 32 characters                                                                                                                                                                          |
| Sensor Name supports emoticons                                                                                                                                                                                  |
| Sensor Name displayed on single row                                                                                                                                                                             |
| Sensor Name plain text (blocks URL, code)                                                                                                                                                                       |
| Sensor Name if set to empty will show default name as placeholder                                                                                                                                               |
| Alerts include alert type, enable/disable, custom description, value range, value set                                                                                                                           |
| User can configure alert even when alert is disabled                                                                                                                                                            |
| Setting alert disabled remembers previously set range values                                                                                                                                                    |
| Movement alert only enable/disabled                                                                                                                                                                             |
| Cloud Connection alert uses set value                                                                                                                                                                           |
| Offset Correction is available for Temperature, Humidity and Pressure. If no sensor onboard RuuviTag the offset is greyed out for the specific sensor                                                           |
| Setting offset will compare difference between original measured value and value that user filled as current known value.                                                                                       |
| Setting an offset will reflect everywhere in the app for values reported by the specific sensor on this specific RuuviTag                                                                                       |
| Offset will also reflect on values sent by app gateway (Android) and csv file export                                                                                                                            |
| Offset is recorded to Ruuvi Cloud and synced between devices                                                                                                                                                    |
| Offset is used for sensor that is shared via Ruuvi Cloud                                                                                                                                                        |
| More info shows MAC address, data format, data received via, battery voltage [x.xxx](http://x.xxx/), acceleration xyz [x.xxx](http://x.xxx/) , tx power, signal strength (RSSI) and measurement sequence number |
| MAC address can be copied to clipboard                                                                                                                                                                          |
| Firmware shows current version                                                                                                                                                                                  |
| If sensor doesn't report current version will show as Old Firmware                                                                                                                                              |
| If old firmware in data format 3 user will be shown update popup every time when accessing the sensor settinggs page                                                                                            |
| Tap on Update firmware opens a subpage which checks latest firmware version from Ruuvi network and compares it with one on sensor                                                                               |
| If old firmware subpage suggests to update according to instructions on the page                                                                                                                                |
| If latest firmware will report no need to update                                                                                                                                                                |
| Remove this sensorbutton opens confirmation: Remove sensor Are you sure you want to remove this sensor? You can add it again later, if needed. Cancel, Confirm                                                  |
| Removing sensor deletes sensor card from it’s location in sensor cards                                                                                                                                          |

### **History view** <a href="#charts" id="charts"></a>

History view visualizes temperature, humidity and air pressure in charts.

\
UI/UX checklist

History view is accessed by tap on sensor card (dashboard) when user has set card action to Open history view in View menu, choosing History view from three dots menu or by pressing charts icon on Sensor Card. History View contains Temperature, Humidity, Pressure charts. Temperature, Humidity, Air Pressure units and their resolution can be set in App Settings and they reflect on Charts X,Y values. Charts also uses Chart Settings in App Settings and calibration settings in Sensor Settings for specific sensor.

History view also contains button to sync sensor history from RuuviTag internal memory via Bluetooth and export for exporting collected sensor history into a csv file.\
\


Charts elements:

| **Top**                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>Sensor Name<br>Move to next/previous sensor card<br>Sync sensor history from Bluetooth<br>View selector<br>Three dots menu</p>                                  |
| **Main**                                                                                                                                                           |
| Chart temperature, values X,Y, min/max/avg for current viewport (when min/max/avg set to visible in three dots menu), latest datapoint, tap to view datapoint info |
| Chart humidity, values X,Y, min/max/avg for current viewport (when min/max/avg set to visible in three dots menu), latest datapoint, tap to view datapoint info    |
| Chart pressure, values X,Y, min/max/avg for current viewport (when min/max/avg set to visible in three dots menu), latest datapoint, tap to view datapoint info    |

QA checklist

| Matches design                                                                      |
| ----------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                              |
| Portrait, landscape modes                                                           |
| On landscape mode user will see 1 chart and can scroll down/up to view other charts |
| Tap on charts icon exists to Sensor Card                                            |
| Tap on arrows moves to previous/next sensor card                                    |
| If last or first card only one arrow available                                      |
| Values use localization (ie comma for EU, dot for US)                               |
| Chart settings (set in App Settings) reflect on History view                        |
| Temperature units (set in App Settings) reflect on History view                     |
| Pressure units (set in App Settings) reflect on History view                        |
| Calibration settings (set in Sensor Settings) reflect on History view               |
| Pinch to zoom in/out navigates on charts                                            |
| Pinch to zoom adjusts zoom value on all charts regardless of which chart is zoomed  |
| Tap on datapoint shows info for selected datapoint in chart                         |

### **App Settings** <a href="#app-settings" id="app-settings"></a>

App Settings contains global settings for Ruuvi Station.\
\


UI/UX checklist

App Settings is accessed via main menu item App Settings.

Menu tree:

| <p>Language<br>Appearance<br>Alert Notifications<br>Background Scanning<br>Temperature<br>Humidity<br>Pressure<br>Ruuvi Cloud<br>Chart Settings<br>Data Forwarding (Android only)<br>Defaults (internal only)</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

QA checklist\
\


| Matches design                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Elements scale on various screen sizes                                                                                                                                                                                                                                       |
| Portrait, landscape modes                                                                                                                                                                                                                                                    |
| App settings: changes are saved when app killed                                                                                                                                                                                                                              |
| App settings: unit settings are synced from cloud                                                                                                                                                                                                                            |
| Language: user will be forwarded to app language settings in OS                                                                                                                                                                                                              |
| Language: app language may differ from OS language (iOS and Android OS 13 or higher)                                                                                                                                                                                         |
| Appearance: appearance setting follow system theme when system selected                                                                                                                                                                                                      |
| Appearance: light or dark theme matches design                                                                                                                                                                                                                               |
| Alert notifications: when enabked Bluetooth alert will trigger 1 time per 1 hour even if it was retriggered.                                                                                                                                                                 |
| Alert notifications: alert sound forwards to sound alert settings in Android OS                                                                                                                                                                                              |
| Alert notifications: alert sound opens it's own subpage in iOS                                                                                                                                                                                                               |
| Background scanning: When enabled app will collect data points according to the selected interval when app is minimized in the background                                                                                                                                    |
| Background scanning: In iOS app user will need to also pair sensor in Sensor Settings in order for data points to be recorded according to this interval                                                                                                                     |
| Background scanning: When disabled no data points will be collected when app minimised                                                                                                                                                                                       |
| Background scanning: default enabled, data logging interval 5 mins                                                                                                                                                                                                           |
| Background scanning: Some Android devices optimise heavily for battery usage and may snooze apps running in the background, which effects background scanning                                                                                                                |
| Background scanning: Removing optimisation features will make app record data points in background smoothly                                                                                                                                                                  |
| Background scanning: switches between foreground/background                                                                                                                                                                                                                  |
| Background scanning: scan interval is reflected in CSV export                                                                                                                                                                                                                |
| <p>Background scanning: background scanning enabled Ruuvi icon appears at top left of device screen when app minimized to indicate scanning is on<br>Background scanning: notification drawer will display sticky notification for scanning interval Scanning every m-s.</p> |
| Temperature, humidity, pressure: setting allows adjusting unit and resolution                                                                                                                                                                                                |
| Temperature, humidity, pressure: setting reflects everywhere in app and also in CSV export                                                                                                                                                                                   |
| Chart settings: show all measurements will draw all recorded datapoints to history view page                                                                                                                                                                                 |
| Chart settings: show datapoints will add points to all recorded datapoints on Android OS                                                                                                                                                                                     |
| Data forwarding: user gives URL in correct format -  app will use app internal interval to send data with POST                                                                                                                                                               |
| Data forwarding: device identifier is free text, a pre-generated id is shown by default                                                                                                                                                                                      |
| Data forwarding: sending location coordinates of device with data adds location data to POST                                                                                                                                                                                 |
| Data forwarding: beta feature forward data while syncing works                                                                                                                                                                                                               |
| Data forwarding: test data forwarding button gives either error or success for HTTP POST attempt                                                                                                                                                                             |
| Data forwarding: URL allows max 200 characters                                                                                                                                                                                                                               |
| Data forwarding: Device identifier allows max 64 characters                                                                                                                                                                                                                  |
| Defaults: normally hidden and not available in production builds                                                                                                                                                                                                             |
| Defaults: internal testing features and settings                                                                                                                                                                                                                             |

\




