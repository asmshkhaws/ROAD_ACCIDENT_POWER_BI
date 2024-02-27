## 1. Data Cleaning
 *   Home -- Transform Data -- Select Acccident_Severity -- Replace Values -- Value to Find(Fetal) -- Repalce With (Fatal) -- Ok -- Close & Apply

## 2. Data Processing
  (a) Create Calender Table
    
 *   Always create a date(Calendar) Table  whenever required in project
  
 *   Make sure Time Intelligence function is on in setting(File -- Option -- Data Load -- Check Auto Date/time for new files)
  
 *   Modelling -- New Table --
```
Calendar = CALENDAR(Min(Data[Accident Date]),MAX(Data[Accident Date]))
```
 *   Add 3 Columns in Calendar Table
```
Year = Year('Calendar'[Date])
Month = FORMAT('Calendar'[Date],"mmm")
Month_Number = MONTH('Calendar'[Date])
```
## 3. Data Modelling
(a) Create Relationship between Calendar and Data Table
 *   Model View -- Drag Accident date from Data -- Drop it in Calendar Table
 *   One to many Relationship is developed between both
## 4. DAX Functionalitites
 *   Primary KPI - Total Casualties and Total Accident values for Current Year and YoY growth
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
PreYr_Casualties = CALCULATE(SUM(Data[Number_of_Casualties]),SAMEPERIODLASTYEAR('Calendar'[Date]))
YoY_Casualties = ([CY_Casualties]-[PreYr_Casualties])/[PreYr_Casualties]
```
 *   Primary KPI's - Total Casualties by Accident Severity for Current Year and YoY growth
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Secondary KPI's - Total Casualties with respect to vehicle type for Current Year
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Monthly trend showing comparison of casualties for Current Year and Previous Year
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Casualties by Road Type for Current year
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Current Year Casualties by Area/ Location & by Day/Night
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Total Casualties and Total Accidents by Location
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
