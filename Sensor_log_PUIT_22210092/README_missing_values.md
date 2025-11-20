
# 🧪 Handling Missing Values in IoT Sensor Data  
## ✨ Forward Fill | Backward Fill | Interpolation | Mean Fill

---

## 📌 Project Overview

This dataset contains IoT sensor readings for **temperature**, **humidity**, and **voltage**. During data collection, some sensor values were not recorded, resulting in **missing values (NaN)**.  

To clean this dataset, we applied **four different methods** to handle missing values and created **four separate DataFrames** for comparison.

---

## 🔍 Missing Value Detection

```python
df.isnull().sum()
```

This identified missing values in:
- `temperature_c` → 2 values missing  
- `humidity_pct` → 1 value missing  
- `voltage_v` → 1 value missing  

---

## 🛠 Methods Used to Fill Missing Values

| Method | Code | Explanation | Best Use Case |
|-------|------|--------------|---------------------------|
| **Forward Fill** | `df.fillna(method='ffill')` | Copies value from the previous row | When values change slowly |
| **Backward Fill** | `df.fillna(method='bfill')` | Copies value from the next row | When future readings are valid |
| **Interpolation** | `df.interpolate()` | Calculates values between two known points | Best for time-series sensor data |
| **Mean Fill** | `df.fillna(df.mean())` | Replaces NaN with column average | Useful for stable datasets |

---

## 🧠 Explanation of Each Method

### 🔹 1. Forward Fill (ffill)
```python
df_forward_fill = df.fillna(method='ffill')
```
✔ Uses **previous sensor value** to fill missing values.  
✔ Assumes sensors change **slowly/gradually**.  

---

### 🔹 2. Backward Fill (bfill)
```python
df_back_fill = df.fillna(method='bfill')
```
✔ Uses **next sensor value** instead.  
✔ Useful when sensor readings are **stable**.  

---

### 🔹 3. Interpolation (Best for Time-Series Data)
```python
df_interpolate = df.interpolate()
```
✔ Calculates a **new value based on surrounding values**  
✔ Ideal for **time-series IoT data**  
✔ Smooth & realistic values  

---

### 🔹 4. Mean Fill
```python
df_mean_fill = df.fillna(df.mean())
```
✔ Uses **column average** to fill all missing values  
✔ Useful when data is **not time-based**

---

## 📁 Generated Clean DataFrames

| Method | DataFrame Name |
|--------|----------------|
| Forward Fill | `df_forward_fill` |
| Backward Fill | `df_back_fill` |
| Interpolation | `df_interpolate` |
| Mean Fill | `df_mean_fill` |

Each version can be exported:
```python
df_forward_fill.to_csv('forward_fill.csv', index=False)
df_back_fill.to_csv('backward_fill.csv', index=False)
df_interpolate.to_csv('interpolated.csv', index=False)
df_mean_fill.to_csv('mean_fill.csv', index=False)
```

---

## 📌 Summary Statistics (After Cleaning)

Use:
```python
df_interpolate.describe()
```

This computes:
- Mean
- Standard Deviation
- Minimum & Maximum
- Quartiles (25%, 50%, 75%)

---

## 📌 Conclusion

| Method | Best For |
|--------|----------|
| Forward Fill | Slow-changing sensor data |
| Backward Fill | Sensors with stable readings |
| **Interpolation** | **Time-series data (BEST)** |
| Mean Fill | Basic data cleaning |

**Interpolation is the most suitable method for IoT sensor data** because values change gradually over time.

---



> “I tested four methods for cleaning missing values: forward fill, backward fill, interpolation, and mean fill. Interpolation was the most realistic because IoT sensors produce time-series data where values change gradually. We created separate DataFrames for each method and compared them for analysis.”

---

## 📂 Project Structure

```
SmartCity_IoT_MissingValue_Study/
├── sensor_log.csv
├── missing_value_cleaning.ipynb
├── README.md  ← THIS FILE
├── forward_fill.csv
├── backward_fill.csv
├── interpolated.csv
└── mean_fill.csv
