### An Explanatory Analysis of Solar PV Installations Across Australian States and Territories in 2023

This report analyzes the average kilowatts per installation and installations per capita to assess solar energy adoption across Australia’s states and territories.

#### About the data:

For this project, I have used three datasets:

- Solar PV Installation: Data on small-scale solar photovoltaic (PV) installations across Australia from the Australian Government Clean Energy Regulator (CER). This dataset is availabe in the csv format and includes information on the location (postcodes), capacity in KW, quantity and installation date of solar PV systems.
  
- Population Data: Population data aggregated by quarters at states level, downloaded from Australian Bureau of Statistics (ABS) as .xlsx format.
  
- Postcode Data: Postcode data used to join the solar energy data with the population data.

#### Data manipulation
**Activities** 
- Download the data programmatically
- Load the data into a pandas DataFrame
- Examine the data and identify relevant columns
- Clean and normalize the data set

_Examine the data_
- datatype and convert if regquired
- dimensions of the dataset (number of rows and columns)
- data entry error and completeness of the data

#### The key findings are:

1.  The average kilowatts per installation reveals a growing preference for larger and more efficient solar systems, particularly in the Northern Territory (NT) and New South Wales (NSW). This trend reflects a shift toward more capable solar technologies in these regions.
![image](https://github.com/user-attachments/assets/af7bf421-4921-4b4d-a1c3-0c8fa0d13047)

2. Installations per capita show a higher penetration of solar energy in communities along the East Coast, indicating broader acceptance and adoption of solar technology in these areas.
![image](https://github.com/user-attachments/assets/159dc717-dfa9-47f3-a670-c326d6474a52)

Overall, the findings highlight regional disparities in solar adoption. The Northern Territory presents an opportunity to further enhance energy capacity and resilience, while the East Coast reflects higher rates of solar usage, driven by greater accessibility, affordability, and awareness
