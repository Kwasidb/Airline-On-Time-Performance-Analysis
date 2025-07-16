# Airline On-Time Performance Analysis

---

## Project Background

The U.S. Department of Transportation (DOT) oversees the performance and reliability of commercial airline operations across the country. As part of its mission to improve transportation efficiency and consumer satisfaction, the DOT collects and analyzes flight performance data from domestic airlines to monitor trends and identify areas for improvement.

This project focuses on analyzing commercial airline flight data from Q4 2024. The dataset includes detailed information on flight delays, cancellations, and route activity across major U.S. carriers and airports.

This analysis was conducted to uncover performance trends, evaluate airport and airline reliability, and provide data-driven recommendations to improve service quality and operational efficiency.

Stakeholders across the DOT, including regulatory teams, airport authorities, infrastructure planners, and policy makers, will use these insights to enhance airline compliance, improve airport operations, optimize route management, and guide policy decisions to boost overall air travel efficiency and passenger experience.

Insights and recommendations are provided on the following key areas:

- Delay Trends: What are the primary contributors to flight delays? Can these delays be mitigated? Where and when are delays most frequently occurring?
  
- Airport & Route Analysis: Which airports experience the highest volumes of delayed flights? Are there specific routes that underperform or show operational challenges?

- Airline Operational Performance: Which airlines consistently meet their schedules? Are certain carriers outperforming others in terms of cancellations and on-time arrivals?

The SQL queries used to inspect and clean the data for this analysis can be found [here](Database%Design.sql).

Targeted SQL queries regarding various business questions can be found [here](Business%20Problems.sql).

An interactive Power BI dashboard used to report and explore performance trends can be found [here](Dashboard.pbix).

---

## Data Structure & Initial Checks

The Department of Transportation’s main database structure for this analysis consists of 6 tables: flights, carriers, airports, cancel codes, markets, and world areas, with a total row count of approximately 1.8 million records. A description of each table is as follows:

- Flights: contains fact details for individual flights including flight ID, date and time, airline code, origin and destination airports, delay times, and cancellation status.

- Carriers: contains unique airline code and name of airline

- Airports: contains unique airport codes, airport name, city, and region

- Cancel Codes: contains unique cancellation codes and descriptions

- Markets: contains unique city-market ID, city name, and region

- World Areas: contains world area code and area name

![Entity Relationship Diagram](Entity%20Relationship%20Diagram.png)

---

## Executive Summary

### Overview of Findings
This analysis of 1.78 million flights reveals that 84% depart on time, yet nearly 292,000 flights experience delays, averaging 67 minutes per delay. Flight volume is highly concentrated among five carriers, who dominate both positive and negative delay performance, with Southwest showing the highest delay rate at 18%. Major metro airports like Dallas/Fort Worth and Chicago lead in total delay minutes, driven mainly by controllable factors such as late aircraft and carrier-related issues, which together account for over 55% of delays. Delays fluctuate across the week, peaking on Sundays and Fridays, aligning with typical weekend travel patterns and passenger behavior.

![Overview](Report%20Images/Overview.png)

## Insights Deep Dive

## Delay Trends

- December saw a sharp spike in delay minutes despite similar flight volumes compared to October and November — with 8.8 million delay minutes in December versus 4.9 million in October (an 80% increase). This indicates a growing delay severity at year-end.

- Analyzing delay causes from October to December shows carrier delays decreased by 8.56%, but late aircraft delays increased by 3.68%, highlighting that equipment availability issues worsened in December.

- National Air System and weather-related delays also rose slightly by 1.75% and 3.16%, respectively, contributing to the overall delay increase during winter months.

- The surge in December delay minutes primarily stems from late aircraft delays at Dallas/Fort Worth (DFW), largely driven by American Airlines, which aligns with their DFW headquarters location.

![Overview](Report%20Images/Delay%20Drivers.png)

- Evening flights have the highest number of delays.
Despite having fewer total flights (451k), evening flights experienced 113k delays, making them the most delayed time block. In contrast, the morning had the most flights (748k) but only 47k delays, highlighting a compounding delay trend as the day progresses.

- Morning has the highest flight volume but fewer delays.
The morning time block accounted for 748k total flights, the highest among all periods. However, it had just 47k delayed flights, the lowest count, indicating that earlier flights are generally more reliable and less affected by system-wide delays.

