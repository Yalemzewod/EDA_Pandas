# Repository Note: EDA_Pandas - Solar PV Adoption Analysis

## Overview
This repository contains an **exploratory data analysis (EDA) of solar photovoltaic (PV) installations across Australian states and territories in 2023**. The analysis uses Jupyter Notebooks to investigate average kilowatts per installation and installations per capita metrics to assess solar energy adoption patterns and regional disparities in renewable energy distribution.

**Focus Area:** Solar energy adoption analysis with geographic comparison across Australian states and territories

## Repository Details
- **Owner:** Yalemzewod
- **Repository:** EDA_Pandas
- **Created:** October 2, 2024
- **Status:** Active (Public)
- **Language:** Jupyter Notebook (100%)
- **Repository Size:** ~166 KB
- **Primary File:** Solar_PV_adoption_EDA.ipynb

## Project Objective

**Research Question:** How does solar energy adoption vary across Australian states and territories, and what are the patterns in installation capacity and penetration?

**Analysis Metrics:**
- Average kilowatts per installation (system size)
- Installations per capita (penetration rate)
- Regional disparities in solar adoption
- Geographic distribution patterns

## Data Sources

### 1. Solar PV Installation Data
- **Source:** Australian Government Clean Energy Regulator (CER)
- **Format:** CSV
- **Content:** Small-scale solar photovoltaic installations across Australia
- **Coverage:** All states and territories

### 2. Population Data
- **Source:** Australian Bureau of Statistics (ABS)
- **Format:** Excel (.xlsx)
- **Content:** Population aggregated by quarters at state level
- **Purpose:** Calculate per capita metrics

### 3. Postcode Data
- **Purpose:** Join solar energy data with population data at geographic level
- **Usage:** Enable state-level aggregation and analysis

## Data Manipulation Activities

### Data Processing Steps

```python
# 1. Download data programmatically
import pandas as pd
import requests

# Fetch solar PV data from CER
solar_data_url = "https://data.cleanenergyregulator.gov.au/..."
solar_df = pd.read_csv(solar_data_url)

# 2. Load Excel population data
population_df = pd.read_excel('population_data.xlsx')

# 3. Load postcode mapping data
postcode_df = pd.read_csv('postcode_data.csv')

# 4. Examine data structure
print(solar_df.head())
print(solar_df.info())
print(solar_df.shape)
```

### Data Examination

```python
# Check data types and convert if required
print(solar_df.dtypes)
solar_df['date_installed'] = pd.to_datetime(solar_df['date_installed'])

# Examine dimensions
print(f"Rows: {len(solar_df)}, Columns: {len(solar_df.columns)}")

# Identify missing values
print(solar_df.isnull().sum())

# Check for data entry errors
print(solar_df.duplicated().sum())

# Verify completeness
completeness = (solar_df.notna().sum() / len(solar_df)) * 100
print(completeness)
```

### Data Cleaning & Normalization

```python
# Remove duplicates
solar_df = solar_df.drop_duplicates()

# Handle missing values
solar_df = solar_df.dropna(subset=['capacity_kw'])

# Normalize state names
solar_df['state'] = solar_df['state'].str.upper().str.strip()

# Merge with population data
merged_df = solar_df.merge(population_df, on='state', how='left')
```

## Key Analysis Outputs

### 1. Average Kilowatts Per Installation

**Finding:** Growing preference for larger and more efficient solar systems

```python
# Calculate average capacity per installation by state
avg_capacity_by_state = solar_df.groupby('state')['capacity_kw'].mean().sort_values(ascending=False)

print("Average Kilowatts per Installation by State:")
print(avg_capacity_by_state)
```

**Key Insights:**
- **Northern Territory (NT):** Highest average kW per installation
- **New South Wales (NSW):** Second highest, indicating preference for larger systems
- **Regional Variation:** Significant differences in system sizing across states
- **Trend:** Indicates shift towards more efficient and larger capacity installations

### 2. Installations Per Capita

**Finding:** Higher penetration along East Coast communities

```python
# Calculate installations per capita by state
installations_per_capita = (solar_df.groupby('state').size() / 
                            population_df.groupby('state')['population'].mean() * 1000)

print("Installations per 1000 Capita by State:")
print(installations_per_capita.sort_values(ascending=False))
```

**Key Insights:**
- **East Coast States:** Higher penetration rates (NSW, Victoria, Queensland)
- **Community Acceptance:** Indicates broader acceptance and adoption
- **Geographic Clustering:** Solar adoption concentrated in developed regions
- **Penetration Disparities:** Significant variation between coastal and inland areas

## Analysis Visualization Framework

### Expected Visualizations
- Bar charts comparing average kW per installation across states
- Choropleth maps showing installations per capita by region
- Time series of installation trends
- Distribution of system sizes
- Regional heatmaps for adoption patterns

## Sample Code Sections

### Data Aggregation Example

```python
# Aggregate installations by state
state_summary = solar_df.groupby('state').agg({
    'capacity_kw': ['mean', 'median', 'sum', 'count'],
    'installation_date': 'min'
}).round(2)

print(state_summary)
```

### Per Capita Calculation

```python
# Merge installation counts with population
state_metrics = pd.DataFrame({
    'installations': solar_df.groupby('state').size(),
    'total_capacity_kw': solar_df.groupby('state')['capacity_kw'].sum(),
})

state_metrics = state_metrics.merge(
    population_df.groupby('state')[['population']].mean(),
    left_index=True,
    right_index=True
)

# Calculate per capita metrics
state_metrics['installations_per_1000'] = (state_metrics['installations'] / 
                                           state_metrics['population'] * 1000)
state_metrics['avg_capacity_kw'] = (state_metrics['total_capacity_kw'] / 
                                   state_metrics['installations'])
```

## Key Findings Summary

1. **System Sizing Trends**
   - Northern Territory and NSW lead in average system capacity
   - Reflects investment in larger, more efficient installations
   - Suggests early adopter advantage and technical expertise

2. **Adoption Penetration**
   - East Coast shows higher community adoption rates
   - Indicates stronger social acceptance and policy support
   - Urban areas demonstrate faster adoption

3. **Regional Disparities**
   - Clear geographic clustering of solar adoption
   - Coastal-inland divide evident in penetration rates
   - Opportunities for Northern Territory capacity expansion

4. **Energy Resilience**
   - NT opportunity to enhance energy capacity
   - East Coast reflects mature solar market
   - Regional variations suggest different policy impacts

## Tools & Libraries Used

- **pandas** - Data manipulation and aggregation
- **numpy** - Numerical computations
- **matplotlib/seaborn** - Data visualization
- **jupyter** - Interactive notebook environment
- **requests** - API calls for data download

## Use Cases

✓ Understanding solar energy distribution patterns  
✓ Policy analysis for renewable energy adoption  
✓ Regional energy planning and investment decisions  
✓ Geographic analysis of technology adoption  
✓ Data cleaning and EDA best practices  
✓ Per capita metric calculation methodology  

---
*This EDA project demonstrates practical data analysis techniques for assessing renewable energy adoption patterns and identifying regional opportunities for solar energy expansion across Australia.*
