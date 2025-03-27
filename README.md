# Airline-Passenger-Satisfaction
This project analyzes airline passenger satisfaction using SQL and EDA to identify key factors affecting experience. It examines demographics, travel behavior, and service ratings, categorizing passengers by generation. Insights on delays, comfort, and service quality help airlines improve retention, reduce dissatisfaction, and optimize operations.
## Table of Contents
#### Introduction
- Project Overview
- Purpose of the Analysis
- Objectives
#### Dataset Overview
- Data Description
- Column Explanations
####  Data Processing
#### Exploratory Data Analysis (EDA)
#### SQL Queries: Extracting Insights
#### Findings & Key Insights
- Factors Contributing to Satisfaction
- Factors Leading to Dissatisfaction
#### Conclusion & Recommendations
- Summary of Insights
-Suggestions for Improving Customer Experience
#### References & Appendix


### Introduction

This project analyzes airline passenger satisfaction using SQL and EDA to identify key factors affecting experience. IT is gotten from Maven Analytics. It examines demographics, travel behavior, and service ratings, categorizing passengers by generation. Insights on delays, comfort, and service quality help airlines improve retention, reduce dissatisfaction, and optimize operations.
- Purpose of the Analysis
  
The primary goal of this analysis is to understand the key factors that influence airline passenger satisfaction. By examining various service aspects—such as flight delays, seat comfort, in-flight entertainment, and cleanliness—this study aims to identify what contributes most to customer satisfaction and dissatisfaction. Understanding these factors helps airlines enhance customer experience, improve operational efficiency, and increase customer loyalty. Additionally, this analysis will provide actionable insights into which areas require improvement, particularly for first-time travelers or economy-class passengers who may have lower satisfaction levels. The findings will guide strategic decisions to improve service quality and overall passenger experience.
- Objectives

This analysis aims to determine the key drivers of airline passenger satisfaction and dissatisfaction. By evaluating service aspects such as seat comfort, in-flight services, cleanliness, and flight punctuality, it identifies areas that impact customer experience. The study also compares satisfaction levels among different passenger segments, including travel class and customer type. These insights help airlines improve service quality, address pain points, and enhance customer loyalty. By using data-driven decision-making, airlines can optimize operations, refine customer service strategies, and create a better overall travel experience, leading to increased passenger retention and higher satisfaction ratings.
### Dataset Overview
| **Field**                                   | **Description**                                                                                                                        |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| **ID**                                      | Unique passenger identifier                                                                                                            |
| **Gender**                                  | Gender of the passenger (Female/Male)                                                                                                  |
| **Age**                                     | Age of the passenger                                                                                                                   |
| **Customer Type**                           | Type of airline customer (First-time/Returning)                                                                                        |
| **Type of Travel**                          | Purpose of the flight (Business/Personal)                                                                                              |
| **Class**                                   | Travel class in the airplane for the passenger seat                                                                                    |
| **Flight Distance**                         | Flight distance in miles                                                                                                               |
| **Departure Delay**                         | Flight departure delay in minutes                                                                                                      |
| **Arrival Delay**                           | Flight arrival delay in minutes                                                                                                        |
| **Departure and Arrival Time Convenience**  | Satisfaction level with the convenience of the flight departure and arrival times from 1 (lowest) to 5 (highest) – 0 means "not applicable" |
| **Ease of Online Booking**                  | Satisfaction level with the online booking experience from 1 (lowest) to 5 (highest) – 0 means "not applicable"                         |
| **Check-in Service**                        | Satisfaction level with the check-in service from 1 (lowest) to 5 (highest) – 0 means "not applicable"                                  |
| **Online Boarding**                         | Satisfaction level with the online boarding experience from 1 (lowest) to 5 (highest) – 0 means "not applicable"                         |
| **Gate Location**                           | Satisfaction level with the gate location in the airport from 1 (lowest) to 5 (highest) – 0 means "not applicable"                       |
| **On-board Service**                        | Satisfaction level with the on-boarding service in the airport from 1 (lowest) to 5 (highest) – 0 means "not applicable"                   |
| **Seat Comfort**                            | Satisfaction level with the comfort of the airplane seat from 1 (lowest) to 5 (highest) – 0 means "not applicable"                         |
| **Leg Room Service**                        | Satisfaction level with the leg room of the airplane seat from 1 (lowest) to 5 (highest) – 0 means "not applicable"                        |
| **Cleanliness**                             | Satisfaction level with the cleanliness of the airplane from 1 (lowest) to 5 (highest) – 0 means "not applicable"                         |
| **Food and Drink**                          | Satisfaction level with the food and drinks on the airplane from 1 (lowest) to 5 (highest) – 0 means "not applicable"                      |
| **In-flight Service**                       | Satisfaction level with the in-flight service from 1 (lowest) to 5 (highest) – 0 means "not applicable"                                   |
| **In-flight Wifi Service**                  | Satisfaction level with the in-flight Wifi service from 1 (lowest) to 5 (highest) – 0 means "not applicable"                              |
| **In-flight Entertainment**                 | Satisfaction level with the in-flight entertainment from 1 (lowest) to 5 (highest) – 0 means "not applicable"                             |
| **Baggage Handling**                        | Satisfaction level with the baggage handling from the airline from 1 (lowest) to 5 (highest) – 0 means "not applicable"                     |
| **Satisfaction**                            | Overall satisfaction level with the airline (Satisfied/Neutral or Unsatisfied)                                                           |
###  Data Processing

