# PBI-Road-Acccident-Analysis

![Dashboard Image](https://github.com/IsaacMwendwa/PBI-Road-Accident-Analysis/blob/main/Final%20Dashboard%20Image.PNG "Final Dashboard Image")

## Table of Contents
* [Introduction](#Introduction)
* [Dashboard Requirements](#Dashboard-Requirements)
* [Installation / Usage](#Installation--Usage)
* [DAX Formulas Used in Measures](#DAX-Formulas-Used-in-Measures)
* [Bug / Feature Request](#Bug--Feature-Request)
* [Authors](#Authors)
  
## Introduction
* This project is aimed at developing a Power BI Dashboard for generating insights about road accident data in the United Kingdom.
* The dataset can be accessed from this link: [Road Accident Data (UK)](https://drive.google.com/drive/folders/1G3BFBOcSn-i-8aJ6c_MgGWJzhYWM_Okb?usp=sharing)
  
## Dashboard Requirements
* Primary KPI's - Total Casualties and Total Accident values for Current Year and YoY Growth
* Primary KPI's - Total Casualties by Accident Severity for Current Year and YoY Growth
* Secondary KPI's - Total Casualties with respect to Vehicle Type for Current Year
* Monthly Trend showing comparison of Casualties for Current Year and Previous Year
* Casualties by Road Type for Current Year
* Current Year Casualties by Area/Location & Day/Night
* Total Casualties and Total Accident by Location

## Data Cleaning

* Labelling the incorrect "Fetal to Fatal" and "Auto traffic sigl" to "Auto traffic signal" for proper grouping of data in "accident_severity" and "Give away or controlled" in these 2 columns

## Creating Relationship

* Creating a new table named Calender using accident_date from data
Formulae = CALENDAR(MIN(Data[Accident Date]),MAX(Data[Accident Date]))

- with columns Year and Month
- Formulae Year = Year('Calendar'[Date])
- Formulae Month = Month = Format('Calendar'[Date],"mmm")

* With this Date Column from Calender and accident_date from data we will create one to many relationship and then using Date column further so we dont come across errors while playing with dates in further visualizations

## Grouping of data

* I have created groups(bucketing) of some columns cause they weren't strutured enough for further visualization and filters perspective
a) Vechile type for visulization in multirow card
b) Weather Conditions and Road surface area for filters

## More DAX Formulas Used in Measures

**1. Total Casualties For Current Year and Year on Year Growth**

(a) Current Year To Date Casualties -- CY Casualties Measure
* `CY Casualties = TOTALYTD(SUM(Data[Number_of_Casualties]), 'Calendar'[Date])`

(b) Previous Year Casualties -- PY Casualties Measure
* `PY Casualties = CALCULATE(SUM(Data[Number_of_Casualties]), SAMEPERIODLASTYEAR('Calendar'[Date]))`

(c) Year on Year Growth of Casualties - YoY Casualties Measure
* `YoY Casualties = ([CY Casualties] - [PY Casualties])/[PY Casualties]`

**2. Total Accidents for Current Year and Year on Year Growth**

(a) Current Year Accidents Count -- CY Accidents Count Measure
*  `CY Accidents Count = TOTALYTD(COUNT(Data[Accident_Index]), 'Calendar'[Date])`

(b) Previous Year Accidents Count -- PY Accidents Count Measure
* `PY Accidents Count = CALCULATE(COUNT(Data[Accident_Index]), SAMEPERIODLASTYEAR('Calendar'[Date]))`

(c) Year on Year Growth of Accidents - YoY Accidents Measure
* `YoY Accidents = ([CY Accidents Count]-[PY Accidents Count])/[PY Accidents Count]`


## Observations and Insights

#### 1.	Casualties by Vehicle Type Analysis:
The major cause of casualties on the roads are cars followed by vans and bikes. Cars caused more than half of casualties (almost 80%). Both vans and bikes caused 8% of casualties. This highlights the significant impact and involvement of cars in road accidents. It is crucial to address factors such as driver behavior, road infrastructure, and vehicle safety measures to mitigate the risks associated with car accidents.

 ![](Casualties%20by%20Vehicle%20Type.png)


#### 2.  Casualties by Road Type Analysis:
The major cause of casualties by road type is caused by single carriageway. This caused over 70% of casualties. Both dual carriageway and roundabout caused about 6% of casualties. This indicates that single carriageway roads pose a significant risk to road users and require attention in terms of safety improvements and accident prevention measures.
Understanding the specific factors contributing to accidents on dual carriageway and roundabouts can also inform targeted interventions.

 ![](Casualties%20by%20Road%20Type.png)


#### 3.	Casualties by Urban/Rural Analysis:
More than 50% of casualties happened in the Urban areas as compared to 38% in the rural areas. This suggests that urban areas pose a higher risk for road accidents and require increased attention to improve road safety measures. Factors such as higher population density, increased traffic volume, complex road networks, and various modes of transportation interacting in urban environments may be contributing to the higher casualty rate.

 ![](Casualties%20by%20Urban_Rural.png)


#### 4.	Casualties by Light Conditions Analysis:
More than 70% of accidents happened during the daytime as compared to 26% at night. This suggests that the risk of accidents is higher when visibility conditions are generally better. Factors such as increased traffic volume, higher speeds, driver fatigue, and distractions during the day may contribute to the higher occurrence of accidents.
While the percentage of accidents at night is lower, around 26%, it still represents a notable portion of the total. Nighttime driving poses its own set of challenges, including reduced visibility, driver impairment, and increased difficulty in perceiving hazards. Therefore, it is important to address factors specific to nighttime driving, such as improving street lighting, promoting driver awareness of nighttime hazards, and enforcing regulations related to impaired driving and visibility-enhancing measures.

 ![](Casualties%20by%20Light%20Conditions.png)


## Visualizations (Report and Dashboard)

The report comprises of a page with two slicers and diverse visuals that interact with each other. 


  ![](Road%20Accident%20Analysis%20Report%20Screenshot.png)





  
