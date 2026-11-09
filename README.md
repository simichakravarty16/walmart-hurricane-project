# walmart-hurricane-project

## Project Overview
This project investigates how Hurricane Helene impacted transaction patterns and consumer behavior across various Walmart locations in Florida. Using transaction records, product catalog information, store locations, inventory data, and historical weather data, we examine changes in purchasing before and during the hurricane.

Our goal was to identify the product categories that experienced the greatest increases in demand during surge periods, investigated how weather conditions influenced purchasing behaviors, and evaluated whether sales increases are the result of genuine demand or data-quality issues. In order to do this, we needed to clean the data by standardizing SKUs and category names, as well as join weather data using an API call.

## Analysis Questions
- Question 1: Demand Surge Identification --> Which product categories experienced the greatest sales surge in the 7 days before hurricane landfall compared to the prior baseline period? Quantify the percentage increase and visualize the daily trend for the top 5 categories.
- Question 2: The Pop-Tarts Effect (SKU Consolidation) --> After standardizing all Pop-Tart SKU variants into a single product, what is the true daily sales volume? How does the uncleaned (fragmented) view compare to the cleaned (consolidated) view? What business decisions would differ between the two views?
- Question 3: Weather Correlation Analysis --> Using weather data pulled from your chosen free API, how do specific weather indicators (wind speed, precipitation, barometric pressure) correlate with daily sales volume across categories? Is there a detectable lag between weather severity escalation and purchasing spikes?
- Question 4: Store-Level Geographic Patterns --> Do all Florida store locations experience the same surge patterns, or do stores closer to the predicted hurricane path show earlier and larger spikes? Identify any stores that appear to be outliers.
- Question 5: Signal vs. Artifact — The Board Games Investigation --> The board games/entertainment category shows a +250% sales increase. Using the SQLite inventory and sales database, investigate whether this is a genuine demand signal or a data artifact (e.g., SKU miscoding, category lumping, inventory reporting lag). Present your evidence and make a recommendation: should Walmart stock extra board games for the next storm?

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
├── DS2002_Midterm_Project_Brief.md
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
```

### File Descriptions

| File | Description |
|---|---|
| `DS2002_Midterm_Project_Brief.md` | Original project instructions and requirements |
| `Walmart Case.pdf` | Background information and case study |
| `walmart_transactions.csv` | Transaction-level POS records |
| `store_locations.csv` | Florida Walmart store metadata |
| `product_catalog.csv` | Product and SKU reference information |
| `distribution_centers.csv` | Distribution center information |
| `inventory_and_sales.db` | SQLite database containing daily sales summaries and inventory levels |
| `team_notebook.ipynb` | Main Jupyter Notebook containing data cleaning, API integration, analysis, visualizations, and findings |  

## How to Run
1. Clone or download this repository.
2. Open `notebooks/team_notebook.ipynb` in Google Colab or Jupyter Notebook.
3. Ensure the `data/` directory is accessible to the notebook.
4. Install the required Python libraries if they are not already available.
5. Run the notebook cells sequentially to reproduce the data-cleaning process, weather data integration, statistical analyses, and visualizations.

Note: Historical weather data is retrieved from Open-Meteo API, so an internet connection is required

## Contributors
Simi Chakravarty and Xiangyu Shi