The dataset is gotten from Maven analytics website mainly for practise purposes. it is represnted in an excel file with asingle table and 129,880 rows and 25 column

#### Data Cleaning
The query below explains the following:
- Prevents NULL values from affecting calculations.
- Ensures consistency in analysis, as some ratings use a 0-5 scale, where 0 means "Not Applicable".
- Useful for statistical operations, such as averages and percentages, avoiding division errors.

```SQL
UPDATE airline_passenger_satisfaction
SET Departure_Delay = COALESCE(Departure_Delay, 0),
    Arrival_Delay = COALESCE(Arrival_Delay, 0),
    Departure_and_Arrival_Time_Convenience = COALESCE(Departure_and_Arrival_Time_Convenience, 0),
    Ease_of_Online_Booking = COALESCE(Ease_of_Online_Booking, 0),
    Check_in_Service = COALESCE(Check_in_Service, 0),
    Online_Boarding = COALESCE(Online_Boarding, 0),
    Gate_Location = COALESCE(Gate_Location, 0),
    On_board_Service = COALESCE(On_board_Service, 0),
    Seat_Comfort = COALESCE(Seat_Comfort, 0),
    Leg_Room_Service = COALESCE(Leg_Room_Service, 0),
    Cleanliness = COALESCE(Cleanliness, 0),
    Food_and_Drink = COALESCE(Food_and_Drink, 0),
    In_flight_Service = COALESCE(In_flight_Service, 0),
    In_flight_Wifi_Service = COALESCE(In_flight_Wifi_Service, 0),
    In_flight_Entertainment = COALESCE(In_flight_Entertainment, 0),
    Baggage_Handling = COALESCE(Baggage_Handling, 0);
```
### Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) helps uncover key patterns and insights from the dataset. First, customer demographics show that a significant portion of passengers are returning customers, with business travelers being the majority. Younger travelers (20-49 years old) form the largest age group.

Analyzing satisfaction levels, factors such as seat comfort, onboard service, and cleanliness have higher average ratings, indicating they contribute positively to customer experience. Conversely, in-flight WiFi, food and drink, and gate location often receive lower scores, highlighting areas for improvement.

Looking at travel-related factors, passengers experiencing longer delays (departure or arrival) tend to report lower satisfaction levels. Flight class significantly influences satisfaction, with business class passengers rating services higher compared to economy travelers.

For operational factors, ease of online booking and check-in services receive generally favorable feedback, suggesting a streamlined booking experience. However, baggage handling remains a point of contention, particularly among dissatisfied passengers.

Overall, high satisfaction is linked to smooth travel experiences with minimal delays and better in-flight services, while dissatisfaction is primarily driven by delays, poor WiFi, and subpar food quality. These insights help airlines identify key areas for service enhancement.

```SQL    
--create a new column
Alter Table airline_passenger_satisfaction
Add Gen int Null
----Grouping the Age into children,teenagers, youth and adult
UPDATE airline_passenger_satisfaction
SET Gen =
    CASE    
        WHEN Age BETWEEN 1 AND 12 THEN 'Children'
        WHEN Age BETWEEN 13 AND 19 THEN 'Teenagers'
        WHEN Age BETWEEN 20 AND 49 THEN 'Youth'
        ELSE 'Adult'
    END;
```
Explanation:
- BETWEEN 1 AND 12 → Categorizes passengers as "Children."

- BETWEEN 13 AND 19 → Categorizes passengers as "Teenagers."

- BETWEEN 20 AND 49 → Categorizes passengers as "Youth."

- ELSE 'Adult' → Categorizes passengers 50 and above as "Adult."

  ### SQL Queries: Extracting Insights
  SQL queries help analyze airline passenger satisfaction by identifying trends and key factors influencing customer experiences. To segment passengers, a Gen column is created based on age groups. Queries can calculate the percentage of satisfied passengers by generation, identify the most common travel class among satisfied passengers, and analyze average ratings for different services (e.g., seat comfort, in-flight WiFi, food quality). Additionally, queries can evaluate the impact of delays on satisfaction by comparing ratings for flights with and without delays. These insights help airlines improve services, enhance customer retention, and optimize operational efficiency.
 #### Satisfaction Analysis by Generation
