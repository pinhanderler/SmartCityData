# Azure Data Engineering Module 
## Project: Data Processing and Transformation

---

## Introduction

In previous modules, data was ingested from external APIs and stored in the **Bronze layer** of the Lakehouse using **Azure Data Factory**.  
Although this raw data is valuable, it is stored in a **nested JSON format**, which is not suitable for analytics or reporting.

This project focuses on the core responsibilities of a **Data Engineer**: transforming raw data into clean, structured, and analytics-ready datasets using **Apache Spark in Microsoft Fabric**, following the **Medallion Architecture (Bronze → Silver → Gold)**.

---

## Learning Outcomes

- Develop Spark code using Microsoft Fabric Notebooks  
- Apply modular design (Config / Logging / Functions)  
- Normalize nested JSON data (Bronze → Silver)  
- Apply business logic and analytics (Silver → Gold)  
- Prepare data for Power BI using Direct Lake  

---

## 1. Bronze Layer – Raw Data

Data ingested from APIs is stored in the Bronze layer as nested JSON files.  
This raw data is not ready for analysis until flattened and normalized.

### Bronze Layer – JSON Example
![Bronze Layer JSON](Screenshot%20Files/Bronze%20layer%20JSON%20example%20%28raw%20data%29.png)

---

## 2. Bronze → Silver: Data Normalization

The Bronze layer contains deeply nested JSON structures.  
In the Silver layer, the data is flattened, exploded, and standardized into a tabular format.

### Key Transformations
- Flatten nested JSON structures  
- Explode arrays into rows  
- Rename columns to `snake_case`  
- Ensure schema consistency for analytical use

### Silver Layer – Before Flatten / Explode
![Silver Before Flatten](Screenshot%20Files/Silver%20layer%20tablo%20before%3Aafter%20%28flatten%20%3A%20explode%29.png)

### Silver Layer – After Flatten / Explode
![Silver After Flatten](Screenshot%20Files/Silver%20layer%20tablo%20before%3Aafter%20%28flatten%20%3A%20explode%29.png)

---

## 3. Silver → Gold: Analytical Preparation

The Gold layer applies analytical and business logic to prepare data for reporting.  
**Note:** No screenshot is provided for Gold; only transformations and business logic are described.

### Key Operations
- Join Energy, Weather, and Air Quality Silver tables  
- Use Spark Window Functions (e.g., rolling averages)  
- Generate derived labels such as **FIRSAT**  
- Optimize schema for Power BI consumption  

---

## 4. Notebook Architecture

### 4.1 `nb_config` – Configuration Notebook

Centralized configuration ensures no hard-coded paths.

**Key Variables**
- `ROOT_PATH`  
- `PATH_BRONZE`  
- `PATH_SILVER`  
- `PATH_GOLD`  

Loaded dynamically using `%RUN nb_config`.

![nb_config run](Screenshot%20Files/nb_config%20run.png)

---

### 4.2 `nb_logging` – Logging Framework

Professional logging replaces print statements and improves traceability.

**Log Levels**
- DEBUG  
- INFO  
- WARNING  
- ERROR  

![nb_logging](Screenshot%20Files/nb_logging.png)

---

### 4.3 `nb_functions` – Reusable Functions

Reusable helper functions ensure clean, maintainable, and scalable code.

**Core Functions**
- `clean_column_names`  
- `explode_and_flatten`  
- `save_to_lakehouse`  
- `generate_surrogate_key`  
- `create_time_series_frame`  
- `select_columns_safe`  
- `join_dataframes`  

![nb_functions](Screenshot%20Files/nb_functions.png)

---

### 4.4 Metadata-Driven Bronze → Silver Engine

A generic ETL engine processes multiple datasets dynamically using **Capsules**.  
Each Capsule defines:
- Source  
- Target  
- Transformation steps  

---

## 5. Power BI Integration

### Direct Lake Mode

Gold tables are connected to Power BI using **Direct Lake**, enabling:
- High performance  
- Near real-time analytics  
- No data duplication  

### KPIs & Metrics
- `FIRSAT` moment count  
- % deviation from rolling average  
- Clean Energy Score (Weather + Air Quality)  

### Power BI Dashboard
*(Screenshot not provided; visualization explained in the project)*

---

## 6. Medallion Architecture Implementation

This project fully implements the **Medallion Architecture** in Microsoft Fabric:

1. **Bronze** – Raw API data  
2. **Silver** – Clean and normalized tables  
3. **Gold** – Analytical and business-ready data  
4. **Power BI** – Direct Lake reporting  

![Medallion Architecture](Screenshot%20Files/Medallion%20Architecture%20Implementation%20in%20Microsoft%20Fabric%20for%20Smart%20City%20Energy%20Optimization.png)

---

## 7. Final Outcome

This project delivers an **end-to-end, scalable, and production-ready data pipeline**.  
Decision-makers can now identify **cost-effective and sustainable energy usage moments** using real-time analytics.

---

## Best Practices Applied

- No hard-coded paths  
- Modular notebook design  
- Metadata-driven ETL  
- BI-optimized Gold layer  
- Enterprise-grade logging  

---
