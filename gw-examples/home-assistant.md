# Home Assistant

The Ruuvi Gateway integration was introduced in Home Assistant 2023.2, see [https://www.home-assistant.io/integrations/ruuvi\_gateway/](https://www.home-assistant.io/integrations/ruuvi\_gateway/)

## Setup

Install [Home Assistant OS 9.5](https://github.com/home-assistant/operating-system/releases/tag/9.5) or newer.

Configure Ruuvi Gateway to use [polling-mode.md](../examples/polling-mode.md "mention") (configure a Bearer token for read-only access).

Adding Ruuvi Gateway to your Home Assistant instance can easily be done by simply clicking on this [link](https://my.home-assistant.io/redirect/config\_flow\_start?domain=ruuvi\_gateway). After that, you'll see the following confirmation:

![](../.gitbook/assets/image.png)

After you click the **OPEN LINK** button, you may be prompted to log in:

![](<../.gitbook/assets/image (30).png>)

Then you will see a confirmation to set up the Ruuvi Gateway in Home Assistant:

![](<../.gitbook/assets/image (1).png>)

After that, you will need to enter the IP address of Ruvvi Gateway and the Bearer token specified when configuring the Gateway:

![](<../.gitbook/assets/image (26).png>)

That's it, then you will see a confirmation that Ruuvi Gateway has been successfully added:

![](<../.gitbook/assets/image (23).png>)

After that, the **Integrations** tab will open, where you can find the Ruuvi Gateway and a set of sensors:

![](<../.gitbook/assets/image (20).png>)

You can manually open the **Integrations** tab:

* In the sidebar click on **Settings**
* From the configuration menu select: **Devices & Services**

You will then need to configure the discovered sensors, select one of them and press the **CONFIGURE** button:

![](<../.gitbook/assets/image (15).png>)

Then press the **SUBMIT** button:

![](<../.gitbook/assets/image (18).png>)

Configure **Area** for the sensor and press the **FINISH** button:

![](<../.gitbook/assets/image (19).png>)

After that, the configured sensor will appear on the **Overview** page:

![](<../.gitbook/assets/image (45).png>)

That's all.
