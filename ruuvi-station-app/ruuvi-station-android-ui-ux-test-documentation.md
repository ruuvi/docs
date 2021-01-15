# Ruuvi Station Android UI/UX test documentation

**Installation, app info**

UI/UX checklist

Ruuvi Station app adds Ruuvi Station icon on Android home screen. Design features a round Ruuvi “eye”.

| App icon shows number of alerts triggered with red counter badge App configuration \(permissions, notifications\) accessible through Apps in Android OS. |
| :--- |
| App icon shows number of alerts triggered with red counter badge App configuration \(permissions, notifications\) accessible through Apps in Android OS. |

QA checklist

Ruuvi Station app takes about 34MB space after installation

| Default notifications: allowed |
| :--- |
| Default permissions \(requested during onboarding\): location |
| Additional permissions: Bluetooth |
| Icon counter badge shows number of triggered alerts |
| Icon counter badge is hidden by default |

### **Onboarding**   <a id="Onboarding[hardBreak]"></a>

Six introductions screens shown with ability to swipe left-right between screens.

UI/UX checklist

Screens:

| 1 WELCOME FRIEND . Swipe to see what Ruuvi Station can do for you |
| :--- |
| 2 Measure environmental data: temperature, relative humidity and air pressure Icon: thermometer |
| 3 Access data for each linked sensor in real time and explore history charts Icon: charts |
| 4 Set alerts and get notified whenever your limits are hit Icon: bell |
| 5 Let the app act as a gateway Icon: download cloud |
| 6 LET’S GET STARTED . Press SCAN to find and add nearby sensors to your Ruuvi Station Button: SCAN |

App will ask for permissions after showing disclaimer popup:

  
Popup:

Enable Bluetooth Scanning

In order to scan nearby Bluetooth devices, Android requires location access to be enabled. Ruuvi Doesn’t track your movements. You’re safe.  
Button: OK

Permissions requested:

| allow Bluetooth |
| :--- |
| allow Location |

QA Checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Swipe to left/right works |
| Button SCAN progress to permissions popup Shown only once after first launch, never show on app update Tap on OK is only way to exit permissions popup |
| App requests following permissions: location, Bluetooth |
| Permissions requested on Nearby Ruuvi Sensors screen |
| Location permission granted |
| Location permission denied, will nag for permission again until granted |
| Bluetooth permission granted |
| Bluetooth permission denied, will nag for permission again until granted |

### **Main menu** <a id="Main-menu"></a>

Main menu gives access to main top level features in app.  
  


UI/UX checklist

Main menu is accessible through top left corner of the app indicated by drawer icon. 

Tap on drawer icon reveals menu from left side of screen.

Menu tree: 

| **Top** |
| :--- |
| Ruuvi Logo |
| **Menu** |
| Add a New Sensor App Settings About / Help Get More Sensors |

