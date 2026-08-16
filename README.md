# 🛵 Food Delivery Performance & Time Prediction Analysis

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis-blue?style=for-the-badge)
![Data Analytics](https://img.shields.io/badge/Data_Analytics-Insights-green?style=for-the-badge)

## 📌 Executive Summary
This project presents an end-to-end data analysis solution for a food delivery dataset containing **50,000+ orders**. The main objective is to identify operational bottlenecks, analyze delivery transit times versus restaurant preparation delays, and evaluate the impact of external environmental factors (weather, festivals, traffic) on overall fulfillment efficiency.

---

## 📸 Dashboard Preview
![Dashboard Preview](food%20delivery.png) 

---

## 💡 Key Business Insights

* **⛈️ Weather Impact:** Delivery duration scales non-linearly with weather severity, starting at **77 mins** during clear conditions and peaking at **114 mins** during severe storms.
* **🎉 Event & Demand Surges:** Festival days experience an increase in delivery time (**95 mins**) compared to normal operational days (**83 mins**).
* **🚴 Vehicle Performance & Agility:** **Bikes** registered the lowest average transit time (**48 mins**) due to short-distance order routing and maneuverability in congestion, whereas traditional **Bicycles** recorded the longest duration (**107 mins**).
* **🍳 Restaurant Kitchen Bottlenecks:** Food preparation time accounts for **28.7%** of total order duration. **Biryani** and **North Indian** cuisines require the longest prep time (~**34 mins**), whereas **Bakery** and **Desserts** average ~**13 mins**.

---

## 🛠️ Data Modeling & DAX Implementation

The project utilizes advanced **DAX Measures** and **Calculated Columns** to drive the analysis:

* **Transit Time Measure:**
```dax
-- Average Total Delivery Time
Avg Delivery Time = AVERAGE(Food_Delivery_Time_Prediction[Time_taken_min])

-- Average Food Preparation Time
Avg Prep Time = AVERAGE(Food_Delivery_Time_Prediction[Preparation_Time_Min])

-- Transit Time in Road Only
Transit Time = 
AVERAGE(Food_Delivery_Time_Prediction[Time_taken_min]) - AVERAGE(Food_Delivery_Time_Prediction[Preparation_Time_Min])

-- Kitchen Delay Ratio
Prep Time % = 
DIVIDE(
    AVERAGE(Food_Delivery_Time_Prediction[Preparation_Time_Min]),
    AVERAGE(Food_Delivery_Time_Prediction[Time_taken_min]),
    0
)
