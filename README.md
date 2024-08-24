
# Apple Data Analysis on Databricks

## Overview
This project demonstrates how to perform data analysis using Databricks, focusing on Apple product sales data. The project includes extracting, transforming, and loading (ETL) workflows designed to analyze customer transactions, particularly focusing on customers who bought AirPods after purchasing iPhones.

## Project Structure

### Data Files
- `Customer_Updated.csv`
- `Products_Updated.csv`
- `Transaction_Updated.csv`

### Loader Factory
#### Abstract Class: `DataSink`
Defines the basic structure for loading data to various destinations.

#### Class: `LoadToDBFS`
Loads data to Databricks File System (DBFS).

#### Class: `LoadToDBFSWithPartition`
Loads data to DBFS with partitioning.

#### Class: `LoadToDeltaTable`
Loads data to a Delta Table on Databricks.

### Reader Factory
#### Abstract Class: `DataSource`
Defines the basic structure for reading data from various sources.

#### Class: `CSVDataSource`
Reads data from CSV files.

#### Class: `ParquetDataSource`
Reads data from Parquet files.

#### Class: `ORCDataSource`
Reads data from ORC files.

#### Class: `DeltaDataSource`
Reads data from Delta Tables.

### Extractor
#### Abstract Class: `Extractor`
Defines the basic structure for extracting data.

#### Class: `AirpodsAfterIphoneExtractor`
Extracts the transaction and customer data required for analysis.

### Transformer
#### Abstract Class: `Transformer`
Defines the basic structure for transforming data.

#### Class: `FirstTransformer`
Identifies customers who bought AirPods after buying an iPhone.

#### Class: `SecondTransformer`
Identifies customers who bought only AirPods and iPhones.

#### Class: `ThirdTransformer`
Provides the filtered DataFrame where customers bought AirPods after buying an iPhone.

### Workflow
#### Class: `FirstWorkFlow`
- **Objective:** Identifies customers who bought AirPods after buying an iPhone.
- **Steps:** 
  - Extracts required data using `AirpodsAfterIphoneExtractor`.
  - Transforms the data using `FirstTransformer`.
  - Loads the results into the destination using `AirpodsAfterIphoneLoader`.

#### Class: `SecondWorkFlow`
- **Objective:** Identifies customers who bought only AirPods and iPhones.
- **Steps:** 
  - Extracts required data using `AirpodsAfterIphoneExtractor`.
  - Transforms the data using `SecondTransformer`.
  - Loads the results into the destination using `OnlyAirpodsandIphoneLoader`.

#### Class: `ThirdWorkFlow`
- **Objective:** Filters data for customers who bought AirPods after buying an iPhone.
- **Steps:** 
  - Extracts required data using `AirpodsAfterIphoneExtractor`.
  - Transforms the data using `ThirdTransformer`.
  - Displays the transformed data.

#### Class: `WorkFlowRunner`
- **Objective:** Runs the specified workflow.
- **Usage:** 
  - Instantiate with the workflow name (e.g., "FirstWorkFlow", "SecondWorkFlow").
  - Call the `runner` method to execute the workflow.

### Loader
#### Abstract Class: `AbstractLoader`
Defines the basic structure for sinking transformed data.

#### Class: `AirpodsAfterIphoneLoader`
Sinks the data into the DBFS path for AirPods after iPhone purchases.

#### Class: `OnlyAirpodsandIphoneLoader`
Sinks the data into the DBFS path and Delta Table for only AirPods and iPhone purchases.

## How to Run
1. Ensure all data files (`Customer_Updated.csv`, `Products_Updated.csv`, `Transaction_Updated.csv`) are available in DBFS.
2. Run the appropriate workflow by instantiating `WorkFlowRunner` with the desired workflow name.
3. Check the output in the specified DBFS path or Delta Table.

## Notes
- The code uses Spark on Databricks for distributed data processing.
- Ensure that the necessary libraries are installed and Spark session is properly configured.

## Future Enhancements
- Implement more complex transformation logic.
- Add support for other data formats (e.g., Avro).
- Integrate with external databases for data loading.
