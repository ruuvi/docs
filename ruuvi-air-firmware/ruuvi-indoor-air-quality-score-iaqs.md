---
noIndex: true
---

# Ruuvi Indoor Air Quality Score (IAQS)

The Ruuvi Indoor Air Quality Score (IAQS) is designed to provide a quick and repeatable overview of the healthiness of current indoor air conditions. The index does not account for temperature or humidity, as these are more closely related to comfort and structural maintenance than to direct health effects. The IAQS considers CO₂ and particulate matter (PM₂.₅), as both can be measured as absolute values and their effects on health and well-being are well studied. The index is calculated by measuring each component’s deviation from its ideal value and using geometric distance to compute a combined “total difference” from the ideal. &#x20;

<table><thead><tr><th width="122">Grade</th><th width="176">IAQS</th><th width="191">CO₂ (ppm)</th><th>PM₂.₅ (μg/m³)</th></tr></thead><tbody><tr><td>Excellent</td><td>90 ≤ IAQS ≤ 100</td><td>CO₂ ≤ 600</td><td>PM₂.₅ ≤ 6</td></tr><tr><td>Good</td><td>80 ≤ IAQS &#x3C; 90</td><td>600 &#x3C; CO₂ ≤ 800</td><td>6 &#x3C; PM₂.₅ ≤ 12</td></tr><tr><td>Fair</td><td>50 ≤ IAQS &#x3C; 80</td><td>800 &#x3C; CO₂ ≤ 1400</td><td>12 &#x3C; PM₂.₅ ≤ 30</td></tr><tr><td>Poor</td><td>10 ≤ IAQS &#x3C; 50</td><td>1400 &#x3C; CO₂ ≤ 2100</td><td>30 &#x3C; PM₂.₅ ≤ 55</td></tr><tr><td>Very Poor</td><td>0 ≤ IAQS &#x3C; 10</td><td>2100 &#x3C; CO₂</td><td>55 &#x3C; PM₂.₅</td></tr></tbody></table>

Expressed graphically, the IAQS maps CO₂ and PM₂.₅ as shown below:&#x20;

<figure><img src="../.gitbook/assets/riaqs.jpg" alt=""><figcaption></figcaption></figure>

The IAQS is calculated using the following formula:&#x20;

```
const AQI_MAX    = 100;

const PM25_MAX   = 60,  PM25_MIN = 0;
const PM25_SCALE = AQI_MAX / (PM25_MAX - PM25_MIN);   // ≈ 1.6667

const CO2_MAX    = 2300, CO2_MIN = 420;
const CO2_SCALE  = AQI_MAX / (CO2_MAX - CO2_MIN);     // ≈ 0.05319

function clamp(x, lo, hi){ return Math.min(Math.max(x, lo), hi); }

function calc_aqi(pm25, co2) {
  if(isNaN(pm25) || isNaN(co2)) { return NaN; }

  pm25 = clamp(pm25, PM25_MIN, PM25_MAX);
  co2  = clamp(co2,  CO2_MIN,  CO2_MAX);

  const dx = (pm25 - PM25_MIN) * PM25_SCALE; // 0..100
  const dy = (co2  - CO2_MIN)  * CO2_SCALE;  // 0..100

  const r  = Math.hypot(dx, dy);             // sqrt(dx*dx + dy*dy)
  return clamp(AQI_MAX - r, 0, AQI_MAX);
}
```

Ruuvi Station apps and Ruuvi Air display the index grade based on the value rounded to the nearest integer. For example, a value of 89.6 is rounded to 90 and displayed as turquoise (“Excellent”), even though the raw value is slightly below the threshold. History graphs also use the rounded color classification; for instance, a sequence of values 89.4, 89.5, and 89.6 transitions from green to turquoise at 89.5.
