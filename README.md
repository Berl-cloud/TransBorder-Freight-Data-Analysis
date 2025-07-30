# **TransBorder Freight Data Analysis**

Project Owner: Berlinda Anaman  
Email: Berlana.d@gmail.com  
Github Profile: [Berlinda Anaman](https://github.com/Berl-cloud)  
LinkedIn Profile: [Berlinda Anaman](https://www.linkedin.com/in/berlinda-anaman/)

## **1\. Project Overview**

Transportation systems are the backbone of modern economies, facilitating the movement of goods, services, and people across cities, states, and nations. They are vital for commerce, tourism, and daily living, directly impacting economic productivity and societal well-being. As transportation networks grow in complexity, so do the challenges they face—ranging from safety concerns to inefficiencies and sustainability issues.

The Bureau of Transportation Statistics (BTS), a branch of the U.S. Department of Transportation, serves as a vital resource in tackling these challenges. It provides comprehensive and reliable data on multiple dimensions of transportation systems, including passenger travel, freight movement, safety incidents, infrastructure capacity, and environmental impacts. This project leverages BTS data to uncover insights related to the efficiency, safety, and environmental impacts of transborder freight transportation.

## **2\. Project Objectives**

The key objectives of this project were to:

1. **Uncover Freight Movement Patterns:** Analyze the movement of freight across different transportation modes, and identify trends in volume, routing, and modes of transportation used across regions and time periods.  
2. **Identify Operational Inefficiencies:** Investigate areas where transportation systems may experience inefficiencies, such as congestion points, delays, or underutilized infrastructure, and propose methods to optimize resource use and improve throughput.  
3. **Analyze Environmental Impact:** Assess the environmental impact of freight transportation by studying data on emissions, fuel usage, and sustainability metrics across different modes of transportation, and recommend strategies for reducing the carbon footprint of the sector.  
4. **Safety and Risk Assessment:** Identify transportation safety incidents related to freight, evaluate their causes and consequences, and suggest recommendations for improving safety protocols.  
5. **Economic Disruptions:** Analyze how economic disruptions (e.g., trade patterns, policy changes, or global events) impact freight movements and overall transportation efficiency.  
6. **Provide Data-Driven Recommendations:** Based on the analysis, provide actionable recommendations to enhance the performance, sustainability, and safety of the transportation systems that handle cross-border freight.

## **3\. Methodology: CRISP-DM Framework**

This project followed the Cross-Industry Standard Process for Data Mining (CRISP-DM) methodology, ensuring a structured and iterative approach to drive valuable business insights and lead to practical recommendations.

### **3.1. Business Understanding**

The initial phase involved understanding the project's goals, the transportation domain, and the specific problems to be addressed. The primary aim was to analyze transborder freight data to identify patterns, inefficiencies, and provide actionable recommendations.

**Analytical Questions Guiding the Project:**

1. What are the primary modes of transportation driving the highest *value* and *weight* in transborder freight, and how do these modes differ in their contributions to exports versus imports?  
2. How have the total value and weight of transborder freight changed over time, specifically identifying the impact of the COVID-19 pandemic and the subsequent recovery patterns across different transportation modes?  
3. Which U.S. states, Mexican states, and Canadian provinces are the most significant hubs for transborder freight in terms of both value and weight, and how do these geographical patterns relate to the dominant modes of transportation in those regions?  
4. What are the top commodities by total value and total weight, and how do these high-value and high-weight commodities typically move across borders (i.e., which modes of transportation are predominantly used for them)?  
5. Are there specific modes of transportation or trade types that exhibit disproportionately high freight charges relative to the value or weight of the goods, indicating potential operational inefficiencies or specialized service costs?  
6. How does the "Domestic/Foreign Produced" status of merchandise influence its trade type (export/import), the mode of transportation used, and the partner country involved?  
7. What are the implications of the "UNKNOWN" or generic codes in geographical and commodity data for a comprehensive understanding of transborder freight, and what steps could be taken to improve data granularity for future analysis and policy recommendations?

### **3.2. Data Understanding**

This phase involved initial data collection and familiarization. The dataset consisted of several CSV files (dot1\_0420.csv, dot2\_0420.csv, dot3\_0420.csv) containing transborder freight data from 2020 to 2024\. Documentation (codes-north-american-transborder-freight-raw-data.pdf) was used to understand column meanings and categorical codes.

* Initial assessment of data types and missing values.  
* Identification of key columns for analysis (TRDTYPE, DISAGMOT, COUNTRY, VALUE, SHIPWT, FREIGHT\_CHARGES, USASTATE, MEXSTATE, CANPROV, COMMODITY2, MONTH, YEAR).

### **3.3. Data Preparation**

This was a crucial phase involving extensive cleaning and preprocessing:

* **Merging Data:** The individual CSV files were concatenated into a single merged\_data DataFrame. An outer join was used to ensure all records from all files were included.  
* **Handling Missing Values:**  
  * FREIGHT\_CHARGES: Missing values were filled with 0, assuming no charge if not recorded.  
  * MEXSTATE, CANPROV, COMMODITY2, USASTATE, PORT\_CODE, CONTCODE: Missing values were filled with 'UNKNOWN' or 'N/A' to preserve information while indicating absence.  
  * DF (Domestic/Foreign Code): Missing values were filled with 0, which was later mapped to 'Unknown/Not Specified'.  
* **Data Type Conversion:** Columns like YEAR, MONTH, VALUE, SHIPWT, FREIGHT\_CHARGES were converted to appropriate numeric types. Object columns were handled for consistency.  
* **Feature Engineering (DATE Column):** A DATE column was created from YEAR and MONTH to facilitate time-series analysis. A dummy DAY of 1 was used. Crucially, MONTH values of 0 were replaced with 1 to prevent ValueError during datetime conversion.  
* **Categorical Mapping:** Numerical codes for TRDTYPE, DISAGMOT, COUNTRY, and DF were mapped to their descriptive names (TRADE\_TYPE, MODE\_OF\_TRANSPORTATION, COUNTRY\_NAME, DOMESTIC\_FOREIGN\_STATUS) using the provided documentation.  
* **Duplicate Handling:** A significant number of exact duplicate rows (over 20 million) were identified and removed, resulting in a cleaner dataset of approximately 5.79 million unique records. This was a critical step for data integrity.  
* **Feature Calculation:** FREIGHT\_CHARGE\_PER\_VALUE and FREIGHT\_CHARGE\_PER\_SHIPWT were calculated to assess cost efficiency.

### **3.4. Exploratory Data Analysis (EDA)**

The EDA phase involved visualizing and summarizing the prepared data to uncover patterns and answer the analytical questions. Key findings include:

* **Trade Type:** Exports have a higher shipment count, but imports account for significantly higher total value and weight.  
* **Mode of Transportation:** Trucking dominates in shipment count and total value. Vessel and Pipeline are paramount for total physical weight, while Rail is strong in both value and weight.  
* **Geographical Hotspots:** Texas is the top U.S. state for known trade. Ontario leads Canadian provinces by value, and Alberta by weight (likely energy). Mexican trade is concentrated near the border, but significant data gaps exist for specific Mexican states.  
* **Temporal Trends:** A clear dip in freight activity was observed in early 2020 (COVID-19 impact), followed by a strong and sustained recovery through 2021-2023.  
* **Commodity Flow:** High-value commodities include vehicles, machinery, and electrical equipment. High-weight commodities are mineral fuels, salt/sulfur, and wood.  
* **Freight Charges:** Air and "Other" modes show higher average freight charges per kilogram, while Pipeline and Rail are most cost-efficient per kilogram.

## **4\. Conclusion and Recommendations**

### **Key Insights from Exploratory Data Analysis (EDA)**

1. **Trade Type Dynamics:**  
   * While the **number of export shipments is higher**, the **total *value* and *weight* of import shipments significantly exceed exports**. This suggests that imported goods are generally of higher individual value and greater physical volume, potentially comprising raw materials or heavier manufactured goods.  
2. **Dominance of Transportation Modes:**  
   * **Trucking is the undisputed leader** in terms of the *number of shipments* and *total economic value* for transborder freight. Its flexibility and extensive network make it the primary choice for a wide range of goods.  
   * For **total *physical weight***, **Vessel and Pipeline transportation are paramount**, indicating their critical role in moving bulk commodities (e.g., oil, gas, minerals) where volume is the primary factor.  
   * Rail transportation holds a strong second position in both value and weight, particularly for Canadian trade.  
3. **Geographical Hotspots and Trade Corridors:**  
   * **Texas (TX)** is the most significant U.S. state for transborder freight in terms of both value and weight among the *known* states, serving as a major gateway to Mexico.  
   * **Ontario (XO)** is the leading Canadian province by *value*, reflecting its industrial ties, while **Alberta (XA)** dominates by *weight*, largely due to energy exports.  
   * Mexican trade is concentrated in states bordering the U.S., though a significant portion of Mexican state data is unclassified ("XX").  
   * **Data Limitation:** A substantial portion of geographical data (U.S. States, Mexican States, Canadian Provinces) is classified as "UNKNOWN" or generic codes, limiting granular regional analysis.  
4. **Temporal Trends and Economic Resilience:**  
   * The data clearly shows a **sharp decline in freight value and weight in early to mid-2020**, directly correlating with the onset of the COVID-19 pandemic.  
   * Following this initial disruption, there has been a **strong and sustained recovery and growth** in transborder freight activity through 2021, 2022, and 2023, reaching levels higher than pre-pandemic. This demonstrates the resilience of the North American supply chain.  
   * Specific monthly patterns by mode indicate that while overall trends follow economic cycles, individual modes might have unique seasonal fluctuations.  
5. **Commodity Flow:**  
   * **Vehicles (87)**, **Mineral Fuels (27)**, and **Machinery (84, 85\)** are the highest-value commodities, reflecting the importance of manufacturing and energy trade.  
   * **Mineral Fuels (27)**, **Salt/Sulfur/Earths/Stone (25)**, and **Wood (44)** dominate in terms of physical weight, highlighting the movement of raw materials and bulk goods.  
   * There's a clear distinction: high-value manufactured goods (vehicles, machinery) drive value, while bulk commodities (fuels, minerals, wood) drive weight.  
6. **Freight Charge Dynamics:**  
   * **Air and "Other" modes** have the highest average freight charges per kilogram, which is expected for expedited or specialized services.  
   * **Pipeline and Rail** are the most cost-efficient modes per kilogram, reinforcing their role in bulk transport.  
   * The relationship between freight charges and value/weight can be complex; further investigation is needed to pinpoint specific inefficiencies beyond these high-level averages.

### **Recommendations**

Based on these insights, here are actionable recommendations to enhance the performance, sustainability, and safety of transborder transportation systems:

1. **Optimize Trucking Operations:**  
   * **Recommendation:** Given trucking's overwhelming dominance in shipment count and value, focus on optimizing truck routes, reducing border wait times, and improving road infrastructure at key border crossings (e.g., Texas-Mexico, Michigan-Ontario).  
   * **Why:** Even small improvements in efficiency for trucking will yield significant overall benefits due to its sheer volume.  
   * **Impact:** Reduced transit times, lower operational costs for businesses, decreased congestion, and improved throughput.  
2. **Leverage Rail and Pipeline for Bulk Efficiency:**  
   * **Recommendation:** Encourage and invest in expanding rail and pipeline capacity, especially for high-weight commodities like mineral fuels, metals, and agricultural products, particularly for trade with Canada (Alberta's weight dominance).  
   * **Why:** These modes offer superior cost-efficiency for bulk transport and can alleviate road congestion.  
   * **Impact:** Lower per-unit shipping costs for bulk goods, reduced environmental footprint compared to trucking for heavy loads, and increased capacity for high-volume trade.  
3. **Address Data Gaps for Granular Analysis:**  
   * **Recommendation:** Implement stricter data collection protocols to minimize "UNKNOWN" or generic codes for U.S. States, Mexican States, and Canadian Provinces, and ensure SHIPWT data is consistently recorded for all Mexican shipments.  
   * **Why:** More complete geographical and weight data would enable more precise routing optimization, infrastructure planning, and a deeper understanding of specific trade corridors and their challenges.  
   * **Impact:** Improved data-driven decision-making, more targeted policy interventions, and better resource allocation.  
4. **Monitor Economic Resilience and Adaptability:**  
   * **Recommendation:** Continue to monitor temporal trends closely, especially in light of global economic shifts or unforeseen events. Develop contingency plans based on the observed resilience and recovery patterns post-COVID-19.  
   * **Why:** Understanding the system's response to past disruptions can inform strategies for future crises, ensuring supply chain stability.  
   * **Impact:** Enhanced supply chain resilience, quicker recovery from disruptions, and minimized economic impact during crises.  
5. **Investigate High-Cost Freight Segments:**  
   * **Recommendation:** Conduct deeper analysis into the specific factors contributing to high freight charges per value/weight for "Pipeline," "Vessel," "Air," and "Other" modes. This might involve looking at specific commodities, distances, or specialized handling requirements.  
   * **Why:** Identifying the root causes of higher costs can reveal opportunities for negotiation, alternative logistics solutions, or technological improvements.  
   * **Impact:** Improved cost-efficiency for high-value/specialized freight, potential for innovation in logistics services.  
6. **Future Data Collection for Sustainability and Safety:**  
   * **Recommendation:** To address the "Environmental Impact" and "Safety and Risk Assessment" objectives fully, future data collection should include metrics such as:  
     * **Emissions data:** Fuel consumption per mode, carbon footprint.  
     * **Safety incident data:** Number of accidents, causes, fatalities, injuries by mode and route.  
     * **Delay/Congestion data:** Average transit times, border wait times, and frequency of delays.  
   * **Why:** Direct data on these aspects is critical for developing targeted strategies for sustainability and safety improvements.  
   * **Impact:** Enables data-driven policies for reducing environmental impact (e.g., promoting greener modes, optimizing fuel use) and enhancing safety protocols, leading to fewer incidents and a more secure transportation network.

## **5\. Skills Used**

* CRISP-DM Methodology  
* Data Engineering  
* Data Wrangling  
* Data Visualization  
* Documentation