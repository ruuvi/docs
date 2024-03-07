---
description: >-
  If you want to install a custom firmware or a previous version of Ruuvi
  Gateway firmware, you can do this using Web-UI.
---

# GW Install custom firmware

## GW  Install previous firmware releases

Open Web-UI, go to "Software Update" page, expand "Advanced Settings" and enable the checkbox "Don't use the software update provided by Ruuvi but download binary files from URL address instead":

<figure><img src="../.gitbook/assets/Screenshot from 2023-12-13 09-36-05.png" alt=""><figcaption></figcaption></figure>

In the URL input field change the version number to the desired one, then press "UPDATE" button.

The list of released versions can be found here: [https://github.com/ruuvi/ruuvi.gateway\_esp.c/releases/](https://github.com/ruuvi/ruuvi.gateway\_esp.c/releases/)

## GW Install custom firmware

You need to prepare firmware binaries and put them on your HTTP server.

1\. First, you need to build firmware:

```bash
idf.py build
```

2\. Next, copy the firmware binaries to some folder (gw\_fw):

```
mkdir gw_fw
cd build
cp ruuvi_gateway_esp.bin fatfs_gwui.bin fatfs_nrf52.bin ../gw_fw
```

3\. Run local HTTP server on port 7000 in the folder with the firmware binaries:

```
cd ../gw_fw
python3 -m http.server 7000
```

Or instead of steps 2 and 3 you can simply run the local HTTP server in the "build" folder:

```
cd build
python3 -m http.server 7000
```

Then open Web-UI, go to "Software Update" page, expand "Advanced Settings", enable checkbox "Don't use the software update provided by Ruuvi but download binary files from URL address instead" and in the URL input field set the address of your local HTTP server, then press "UPDATE" button:

<figure><img src="../.gitbook/assets/Screenshot from 2023-12-13 09-39-08.png" alt=""><figcaption></figcaption></figure>

