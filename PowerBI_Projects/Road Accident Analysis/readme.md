# 🚦 Road Accident Analysis Dashboard

## 🎯 Business Objective
To analyze road accident data and identify major factors contributing to accidents and casualties, and to monitor Year-over-Year (YoY) trends to evaluate the effectiveness of road safety measures.

---

## 📊 Dashboard Highlights
- Total Accidents & Total Casualties (Current Year & YoY Growth)
- Casualties by Accident Severity
- Casualties by Vehicle Type
- Casualties by Road Type
- Casualties by Area (Urban vs Rural)
- Casualties by Day & Night
- Monthly Trend: Current Year vs Previous Year
- Accidents & Casualties by Location

---

## 💡 Useful Insights

### ✅ Positive Insights 👍
- **Total Casualties reduced by 12% (YoY)**
- **Total Accidents reduced by 11.7% (YoY)**
- **Fatal casualties reduced by 33.33%**, showing improvement in emergency response and safety measures

### ❌ Negative Insights 👎
- Maximum casualties and accidents involve **Car-type vehicles**
- Nearly **75% of total casualties occurred on Single Carriageway roads**
- Over **60% of casualties occurred in Urban areas**

---

## 📌 Conclusion & Business Recommendations

Based on the analysis, to further reduce accidents and casualties:

- Convert **Single Carriageways into Dual Carriageways** where traffic density is high 
- Enforce **strict driving tests** before issuing four-wheeler driving licenses  
- Improve **road width, surface quality, markings, and street lighting**  
- Promote **public awareness programs** for traffic rules and safe driving behavior  
- Increase surveillance and penalties in **high-risk urban zones**

---

## 🛠 Tools Used
- Power BI
- Excel Dataset

---

## 📐 DAX Measures Used

### 🔹 Casualties KPIs

```DAX
CY Casualties =
TOTALYTD(
    SUM(Road_Accident_Data[Number_of_Casualties]),
    Calendar_lookup[Date],
    "12/31"
)

PY Casualties =
CALCULATE(
    [CY Casualties],
    SAMEPERIODLASTYEAR(Calendar_lookup[Date])
)

YoY Casualties =
DIVIDE(
    [CY Casualties] - [PY Casualties],
    [PY Casualties]
)

Accidents KPIs
CY Accidents =
TOTALYTD(
    COUNT(Road_Accident_Data[Accident_Index]),
    Calendar_lookup[Date],
    "12/31"
)

PY Accidents =
CALCULATE(
    [CY Accidents],
    SAMEPERIODLASTYEAR(Calendar_lookup[Date])
)

YoY Accidents =
DIVIDE(
    [CY Accidents] - [PY Accidents],
    [PY Accidents]
)
```
## 📁 Files
  👉 [Road Accident Analysis](https://app.powerbi.com/view?r=eyJrIjoiYjZkZTQxNDYtNWFkYy00ZjFkLWE0NTUtYWEzMzVmZmQwY2IwIiwidCI6Ijc3ZWYwMzdjLWU5N2MtNDUzZi04MmY2LTI0Y2M2NGViNGEyMCJ9)
- Overview
   ![Screenshot](Road Accident.png)
