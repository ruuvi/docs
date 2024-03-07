# Backend: MQTT(s)

You can configure relaying data to MQTT server:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-36-28.png" alt=""><figcaption></figcaption></figure>

You can choose the data format - raw data received from Bluetooth sensors or decoded data for Ruuvi sensors:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-19 21-37-49.png" alt=""><figcaption></figcaption></figure>

By default, data received from Bluetooth sensors is retransmitted over MQTT immediately, but if you have a lot of sensors you may want to limit the data flow. In order to do this you can set a sending interval:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-13 09-14-51.png" alt=""><figcaption></figcaption></figure>

It also supports MQTT client authentication via SSL by enabling the upload of a client certificate and its associated private key, ensuring secure and verified client-server communication. You can use a server SSL Certificate if you want to be independent of public Certificate Authorities (CAs) or if you have deployed a self-signed certificate on the HTTPS server, giving you greater control and customization over your security infrastructure:

<figure><img src="../../../.gitbook/assets/Screenshot from 2023-12-13 09-10-23.png" alt=""><figcaption></figcaption></figure>
