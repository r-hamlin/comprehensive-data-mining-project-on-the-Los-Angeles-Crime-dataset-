# comprehensive-data-mining-project-on-the-Los-Angeles-Crime-dataset-
This is a comprehensive data‑mining project on the Los Angeles Crime dataset (≈10 million records, 28 features)
Comprehensive Data‑Mining Project on the Los Angeles Crime Dataset
Overview
This project explores the Los Angeles Police Department’s Crime Data from 2020 to the present (≈ 10 million records across 28 features). It was originally completed as part of a graduate‑level data‑mining course. The goal was to perform a thorough exploratory analysis, engineer meaningful features, and test a set of hypotheses about how crime relates to demographics, location, and time.
The cleaned notebook and code live in this repository so that others can reproduce the analysis and build upon it. The project is organized to separate raw data, processing scripts, and results. See the notebooks/analysis.ipynb for the full interactive exploration.

Dataset
The raw dataset (Crime_Data_from_2020_to_Present.csv) is published by the City of Los Angeles and contains every reported incident within city limits, with fields such as:
•	DR No – unique incident identifier
•	Date RPTD / DATE OCC – report and occurrence timestamps
•	AREA / AREA NAME – police district codes and names
•	Crm Cd / Crm Cd Desc – numeric crime codes and their descriptions
•	Weapon Used Cd / Weapon Desc – codes and descriptions of any weapons involved
•	Vict Age, Sex, Descent – victim demographics
•	LAT / LON – latitude and longitude of the incident

Because the CSV is very large (≈ 10 M rows), it is not included in this repository. To reproduce the analysis, download the latest version from the LAPD Open Data portal and place it in a data/ directory.

Methodology
1.	Data cleaning and preprocessing
-	Removed extremely sparse columns (crime codes 3 and 4).
- Filled missing categorical values with “Unknown” and dropped rows with impossible ages or coordinates.
- Converted DATE OCC and TIME OCC to more usable features: year, month, day‑of‑week, seasonal labels and time‑of‑day buckets (Morning, Afternoon, Evening, Late Night).
- Simplified premise descriptions into broader categories (e.g. Residential, Business/Office, Retail/Restaurant) and derived a binary IS_VIOLENT flag based on keywords like assault, robbery, homicide, etc.
  
2. Exploratory analysis
- Investigated distributions and missing values, visualizing which columns required imputation[1].
- Profiled top weapon codes, crime codes and premises.
- Constructed bar charts and facet grids comparing the share of violent vs. non‑violent incidents across victim age groups and simplified premises[1].

3. Hypothesis testing
- H1 – Victim demographics and premises influence crime type and severity: Younger victims, particularly teens, are involved in a higher share of violent incidents; violence rates vary by premise (e.g. parks vs. retail).
- H2 – Seasonal patterns: Bootstrap resampling showed no statistically significant increase in crime during summer compared with winter (Δ≈ –29 incidents/day, 95 % CI [–77.5, 18.4])[2].
- H3 – Crime co‑occurrence: Lift matrices revealed which crime types co‑occur within districts and time‑of‑day buckets; most lift values hovered slightly above 1, indicating weak positive associations[3].

4. Outputs and artifacts
- The cleaned dataset (crime_data_cleaned.csv) and a co‑occurrence table (crime_cooccurrence.csv) summarising paired crimes.
- Figures saved in the figures/ directory, including missing‑value charts, violent/non‑violent share plots, seasonal line plots and co‑occurrence heatmaps.
- A plain‐text summary of the bootstrap analysis (H2_summer_winter_bootstrap.txt).
    
Project structure
la-crime-analysis/
├── data/               # place the raw CSV here (ignored by Git)
├── notebooks/
│   └── analysis.ipynb  # interactive analysis (this notebook)
├── outputs/            # cleaned data and co‑occurrence tables
├── figures/            # generated charts
├── src/                # optional: reusable preprocessing functions
├── README.md           # project overview (you’re reading it)
└── requirements.txt    # package dependencies

Requirements & setup
Install the required Python packages using pip:
pip install -r requirements.txt
Place the raw dataset into a data/ folder, then open notebooks/analysis.ipynb in Jupyter Notebook or JupyterLab and run the cells in order. All output files and figures will be saved into the appropriate sub‑folders.

License
This project is provided for educational purposes. The underlying crime dataset is licensed by the City of Los Angeles under public‑domain terms. Please cite appropriately if you build upon this work.
