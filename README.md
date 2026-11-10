# walmart-hurricane-project

## Project Overview
This project investigates how Hurricane Helene (Steptember 26, 2024) impacted transaction patterns and consumer behavior across various Walmart locations in Florida. Using transaction records, product catalog information, store locations, distribution centers, inventory data, and historical weather data, we examine changes in purchasing patterns before and during the hurricane.

Our goal was to identify the product categories that experienced the greatest increases in demand during the surge period (September 19-25) compared to the baseline period (September 1-15), investigated how weather conditions influenced purchasing behaviors, and evaluated whether increases in sales reflected genuine demand or data quality issues. To accomplish this, we cleaned and standardized the data, including SKUs and product category names, and integrated historical weather data using an API.

## Analysis Questions
This project investigates five key questions surrounding Walmart's sales and supply chain dynamics before Hurricane Helene.

| # | Analysis Question | Focus |
|---|---|---|
| 1 | **Demand Surge Identification** | Identify the five product categories with the greatest sales increases during the seven days preceding hurricane landfall. Quantify percentage changes and visualize daily sales trends. |
| 2 | **The Pop-Tarts Effect (SKU Consolidation)** | Consolidate fragmented Pop-Tart SKUs to determine true daily sales volume and evaluate how SKU standardization changes demand estimates and business decisions. |
| 3 | **Weather Correlation Analysis** | Examine relationships between wind speed, precipitation, barometric pressure, and daily sales. Investigate potential time lags between weather escalation and purchasing spikes. |
| 4 | **Store-Level Geographic Patterns** | Compare sales surges across Florida Walmart locations to determine whether proximity to the predicted hurricane path influences purchasing behavior. Identify geographic outliers. |
| 5 | **Signal vs. Artifact: Board Games Investigation** | Use SQLite inventory and sales records to investigate the reported 250% increase in entertainment sales, distinguish genuine demand from data artifacts, and recommend inventory adjustments. |

## Reflection Questions
We also answered these reflection questions to evaluate our analyses and teamwork throughout this project.

| # | Reflection Question | Focus |
|---|---|---|
| 1 | **Data Quality Impact** | Describe a specific data quality issue encountered in the supplied data, explain how the cleaning decision affected the analysis, and consider what might have happened if the issue had gone unnoticed. |
| 2 | **ETL Trade-offs** | Examine one decision involving SKU standardization, missing timestamps, or weather data joins. Consider an alternative approach and explain how it might have changed the results. |
| 3 | **Pipeline Trust** | Evaluate the Walmart CDO's argument that the greatest risk lies in the data pipeline rather than the model. Discuss whether you agree and identify the most fragile part of your team's pipeline. |
| 4 | **Business vs. Data** | Reflect on the board game investigation (Question 5), explaining how your team balanced statistical evidence from imperfect data against potential business risks when making its recommendation. |
| 5 | **Team Collaboration** | Describe how your team divided responsibilities, identify the most valuable skill each member contributed, and discuss what your team would approach differently with another week to work. |

## Data Sources
The analysis incorporates the following datasets:
- Walmart Transactions: Individual transaction records containing timestamps, product identifiers, quantities, prices, and store IDs.
- Product Catalog: Product information, including SKUs, product names, categories, suppliers, and package sizes.
- Store Locations: Geographic and regional information for Walmart stores across Florida.
- Distribution Centers: Distribution center information, including surge capacity and shipping costs.
- Inventory and Sales Database: SQLite database containing inventory records and daily sales summaries.
- Historical Weather Data: Daily precipitation, maximum wind speed, and mean sea-level pressure retrieved using the Open-Meteo Historical Weather API.

## Repository Structure
```text
walmart-hurricane-project/
│
├── README.md
├── CHARTER.md
├── Walmart Case.pdf
├── DS2002_Midterm_Project_Brief.md
├── Midterm Project Presentation.pptx
│
├── data/
│   ├── walmart_transactions.csv
│   ├── store_locations.csv
│   ├── product_catalog.csv
│   ├── distribution_centers.csv
│   └── inventory_and_sales.db
│
└── notebooks/
    └── team_notebook.ipynb
    └── 2026-10-23 — Midterm Checkpoint — Lab.ipynb
    └── 2026-10-30 — Midterm Progress — Lab.ipynb
    └── scratch/
        └── 2026-10-19 — Midterm Kickoff and Team Formation — Lecture.ipynb
        └── 2026-10-21 — Weather API Join — Studio.ipynb
        └── 2026-10-26 — Midterm Clinic Cleaning and Joins — Lecture.ipynb
        └── 2026-10-28 — Midterm Clinic Analysis and Charts — Studio.ipynb
        └── 2026-11-04 — Reflection What Broke What Mattered — Studio.ipynb
```

### File Descriptions

| File | Format | Description |
|---|---|---|
| `README.md` | Markdown | Project overview, analytical and reflection questions, repository structure, file descriptions, instructions for running `team_notebook.ipynb`, and contributors |
| `CHARTER.md` | Markdown | Team members, project goals, and individual roles |
| `Walmart Case.pdf` | PDF | Background information and case study |
| `DS2002_Midterm_Project_Brief.md` | Markdown | Original project instructions and requirements |
| `Midterm Project Presentation.pptx` | PowerPoint | Presentation slides covering data quality issues, the data cleaning pipeline, key graphs and findings, recommendations, and what broke during the project|
| `walmart_transactions.csv` | CSV | Transaction-level POS records |
| `store_locations.csv` | CSV | Florida Walmart store metadata |
| `product_catalog.csv` | CSV | Product and SKU reference information |
| `distribution_centers.csv` | CSV | Distribution center information |
| `inventory_and_sales.db` | SQLite | SQLite database containing daily sales summaries and inventory levels |
| `team_notebook.ipynb` | Jupyter Notebook | Main Jupyter Notebook containing data cleaning, weather API integration, analysis, visualizations, findings, and reflections |  
| `2026-10-23 — Midterm Checkpoint — Lab.ipynb` | Jupyter Notebook | Midterm project checkpoint and progress documentation |
| `2026-10-30 — Midterm Progress — Lab.ipynb` | Jupyter Notebook | Midterm project progress updates, including answers to analytical questions Q1-Q3 |
| `scratch/` | Folder | Lecture and studio notebooks related to the midterm project |

## How to Run
1. Clone or download this repository.
2. Open `notebooks/team_notebook.ipynb` in Google Colab or Jupyter Notebook.
3. Ensure the `data/` directory is accessible to the notebook.
4. Install the required Python libraries if they are not already available.
5. Run the notebook cells sequentially to reproduce the data-cleaning process, weather data integration, statistical analyses, and visualizations.

Note: Historical weather data is retrieved from Open-Meteo API, so an internet connection is required

## Contributors
Simi Chakravarty and Xiangyu Shi
