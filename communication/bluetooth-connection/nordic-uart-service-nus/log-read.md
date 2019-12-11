# Read logged history

### **Log read flow**

The log read is initiated by central which requests for the type of data and time range of the logs. The log is read with command that has a header destination set to physical quantity being read, source to any and type as a log read. The payload is two 32-bit timestamps, seconds since unix epoch. First timestamp is current time, and second time is the lower bound of log data timestamps. For example if the timestamps are 1567047917 and 1566047917 data from time between 2019-08-13 13:18 and 2019-08-29 03:05 is sent.

The logs are sent in format where header destination is the source of read command, source is the physical quantity and type is log write. Payload is 4 bytes of timestamp and 4 bytes of  value. Interpretation of value depends on the type of data, possible types are listed below.

When the log buffer is sent and no more data remains, a special message with the entire payload set to 0xFF is sent. It should be noted that there is no way to send only “missing sections” of data from the middle of the logs, logs are always retrieved to the end of the stored data.

### **Example communication - read temperature**

| **Device** | **Header** | **Payload** | **Description** |
| :--- | :--- | :--- | :--- |
| Central | 0x30 30 11 | 0x5D6740ED 5D57FEAD | “To: temperature. From: temperature. Action: read log data. Clock is 2019-08-29 03:05 now, start from 2019-08-13 13:18” |
| Peripheral | 0x30 30 10 | 5D57FEAD 000000098D | “To: temperature. From: temperature. Action: write log data. Temperature at  2019-08-13 13:18 24.45 C“ |
| . | . | . | Log entry |
| . | . | . | Log Entry |
| Peripheral | 0x30 30 10 | 0x5D6740ED FFFFF8AC | “To: temperature. From: temperature. Action: write log data. Temperature at 2019-08-29 0305 -18.76 C” |
| Peripheral | 0x30 30 10 | 0xFFFFFFFF FFFFFFFF | “To: temperature. From: temperature. Action: write log data. No more logs” |

### **Example communication - read all environmental data**

| **Device** | **Header** | **Payload** | **Description** |
| :--- | :--- | :--- | :--- |
| Central | 0x3A 3A 11 | 0x5D6740ED 5D57FEAD | “To: environmental. From: environmental. Action: read log data. Clock is 2019-08-29 03:05 now, start from 2019-08-13 13:18” |
| Peripheral | 0x3A 30 10 | 5D57FEAD 000000098D | “To: environmental. From: temperature. Action: write log data. Temperature at  2019-08-13 13:18 24.45 C“ |
| Peripheral | 0x3A 31 10 | 5D57FEAD 000000098D | “To: environmental. From: humidity. Action: write log data. Humidity at  2019-08-13 13:18 24.45 RH-%“ |
| Peripheral | 0x3A 32 10 | 5D57FEAD 000000098D | “To: environmental. From: pressure. Action: write log data. Humidity at  2019-08-13 13:18 2445 Pa“ |
| . | . | . | Log entry |
| . | . | . | Log Entry |
| . | . | . | Log Entry |
| Peripheral | 0x3A 3A 10 | 0xFFFFFFFF FFFFFFFF | “To: environmental. From: environmental. Action: write log data. No more logs” |

### **Data endpoints**

| Endpoint byte | Value | Interpretation |
| :--- | :--- | :--- |
| 0x30 | Temperature | int32\_t, 0.01 C per LSB |
| 0x31 | Humidity | uint32\_t, 0.01 RH-% per LSB |
| 0x32 | Air pressure | uint32\_t, 1 Pa per LSB |
| 0x3A | All environmental values | Special value which can be used to query all environmental data at once.  |

### **Full length data**

File below is abbreviated nRF Connect log with some heartbeat transmissions and clutter removed. Log read command was added manually 

{% file src="../../../.gitbook/assets/v3\_28\_0\_connection.txt" caption="Connection log" %}



