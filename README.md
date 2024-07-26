# Customer-Churn-Analysis


## Problem Statement

This dashboard helps companies understand the factors driving customer churn.  By analyzing various metrics such as customer satisfaction scores, usage patterns, and services interactions, the dashboard provide comprehensive insight into why customers are leaving.  Companies can identify specific areas where improvements are needed to reduce churn rates and enhance customer retentions strategies.

The dashboard highlights that a significant portions of customers (around 57%) are churning compared to the 43% retentions rate.  This indicates a pressing need for the company to address the underlying issues to customer dissatisfaction and attrition.  Additionaly, the average customer tenure before churning is 15 months, suggesting that there is an opportunity to increase this duration through targeted interventions and improved service offering.

By leveraging this dashboard, companies can priotize key areas for improvement, develop effective retention strategies, and ultimately work towards reducing churn and increasing customer loyalty.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except column named "Arrival Delay".
- Step 5 : For calculating  null values were not taken into account as only less than 1% values are null in this column
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Since the data contains various ratings, thus in order to represent ratings, a new visual was added using the three ellipses in the visualizations pane in report view. 
- Step 8 : Visual filters (Slicers) were added for five fields named "Year", "Month name", "Location" & "Category","gender category".
- Step 9 : Seven card visuals were added to the canvas, representing total customers, active and inactive members, exit and retain customers, and credit card and non credit card holders.
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
           Although, by default, while calculating average, blank values are ignored.
- Step 10 : A bar chart was also added to the report design area representing the number of total customer, exit customers by credit card. While creating this visual, field named "Gender" was also added to the Legends bucket, thus number of customers are also seggregated according the gender. 

  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

 
- Step 11 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Credit type = SWITCH(TRUE(),Bank_Churn[CreditScore]>=800 && Bank_Churn[CreditScore]<=850,"Excellent",
        Bank_Churn[CreditScore]>=740 && Bank_Churn[CreditScore]<=799," Very good",Bank_Churn[CreditScore]>=670
        && Bank_Churn[CreditScore]<=799,"Good",Bank_Churn[CreditScore]>=580 &&Bank_Churn[CreditScore]<=699,
        "Fair",Bank_Churn[CreditScore]>=300 && Bank_Churn[CreditScore]<=579,"Poor")
        
Snap of new calculated column ,

![Screenshot 2024-07-26 155243](https://github.com/user-attachments/assets/9e90af5f-3a63-421c-9de7-fd45a9b4f08b)

        
- Step 12 : New measure was created to find total count of customers.

Following DAX expression was written for total customer,
        
        Total Customers = COUNT(Bank_Churn[CustomerId])
        
A card visual was used to represent total number of customers.

![SS](https://github.com/user-attachments/assets/cef33971-bebe-45da-8fc9-e3acc94769a5)

        
 - Step 13 : New measure was created to find active and inactive members,
 
 Following DAX expression was written to find active and inactive members,
 
Active Members = CALCULATE(COUNT(Bank_Churn[CustomerId]),'Active customers'[ActiveCategory]="Active Member")

Inactive Members = CALCULATE(COUNT(Bank_Churn[CustomerId]),'Active customers'[ActiveCategory]="Inactive member")
 
 A card visual was used to represent this perecntage.
 
 Snap of Active customer and inactive customer
 
![ss](https://github.com/user-attachments/assets/69d418df-3443-4bea-a255-0cc875e96f40)

 
 - Step 14 : New measure was created to calculate card holders.
 
 Following DAX expression was written to find card holders and non card holders.
 
Credit card holders = CALCULATE(COUNT(Bank_Churn[CustomerId]),'Credit card'[Category]="credit card holder")

Non credit card holders = CALCULATE(COUNT(Bank_Churn[CustomerId]),'Credit card'[Category]="non credit card holder")
    
 A card visual was used to represent the card holders.
 
 
![sss](https://github.com/user-attachments/assets/6ecd5ef6-26e1-4cd4-b5e7-bd3589ecba65)

Step 15: This card represented the Exit and Retain customer 

Following DAX expression

Exit Customers = CALCULATE(COUNT(CustomerInfo[CustomerId]),'Customer Exit'[ExitCategory]="Exit")

Retain Customers = [Total Customers]-[Exit Customers]

![ssss](https://github.com/user-attachments/assets/0eaa6b5a-6d84-4f62-b07b-2f5ead744513)
 
 - Step 16 : The report of customer churn analysis
 
 # Report Snapshot (Power BI DESKTOP)

 
![Screenshot](https://github.com/user-attachments/assets/4cc2ae32-262a-4db9-a1de-921568bec8a6)

# Insights

A single page report was created on Power BI Desktop.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 10k

   Number of Female customers = 4543

   Number of Male customers = 5457





          thus, higher number of customers are Male.
           
### [2] Number fo customers active and inactive by Location

Number of customer Active and Inactive in Spain

active = 1312, inactive = 1165

Number of customer Active and Inactive in Germany

active = 1248 inactive = 1261

Number of customer Active and Inactive in France

active = 2591, inactive = 2423
  
  
