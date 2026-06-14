# 🏦 Bank Loan Analysis Dashboard

## 🎯 Business Objective
To analyze loan applications, funded amounts, repayments, loan quality, and borrower behavior to help banks make data-driven lending decisions, manage risk, and improve portfolio performance.

A.	BANK LOAN REPORT | SUMMARY

### KPI 1 Total Loan Applications
Select count(id) as total_loan_applications
from bank_loan_data

MoM Loan Applications 
Select count(id) as total_loan_app_by_latestmonth
from bank_loan_data
where month(issue_Date) = (select month(max(issue_date)) from bank_loan_data)
Select count(id) as total_loan_app_by_prevmonth
from bank_loan_data
where month(issue_Date) = (select month(max(issue_date))-1 from bank_loan_data)
 
 

Advance Method :
Declare @CurrentMonth decimal(10,2);
Select @CurrentMonth = count(id)
from bank_loan_data
where month(issue_Date) = (select month(max(issue_date)) from bank_loan_data);

Declare @PrevMonth decimal(10,2);
Select @PrevMonth = count(id)
from bank_loan_data
where month(issue_Date) = (select month(max(issue_date))-1 from bank_loan_data);

Declare @MoM_LoanApp decimal(10,2);
Set @MoM_LoanApp = ((@CurrentMonth -@PrevMonth) / @PrevMonth) * 100

Select concat(@MoM_LoanApp, ' %') as MoM_LoanAppPercent;

 

### KPI 2 Total Fund MoM
Declare @totalfund decimal(15,2)
Select @totalfund =sum(loan_amount) from bank_loan_data

Declare @LatestMonthFundedAmnt decimal(10,2)
Select @LatestMonthFundedAmnt =sum(loan_amount) from bank_loan_data
where month(issue_date)= (select month(max(issue_date)) from bank_loan_data)

Declare @PrevMonthFundedAmnt decimal(10,2)
Select @PrevMonthFundedAmnt =sum(loan_amount) from bank_loan_data
where month(issue_date)= (select month(max(issue_date))-1 from bank_loan_data)

Declare @MoMFundedAmountPerc decimal(10,2)
Set @MoMFundedAmountPerc = ((@LatestMonthFundedAmnt -@PrevMonthFundedAmnt)/@PrevMonthFundedAmnt) * 100

Select 
@totalfund as totalfund,
@LatestMonthFundedAmnt as latestmonthfund,
@PrevMonthFundedAmnt as prevmonthfund, 
concat(@MoMFundedAmountPerc,' %') as MoMFundedAmountPercent

 


### KPI 3 Total Received Amount (MoM)
Declare @totReceivedAmnt decimal(15,2)
Select @totReceivedAmnt =sum(total_payment) from bank_loan_data

Declare @LatestMonthReceivedAmnt decimal(10,2)
Select @LatestMonthReceivedAmnt =sum(total_payment) from bank_loan_data
where month(issue_date)= (select month(max(issue_date)) from bank_loan_data)

Declare @PrevMonthReceivedAmnt decimal(10,2)
Select @PrevMonthReceivedAmnt =sum(total_payment) from bank_loan_data
where month(issue_date)= (select month(max(issue_date))-1 from bank_loan_data)

Declare @MoMReceivedAmountPerc decimal(10,2)
Set @MoMReceivedAmountPerc = ((@LatestMonthReceivedAmnt -@PrevMonthReceivedAmnt)/@PrevMonthReceivedAmnt) * 100

Select 
@totReceivedAmnt as TotalReceivedAmount,
@LatestMonthReceivedAmnt as LatestmonthReceivedAmount,
@PrevMonthReceivedAmnt as PrevmonthReceivedAmount,
concat(@MoMReceivedAmountPerc,' %') as MoMReceivedAmountPercent

 





### KPI 4 Average Interest rate(MoM)
Declare @AvgIntrate decimal(10,2)
Select @AvgIntrate=avg(int_rate)*100 from bank_loan_data

Declare @AvgIntrateCurrMnth decimal(10,2)
Select @AvgIntrateCurrMnth=avg(int_rate)*100 from bank_loan_data
where month(issue_date)= (select month(max(issue_date)) from bank_loan_data)

Declare @AvgIntratePrevMnth decimal(10,2)
Select @AvgIntratePrevMnth=avg(int_rate)*100 from bank_loan_data
where month(issue_date)= (select month(max(issue_date))-1 from bank_loan_data)

Declare @AvgIntrateMoM decimal(10,2)
Set @AvgIntrateMoM = ((@AvgIntrateCurrMnth-@AvgIntratePrevMnth)/@AvgIntratePrevMnth)*100

Select 
@AvgIntrate as AvgInterestRate,
@AvgIntrateCurrMnth as AvgInterestRateCurrMonth,
@AvgIntratePrevMnth as AvgInterestRateLatMonth,
concat(@AvgIntrateMoM,' %') as MoMAvgInterestRate
 

