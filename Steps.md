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
## 4. DAX Functionalitites & Data Visualization
(a) Primary KPI - Total Casualties and Total Accident values for Current Year and YoY growth
Measure to calculte total current year casualties
```
CY_Casualties = TOTALYTD(Sum(Data[Number_of_Casualties]),'Calendar'[Date])
```
 *   Add Card Total Casualties
 *   Add Card Field : CY_Casualties
 *   Format Card Accordingly
Measure to calculte total Previous year casualties
```
PreYr_Casualties = CALCULATE(SUM(Data[Number_of_Casualties]),SAMEPERIODLASTYEAR('Calendar'[Date]))
```
Measure to calculte YOY Difference in casualties
```
YoY_Casualties = ([CY_Casualties]-[PreYr_Casualties])/[PreYr_Casualties]
```
 *   Add Card Total Casualties
 *   Add Card Field : YoY_Casualties
 *   Format Card : Convert it to %
 *   Place it below CY Casualties card
 *   Select both card and group it

Copy Grouped Card and paste it for accident values card

Measure to calculate Current Year Accidents
```
CY_Accidents = TOTALYTD(Count(Data[Accident_Index]), 'Calendar'[Date])
```
Measure to calculate Previous Year Accidents
```
PreYr_Accidents = CALCULATE(COUNT(Data[Accident_Index]),SAMEPERIODLASTYEAR('Calendar'[Date]))
```
Measure to calculte YOY Difference in accidents
```
YoY_Accidents = ([CY_Accidents]-[PreYr_Accidents])/[PreYr_Accidents]
```
 *   Edit CY_Accidents, YoY_Accidents measures in the new grouped card

(b) Primary KPI's - Total Casualties by Accident Severity for Current Year and YoY growth

 *   Copy Casualties Grouped Card and paste it 3 times for accident severity card
 *   Double click on Casaulties value of card -- Drag Accident severity and drop it in filters of the card visual -- Select only "Fatal" value
 *   Similary Double click on YOY Difference value of card -- Drag Accident severity and drop it in filters of the card visual -- Select only "Fatal" value
 *   Follow the same procedure for remaining cards (i.e. Serious, Slight)

(c) Secondary KPI's - Total Casualties with respect to vehicle type for Current Year

Since there are multiple vehicle types in "Vehicle_Type" column, so we need to create new group called "Vehicle_Type(group)":
 *   Right click on "Vehicle_Type" -- New group -- Group all different vehicles into {Agriculture, Bike, Bus, Car, Other, Van}.
 *   Add Multi-row card -- Fields: [Vehicle_Type(group), CY_Casualties]
 *   Card -- visual -- uncheck Category labels
 *   Format the card & add icons for different vehicles.

(d) Monthly trend showing comparison of casualties for Current Year and Previous Year
 *   Add Area Chart (CY Casualties vs PY Casualties Monthly Trend)
 *   X-axis: Month, Y-axis: No. of Casualties, Legend: Date(Year)
 *   Format the chart
   
(e) Casualties by Road Type for Current year
 *   Add Stacked Bar Chart (Casualties by Road_Type)
 *   X-axis: Road_Type, Y-axis: CY_Casualties
 *   Format the chart
   
(f) Current Year Casualties by Area/ Location & by Day/Night
 *   Add Donut Chart (Casualties by Urban/Rural)
 *   Values: CY_Casualties, Legend: Urban/Rural_area
 *   Format the chart
 *   Similarly add Area/Location donut chart
 *   Right click on "Light_condition" -- New group -- Group all different condition into {Night, Day}.
 *   Values: CY_Casualties, Legend: Light_condition(group)
 *   Format the chart

(g) Total Casualties and Total Accidents by Location
 *   Add Maps (Casualties by Location)
 *   Location: Local_Authority_District, Latitude:Avg Latitude , Longitude: Avg Longitude
 *   Tooltip: Number_of_Casualties, Number_of_Vehicle
