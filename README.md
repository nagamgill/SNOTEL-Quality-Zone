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
