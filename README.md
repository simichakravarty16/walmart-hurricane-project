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

| # | Reflection Question | Focus | Answer |
|---|---|---|---|
| 1 | **Data Quality Impact** | Describe a specific data quality issue encountered in the supplied data, explain how the cleaning decision affected the analysis, and consider what might have happened if the issue had gone unnoticed. | One data quality issue we encountered in the walmart_transactions and product_catalog datasets was fragmented SKUs, where the same products appeared under multiple different SKUs. To address this issue, we consolidated SKUs representing the same products into one standardized SKU. Before consolidation, we had 45 distinct SKUs, which were reduced to 20 canonical products after cleaning. From our Q2 analysis, we found that four different SKUs (POPTART-STRAW, PT-12, PT_STRAWBERRY, and SKU#459812) represented the same Strawberry Pop-Tarts product, which was the largest consolidated SKU family. Before consolidation, these four SKUs recorded 1,239, 1,332, 1,230, and 1,204 units sold, respectively based on transactions with valid dates. After consolidation, they were combined into a single standardized SKU, POPTART-STRAW, showing a total of 5,005 units sold. This allowed us to accurately measure the total sales of Strawberry Pop-Tarts as one product rather than treating the four SKUs as separate products. If we had not caught this issue, we might have underestimated the overall demand for Strawberry Pop-Tarts and other products by treating different SKUs representing the same product as separate products. This could have changed our conclusions about which products had the highest daily sales and which experienced the greatest increases in average daily sales from the baseline to the surge period. |
| 2 | **ETL Trade-offs** | Examine one decision involving SKU standardization, missing timestamps, or weather data joins. Consider an alternative approach and explain how it might have changed the results. | After converting timestamps to datetime and missing or invalid timestamps to NaT, we decided to keep rows with missing timestamps during the initial data cleaning because they still contained useful transaction information, such as SKU, product name, quantity, and unit price. We wanted to preserve this information because removing these rows could lead to an underestimation of overall sales and revenue in analyses that did not require dates. An alternative approach we could have taken was to remove rows with missing timestamps during initial cleaning, which would have reduced the number of available transactions. However, our analytical questions primarily focused on daily sales trends and comparisons between the baseline and surge periods, which required valid transaction dates. After merging with the weather API data, we excluded 881 rows with missing dates for the weather-based analysis and other date-dependent analyses. In Q2, we excluded transactions with missing dates from both the fragmented and consolidated Strawberry Pop-Tarts sales comparisons to ensure consistency with our daily sales analysis. Therefore, removing these rows earlier would not have changed our reported results, but keeping them preserved useful information for other potential analyses. |
| 3 | **Pipeline Trust** | Evaluate the Walmart CDO's argument that the greatest risk lies in the data pipeline rather than the model. Discuss whether you agree and identify the most fragile part of your team's pipeline. | We agree with the Walmart CDO that the biggest risk is the data pipeline rather than the model because errors during data cleaning and preparation can lead to inaccurate results, even if the analysis code runs correctly. These inaccurate results could also lead to poor business and financial decisions, such as ordering too much or too little inventory, which could result in financial losses or product shortages. The most fragile part of our data pipeline was standardizing SKUs, product names, and categories because the same products appeared under different values in these columns. We needed to carefully determine which values represented the same product and map them consistently. If we incorrectly combined different products or failed to identify equivalent products, our sales calculations could have produced inaccurate results, leading to incorrect conclusions about demand changes between the baseline and surge periods. |
| 4 | **Business vs. Data** | Reflect on the board game investigation (Question 5), explaining how your team balanced statistical evidence from imperfect data against potential business risks when making its recommendation. | For this question, we had to verify whether the claim of a 250% increase in the board games/Entertainment category was valid. However, the data was imperfect, as there were multiple SKUs present within the category and the time periods needed to be separated into baseline and surge periods. When looking at the SQLite and CSV data, the evidence suggested that the reported increase in board-game-related sales reflected a genuine demand signal and, since we audited the SKUs and categories, we knew that miscoded SKUs were not causing the previously defined signal. However, it appeared as though the magnitude of the increase was not entirely accurate, as we found a 125-145% sales increase in the Entertainment category depending on which source was consulted. Based on the statistical evidence, the direction of the effect was maintained but we didn’t know by how much the sales increase was reflected in this specific scenario. Since it would be more costly to be out of stock than to overstock a shelf-stable item, we decided to recommend Walmart to stock additional quantities of selected products, particularly Monopoly, before the next storm, provided that they analyze the SKU mappings and reconcile their data before. If we had more time or more data, we would try to test significance, instead of solely comparing the means of each group. We could also try to use data from more than one hurricane or from more than one state to see if this effect repeats across different conditions. |
| 5 | **Team Collaboration** | Describe how your team divided responsibilities, identify the most valuable skill each member contributed, and discuss what your team would approach differently with another week to work. | As a team, we tried to divide the work as equally as possible by meeting frequently to discuss how we should complete each portion of the assignment. We decided that it would be best for each of us to focus on a specific portion of the assignment and develop familiarity with the concepts, which enabled us to answer all the subsequent questions on the topic. For example, Xiangyu took the lead on the data cleaning pipeline, Q1-Q2 of the analytical questions, and Q1-Q3 of the reflection questions. Simi took the lead on the weather API requirement, Q3-Q5 of the analytical questions, and Q4-Q5 of the reflection questions. If we had another week to work on the project, we would attempt to refine additional aspects of our code and analysis. One area that Simi believed could have benefited from further analysis was Q4 of the analytical questions, particularly how store geography and distance from the hurricane path impacted surge patterns. Since the hurricane path was not provided, we had to look for a reliable source containing information on the hurricane path. However, the source we found did not have information for every day included in the sales data, so we had to make some adjustments and assumptions. If we had more time, we could have worked together to find a new source, or perhaps used another API call to obtain hurricane path data. Regarding the most valuable skills that each team member contributed, Xiangyu was very diligent with her data cleaning code and provided extremely detailed explanations. She was also punctual and asked the TAs for help whenever our group had questions. Simi was also very diligent and contributed valuable skills in creating visualizations with annotations. She paid close attention to how the data was presented and made sure the charts were clear, easy to understand, and effectively communicated the findings. We both previously took DS2003 Communicating with Data before and the skills we developed in that class have translated well to this project. |

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
├── CHARTER.md
├── DS2002_Midterm_Project_Brief.md
├── Midterm Project Presentation.pptx
├── README.md
├── Walmart Case.pdf
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
    └── scratch/
        └── 2026-10-19 — Midterm Kickoff and Team Formation — Lecture.ipynb
        └── 2026-10-21 — Weather API Join — Studio.ipynb
        └── 2026-10-23 — Midterm Checkpoint — Lab.ipynb
        └── 2026-10-26 — Midterm Clinic Cleaning and Joins — Lecture.ipynb
        └── 2026-10-28 — Midterm Clinic Analysis and Charts — Studio.ipynb
        └── 2026-10-30 — Midterm Progress — Lab.ipynb
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
| `scratch/` | Folder | Lecture, studio, and lab notebooks related to the midterm project |

## How to Run
1. Clone or download this repository.
2. Open `notebooks/team_notebook.ipynb` in Google Colab or Jupyter Notebook.
3. Ensure the `data/` directory is accessible to the notebook.
4. If using Google Colab, download all four CSV files and the SQLite database file from the `data/` directory and upload them to the Colab environment. 
5. Install the required Python libraries if they are not already available.
6. Run the notebook cells sequentially to reproduce the data-cleaning process, weather data integration, statistical analyses, and visualizations.

Note: Historical weather data is retrieved from Open-Meteo API, so an internet connection is required

## Contributors
Simi Chakravarty and Xiangyu Shi
