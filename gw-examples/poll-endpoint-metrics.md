# Poll endpoint "/metrics"

Extended internal information on the status of the Ruuvi Gateway can be obtained by polling the endpoint "/metrics".

On the "Access Settings" page, enable bearer authentication and set the bearer token:

<figure><img src="../.gitbook/assets/Screenshot from 2023-12-13 10-19-16.png" alt=""><figcaption></figcaption></figure>

After that it is possible to poll data using the "/metrics" endpoint:

```shell
curl -v http://<RUUVI_GW_IP>/metrics 
    -H "Authorization: Bearer Uj+4tj24unVekco/lTLTRyxUfv1J8M6U+sbNsKTWRr0="
```

Example of the response:

```
ruuvigw_received_advertisements 500999
ruuvigw_uptime_us 171619762770
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_EXEC"} 107564
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_32BIT"} 107564
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_8BIT"} 59012
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DMA"} 59012
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID2"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID3"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID4"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID5"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID6"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID7"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_SPIRAM"} 0
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_INTERNAL"} 107564
ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DEFAULT"} 59012
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_EXEC"} 55568
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_32BIT"} 55568
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_8BIT"} 55568
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DMA"} 55568
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID2"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID3"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID4"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID5"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID6"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID7"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_SPIRAM"} 0
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_INTERNAL"} 55568
ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DEFAULT"} 55568
ruuvigw_info{mac="C8:25:2D:8E:9C:2C",esp_fw="v1.12.4-29-g708c35d-dirty",nrf_fw="v1.0.0"} 1
ruuvigw_gw_cfg_crc32 1041546679
ruuvigw_ruuvi_json_crc32 3490230955

```
