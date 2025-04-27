🏎️ Formula 1 Data Engineering Project - Azure Databricks (Single CSV)
📋 Table of Contents
Project Overview

➡️ Architecture Overview
➡️ Tech Stack Used
➡️ Dataset Description
➡️ Medallion Architecture Layers
➡️ Data Processing Steps (Detailed)
➡️ Star Schema Design
➡️ Gold Layer KPIs & Aggregations
➡️ Databricks Visualizations
➡️ Folder Structure
➡️ How to Run the Project
➡️ Final Deliverables
➡️ License

📌 Project Overview
This project processes a single Formula 1 historical dataset (formula_one.csv) using a full Data Engineering Pipeline.
We apply the Medallion Architecture (Bronze ➡️ Silver ➡️ Gold), build a Star Schema, generate KPIs, Aggregations, and Visualizations using Azure Databricks and Delta Lake.

🏛️ Architecture Overview
formula_one.csv ➡️ Bronze Layer ➡️ Silver Layer (cleaned) ➡️ Gold Layer (Star Schema) ➡️ Analytics Layer ➡️ Visualizations

⚙️ Tech Stack Used
Technology	- Purpose
Azure Databricks	- Cloud-based Data Engineering workspace
Apache Spark (PySpark)	- Distributed data processing
Delta Lake	- Storage with ACID transactions
Azure Data Lake Gen2	- Scalable cloud storage
Python (PySpark)	- Data cleaning, transformation, and aggregation
Databricks Visualization	- Dashboards, maps, charts
GitHub	- Version control and project storage
🗃️ Dataset Description

Dataset	Description
formula_one.csv	Single CSV containing all necessary information about races, drivers, constructors, circuits, lap times, qualifying, and results.

Important Columns:
Driver Details (driver_ID, driver_name, nationality, code)
Constructor Details (constructor_ID, constructor)
Circuit Details (circuit_ID, circuit_name, country, lat, long)
Race Details (race_ID, race_name, season, date, round, distance, weather)
Result Details (points, finish_position, status, time)
Qualifying Details (qualify_Position, qualify_Best_Time, qualify_Worst_Time, qualify_Average_Time)

🧹 Medallion Architecture Layers
Layer	Purpose	Storage Path
Bronze - 	Raw ingestion of formula_one.csv	/mnt/mybronze/
Silver -	Cleaned and processed data	/mnt/mysilver/
Gold	- Star schema modeling (Facts + Dimensions)	/mnt/mygold/f1_star_schema/
Analytics	- KPIs and Data Marts	/mnt/mygold/f1_star_schema_analytics/

🔥 Data Processing Steps (Detailed)
Bronze Layer: Read formula_one.csv directly.
Save it as Delta Table.

Silver Layer: Data Cleaning:
Drop duplicates
Standardize date and timestamp formats
Handle missing values
Save as clean Delta Table.

Gold Layer (Star Schema)

Create Dimension Tables:
dim_driver
dim_constructor
dim_circuit
dim_date
dim_race
dim_qualifying

Create Fact Table:
fact_race_results (joining drivers, constructors, circuits, races)

Analytics Layer:
Generate KPIs, Aggregations, and Data Marts.
Save outputs to Delta format.

🛤️ Star Schema Design
plaintext
Copy
Edit
          dim_driver
             |
dim_date - fact_race_results - dim_constructor
             |
         dim_circuit
             |
      dim_race, dim_qualifying
      
📈 Gold Layer KPIs & Aggregations
KPI / Mart	Description
kpi_season_avg_points	Average points per season
kpi_driver_avg_points	Average points per driver
kpi_driver_win_rate	Driver win rate (wins/total races)
kpi_constructor_most_wins	Constructor (car company) with the most wins
kpi_races_per_country	Number of races hosted per country
mart_driver_summary	Driver profile summary (points, wins, nationality)
✅ Each KPI is saved inside Delta format in /mnt/mygold/f1_star_schema_analytics/

📊 Databricks Visualizations
World Map: Plotting Circuits by coordinates (lat, long)
Bar Chart: Top Constructors by Wins
Line Graph: Season-wise Points trend
Pie Chart: Races per Country
Tables: Driver Summary Tables, Win Rates

📂 Folder Structure (Recommended GitHub Structure)
kotlin
Copy
Edit
f1-data-engineering/
│
├── notebooks/
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_silver_cleaning.ipynb
│   ├── 03_gold_star_schema.ipynb
│   ├── 04_kpi_aggregations.ipynb
│   ├── 05_visualizations.ipynb
│
├── datasets/
│   └── formula_one.csv
│
├── README.md
└── requirements.txt (if needed)

🧑‍💻 How to Run the Project
Clone this GitHub Repository.
Upload formula_one.csv into your Databricks workspace.
Mount your Azure Data Lake Gen2 storage.
Run the notebooks in order:
Bronze ➡️ Silver ➡️ Gold ➡️ KPIs ➡️ Visualization
Validate Delta Tables.
Create Visualizations using Databricks UI.

✅ Final Deliverables
✅ Silver Layer Clean Delta Table
✅ Star Schema Modeled Gold Layer
✅ KPIs, Aggregations, Marts
✅ Visualizations
✅ Full GitHub Project

📚 License
This project is for educational purposes.
Feel free to fork, clone, or modify it! 🚀

🚀 THANK YOU!
If you found this helpful, consider ⭐ starring the repository!

