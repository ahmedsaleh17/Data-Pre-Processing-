# Bank Marketing Campaign Data Cleaning

## 📋 Overview

This project focuses on cleaning and normalizing a raw bank marketing campaign dataset into structured, analysis-ready tables. The data is transformed from a single flat file into three normalized tables organized by domain: client information, campaign metrics, and economic indicators.

## 🎯 Project Objectives

- Clean raw marketing data by standardizing formats and handling inconsistencies
- Convert categorical variables to appropriate data types (boolean, datetime)
- Engineer new features (date columns) from existing data
- Segment data into logically organized, normalized tables
- Prepare data for statistical analysis and machine learning applications

## 📊 Data Flow

```
bank_marketing.csv (Raw Data)
        ↓
    [Cleaning Process]
        ↓
    [Data Transformation]
        ↓
    [Data Segmentation]
        ↓
    ├── client.csv
    ├── campaign.csv
    └── economics.csv
```

## 🔧 Data Cleaning Operations

### 1. String Normalization
Replace special characters with underscores for consistency:
- **Job column**: "." → "_" (e.g., "technician." → "technician_")
- **Education column**: "." → "_"

### 2. Unknown/Missing Value Handling
- **Education column**: Replace "unknown" with NaN for proper missing value treatment

### 3. Boolean Conversion (0/1 Encoding)
Convert categorical yes/no responses to numeric boolean format:

| Column | Conversion |
|--------|-----------|
| `credit_default` | "yes" → 1, else → 0 |
| `mortgage` | "yes" → 1, else → 0 |
| `campaign_outcome` | "yes" → 1, else → 0 |
| `previous_outcome` | "success" → 1, else → 0 |

### 4. Date Engineering
Create `last_contact_date` column by combining temporal fields:
- **Source columns**: `day`, `month` (pre-existing)
- **Added column**: `year` = 2022 (constant)
- **Format**: YYYY-MM-DD (e.g., "2022-03-15")
- **Data Type**: DateTime (using pandas `pd.to_datetime()`)

## 📁 Output Tables

### 1. **client.csv** - Client Demographics & Credit Profile
Essential client information for segmentation and profiling:

| Column | Type | Description |
|--------|------|-------------|
| `client_id` | Integer | Unique client identifier |
| `age` | Integer | Client age in years |
| `job` | String | Client occupation |
| `marital` | String | Marital status |
| `education` | String | Education level |
| `credit_default` | Boolean | Has credit default history (1/0) |
| `mortgage` | Boolean | Has mortgage (1/0) |

**Use Case**: Client targeting, demographic analysis, risk assessment

---

### 2. **campaign.csv** - Campaign Interaction & Outcomes
Detailed campaign contact history and response metrics:

| Column | Type | Description |
|--------|------|-------------|
| `client_id` | Integer | Unique client identifier (foreign key) |
| `number_contacts` | Integer | Total contacts during campaign |
| `contact_duration` | Integer | Duration of last contact (seconds) |
| `previous_campaign_contacts` | Integer | Contacts from previous campaigns |
| `previous_outcome` | Boolean | Success in previous campaign (1/0) |
| `campaign_outcome` | Boolean | Current campaign response (1/0) |
| `last_contact_date` | DateTime | Date of most recent contact (YYYY-MM-DD) |

**Use Case**: Campaign effectiveness analysis, contact frequency optimization, engagement prediction

---

### 3. **economics.csv** - Economic Indicators
Macroeconomic conditions at time of campaign:

| Column | Type | Description |
|--------|------|-------------|
| `client_id` | Integer | Unique client identifier (foreign key) |
| `cons_price_idx` | Float | Consumer price index |
| `euribor_three_months` | Float | 3-month EURIBOR rate (%) |

**Use Case**: Economic influence analysis, temporal trend identification

## 📝 Processing Workflow

The notebook (`bankdata_cleaning.ipynb`) executes the following steps:

1. **Import Libraries**: pandas, numpy
2. **Load Data**: Read `bank_marketing.csv`
3. **Inspect Data**: Use `.info()` to examine structure
4. **Clean Job Column**: Replace "." with "_"
5. **Clean Education Column**: Replace "." with "_" and "unknown" with NaN
6. **Convert Boolean Columns**: Apply lambda functions for yes/no → 0/1 conversion
7. **Engineer Date**: Combine day + month + 2022 year into datetime column
8. **Segment Data**: Extract relevant columns into three separate dataframes
9. **Type Conversion**: Convert boolean columns to bool datatype
10. **Export Data**: Save each table as CSV

## 📂 Files

| File | Size | Description |
|------|------|-------------|
| `bank_marketing.csv` | Raw input | Original unprocessed marketing data |
| `bankdata_cleaning.ipynb` | Jupyter Notebook | Interactive cleaning workflow and transformations |
| `client.csv` | Output | Cleaned client demographic data |
| `campaign.csv` | Output | Cleaned campaign metrics and outcomes |
| `economics.csv` | Output | Cleaned economic indicator data |

## 🔗 Data Relationships

The three output tables share a common key for joining:

```
client ──────┐
             ├─→ Joined on client_id
campaign ────┤
             ├─→ Joined on client_id
economics ───┘
```

This normalized structure enables:
- Efficient data queries
- Reduced redundancy
- Better analytical flexibility
- Support for database design patterns

## 🛠️ Technologies

- **Python 3.x**
- **Pandas** - DataFrames, data cleaning, CSV I/O
- **NumPy** - Missing value handling (np.nan)
- **Jupyter** - Interactive data exploration and documentation

## 📊 Data Quality Improvements

| Issue | Solution | Benefit |
|-------|----------|---------|
| Inconsistent separators | Replace "." with "_" | Standardized naming |
| Unknown values | Convert to NaN | Proper missing data handling |
| Categorical yes/no | Convert to 0/1 | Machine learning compatibility |
| Mixed date formats | Create datetime column | Time-series analysis ready |
| Flat structure | Normalize into 3 tables | Reduced data redundancy |

## 💡 Key Insights

- **Data Normalization**: Breaking into three tables improves data integrity and query efficiency
- **Type Consistency**: Boolean conversion enables proper statistical analysis
- **Date Engineering**: Standardized datetime format supports temporal analysis
- **Missing Value Treatment**: NaN values in education enable proper imputation strategies

## 🎓 Learning Outcomes

This project demonstrates:
✓ Pandas string operations (`.str.replace()`, lambda functions)  
✓ Missing value handling with NaN and `.apply()`  
✓ Boolean/categorical encoding  
✓ DateTime parsing and formatting  
✓ Data segmentation and normalization  
✓ CSV import/export workflows  

## 📖 Usage

### Run the Cleaning Process
```bash
jupyter notebook bankdata_cleaning.ipynb
```

### Load Processed Data
```python
import pandas as pd

client = pd.read_csv('client.csv')
campaign = pd.read_csv('campaign.csv')
economics = pd.read_csv('economics.csv')

# Join tables
merged = client.merge(campaign, on='client_id').merge(economics, on='client_id')
```

## 🔄 Data Validation Checks

- ✓ No missing values in `client_id` (referential integrity)
- ✓ Boolean columns contain only 0/1 values
- ✓ `last_contact_date` is valid datetime format
- ✓ All rows preserved through transformations (no data loss)
----
