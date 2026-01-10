# 👥 HR Attrition Dashboard

## 🎯 Business Objective
To analyze employee attrition and identify the major factors contributing to employee turnover, helping HR teams take data-driven decisions to improve retention.

---

## 📊 Dashboard Highlights
- Overall Attrition Rate
- Attrition by Education Background
- Attrition by Age & Gender
- Attrition by Distance from Home
- Attrition by Job Role & Job Satisfaction
- Attrition by Salary Slab
- Attrition by Years at Company

---

## 💡 Key Insights

1. Maximum attrition observed among employees with **Life Science** education, followed by **Medical** background.  
2. **Male employees aged 55+** and **female employees aged 18–25** recorded the highest attrition.  
3. **Distance from home (>10 km)** significantly impacts female attrition.  
4. **Laboratory Technicians** show the highest attrition based on job satisfaction levels.  
5. Average salary is **6.5K**, and employees earning **below this slab** show higher attrition.  
6. Most **male attrition occurs within the first year**, while for females it is around **one year of service**.  
7. **Sales Representative** role shows the highest attrition:  
   - Male: **38%**  
   - Female: **43%**

---

## ✅ Business Recommendations

Based on the analysis, to reduce attrition:

- Prefer hiring candidates with **diverse educational backgrounds**, not only Life Science and Medical.
- Provide **better facilities and security**, especially to support female employees.
- Offer **salary revisions** based on skills, experience, and performance.
- Introduce **training programs, skill development, and internal promotions** to increase motivation.
- For **Sales Representative and Lab Technician roles**, prioritize hiring **male candidates below 30 years** where suitable.

---

## 🛠 Tools Used
- Power BI
- Excel / SQL (Data Source)


## 📐 DAX Measures Used
```DAX
AttritionRate = 
DIVIDE(
    SUM(HR_Analytics[Attrition Count]),
    SUM(HR_Analytics[EmployeeCount])
)
```
## 📁 Files
- HR_Attrition_Dashboard.pbix
   [HR_Attrition_Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZmUwNWExNWQtZWNjOC00OTk2LWJlNmEtOTg3Y2U2NWQ3M2U3IiwidCI6Ijc3ZWYwMzdjLWU5N2MtNDUzZi04MmY2LTI0Y2M2NGViNGEyMCJ9)
- Overview
   ![Screenshot](HR_Attrition.png)

