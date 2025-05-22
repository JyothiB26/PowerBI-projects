# Customer Churn Analysis Dashboard using PowerBI
![image](https://github.com/user-attachments/assets/06c09a83-9834-4c53-80b3-59dcfcf5d7d1)

## Project Description
This Power BI project analyzes customer churn using a bank’s dataset of 10,000 customers. The dashboard provides visual insights into the churn rate, customer behavior, and demographics, empowering business stakeholders to make data-driven decisions to reduce churn.

## Dataset Overview
- Source: Churn_Modelling.csv
- Records: 10,000 bank customers
- Target Variable: Exited (1 = Customer churned, 0 = Customer retained)

The dataset contains 10,000 customer records and includes the following key features:

| Column Name       | Description                                                                |
|-------------------|----------------------------------------------------------------------------|
| CustomerID        | Unique ID for each customer                                                |
| Surname           | Customer's last name                                                       |
| CreditScore       | Credit score of the customer                                               |
| Geography         | Country of residence (e.g., France, Germany, Spain)                        |
| Gender            | Male/Female                                                                |
| Age               | Age of the customer                                                        |
| Tenure            | Number of years the customer has been with the bank                        |
| Balance           | Account balance                                                            |
| NumOfProducts     | Number of products held by the customer                                    |
| HasCrCard         | Whether the customer has a credit card (1 = Yes, 0 = No)                   |
| IsActiveMember    | Activity status (1 = Active, 0 = Inactive)                                 |
| EstimatedSalary   | Estimated annual salary                                                    |
| Exited            | Target variable — whether the customer has churned (1 = Yes, 0 = No)       |

## Project Overview
### Objective
To build an interactive **Power BI dashboard** to:
- Monitor overall churn rate
- Understand customer churn by geography, tenure, balance, age ,gender, creditscore and demographics
- Analyze financial behavior and product usage
- Identify patterns among active/inactive customers

### Tools & Technologies
- **Power BI Desktop** for dashboard design and interactivity
- **DAX** for creating calculated measures and KPIs
- **Power Query** for data cleaning and transformation

---

##  Dashboard Features & Visual Insights

###  **Top KPIs**
- **Total Customers**: 10.00K  
- **Churn Count**: 2,038  
- **Churn Rate**: 20.38%  
- **Active Members**: 5,150

###  **Churn Rate by Geography**
- **Germany** has the highest churn rate at **32.47%**
- **France** and **Spain** have much lower churn rates (~16%)

###  **Churn Distribution**
- **79.62%** of customers retained, while **20.38%** have churned

###  **Churn Rate by Tenure**
- Churn rate **peaks at lower and mid tenures**, then dips before rising again at the 10-year mark
- Highest churn around **1–2 years** of tenure

###  **Estimated Salary by Churn & Gender**
- Customers with higher salaries are more likely to stay
- Female churners have slightly lower estimated salaries

###  **Active Members by Tenure Group**
- Highest active members in **3–5 years** and **6–8 years** tenure brackets

###  **Churn vs Active Membership & Account Balance**
- Most churners are **inactive members**
- **Inactive customers** have lower retention and varying balances

###  **Interactive Filters**
- Slicers for **Active Status**, **Age Group**, **Gender**, and **Geography** allow for deep-dives and ad hoc analysis

---

##  Files Included
- `Churn_Modelling.csv` – Source dataset
- `.pbix` file – Power BI dashboard file (add if uploading)
- `Customer_Churn_Dashboard_snip.png` – Dashboard snapshot

---

##  Business Insights
- Focus retention efforts in **Germany** and among **inactive members**
- Improve onboarding experience for **new customers (0–2 years)** to reduce early churn
- Target customers with **multiple products** and **moderate balances** for upselling strategies

---

##  Conclusion
This Power BI dashboard enables a comprehensive view of customer churn across multiple dimensions and empowers strategic action to reduce churn, retain high-value customers, and optimize banking services.

---

## 🧮 DAX Measures & Columns

### 🔢 Measures
```dax
TotalCustomers = COUNTROWS(Churn_Modelling)

ChurnCount = CALCULATE(COUNTROWS(Churn_Modelling),Churn_Modelling[Churn]=1)

ChurnRate = DIVIDE(CALCULATE(COUNTROWS(Churn_Modelling),Churn_Modelling[Churn]=1),COUNTROWS(Churn_Modelling))

ActiveMembers = CALCULATE(COUNT(Churn_Modelling[CustomerId]),Churn_Modelling[Active]="Yes")
```

### 📊 Calculated Columns
```dax
Active = IF('Churn_Modelling'[IsActiveMember]=1,"Yes","No")

Churn Distribution = IF('Churn_Modelling'[Churn]=1,"Yes","No")

TenureGroup = 
SWITCH(
    TRUE(),
    Churn_Modelling[Tenure] <= 2, "0–2 years",
    Churn_Modelling[Tenure] <= 5, "3–5 years",
    Churn_Modelling[Tenure] <= 8, "6–8 years",
    Churn_Modelling[Tenure] > 8,  "9–10 years",
    "Unknown"
)

AgeGroup = SWITCH(TRUE(),Churn_Modelling[Age]<30,"Under 30",Churn_Modelling[Age]>=30&&Churn_Modelling[Age]<40,"30-39",Churn_Modelling[Age]>=40&& Churn_Modelling[Age]<50,"40-49","50+")

TenureSortOrder = SWITCH(TRUE(),Churn_Modelling[Tenure]<=2,1,Churn_Modelling[Tenure]<=5,2,Churn_Modelling[Tenure]<=8,3,4)
```
