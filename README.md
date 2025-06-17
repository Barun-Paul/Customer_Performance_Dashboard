# 📊 Customer Performance Dashboard - Power BI

This Power BI project is a Customer-Centric Performance Dashboard built using the AdventureWorks dataset. It visualizes essential customer metrics and revenue insights to help stakeholders make data-driven decisions.

## 🔍 Key Features

- Average Age of Customers  
- Total Customer Count  
- Customer Segmentation:
  - VIP Customers: Total Orders ≥ 2 and Total Purchases ≥ 100  
  - Loyal Customers: Total Orders ≥ 2  
  - Periodic Buyers: All others  
- Revenue Comparison: Customers With vs. Without Children  
- Revenue by Gender  
- Dynamic Ranking of Top-Performing Customers  
- Light Mode and Dark Mode Toggle Buttons  

## 🌓 Light & Dark Mode

The dashboard includes a toggle button to switch between Light and Dark mode, implemented using bookmarks and selection panes for improved user accessibility and preference control.

## 📐 DAX Usage

DAX (Data Analysis Expressions) was used to implement all key logic:

**Average Age:**
```DAX
AverageCustomerAge = AVERAGE(DimCustomer[Customer Age])
```

**Customer Segmentation:**
```DAX
Customer Type = 
        VAR _TotalOrders = [#Transaction]
        VAR _TotalPurchases = [Qty Ordered]
        RETURN
            IF( _TotalOrders >= 2 && _TotalPurchases >= 100 ,
                "VIP Customers" ,
                IF( _TotalOrders >= 2 ,
                    "Loyal Customers" ,
                    "Periodic Buyers"))
```

**Top Customer Ranking:**
```DAX
Dynamic Customers = 
    VAR _TopCustomers =
        RANKX(
              ALL(DimCustomer[Full Name]) , [Total Revenue] , , DESC)
    RETURN
        IF( _TopCustomers <= 'Dynamic Customers'[Dynamic Customers Value] ,
            [Total Revenue])
```

**Revenue by Customer with Children:**
```DAX
CWC Revenue = --This calculates total revenue from the customers with children
    CALCULATE(
        [Total Revenue],
        FILTER(
               DimCustomer,
               DimCustomer[TotalChildren] > 0))
```
**And More**

## 📸 Screenshots

**☀️ Light Mode**

![Dashboard_01](https://github.com/user-attachments/assets/1986ee99-49ad-4da5-801f-3b9b918b925c)



**🌙 Dark Mode**

![Dashboard_02](https://github.com/user-attachments/assets/2207283e-dcad-42ec-8521-f9a6ece74519)


## 🧠 Insights & Conclusions

- VIP Customers contribute the highest revenue and show consistent buying behavior.  
- Loyal Customers buy frequently but with slightly lower spend.  
- Customers with children tend to generate more revenue.  
- Female customers show slightly higher purchase activity.  
- Ranking helps identify high-value customer segments quickly.  

## 📁 File

- `PowerBI_AdventureWorks.pbix`: Main Power BI dashboard file with visuals, bookmarks, themes, and DAX logic.

## 🚀 How to Use

1. Clone or download this repository.  
2. Open the `.pbix` file using Power BI Desktop.  
3. Use filters, slicers, and the theme toggle to interact with the dashboard.  

## 💡 Tools Used

- Microsoft Power BI  
- AdventureWorks Dataset  
- DAX (Data Analysis Expressions)  

