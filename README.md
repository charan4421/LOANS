PROBLEM STATEMENT(BANK LOAN REPORT)
This project focuses on a Bank Loan Report Dashboard that visualizes data related to loan applications, funded amounts, interest rates, and Debt-to-Income (DTI) ratios using Power BI. The dashboard provides comprehensive insights into loan performance across different categories, such as loan purpose, homeownership status, loan grade, and more.

Before visualizing the data in Power BI, Machine Learning techniques were applied using Python to extract meaningful insights and predict trends.


Data Sources:

***** STEP : 1  The raw data consists of loan applications, funded amounts, interest rates, installments, and more. It was processed and transformed using Python before being imported into Power BI for visualization.

***** STEP : 2  Machine Learning Techniques:

Data Preprocessing:

Missing data was handled using imputation methods (e.g., mean, mode imputation).

Data normalization techniques were applied to ensure the features used in machine learning models are on a similar scale.

******STEP : 3   Feature Engineering:

Additional features were engineered, such as a "Risk Score" based on loan grade, subgrade, and the borrower’s DTI ratio.

Time-based features (such as loan_issue_date) were extracted for time-series analysis.

****** STEP :4  Predictive Modeling:

Logistic Regression: Used to predict the probability of loan default based on features such as loan purpose, homeownership status, interest rates, and more.

Random Forest: A Random Forest Classifier was trained to predict loan risk levels based on multiple features (e.g., loan amount, grade, DTI).

Linear Regression: Applied to predict the total amount to be received over time based on installment and interest rate.

K-Means Clustering: Used to group loans into different clusters based on funding amounts, grades, and interest rates for identifying high-risk segments.

STEP 5 : Now add the data into the power bi
Step 6 : Again Transform the Data For Accurate Insights and load the data into the REPORT VIEW
STEP 7: create a new measure for finding total application

        1)	Total Loan Application = Count(Loan_table[id])
        2)	MTD Loan Applications = calculate(totalmtd([Total Loan Application],'DATE TABLE'[date]))
        3)	PMTD Loan Applications = calculate([Total Loan Application],Datesmtd(dateadd('DATE TABLE'[Date],-1,month)))
        4)	Mom Loan Application = ([Mtd loan applications]-[PMTD Loan Applications])/[PMTD Loan Applications]  
        
 STEP 8: Create a new Measure For Finding total funded Amount

        1)	total Funded Amount = Sum(Loan_table[loan_amount])
        2)	MTD Funded amount = calculate(totalmtd([total Funded Amount],'DATE TABLE'[date]))
        3)	PMTDtotal funded amount = calculate([total Funded Amount],Datesmtd(dateadd('DATE TABLE'[Date],-1,month)))
        4)	Mom total Funded Amount = ([MTD Funded amount]-[PMTDtotal funded amount])/[PMTDtotal funded amount]

  STEP 9: Create a new Measure for total amoount Recieved

         1)	Total Amount Received = sum(Loan_table[total_payment])
         2)	MTD Total Amount Recived = calculate(totalmtd([Total Amount Received],'DATE TABLE'[Date]))
         3)	pmtd total amount Recieved = calculate([MTD Total Amount Recived],datesmtd(dateadd('DATE TABLE'[date],-1,month)))
         4)	mom Total Amount recieved = ([MTD Total Amount Recived]-[pmtd total amount Recieved])/[pmtd total amount Recieved]

  STEP 10 : Create a new measure for Avg Interest rate
       1)	Avg Interest Rate = average(Loan_table[int_rate])
       2)	MTD Average Int rate = calculate(totalmtd([Avg Interest Rate],'DATE TABLE'[date]))
       3)	PMTDtotal average int amount = calculate([Avg Interest Rate],Datesmtd(dateadd('DATE TABLE'[Date],-1,month)))
       4)	Mom Avg Interst Amount = ([MTD Average Int rate]-[PMTDtotal average int amount])/[PMTDtotal average int amount]

   STEP 11 : create a new measure for  Average DTI

       1)	Avg DTI = average(Loan_table[dti])
       2)	MTD Average DTI = calculate(totalmtd([Avg DTI],'DATE TABLE'[date]))
       3)	PMTD Avg DTI = calculate([Avg DTI],Datesmtd(dateadd('DATE TABLE'[Date],-1,month)))
       4)	Mom Average Dti = ([MTD Average DTI]-[PMTD Avg DTI])/[PMTD Avg DTI]

  STEP 12:  Create a new measure for GOOD LOAN APPLICATIONS

  
       1)	Good Loan Applications = calculate([Total Loan Application],Loan_table[Good Vs Bad Loan]="Good Loan")
       2)	Good Loan % = (CALCULATE([Total Loan Application],Loan_table[Good Vs Bad Loan]="good loan"))/[Total Loan Application]
       3)	Good Loan Funded Amount = calculate([total Funded Amount],Loan_table[Good Vs Bad Loan]="Good Loan")
       4)	Good Recievd Amount = calculate([Total Amount Received],Loan_table[Good Vs Bad Loan]="Good Loan")

 Step 13 :Create a new measure for  BAD LOAN APPLICATION

 
      1)	Bad Loan Applications = calculate([Total Loan Application],Loan_table[Good Vs Bad Loan]="Bad Loan")
      2)	Bad Loan % = (CALCULATE([Total Loan Application],Loan_table[Good Vs Bad Loan]="bad loan"))/[Total Loan Application]
      3)	Bad Recievd Amount = calculate([Total Amount Received],Loan_table[Good Vs Bad Loan]="Bad Loan")
      4)	Bsd Loan Funded Amount = calculate([total Funded Amount],Loan_table[Good Vs Bad Loan]="Bad Loan")


