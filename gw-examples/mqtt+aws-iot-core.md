# MQTT+AWS IoT Core

To send data to AWS IoT Core via MQTT, you need to configure Ruuvi Gateway in the following way:

1. Set MQTT transport type to "MQTT over SSL". Please ensure that AWS is configured to use TLS 1.2 since Ruuvi Gateway currently doesn't support TLS 1.3;
2. Set AWS endpoint as the Server address;
3. Set Port to 8883;
4. Set "Disable the use of retained messages";
5. Set "Use client SSL certificate (\*.pem)", then upload the client certificate file and the client private key file (both files should have \*.pem extension);
6. Set "Use custom SSL certificate for the server (\*.pem)", then upload the server SSL certificate.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
