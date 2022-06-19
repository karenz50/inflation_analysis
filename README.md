# inflation_analysis
Personal project to analyze the relationship between gas prices and inflation

Used GCP BigQuery to store gas price and GDP information with the goal of predicting recessions with changes in the gas prices and GDP.

## Dataset
GCP BigQuery uses datasets instead of databases; any references to a "dataset" refers to a database.

This is the command to create and verify a dataset:

``` bigquery
bq mk -d --description "My recession analysis" recession_db
bq ls
bq show --format=prettyjson recession_db
```

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
### GDP Table
A json schema file is used for creating the gdp table.

#### gdp_schema.json
``` json
[
  {
    "mode": "REQUIRED", 
    "name": "gdp_date", 
    "type": "DATE"
  }, 
  {
    "mode": "REQUIRED", 
    "name": "gdp_value", 
    "type": "FLOAT"
  }, 
  {
    "mode": "REQUIRED", 
    "name": "gdp_change", 
    "type": "FLOAT"
  }
]
```
The first line of code below creates recession_db.gdp table using gdp_schema.json, the second line shows the schema of the table, and the last line verifies that there are no rows in the table.
``` bigquery
bq mk --table recession_db.gdp gdp_schema.json
bq show --schema --format=prettyjson recession_db.gdp
bq query --nouse_legacy_sql 'SELECT count(*) Total from recession_db.gdp'
```