QA checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Menu is shown after onboarding is completed on cards scene \(first launch\). |
| Menu can be revealed by swipe from left side of screen |
| Menu can be hidden by swipe right on the menu |
| Menu is shown on dashboard view |
| When dashboard view enabled swipe from left side of screen only works on dashboard not on cards scene |
| Add a New Sensor brings to Nearby Ruuvi Sensors view |
| App Settings brings to App Settings view |
| About / Help brings to About / Help screen |
| About / Help screen shows version, seen sensors, added sensors, stored measurements and database size at the bottom of the screen |
| Get More Sensors opens default mobile browser with URL [ruuvi.com](http://ruuvi.com/) |

### **Nearby Ruuvi Sensors** <a id="Nearby-Ruuvi-Sensors"></a>

User is shown a real time list of nearby sensors.

UI/UX checklist

| Tap on any listed tag will create a new Sensor Card and add it to the rightmost location in cards. |
| :--- |
| Sensors in/out of range are updated using foreground scan interval. |
| Menu item \(main menu\): Add a New Sensor |

QA Checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Sensor shows: MAC address, dBm value, signal strength using blue volume indicator |
| Sensors list sorted according to signal strength \(nearest at the top\) |
| List entries separated by line |
| If Bluetooth disabled app requests for permission |
| Arrow at top left: if no existing sensor cards will show NO SENSORS ADDED, PRESS HERE TO ADD SENSORS placeholder |
| Arrow at top left: if sensor cards exist will show previous viewed sensor card |

### **Sensor Card** <a id="Sensor-Card"></a>

  
Sensor card will be created when user taps on sensor in Nearby Ruuvi Sensors screen. Sensor card shows realtime information regarding a sensor.

UI/UX checklist

Sensor card elements: 

|  |
| :--- |
| **Top** |
| Ruuvi logo Alert indicator Charts icon Sensor Card settings icon |
| **Main** |
| Sensor Name Temperature Humidity Air Pressure Signal Strength Last updated Background image |

Temperature, Humidity, AirPressure units can be set in App Settings.

  
QA Checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Ruuvi logo |
| Alert indicator greyed when disabled |
| Alert indicator blinking when alert triggered |
| Alert indicator bell when alert enabled |
| Charts icon thermometer by default, charts icon when switched to charts view |
| Sensor Card Settings opens sensor settings screen in full screen mode |
| Sensor name shown as capitalized, in single line |
| Sensor name shows MAC address as default |
| Long tag name shortens with … to fit on screen |
| Can use emoticon as name |
| Name will not link URL or code |
| Value separator uses localization: ie comma for EU, dot for US |
| Temperature shown with xx,xx value \(current fw\) |
| Temperature uses units set in App Settings/Temperature unit |
| Humidity shown with xx.xx value \(current fw\) |
| Humidity uses units set in App Settings/Humidity unit |
| Pressure shown with xx.xx value \(current fw\) |
| Pressure uses units set in App Settings/Pressure unit |
| Signal strength shows dBm value -100 - 0 |
| Updated ago shows values in h/m/s/ or date + h/m/s |
| Updated ago uses foreground interval when app in foreground |
| Adding/removing sensor reflects on Sensor Card list |
| Renaming sensor in Sensor Settings reflects on Sensor Card |

### **Dashboard** <a id="Dashboard"></a>

When Dashboard enabled in App Settings, a list of sensors will be shown as new home screen.

Notice! This requires killing app and restarting it.  
  


UI/UX checklist

Dashboard elements:  
  


| **Top** |
| :--- |
| Main Menu |
| Ruuvi Logo |
| **Main** |
| Sensor Avatar \(round circle contains first letter of sensor name\) |
| Sensor Name |
| Alert status |
| Temperature icon, temperature |
| Humidity icon, humidity |
| Air pressure icon, air pressure |
| Signal strength icon, signal strength |
| Updated, real time status |

Tap on any row will open the respective Sensor Card view.

QA checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Main menu in Sensor Card view has been replaced with Back button |
| Back button in Sensor Card view will bring back to Dashboard |
| Scrollable |
| Changing temperature units in App Settings reflects on dashboard |
| Changing humidity units in App Settings reflects on dashboard |
| Changing pressure units in App Settings reflects on dashboard |
| Adding/removing sensor reflects on dashboard |
| Renaming sensor in Sensor Settings reflects on dashboard |

### **Sensor Settings** <a id="Sensor-Settings"></a>

  
Sensor Settings contains settings and information regarding a single sensor.

  
UI/UX checklist  
Sensor Settings is accessed via gears icon on Sensor Card. Sensor card settings shows sensor information, alerts and real time voltage/acceleration information.

Sensor Settings elements: 

| **Top** |
| :--- |
| Back to Sensor Card view \(arrow icon\) |
| Export data to file \(export icon\) |
| Background image |
| Background image random button |
| Background image take photo/choose from gallery |
| **Main** |
| Sensor Name |
| Alerts |
| More info |
| Calibrate hygrometer button |
| Button: Remove this Ruuvitag |

QA Checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">Matches design</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Elements scale on various screen sizes</td>
    </tr>
    <tr>
      <td style="text-align:left">Portrait, landscape modes</td>
    </tr>
    <tr>
      <td style="text-align:left">Back icon exists to Sensor Card</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Export icon creates csv datafile and opens export options</p>
        <p>CSV file contains: timestamp yyy-mm-dd hh-mm-ss-timezone, temperature
          <a
          href="http://xxx.xxx/">xxx.xxx</a>, humidity xxx.xxxx, pressure, rssi, acceleration x <a href="http://x.xxx/">x.xxx</a>,
            acceleration y <a href="http://x.xxx/">x.xxx</a>, acceleration z <a href="http://x.xxx/">x.xxx</a>,
            voltage <a href="http://x.xxx/">x.xxx</a>, movement counter, measurement
            sequence number</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Random background image is set on sensor card creation</td>
    </tr>
    <tr>
      <td style="text-align:left">Background image reload icon cycles between default images</td>
    </tr>
    <tr>
      <td style="text-align:left">Background image camera icon opens camera/or gallery</td>
    </tr>
    <tr>
      <td style="text-align:left">Permissions to use camera/access gallery is requested when first time
        accessing camera icon</td>
    </tr>
    <tr>
      <td style="text-align:left">Camera can take photo using device camera</td>
    </tr>
    <tr>
      <td style="text-align:left">User can bring image from device internal/external location</td>
    </tr>
    <tr>
      <td style="text-align:left">Supported image file formats: jpg, png, when no support error displayed</td>
    </tr>
    <tr>
      <td style="text-align:left">Image automatically scaled to fit various screen sizes, portrait/landscape</td>
    </tr>
    <tr>
      <td style="text-align:left">Default sensor name is device MAC address</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensor Name supports max 30 characters</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensor Name supports emoticons</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensor Name displayed on single row</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensor Name plain text (blocks URL, code)</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensor Name cannot be empty, if empty will show MAC address</td>
    </tr>
    <tr>
      <td style="text-align:left">Alerts include alert type, value range, enable/disable box</td>
    </tr>
    <tr>
      <td style="text-align:left">Setting alert enabled allows user to adjust range values</td>
    </tr>
    <tr>
      <td style="text-align:left">Setting alert disabled remembers previously set range values</td>
    </tr>
    <tr>
      <td style="text-align:left">Movement alert only enable/disabled</td>
    </tr>
    <tr>
      <td style="text-align:left">More info shows MAC address, voltage <a href="http://x.xxx/">x.xxx</a>,
        acceleration xyz <a href="http://x.xxx/">x.xxx</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Calibrate hygrometer opens popup:</p>
        <p>In order to measure relative humidity as accurately as possible, a sodium
          chloride (salt) calibration is recommended. See video tutorials (link)
          on how to easily do it at home. Note that calibration data will be stored
          locally on your mobile device. After Ruuvi Station uninstall &amp; reinstall
          you may need to recalibrate.
          <br />
          <br />Calibration value xx% -&gt; xx%</p>
        <p>Cancel, Calibrate</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">If hygrometer calibration exists, calibrated timestamp shown and clear
        calibration option enabled</td>
    </tr>
    <tr>
      <td style="text-align:left">Remove button opens confirmation: Remove sensor Are you sure you want
        to remove this sensor? Cancel, OK</td>
    </tr>
    <tr>
      <td style="text-align:left">Removing sensor deletes sensor card from it&#x2019;s location in sensor
        cards</td>
    </tr>
  </tbody>
</table>

### **Charts** <a id="Charts"></a>

Charts visualizes temperature, humidity and air pressure in charts view.

  
UI/UX checklist

Charts view is accessed pressing charts icon on Sensor Card. View contains Temperature, Humidity, Pressure charts. Temperature, Humidity, Air Pressure units can be set in App Settings and they reflect on Charts X,Y values. Charts also uses Chart Settings in App Settings.  
  


Charts elements:

| **Top** |
| :--- |
| Sensor Name |
| **Main** |
| Chart temperature, values X,Y |
| Chart humidity, values X,Y |
| Chart pressure, values X,Y |

QA checklist

| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Tap on charts icon exists to Sensor Card |
| Values use localization \(ie comma for EU, dot for US\) |
| Chart settings \(set in App Settings\) reflect on Charts |
| Temperature units \(set in App Settings\) reflect on Charts |
| Pressure units \(set in App Settings\) reflect on Charts |
| Pinch to zoom in/out navigates on charts |
| Pinch to zoom adjusts zoom value on all charts regardless of which chart is zoomed |

### **App Settings** <a id="App-Settings"></a>

App Settings contains global settings for Ruuvi Station, including background scanning, temperature and humidity units, gateway and chart settings as well as enable/disable dashboard.  
  


UI/UX checklist

App Settings is accessed via main menu item App Settings.

Menu tree:

| Background Scanning Settings |
| :--- |
| Temperature unit |
| Humidity unit |
| Pressure unit |
| Dashboard |
| Gateway Settings |
| Chart Settings \(text: Configure interval between points shown on chart\) |

QA checklist  
  


| Matches design |
| :--- |
| Elements scale on various screen sizes |
| Portrait, landscape modes |
| Chosen background scanning method shown |
| Chosen temperature unit shown |
| Chosen humidity unit shown |
| Chosen pressure unit shown |
| Dashboard toggle enabled/disabled |
| Gateway url shown |

  
_Background scanning settings_  
  


Settings for background scanning. 

UI/UX checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>No background scanning</p>
        <p>Explainer: This feature enables background scanning, meaning that your
          phone will periodically search for beacons, even when you are not using
          it.</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Continuous background scanning</p>
        <p>Explainer: The app will periodically search for beacons using a service
          (with notifications), allowing for a very frequent and reliable scanning,
          even when you are not using it.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Background scanning interval</p>
        <p>Interval selector shown with two up/down scrolling wheels with titles
          <br
          />Minutes, Seconds (min 0:10 max 59:59)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Background scan important note</p>
        <p>If you experience any issues with background scanning you should disable
          battery optimization for Ruuvi Station. This procedure may vary depending
          on your device vendor, model and Android version.</p>
        <p>On Samsung devices go to Android Settings -&gt; Device Maintenance (or
          Device Care) -&gt; Battery. Disable Put unused apps to sleep. Disable Auto-disable
          unused apps. Remove Ruuvi Station from the list of sleeping apps. Disable
          background restrictions for Ruuvi Station.</p>
      </td>
    </tr>
  </tbody>
</table>

QA checklist

| Default no background scanning |
| :--- |
| Updating app remembers setting |
| If update from old version with lazy scanning, no background scanning will be selected |
| Switches between foreground and continuous scanning when switching to bg/fg |
| Scan interval is reflected on CSV export |
| When Continuous background scanning enabled Ruuvi icon appears at top left of device screen when app minimized to indicate scanning is on |
| Notification drawer will display sticky notification for scanning interval Scanning every m-s. |

_Temperature unit_

  
Setting for global temperature units. This affects: sensor card, graphs, alerts, csv export.

UI/UX checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Radio button:</p>
        <p>Celsius (&#xB0;C)
          <br />Fahrenheit (&#xB0;F)
          <br />Kelvin (K)</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Explainer: Choose the temperature unit you want to be displayed.

  
QA checklist  
  


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Changing temperature unit reflects on:</p>
        <p>Sensor card
          <br />Alerts
          <br />Charts
          <br />CSV export</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Temperature unit shows on App Settings under Temperature unit title  
  


_Humidity unit_

Setting for global humidity units. This affects: sensor card, graphs, alerts, csv export.

UI/UX checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Radio button:</p>
        <p>Relative (%)
          <br />Dew Point (&#xB0;)
          <br />Absolute (g/m3)</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Explainer: Choose the humidity unit you want to be displayed.  
  


QA checklist  
  


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Changing humidity unit reflects on:</p>
        <p>Sensor card
          <br />Alerts
          <br />Charts
          <br />CSV export</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Humidity unit shows on App Settings under Humidity unit title  
  


_Pressure unit_

Setting for global pressure units. This affects: sensor card, graphs, alerts, csv export.

UI/UX checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Radio button:</p>
        <p>Pascal (Pa)
          <br />Hectopascal (hPa)
          <br />Millimetre of mercury (mmHg)
          <br />Inch of mercury (inHg)</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Explainer: Choose the pressure unit you want to be displayed.  
  


QA checklist  
  


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Changing pressure unit reflects on:</p>
        <p>Sensor card
          <br />Alerts
          <br />Charts
          <br />CSV export</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Pressure unit shows on App Settings under Pressure unit title

_Dashboard_

Enabling dashboard will enable a dashboard homescreen with simplified top-down overview list of sensors.  
  


UI/UX checklist

| Simple enable/disable toggle. After enabling or disabling this setting user must kill app for app to show/hide dashboard. |
| :--- |
| Explainer: Use a dashboard view to see multiple sensors at a glance. Restart the app after enabled. |

QA checklist

| Enable and kill app, will show dashboard homescreen on next app launch |
| :--- |
| Disable and kill app, will show default view on next app launch |

_Gateway Settings_

Gateway setting allows sending sensor data to an external gateway through HTTP POST.

UI/UX checklist  
  


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Toggle: Keep the device awake while scanning</p>
        <p>Explainer: This will make the device stay awake while background scanning
          is enabled. It will improve background scanning reliability but will make
          the app use more battery.</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Gateway URL field</p>
        <p>Explainer: <a href="http:/#">https://your.gateway/&#x2026;</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Device identifier field</p>
        <p>A pre-generated id shown by default.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Button: Test gateway</p>
        <p>Indicator below button: RED Nope, did not work. Is the URL correct? GREEN
          Gateway works! Response code: 200</p>
        <p>Explainer: When you add a URL here, the app will execute an HTTP POST
          with the linked sensors when it does background scanning. For more info,
          check the documentation (url <a href="https://docs.ruuvi.com/ruuvi-station-app/gateway">https://docs.ruuvi.com/ruuvi-station-app/gateway</a>)</p>
      </td>
    </tr>
  </tbody>
</table>

QA checklist

| Gateway URL allows max 200 characters |
| :--- |
| Gateway URL explainer replaced with user added url |
| Gateway URL shows on App Settings under Gateway Settings title |
| Device identifier allows max 64 characters |
| Device identifier reflected on external gateway data |
| Gateway test failed RED Nope, did not work. Is the URL correct?  |
| Gateway test failed RED Nope, did not work. Is the URL correct?  |
| Gateway test passed GREEN Gateway works! Response code: 200 |

_Chart Settings_

Chart settings control the way charts are shown.  
  


UI/UX checklist

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>Toggle: Show all points</p>
        <p>Explainer: Enabling it may cause charts to update slowly</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Draw dots in chart
        <br />
        <br />Explainer: Small dots will help to understand when measurements were collected</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Chart interval</p>
        <p>Explainer: set interval between points for chart from 1 to 60 minutes.
          Less value means more accurate chart, but higher requirements to performance
          of your device</p>
        <p>Interval selector shown with one up/down scrolling wheel with title
          <br
          />Minutes (min 1 max 60)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Chart history view period</p>
        <p>Explainer: Configure history diapason to be shown on chart from 1 to 72
          hours</p>
        <p>Interval selector shown with one up/down scrolling wheel with title
          <br
          />Hours (min 1 max 72)</p>
      </td>
    </tr>
  </tbody>
</table>

QA checklist  
  


| Show all points will show all recorded datapoints in charts |
| :--- |
| Show all points enabled disables Chart interval setting \(greyed out\) |
| Chart interval reduces or increases datapoints shown in charts |
| Chart history view period reflects maximum window shown in Charts view |

