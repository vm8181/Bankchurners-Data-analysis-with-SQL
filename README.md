# Bankchurners-Data-analysis-with-SQL

create database bankcustomers;
use bankcustomers;
select	* from bankchurners;

/*Count number of column in the table*/

SELECT count(*) as No_of_Column FROM information_schema.columns
WHERE table_name ='bankchurners';

/*distribution of attrited customers based on ages*/

select case when Customer_Age < 20 then '0-20' 
when Customer_Age between 20 and 30 then '20-30'
when Customer_Age between 30 and 40 then '30-40'
when Customer_Age between 40 and 50 then '40-50'
when Customer_Age between 50 and 60 then '50-60'
when Customer_Age between 60 and 70 then '60-70'
when Customer_Age> 80 then 'above 80' end as Age_range,
count(*) from bankchurners where Attrition_Flag = 'Attrited Customer'
group by Age_range order by Age_range;
 
/*number of male and females in existing & attrited customers*/

select sum(if(Gender='M',1,'Null')) as MaleExistingCustomer, sum(if(Gender = 'F', 1, 'NULL')) as FemaleExistingCustomers 
from bankchurners where Attrition_Flag = 'Existing Customer';
select sum(if(Gender = 'M', 1, 'Null')) as MaleAttritedCustomer, sum(if(Gender = 'F', 1, 'Null')) as FemaleAttritedCustomers
from bankchurners where Attrition_Flag = 'Attrited Customer';

/*education level wise distribution of existing & attrited customers*/

select distinct Education_Level from bankchurners;
select Education_Level, count(*) as 'count_of_customers' from bankchurners 
where Attrition_Flag = 'Existing Customer'
group by Education_Level order by Education_Level;
select Education_Level, count(*) as 'count_of_customers' from bankchurners 
where Attrition_Flag = 'Attrited Customer'
group by Education_Level order by Education_Level;

/*martial statuswise distribution of existing & attrited customers*/

select distinct Marital_Status from bankchurners;
select Marital_Status, count(*) as count_of_customers from bankchurners
where Attrition_Flag = 'Existing Customer'
group by Marital_Status order by Marital_Status; 
select Marital_Status, count(*) as count_of_customers from bankchurners
where Attrition_Flag = 'Attrited Customer'
group by Marital_Status order by Marital_Status; 

/*card categorywise distribution of existing & attrited customers*/

select distinct Card_Category from bankchurners;
select Card_Category, count(*) as count_of_customers from bankchurners
where Attrition_Flag = 'Existing Customer'
group by Card_Category order by Card_Category; 
select Card_Category, count(*) as count_of_customers from bankchurners
where Attrition_Flag = 'Attrited Customer'
group by Card_Category order by Card_Category; 

/*distribution of attrited customers based on months on book*/

select case when Months_on_book < 20 then '0-20' 
when Months_on_book between 20 and 30 then '20-30'
when Months_on_book between 30 and 40 then '30-40'
when Months_on_book between 40 and 50 then '40-50'
when Months_on_book between 50 and 60 then '50-60'
when Months_on_book between 60 and 70 then '60-70'
when Months_on_book > 60 then 'above 60' end as Months_on_book_range,
count(*) from bankchurners where Attrition_Flag = 'Attrited Customer'
group by Months_on_book_range order by Months_on_book_range;

/*dependent countwise distribution of existing and attrited customers*/

select Dependent_count, count(*) as 'Dependent_count' from bankchurners 
where Attrition_Flag = 'Existing Customer' group by Dependent_count order by Dependent_count DESC;
select Dependent_count, count(*) as 'Dependent_count' from bankchurners 
where Attrition_Flag = 'Attrited Customer' group by Dependent_count order by Dependent_count DESC;

/*existing and attrited customer based on average utilization*/

select Months_Inactive_12_mon, count(*) as 'Months_Inactive_12_mon' from bankchurners 
where Attrition_Flag = 'Existing Customer' group by Months_Inactive_12_mon order by Months_Inactive_12_mon DESC;
select Months_Inactive_12_mon, count(*) as 'Months_Inactive_12_mon' from bankchurners 
where Attrition_Flag = 'Attrited Customer' group by Months_Inactive_12_mon order by Months_Inactive_12_mon DESC;

/*existing and attrited customer based on inactive month*/

select Attrition_Flag, round(avg(Avg_Utilization_Ratio)*100,2) as Avg_Utilization from bankchurners
where Attrition_Flag = 'Existing Customer';
select Attrition_Flag, round(avg(Avg_Utilization_Ratio)*100,2) as Avg_Utilization from bankchurners
where Attrition_Flag = 'Attrited Customer';