### KPI 5 Average Debt To Income (MoM)
Declare @AvgDTI decimal(10,2)
Select @AvgDTI=avg(dti)*100 from bank_loan_data

Declare @AvgDTICurrMnth decimal(10,2)
Select @AvgDTICurrMnth=avg(dti)*100 from bank_loan_data
where month(issue_date)= (select month(max(issue_date)) from bank_loan_data)

Declare @AvgDTIPrevMnth decimal(10,2)
Select @AvgDTIPrevMnth=avg(dti)*100 from bank_loan_data
where month(issue_date)= (select month(max(issue_date))-1 from bank_loan_data)

Declare @AvgDTIMoM decimal(10,2)
Set @AvgDTIMoM = ((@AvgDTICurrMnth-@AvgDTIPrevMnth)/@AvgDTIPrevMnth)*100

Select 
@AvgDTI as AvgDebtToIncome,
@AvgDTICurrMnth as CurrMonthAvgDebtToIncome,
@AvgDTIPrevMnth as LatMonthAvgDebtToIncome,
concat(@AvgDTIMoM,' %') as MoMAvgDebtToIncome

 









### KPI 6 Good Loan KPI’s

Declare @TotalLoanApp decimal(10)
Select  @TotalLoanApp= count(id) from bank_Loan_data

Declare @GoodLoanApp decimal(10)
SELECT @GoodLoanApp = COUNT(*) FROM bank_Loan_data
WHERE loan_status IN ('Fully Paid', 'Current');

Declare @GoodLoanAppPerc decimal(5,2)
SET @GoodLoanAppPerc= (@GoodLoanApp*100) / @TotalLoanApp

Declare @GoodLoanFundedAmount decimal (15,2)
Select @GoodLoanFundedAmount=sum(loan_amount) from bank_Loan_data
WHERE loan_status IN ('Fully Paid', 'Current');

Declare @GoodLoanReceivedAmount decimal(15,2)
Select @GoodLoanReceivedAmount=sum(total_payment) from bank_Loan_data
WHERE loan_status IN ('Fully Paid', 'Current');

Select @TotalLoanApp as TotalLoanApplications,
@GoodLoanApp as GoodLoanApplications,
concat(@GoodLoanAppPerc,' %') as GoodLoanApplicationPercentage,
@GoodLoanFundedAmount as GoodLoanFundedAmount,
@GoodLoanReceivedAmount as GoodLoanReceivedAmount

 

### KPI 7 BAD Loan KPI’s
Declare @TotalLoanApp decimal(10)
Select  @TotalLoanApp= count(id) from bank_Loan_data

Declare @BadLoanApp decimal(10)
SELECT @BadLoanApp = COUNT(*) FROM bank_Loan_data
WHERE loan_status ='Charged Off';

Declare @BadLoanAppPerc decimal(5,2)
SET @BadLoanAppPerc= (@BadLoanApp*100) / @TotalLoanApp

Declare @BadLoanFundedAmount decimal (15,2)
Select @BadLoanFundedAmount=sum(loan_amount) from bank_Loan_data
WHERE loan_status ='Charged Off';

Declare @BadLoanReceivedAmount decimal(15,2)
Select @BadLoanReceivedAmount=sum(total_payment) from bank_Loan_data
WHERE loan_status ='Charged Off';

Select @TotalLoanApp as TotalLoanApplications,
@BadLoanApp as BadLoanApplications,
concat(@BadLoanAppPerc,' %') as BadLoanApplicationPercentage,
@BadLoanFundedAmount as BadLoanFundedAmount,
@BadLoanReceivedAmount as BadLoanReceivedAmount

 


### KPI 8 LOAN STATUS
SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM
        bank_loan_data
    GROUP BY
        loan_status
 

SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data
WHERE MONTH(issue_date) =(select month(max(issue_date)) from bank_loan_data)
GROUP BY loan_status
 

BY MONTH
SELECT 
	MONTH(issue_date) AS Month_Munber, 
	DATENAME(MONTH, issue_date) AS Month_name, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date)

 

BY STATE
SELECT 
	address_state AS State, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY count(id) desc
 


BY TERM
SELECT 
	term AS Term, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term
 

BY EMPLOYEE LENGTH
SELECT
    emp_length AS Employee_Length,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY
    CASE
        WHEN emp_length = '< 1 year' THEN 0
        WHEN emp_length = '1 year' THEN 1
        WHEN emp_length = '2 years' THEN 2
        WHEN emp_length = '3 years' THEN 3
        WHEN emp_length = '4 years' THEN 4
        WHEN emp_length = '5 years' THEN 5
        WHEN emp_length = '6 years' THEN 6
        WHEN emp_length = '7 years' THEN 7
        WHEN emp_length = '8 years' THEN 8
        WHEN emp_length = '9 years' THEN 9
        WHEN emp_length = '10+ years' THEN 10
        ELSE 11
    END;
 


BY PURPOSE
SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY purpose
 

BY HOME OWNERSHIP
SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY home_ownership
ORDER BY home_ownership
 

