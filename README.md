# Data Pre-Processing

A comprehensive data preprocessing and data wrangling project demonstrating best practices for data cleaning, handling missing values, and transforming raw data into analysis-ready datasets.

## 📋 Overview

This repository contains two main data preprocessing projects:

1. **Automobile Data Wrangling** - Automotive dataset cleaning and normalization
2. **Bank Marketing Campaign Data Cleaning** - Financial/campaign dataset transformation and segmentation

## 🗂️ Project Structure

```
├── auto_before.csv                          # Raw automobile data
├── clean_df.csv                             # Cleaned automobile dataset
├── data_wrangling.ipynb                     # Automobile data wrangling notebook
├── README.md                                # This file
└── Project Cleaning Bank Marketing Campaign Data/
    ├── bank_marketing.csv                   # Raw bank marketing data
    ├── bankdata_cleaning.ipynb              # Bank data cleaning notebook
    ├── client.csv                           # Cleaned client information
    ├── campaign.csv                         # Cleaned campaign metrics
    └── economics.csv                        # Economic indicators data
```

## 🚗 Project 1: Automobile Data Wrangling

### Purpose
Clean and normalize automotive dataset by handling missing values and converting raw data into analysis-ready format.

### Key Features
- **Data Import**: Loads raw automobile data with 26 features (symboling, make, fuel-type, price, etc.)
- **Missing Value Identification**: Detects and quantifies missing values represented as "?" symbols
- **Missing Value Treatment**:
  - **Mean Imputation** for numeric columns:
    - `normalized-losses` (41 missing values)
    - `stroke`, `bore` (4 missing values each)
    - `horsepower`, `peak-rpm` (2 missing values each)
  - **Frequency-based Imputation** for categorical columns:
    - `num-of-doors` (2 missing values) → replaced with "four" (most frequent, 84% of data)

### Input/Output
- **Input**: `auto_before.csv` (raw data)
- **Output**: `clean_df.csv` (processed data)

---

## 🏦 Project 2: Bank Marketing Campaign Data Cleaning

### Purpose
Transform bank marketing campaign data into structured, analytical tables by cleaning, standardizing, and segmenting into domain-specific datasets.

### Key Features

#### Data Cleaning Operations
1. **Character Replacement**: Replace "." with "_" in `job` and `education` columns
2. **Unknown Value Handling**: Replace "unknown" with NaN in education field
3. **Boolean Conversion**: Convert yes/no values to 0/1 in:
   - `credit_default`
   - `mortgage`
   - `campaign_outcome`
   - `previous_outcome` (success → 1, else → 0)

#### Date Engineering
- Creates `last_contact_date` by combining day, month, and fixed year (2022)
- Format: YYYY-MM-DD (e.g., 2022-03-15)

#### Data Segmentation
The raw dataset is split into three normalized tables:

**📊 client.csv** - Client Demographics
- `client_id`, `age`, `job`, `marital`, `education`, `credit_default`, `mortgage`

**📈 campaign.csv** - Campaign Metrics
- `client_id`, `number_contacts`, `contact_duration`, `previous_campaign_contacts`
- `previous_outcome`, `campaign_outcome`, `last_contact_date`

**💹 economics.csv** - Economic Indicators
- `client_id`, `cons_price_idx`, `euribor_three_months`

### Input/Output
- **Input**: `bank_marketing.csv` (raw data)
- **Output**: 
  - `client.csv` (client information)
  - `campaign.csv` (campaign details)
  - `economics.csv` (economic indicators)

---

## 🛠️ Technologies & Libraries

- **Python 3.x**
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical operations and NaN handling
- **Jupyter Notebooks** - Interactive data analysis environment

## 📊 Data Preprocessing Techniques Demonstrated

| Technique | Application | Example |
|-----------|-------------|---------|
| **Missing Value Detection** | Identifying gaps in data | "?" symbols in automobile data |
| **Mean Imputation** | Filling numeric missing values | Horsepower, bore, stroke columns |
| **Mode/Frequency Imputation** | Filling categorical missing values | Door count based on frequency |
| **Data Type Conversion** | Converting to appropriate types | String → Boolean, String → DateTime |
| **String Normalization** | Standardizing text fields | Replacing "." with "_" |
| **Date Engineering** | Creating datetime features | Combining day/month/year columns |
| **Data Segmentation** | Splitting into logical tables | Bank data into client/campaign/economics |

