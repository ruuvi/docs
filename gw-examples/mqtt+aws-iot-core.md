# MQTT+AWS IoT Core

Follow these detailed steps to establish a secure connection and send data from your Ruuvi Gateway to AWS IoT Core using MQTT. This setup uses MQTT over SSL/TLS for encrypted data transmission, ensuring secure communication.

1. **Select MQTT Transport Type**:
   * For the transport type, choose **"MQTT over SSL"**. This option encrypts the data, providing a secure connection to AWS IoT Core.
2. **Configure Server Address**:
   * Input your AWS endpoint as the **Server Address**. You can find your unique AWS endpoint in the AWS IoT Core console under the Settings section.
3. **Set Communication Port**:
   * Specify **8883** as the port. This is the standard port for MQTT over SSL, ensuring encrypted communication.
4. **Configure Client ID**:
   * Input the **Client ID** provided by AWS, which uniquely identifies your Ruuvi Gateway. You will find this ID in the AWS IoT Core console, formatted as **"iotconsole-xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"**. The Client ID ensures AWS IoT Core correctly recognizes and manages your device's connection.
5. **Important: Disable Retained Messages**:
   * Due to AWS's policy, enabling retained messages can cause AWS IoT Core to immediately close the connection upon receiving the Last Will and Testament (LWT) message. Therefore, it is crucial to **disable the use of retained messages** to maintain a stable connection. This step prevents potential disruptions and ensures continuous data transmission to AWS IoT Core.
6. **Configure SSL/TLS Certificates**:
   * Enable **"Use client SSL certificate"**.
     * Upload the **Client Certificate File** (.crt) and the **Client Private Key File** (.key) provided by AWS when you registered your device.
   * Enable **"Use custom SSL certificate for the server"**.
     * Upload the **Server SSL Certificate**. This is usually the Amazon Root CA 1 certificate available from AWS documentation.
7. **Select Data Format**:
   * Choose the preferred format for the data you are sending to AWS IoT Core. Options typically include:
     * **Raw Data**: Sends the data as collected by sensors without processing.
     * **Decoded Data**: Sends data that has been processed or formatted.
     * **Both**: Sends both raw and decoded data, providing comprehensive information.

<figure><img src="../.gitbook/assets/Screenshot from 2024-02-09 13-42-50.png" alt=""><figcaption></figcaption></figure>