Step 14 : Additionally create new measure for Date Table for further use

       DATE TABLE = CALENDAR(min(Loan_table[issue_date]),max(Loan_table[issue_date]))
       Month = format('DATE TABLE'[Date],"mmm")
       Month Number = month('DATE TABLE'[Date])


Step 15 : Link the loan table with Date table by primary and foreign keys

*** AFTER APPLYING VISUALISATION THE REPORT LOKKS LIKE******
![Screenshot 2024-09-13 172737](https://github.com/user-attachments/assets/0829ada1-a536-400f-af7e-be6502b84709)



Evaluation:

Models were evaluated using metrics such as accuracy, precision, recall, and F1-score for classification models. For regression models, R-squared and Mean Squared Error (MSE) were used.

******INSIGHTS FOR THE PROJECT*****

1. Loan Applications:

Total loan applications: 38.6K

Monthly increase (MoM): 6.9%

There has been a 4.3K loan application increase month-over-month, showing a steady rise in demand for lo                       


2. Total Funded Amount:

The total funded amount reached $435.8M, with a 13.0% month-over-month growth.

This indicates healthy bank operations and increased approval rates.

3. Total Amount Received:

The total amount received stood at $473.1M, a 15.8% month-over-month growth.


4. Interest Rates:

The average interest rate across all loans is 12.0%, with minor variations (MoM: 3.5%).


5. Debt-to-Income (DTI):

The average DTI ratio is 13.3%, which has seen a slight reduction of 2.7% MoM. This suggests better creditworthiness among borrowers.



6. Loan Distribution:

Loans for car purchases dominate, with a high percentage having mortgage as their home ownership status.

Majority of the loans fall in Grade A and Sub-Grade A1, indicating high-quality loans.



7. Installments:

A range of installment amounts is observed, with the highest installment being $1,988.98, contributing significantly to the total amount received.

Project Structure:

data_preprocessing.py: Contains all scripts used for cleaning and transforming raw data.

feature_engineering.py: Performs feature extraction and engineering.

modeling.py: Scripts for applying machine learning models.

visualization.pbix: The Power BI file containing the visualized dashboard.






















  
 

        
     



  

