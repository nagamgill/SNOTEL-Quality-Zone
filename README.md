# SNOTEL-Quality-Zone
Cleanup Script

Description

This script is designed to fetch temperature data from the NRCS’s Automated Water Database (AWDB) using their REST API. It retrieves two sets of temperature data: hourly temperature observations (TOBS) and daily maximum temperatures (TMAX). The script then preprocesses, cleans up the data, and visualizes it. The cleaned data is finally saved to a CSV file.

Components

	•	Data Fetching:
	•	The script uses the requests library to make GET requests to the AWDB API.
	•	It fetches data for a specified station using parameters such as station ID, date range, and the type of temperature data (TOBS for hourly and TMAX for daily).
	•	Data Preprocessing:
	•	The JSON response from the API is transformed into a pandas DataFrame.
	•	Date strings are parsed into datetime objects, and the data is indexed by date for easier manipulation and visualization.
	•	Data Visualization:
	•	The script uses matplotlib to plot the raw temperature data.
	•	It provides a visual comparison between hourly and daily temperature observations before cleaning.
	•	Data Cleaning:
	•	A custom cleaning function is applied to the data to handle discrepancies.
	•	It involves normalizing timestamps, resampling for daily maximums, and merging datasets.
	•	A threshold-based approach is used to verify and correct the data.
	•	Output:
	•	The cleaned data is plotted to show the effects of the cleaning process.
	•	Final cleaned data is saved to a CSV file for further use or analysis.

Usage

To use this script, the user must provide the correct station triplet, elements, and date range for the data fetch. The script is structured in functions to allow for modularity and reuse. Data visualization and cleaning are separated into distinct steps for clarity and maintainability.

Cleaning Logic Description

Objective

The primary goal of the cleaning process in this script is to refine the daily maximum temperature data (TMAX) obtained from the Automated Water Database (AWDB). This refinement is achieved by comparing reported daily max temperatures with calculated daily max temperatures derived from hourly temperature observations (TOBS). The process ensures the accuracy and reliability of the max temperature data by identifying and correcting discrepancies beyond an acceptable range.

Steps

	1.	Normalization: The cleaning process begins with normalizing the timestamp of hourly temperature data (TOBS) to ensure each entry is associated with the correct date. This normalization is crucial for accurate daily aggregation and comparison.
	2.	Daily Maximum Calculation: From the normalized hourly data, we calculate the daily maximum temperature for each day within the dataset. This calculation provides us with a baseline to compare against the reported daily maximum temperature data (TMAX).
	3.	Data Merging: The reported TMAX data and the calculated daily max temperatures from TOBS data are merged based on the date index. This merging creates a unified dataset containing both reported and calculated values for each day, enabling direct comparison.
	4.	Discrepancy Evaluation: For each day, the difference between the reported daily maximum temperature and the calculated value from hourly data is assessed. This step identifies the magnitude of discrepancies and is pivotal in determining the need for correction.
	5.	Threshold-Based Correction: A predefined acceptable range (threshold) is used to evaluate discrepancies. If the difference between the reported and calculated daily max temperatures is within this range, the reported value is considered accurate (“Verified”). If the discrepancy exceeds the acceptable range, it indicates a potential error in the reported data, prompting a correction. In such cases, the calculated value from hourly observations is deemed more accurate and is used as the “final” daily max temperature (“Corrected”).
	6.	Final Dataset Creation: The outcome of the cleaning process is a dataset that includes the calculated daily max temperature, the reported daily max temperature, the final (verified or corrected) daily max temperature, and the status indicating whether the original reported value was verified or corrected.

Rationale

The rationale behind this cleaning logic is to enhance data integrity and reliability. By leveraging hourly temperature observations to verify or correct daily max temperature reports, we ensure that the dataset reflects the most accurate temperature readings possible. This approach minimizes potential errors or inaccuracies in the reported daily max temperatures, making the dataset more reliable for further analysis, modeling, or reporting.

Output

The cleaned dataset, containing both the original and corrected daily max temperatures along with their verification status, is saved to a CSV file named cleaned_max_temp_data.csv. This file serves as a ready-to-use resource for accurate temperature analysis and applications.
