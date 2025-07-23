WELLINGTON ZONE 1 POWER CONSUMPTION & ENVIRONMENTAL FACTORS  
Hourly data – 52 ,584 rows × 9 columns – 2019 to 2024  
README (TXT version)

────────────────────────────────────────────────────────
1.  CONTEXT & MOTIVATION
────────────────────────────────────────────────────────
Balancing Wellington’s electric grid requires accurate short-term demand
forecasts. Weather, air-quality and cloud cover heavily influence how much
power Zone 1 draws each hour. This dataset merges six years of hourly load
measurements with local meteorological variables so analysts can:

• build regression / time-series / deep-learning models  
• measure which weather factors drive demand spikes  
• practise feature engineering, explainable AI and AutoML on real energy data  

────────────────────────────────────────────────────────
2.  DATA AT A GLANCE
────────────────────────────────────────────────────────
Rows    : 52 ,584  
Columns  : 9  
Time span : 1 Jan 2019 – 31 Dec 2024  
Frequency : hourly  
File size : ≈ 5 MB (Excel XLSX)

Spreadsheet file: City Power Consumption.xlsx
Sheet name: City Power Consumption

────────────────────────────────────────────────────────
3.  COLUMN DICTIONARY
────────────────────────────────────────────────────────
sr_no                    — Row index (1 … 52 ,584)  
temperature              — Ambient air temperature (°C)  
humidity                 — Relative humidity (% or g · m⁻³)  
wind_speed               — Wind speed (knots, i.e., nautical miles / hour)  
general_diffuse_flows    — Diffuse global solar irradiance (W · m⁻²)  
diffuse_flows            — Diffuse sky solar irradiance (W · m⁻²)  
air_quality_index        — Particulate-based AQI (µg · m⁻³)  
cloudiness               — 0 = clear, 1 = cloudy  
zone1_power_consumption  — Instantaneous power demand (kW)  ← TARGET

Note: kW values are instantaneous, **not** cumulative kWh.

────────────────────────────────────────────────────────
4.  QUICK-START (PYTHON EXAMPLE)
────────────────────────────────────────────────────────
import pandas as pd

df = pd.read_excel('City Power Consumption.xlsx', sheet_name='City Power Consumption')

# optional: create lag features
for lag in [1, 24, 168]:           # 1 h, 1 day, 1 week
    df[f'power_lag_{lag}h'] = df['zone1_power_consumption'].shift(lag)

print(df.head())

────────────────────────────────────────────────────────
5.  DATA QUALITY NOTES
────────────────────────────────────────────────────────
• Duplicate timestamps (~0.3 %) were averaged.  
• 1.6 % missing power readings forward-filled (ffill).  
• All features aligned to the same hourly index.  
• Extreme outliers above the 99.9th percentile winsorised.  
• Units harmonised: wind in knots, irradiance in W · m⁻².

Feel free to re-impute or rescale as needed.

────────────────────────────────────────────────────────
6.  LICENSE
────────────────────────────────────────────────────────
Creative Commons Attribution 4.0 International (CC BY 4.0)  
Use, modify, and redistribute the data. Credit the sources below.

────────────────────────────────────────────────────────
7.  SOURCE & ACKNOWLEDGEMENTS
────────────────────────────────────────────────────────
• Wellington City Council Open Data Portal
• Transpower NZ – regional load statistics  
 
This dataset is not endorsed by either organisation; any errors are mine alone.

Happy forecasting!
