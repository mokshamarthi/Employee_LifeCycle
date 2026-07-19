# Employee Lifecycle & Attrition Analytics Pipeline

## Overview

This project demonstrates an end-to-end Azure Data Engineering solution for processing employee lifecycle data using a Medallion Architecture (Bronze, Silver, and Gold layers).

The pipeline is orchestrated using Azure Data Factory and processes employee data stored in Azure Blob Storage through Azure Databricks notebooks. Historical employee records are maintained using Slowly Changing Dimension (SCD Type 2), while analytical datasets are generated for workforce reporting.

---

# Architecture

```
                Employee CSV Files
                        │
                        ▼
          Azure Blob Storage (Raw Data)
                        │
                        ▼
             Azure Data Factory Pipeline
                        │
                        ▼
                Bronze Notebook
                        │
                        ▼
                Silver Notebook
                        │
                        ▼
              SCD Type 2 Notebook
                        │
                        ▼
                 Gold Notebook
                        │
                        ▼
      Delta Tables / Analytical Outputs
                        │
                        ▼
             Power BI (Optional)
```

---

# Technologies Used

- Azure Blob Storage
- Azure Data Factory
- Azure Databricks
- Apache Spark (PySpark)
- Delta Lake
- Unity Catalog
- SQL
- Git & GitHub

---

# Project Workflow

## Bronze Layer

- Reads raw employee CSV files from Azure Blob Storage
- Performs schema inference
- Stores raw data in Delta format
- Preserves original source data

Output:

- Bronze Delta Table

---

## Silver Layer

Data cleaning and transformation:

- Removes duplicate records
- Handles null values
- Standardizes column names
- Trims unnecessary spaces
- Converts data types
- Produces clean employee data

Output:

- Silver Delta Table

---

## SCD Type 2 Layer

Maintains historical employee information.

Implemented:

- New employee detection
- Updated employee detection
- Historical record preservation
- Current active record maintenance

Columns maintained:

- effective_start_date
- effective_end_date
- is_current

Output:

- Employee History Delta Table

---

## Gold Layer

Creates analytical datasets using Spark SQL.

Generated reports include:

- Current Employees
- Department Summary
- Salary Summary
- Employee Status Summary
- Department Salary Ranking
- Salary Bands
- Top 3 Highest Paid Employees by Department

SQL concepts used:

- GROUP BY
- Aggregate Functions
- CASE
- CTE
- Window Functions
- ROW_NUMBER()
- RANK()

Output:

- Gold Delta Tables
- CSV Exports

---

# Azure Data Factory Pipeline

Pipeline execution order:

```
Bronze
   ↓
Silver
   ↓
SCD Type 2
   ↓
Gold
```

Each notebook is executed sequentially after the successful completion of the previous notebook.

---

# Outputs

After a successful pipeline execution, outputs can be viewed in:

### Azure Data Factory

Navigate to:

```
Monitor
→ Pipeline Runs
```

This shows the execution status of each notebook.

---

### Azure Databricks

Navigate to:

```
Catalog
→ EmployeeLifecycleWorkspace
→ default
```

Available Delta Tables:

- Bronze Table
- Silver Table
- Employee History Table
- Department Summary
- Salary Summary
- Current Employees

---

### Unity Catalog Volume

Generated CSV files are available inside the configured Unity Catalog Volume.

Example outputs:

- department_summary.csv
- salary_summary.csv
- employee_history.csv
- current_employees.csv

---

# Prerequisites

To run this project, the following Azure resources are required:

- Azure Subscription
- Azure Blob Storage
- Azure Data Factory
- Azure Databricks Workspace
- Unity Catalog
- Running Databricks Cluster

---

# Setup Instructions

## Step 1

Clone the repository.

```bash
git clone https://github.com/<your-username>/Employee-Lifecycle-Pipeline.git
```

---

## Step 2

Create Azure Resources

Create:

- Resource Group
- Storage Account
- Blob Container
- Azure Data Factory
- Azure Databricks Workspace

---

## Step 3

Upload Dataset

Upload the employee CSV files into the Blob Storage container.

Example structure:

```
day_1/
day_2/
day_3/
day_4/
day_5/
```

---

## Step 4

Import Databricks Notebooks

Import the following notebooks:

- Bronze.ipynb
- Silver.ipynb
- SCD_03.ipynb
- Gold.ipynb

---

## Step 5

Configure Azure Resources

Update the notebooks with your Azure resources:

- Storage Account Name
- Blob Container Name
- Volume Name
- Unity Catalog
- Databricks Cluster

---

## Step 6

Import Azure Data Factory

Import the Azure Data Factory artifacts from the repository.

Configure:

- Linked Services
- Datasets
- Databricks Linked Service
- Personal Access Token
- Existing Interactive Cluster

---

## Step 7

Publish

Publish the Azure Data Factory.

---

## Step 8

Run Pipeline

Trigger the pipeline from Azure Data Factory.

Execution Flow:

```
Bronze
↓
Silver
↓
SCD Type 2
↓
Gold
```

---

# Sample Outputs

The project generates:

- Bronze Delta Table
- Silver Delta Table
- Employee History Table
- Department Summary
- Salary Summary
- Employee Status Summary
- Current Employees

---

# Future Enhancements

- Incremental Data Loading
- Parameterized Pipelines
- Power BI Dashboard
- Azure Key Vault Integration
- CI/CD using Azure DevOps

---

# Author

**Moksha Sri Marthineni**

Computer Science & Engineering

Azure Data Engineering Project
