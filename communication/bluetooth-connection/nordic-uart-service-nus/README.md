# NUS \(Nordic UART Service\)

**Introduction**

Nordic Uart Service emulates Universal Asynchronous Receiver Transmitter over Bluetooth. NUS has 2 characteristics, RX and TX. Central registers to TX notifications and once notification registration is acknowledged central can start writing to RX characteristic. Each characteristic accepts up to 20 byte payloads, interpretation of those payloads depends on application. 

In development versions of firmware there is 120 second delay from starting of the connection in which the central must complete the registration process. If the deadline is not met, tag assumes that there is a software lockup and reboots. In production versions this deadline is 12 seconds. 

The Ruuvi Firmware standard messages have a structure of 3 byte header and 8 byte payload. The header has a structure of destination, source and type. Last bit of the type is R / !W bit, if the last bit is set \(odd number\) the message is understood as a read command. The payload is defined by the header.  
  
**Technical details**

| **Service** | UUID |
| :--- | :--- |
| Nordic UART Service | 6E400001-B5A3-F393-E0A9-E50E24DCCA9E |

| Characteristic | UUID | Read | Write | Notify |
| :--- | :--- | :--- | :--- | :--- |
| RX | 6E400002-B5A3-F393-E0A9-E50E24DCCA9E |  | X |  |
| TX | 6E400003-B5A3-F393-E0A9-E50E24DCCA9E | X |  | X |



