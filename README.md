# 📊 HR Workforce Intelligence Dashboard

## 📌 Project Overview

This project presents a comprehensive HR Workforce Intelligence Dashboard developed using Power BI.

The objective of this solution is to transform raw HR data into actionable workforce intelligence by analyzing employee distribution, attrition behavior, demographic trends, and department-level risk exposure.

The dashboard integrates structured data modeling, advanced DAX calculations, and interactive reporting to support strategic HR decision-making.

---

## 🏗 Data Model Architecture

A star-schema-based data model was implemented to ensure scalability and accurate time intelligence.

### Tables Used

**Fact Table**
- HRDataset

**Dimension Table**
- Date Table

### Date Table Columns

- Date  
- Month Name  
- Month Number  
- Year  

### Relationships Implemented

- Date Table[Date] → HRDataset[DateOfHire] (Active Relationship)
- Date Table[Date] → HRDataset[DateOfTermination] (Inactive Relationship)

The inactive relationship is dynamically activated using:

```DAX
USERELATIONSHIP('Date Table'[Date], HRDataset[DateofTermination])
```

This approach enables independent and accurate analysis of hiring trends and termination trends within the same data model.

---

## 📐 DAX Measures Engineered

### Total Employees

```DAX
Total Employee = DISTINCTCOUNT(HRDataset[EmpID])
```

### Active Employees

```DAX
Active Employee =
CALCULATE(
    [Total Employee],
    FILTER(HRDataset, HRDataset[EmploymentStatus] = "Active")
)
```

### Terminated Employees

```DAX
Terminated Employees =
CALCULATE(
    [Total Employee],
    HRDataset[EmploymentStatus] <> "Active",
    USERELATIONSHIP('Date Table'[Date], HRDataset[DateofTermination])
)
```

### Attrition Rate

```DAX
Attrition Rate =
DIVIDE([Terminated Employees], [Active Employee])
```

### Average Salary

```DAX
Avg Salary = AVERAGE(HRDataset[Salary])
```

---

## 📊 Calculated Columns

### Employee Age

```DAX
Employee Age =
DATEDIFF(HRDataset[DOB], TODAY(), YEAR)
```

### Employee Age Band

```DAX
Employee Age Band =
SWITCH(
    TRUE(),
    HRDataset[Employee Age] >= 33 && HRDataset[Employee Age] < 40, "33-39",
    HRDataset[Employee Age] >= 40 && HRDataset[Employee Age] < 50, "40-49",
    HRDataset[Employee Age] >= 50 && HRDataset[Employee Age] < 60, "50-59",
    HRDataset[Employee Age] >= 60 && HRDataset[Employee Age] < 75, "60-74",
    "Other"
)
```

These calculated columns enable demographic segmentation and workforce distribution analysis.

---

## 📊 Dashboard Structure

### 1️⃣ Overview Page

- Total Workforce Size
- Average Salary
- Attrition Rate
- Department-Level Distribution
- Demographic Breakdown (Sex, Citizenship, Marital Status)
- Age Band Distribution

### 2️⃣ Attrition Analysis Page

- Monthly & Yearly Attrition Trends
- Termination by Reason
- Gender-Based Termination Distribution
- Time-Based Workforce Movement

### 3️⃣ Employee Details Page

- Employee-Level Drill-Down
- Filters by Year, Department, Age
- Workforce Demographic Table View

---

## 🔎 Key Analytical Insights

### Workforce Stability Risk

The attrition rate exceeds 50%, indicating significant workforce turnover that may impact operational continuity and organizational stability.

### Departmental Exposure

The Production department holds the largest workforce concentration, creating operational dependency risk if attrition increases within this unit.

### Primary Attrition Drivers

Top termination reasons include:

- Career advancement opportunities  
- Compensation factors  
- Employee dissatisfaction  

These drivers suggest attrition is partially controllable through strategic HR policy adjustments.

### Demographic Risk

The 40–49 age band represents the highest workforce concentration, highlighting potential succession planning challenges and long-term workforce aging risk.

### Temporal Attrition Patterns

Attrition trends display noticeable spikes during specific periods, indicating potential seasonal or policy-cycle influences.

---

## 🚀 Business Impact

This dashboard enables HR leadership to:

- Monitor workforce health in real-time  
- Identify high-risk departments  
- Detect preventable attrition drivers  
- Support compensation benchmarking decisions  
- Improve workforce planning and retention strategies  

---

## 🛠 Tools Used

- Power BI  
- Excel  
- PowerPoint  

---

## 📈 Future Enhancements

- Tenure Calculation & Tenure-Based Attrition Analysis  
- Department-Level Attrition Percentage  
- Workforce Risk Scoring Model  
- Predictive Attrition Modeling using Machine Learning  
- Deployment to Power BI Service with Scheduled Refresh  

---

## 📬 Contact

<p align="left">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" width="25" alt="LinkedIn"/>
  &nbsp; <a href="https://www.linkedin.com/in/muhammed-dhanish00017">linkedin.com/in/muhammed-dhanish00017</a>
</p>

<p align="left">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/google/google-original.svg" width="25" alt="Email"/>
  &nbsp; <a href="mailto:dhanish00017@gmail.com">dhanish00017@gmail.com</a>
</p>
