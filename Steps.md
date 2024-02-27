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
