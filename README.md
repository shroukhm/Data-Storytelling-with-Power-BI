#      HR analysis dashboard

### Dashboard Link : https://app.powerbi.com/links/YD2uVgYrXN?ctid=77255288-5298-4ea5-81aa-a13e604c30ac&pbi_source=linkShare

## Problem Statement

Market fluctuations and rapidly changing technology have affected the global market. Many published reports showed that around half of the employees wanted to change jobs. While some market researchers said that flexible working and job security were their primary factors, few admitted that a higher salary was their aim.

Different regions saw an increase and a decrease in salaries over the years. While the increase was to retain top-level professional employees, the pay cuts were due to market fluctuations and were resorted after the market conditions improved. HR people across the globe are hiring new employees, trying to retain and understand the needs of employees who got separated (those who left the company).

So, how does the HR department make these decisions in volatile market conditions? They rely on HR analytics to understand the existing situation and develop a new modern approach. For this requirement, you have been asked in your company to build a dashboard in Power BI considering the following challenges of HR people and provide an effective way to find the answers to their day-to-day questions.

### Steps followed 

- Step 1 : Load the HR data set into Power BI Desktop, dataset is a excel file.
- Step 2 : Load data into the Power BI Query Editor and perform the required actions.
- Step 3 : Establish the required relationships.
- Step 4 : Create the DAX column in the BU table:

              Region = mid('BU'[RegionSeq], 3,15).

    Create the below columns in the Employee table:

              AgeGroupID = IF([Age]<30, 1, IF([Age]<50, 2, 3)) 

              isNewHire = IF(YEAR([date]) = YEAR([HireDate]) &&    
              MONTH([date])=MONTH([HireDate]), 1)

              TenureDays = IF([date]-[HireDate]<0,[HireDate]-[date],[date]-[HireDate])  
      
- Step 5 :  Create a new measure table (separate table using Enter data) and place all the measures into this table.
- Step 6 : Create a new Measure EmpCount :

      EmpCount = CALCULATE(COUNT(Employee[EmplID]), FILTER(ALL('Date'[PeriodNumber]), 'Date'[PeriodNumber] = MAX('Date'[PeriodNumber])))

- Step 7 : Create a Measure for Active Employees:

      Actives = CALCULATE([EmpCount], FILTER(Employee, ISBLANK(Employee[TermDate]))) //total active employees 
- Step 8 :  Create a Measure called New Hires, which will have the sum of the new NewHire in the Employee table.
- Step 9 : Create a Measure called Separations :

      Separations = CALCULATE(COUNT(Employee[EmplID]), FILTER(Employee, NOT(ISBLANK(Employee[TermDate]))))     //separations/employees who left
- Step 10 : Create a Measure called AVG Tenure Days which has an average column TenureDays from Employee table.
- Step 11 : Create a Measure called AVG Tenure Months :

      AVG Tenure Months = ROUND([AVG Tenure Days]/30, 1)-1

- step 12 : Create a Measure called Female Emp Actives :


      Female Emp Actives = CALCULATE([Actives],Gender[Gender]=”Female”)
- step 13 : Create a Measure called Female New Hires using New Hires.
- step 14 : Create a Measure called Female Separationss

       Female Separationss = CALCULATE([Separations],Gender[Gender]="Female")    

- step 15 : Create a Measure called Male Actives :

      Male Actives = CALCULATE([Actives],Gender[Gender]="Male") //how many Active male employees 

- step 16 : Create a Measure called Male New Hires :

      Male New Hires = CALCULATE([New Hires],Gender[Gender]="Male") //how many new hire male employees 

- step 17 : Create a Measure called Male Separations :

      Male Separations = CALCULATE([Separations],Gender[Gender]="Male") // male employees who leftor separations       
  

- step 18 : create the report in Power BI.
     - show ative employees in cards 
     - employees separations in cards 
     - new Hires in cards
     - make steaked bar chart to show Active employee by age group
     - make clustered column chart to show AVG Tenure Months by Region and Gender
     - make line chart to show New Hire by Region and Job type
     - make bar plot to show New Hire by age group
     - make steaked bar chart to show Separations by Region and Age group
 - Step 19 : The report was then published to Power BI Service.
 

# Snapshot of Dashboard (Power BI Service)

![Capture](https://github.com/shroukhm/Data-Storytelling-with-Power-BI/assets/134003439/d3b82af9-1307-4b7d-8cbf-710780964e51)

 
