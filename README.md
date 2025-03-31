# NBA Analytics Pipeline
## Problem Description
This project addresses the challenge of processing, analyzing, and visualizing NBA performance data to identify key factors that contribute to team success. NBA analytics has become crucial in basketball operations, helping teams make data-driven decisions about player evaluation, game strategy, and roster construction.

The NBA Analytics Pipeline provides insights on:
 - Conference and division performance comparisons
 - Scoring pattern evolution over NBA history
 - Statistical indicators most strongly correlated with winning
   
Through this end-to-end pipeline, we can access clean, processed NBA data and visualize performance trends through an interactive dashboard.

## Architecture
This project implements a complete data pipeline with the following components:

1. Data Extraction: R script extracts NBA data using hoopR
2. Data Lake: Raw data stored in Google Cloud Storage
3. Data Processing: Data loaded into BigQuery using dlt
4. Data Warehouse: Optimized tables in BigQuery with partitioning (using dbt)
5. Transformations: dbt models create analytical tables
6. Visualization: [R shiny dashboard](https://rstudio.github.io/shinydashboard/) provides interactive insights
7. Orchestration: Kestra automatically schedules and manages workflow execution at the end of each NBA season
![image](https://github.com/user-attachments/assets/d62e10d2-4556-48b9-8d03-0fce4cdb996a)

## Dataset
the data were extracted by [`hoopR`](https://hoopr.sportsdataverse.org/). it is an R package for working with men’s basketball data.
just run this code `dat <- hoopR::load_nba_pbp(seasons = year)` you could collect the NBA data form that seaons.

## Infrastructure
the following tools are used:
 - Cloud/Data warehouse: Google Cloud Platform/BigQuery
 - Orchestration: Kestra
 - Batch Processing: Python with Kestra and dlt
 - Transformation: dbt
 - Dashboard: [R shiny dashboard](https://rstudio.github.io/shinydashboard/)

## Dashboard
Please see this [link](https://lai-clement.shinyapps.io/NBA_stats/) for the dashboard
![image](https://github.com/user-attachments/assets/2e9e62ab-92bd-4f83-8709-28b319c1339d)
The R Shiny dashboard provides interactive visualizations of NBA data with:
 -  A multi-tab interface showing team performance metrics, player statistics, and league-wide trends in an organized, easy-to-navigate layout.

## Steps to Reproduce

### Prerequisites
 - Google Cloud Platform account
 - dbt cloud account
 - R
 - Python with dbt package
 - Kestra instance

### Step1: Kestra Setup
Set the following value using KV Store in the Kestra:
| Key | Description |
|-----|-------------|
| GCP_LOCATION | Google Cloud Platform's project location |
| GCP_PROJECT_ID | Google Cloud Platform's project ID |
| GCP_CREDS | GCP credentials JSON |
| GCP_BUCKET_NAME | GCS bucket name for data lake |
| GCP_DATASET | BigQuery dataset name |
| GITHUB_ACCESS_TOKEN | GitHub personal access token (for your dbt models) |
| BQ_CREDENTIALS_PROJECT_ID | Google Cloud Platform's project ID |
| BQ_CREDENTIALS_CLIENT_EMAIL | Google Cloud Platform's client email |
| BQ_CREDENTIALS_PRIVATE_KEY | Google Cloud Platform's private key |
| BQ_LOCATION | BigQuery's dataset location |
| BQ_AUTODETECT_SCHEMA | "TRUE" |

### Step 2: Data Extraction and Loading
In Kestra, use the "Backfilled" option to execute the R_collecting_NBA_data flow. This will:
 - Extract NBA data for the specified season using R (hoopR)
 - Load the data into BigQuery using dlt
   
This flow will automatically execute every July 1st to capture each complete NBA season.

### Step 3: Data Transformation
Execute the dbt_test flow in Kestra to transform the data within BigQuery. This workflow:
 - Runs dbt models to create analytical tables
Is automatically scheduled to run every July 2nd after data loading



### Step 4: Dashboard Deployment
1. Download the transformed data from BigQuery
2. Generate a dashboard by running the Shiny_R.R script
3. Install required R packages using:
```
install.packages(c("shiny", "shinydashboard", "DT", "plotly", "bigrquery"))
```
4. Access the dashboard locally through your web browser

# Future Improvements
 - Add real-time data processing for in-game analytics
 - Implement server-side data connections in R Shiny to enable automatic dashboard updates
 - Expand the dataset to include player tracking data




