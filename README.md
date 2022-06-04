# inflation_analysis
Personal project to analyze the relationship between gas prices and inflation

Used GCP BigQuery to store gas price and GDP information with the goal of predicting recessions with changes in the gas prices and GDP.
## Tables
The project included one dataset, recession_db, with 2 tables, gas_price and gdp.

### Table gas_price: 
| Column Name | Type | Mode |
| ----------- | ---- | ---- |
| price_date | DATE | REQUIRED |
| price_per_gallon | FLOAT | REQUIRED |
| price_year | INTEGER | REQUIRED |

### Table gdp: 
| Column Name | Type | Mode |
| ----------- | ---- | ---- |
| gdp_date | DATE | REQUIRED |
| gdp_value | FLOAT | REQUIRED |
| gdp_change | FLOAT | REQUIRED |

## Source of Data
### Gas Price Data 
Weekly Texas Regular Conventional Retail Gasoline Prices: https://www.eia.gov/dnav/pet/hist/LeafHandler.ashx?n=PET&s=EMM_EPMRU_PTE_STX_DPG&f=W
### GDP Data
Gross Domestic Product of the United States (US GDP): 
https://datahub.io/core/gdp-us

## Create Tables