```SQL
 	---percentage of airline passengers are satisfied using Gen
SELECT Gen,
    COUNT(CASE WHEN Satisfaction = 'Satisfied' THEN 1 END) * 100 / COUNT(*) AS SP
FROM airline_passenger_satisfaction
GROUP BY Gen
ORDER BY SP DESC
```
Explanation
- Gen: Groups the results by generation (Children, Teenagers, Youth, Adults).
- COUNT(CASE WHEN Satisfaction = 'Satisfied' THEN 1 END): Counts only the passengers who marked their satisfaction as "Satisfied".
- COUNT(*): Counts all passengers in that generation.
- Multiplication by 100.0 ensures accurate percentage calculation (avoids integer division).
- Sorts the results in descending order, so the generation with the highest satisfaction percentage appears first.

```SQL
--- numbers of the total trip taken by returning passengers grouped by GEN
SELECT Gen,  
    COUNT(*) AS Total_Trips
FROM airline_passenger_satisfaction
WHERE Customer_type = 'Returning'
GROUP BY Gen
ORDER BY Total_Trips DESC;
```
Explanation
- Gen: Groups passengers by generation (Children, Teenagers, Youth, Adults).
- COUNT(*) AS Total_Trips: Counts the total number of trips taken by returning passengers in each generation.
- Filters the data to include only returning passengers (Customer_type = 'Returning').
- Groups passengers by generation to calculate trip totals per age group.
- Sorts the results in descending order, displaying the generation with the highest number of trips first.

```SQL
--numbers of average flight distance, delays, and Time Convenience for returning passengers.
SELECT 
    Gen,  
    AVG(Flight_Distance) AS Avg_Flight_Distance,
    AVG(Departure_Delay) AS Avg_Departure_Delay,
	AVG(Arrival_Delay) AS Avg_Arrival_Delay,
    AVG(Departure_and_Arrival_Time_Convenience) AS Avg_Departure_and_Arrival_Time_Convenience
FROM airline_passenger_satisfaction
WHERE Customer_type = 'Returning'
GROUP BY Gen
ORDER BY Avg_Flight_Distance DESC;
```
Purpose
This analysis helps airlines understand flight behavior and experience across different generations:
- Which generation travels the longest distances?
- Which generation experiences the most delays?
- How satisfied are different age groups with flight timing?

For example:
- If Adults travel the longest distances but have high delays, airlines may need to improve long-haul flight scheduling.
- If Youth have low time convenience ratings, flexible scheduling or more direct flights may improve satisfaction.

```SQL
---the experience ratings by returning Passengers
SELECT 
    Gen,  
    AVG(Ease_of_Online_Booking) AS Avg_Online_Booking_Ease,
    AVG(Check_in_Service) AS Avg_Checkin_Service,
    AVG(Online_Boarding) AS Avg_Online_Boarding,
    AVG(On_board_Service) AS Avg_Onboard_Service,
    AVG(Seat_Comfort) AS Avg_Seat_Comfort,
    AVG(Leg_Room_Service) AS Avg_Leg_Room_Service,
    AVG(Cleanliness) AS Avg_Cleanliness,
    AVG(Food_and_Drink) AS Avg_Food_and_Drink,
    AVG(In_flight_Service) AS Avg_In_flight_Service,
    AVG(In_flight_Wifi_Service) AS Avg_In_flight_Wifi,
    AVG(In_flight_Entertainment) AS Avg_In_flight_Entertainment,
    AVG(Baggage_Handling) AS Avg_Baggage_Handling
From airline_passenger_satisfaction
WHERE Customer_type = 'Returning'
GROUP BY Gen
ORDER BY Avg_Online_Boarding DESC;
```
Purpose of the Query

This analysis helps airlines understand how different generations experience air travel and identify pain points.

For example:
- If Youth rate In-flight WiFi poorly, airlines might invest in better connectivity.
- If Adults have low Check-in ratings, they may prefer faster check-in options or priority services.
- If Teenagers rate Online Boarding highly, the airline’s digital systems may already be effective for tech-savvy users.

```SQL
--does longer delays lead to lower satisfaction grouped by GEN
SELECT 
	Gen,
    Satisfaction, 
    AVG(Departure_Delay) AS Avg_Departure_Delay,
    AVG(Arrival_Delay) AS Avg_Arrival_Delay
FROM airline_passenger_satisfaction
GROUP BY Gen, Satisfaction
ORDER BY Gen, Satisfaction;
```
Insights
- If longer delays (higher Avg_Departure_Delay and Avg_Arrival_Delay) correlate with lower satisfaction, we expect:
- Higher delays for Neutral/Unsatisfied passengers.
- Lower delays for Satisfied passengers.
- If satisfaction is not impacted by delays, both satisfied and unsatisfied passengers will have similar delay averages.

#### Analysis on Customers
```SQL
-----Filtering based on levels 
--- people who took economy class for a business trip
 Select *
From airline_passenger_satisfaction
where Class = 'Economy'
and Type_of_Travel = 'business'
```
Insights
- Number of Business Travelers in Economy:
- Helps identify how many business passengers choose Economy class over Business or First class.
- Satisfaction Trends:
 Further analysis can compare if business travelers in Economy class are more or less satisfied than those in higher classes.
- Flight Delay Impact:
 Check if Economy-class business travelers experience more delays than those in higher classes.