- Flight activity and delays drop significantly at night.
Only 60k flights occurred during the night hours, with 48k delays. While delays per flight are proportionally high at night, the overall volume is very low, suggesting limited late-night operations and potential knock-on effects from earlier delays.

- Average flight distance steadily increases through Q4.
Flights in October averaged 816 miles, rising to 826 miles in November, and 843 miles in December. This trend could reflect longer holiday-season travel and contributes to strain on operations, increasing the risk of cumulative delays throughout the day.

![Overview](Report%20Images/Time%20Analysis.png)

### Airport & Route Analysis

- ATL (Atlanta) is the busiest airport in the U.S.
From the dataset, ATL recorded the highest number of flights, consistently topping monthly volume charts. This aligns with ATL’s role as a major domestic and international hub.

- DFW (Dallas-Fort Worth) has the highest number of delays among origin airports.
Despite not being the busiest, DFW had the most origin delays overall. This may be due to its size, complexity, and hub operations — especially considering American Airlines’ heavy presence.

- LAX to SFO is the most frequently flown route.
This high-traffic short-haul route saw the highest number of flights across the dataset. It highlights strong regional travel demand in California.

- LAX to JFK is the most delayed route.
This long-haul coast-to-coast route recorded the highest number of delays, suggesting persistent congestion or operational challenges between two of the country's busiest airports.

- Chicago, Atlanta, Dallas-Fort Worth, Denver, and New York were the top 5 flight hubs by volume. Chicago held the #1 position for overall flight traffic, making it a key operational and strategic hub.

- Flight routes between major metro pairs—Chicago–New York, New York–Boston, LA–SF—dominated traffic, collectively accounting for thousands of flights. These routes are prime targets for demand forecasting and dynamic pricing.

- Dallas/Fort Worth, O'Hare, and Denver experienced the most weather-related departure delays, with Dallas/Fort Worth accumulating the highest total. These insights can support airport-level planning and weather contingency strategies.

- Hartsfield–Jackson Atlanta International consistently ranked as the #1 airport for monthly flight volume, maintaining its dominance across all three months of Q4.

![Overview](Report%20Images/Location%20Analysis.png)

### Airline Operational Performance

- Endeavor Air Inc. consistently led all airlines in on-time arrival performance across Q4, ranking #1 each month. Their on-time rate exceeded 90%, significantly outperforming peers.

- Despite industry-wide delays, some airlines maintained low delay percentages. For example, top third of airlines in on-time departures had average departure delays under 30 minutes, compared to over an hour for the bottom third.

- Flight cancellations were overwhelmingly driven by weather conditions (77%), followed by carrier-related issues (14%). This shows that external factors dominate airline reliability, suggesting limited control over total disruptions.

- Controllable delays (carrier and national system-related) made up a significant share of total delays for certain airlines—up to 60%, indicating room for internal process improvements.

---
## Recommendations

Based on the insights and findings above, we would recommend the Operations and Network Planning teams to consider the following:

- Observation: Delays spike significantly during evening hours, with 113K delayed flights out of 451K total in that timeframe.
Recommendation: Evaluate flight schedules and staffing strategies for evening operations to reduce congestion and delay risks.

- Observation: Sunday is the busiest day for flights, and also shows high delay counts.
Recommendation: Increase operational capacity (e.g., more ground crew, longer buffers) during Sundays to improve on-time performance.

- Observation: DFW is the most delayed origin airport.
Recommendation: Investigate ground operations, runway capacity, and weather patterns at DFW to identify root causes and implement targeted delay-reduction strategies.

- Observation: LAX to JFK is the most delayed route.
Recommendation: Consider adjusting buffer times or rescheduling flight slots for this route to align with congestion periods at both endpoints.

- Observation: Flight distances and volume trend upward from October to December, indicating a seasonal surge.
Recommendation: Prepare for higher demand and longer routes in Q4 with proactive resource planning and route optimization efforts.

--- 

## Assumptions and Caveats:

Throughout the analysis, the following assumptions were made:

- Controllable delays: Factors such as carrier-related delays and national air system issues.
- Uncontrollable delays: Causes including weather conditions, late aircraft arrivals, and security-related interruptions.
- The classification of delay types may vary depending on the specific context or analysis framework.

---

## Technologies and Key Skills Used

- PostgreSQL
- Power BI
- Power Query
- DAX
- Excel
- Data Cleaning & Quality
- Data Modeling
- Data Visualization

---

## Dataset

- The dataset is sourced directly from the Department of Transportation and can be found [here](https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FGJ).
