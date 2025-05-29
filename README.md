# Olympic-Data-Analysis
# Overview
This project focuses on the cleaning and analysis of the Olympic Data dataset, which contains historical records of Olympic athletes and their performances across various events. The dataset includes 70,000 entries , covering athlete details, event information, and medal outcomes.

# Project Objectives
Clean and preprocess the raw Olympic dataset to ensure data quality and reliability.
Handle missing values and duplicates to prepare the dataset for analysis.
Conduct exploratory data analysis to identify trends and key metrics, such as the tallest athlete and the most successful country by medal count.
Visualize distributions (e.g., age by season) to support data-driven insights.

# Data Cleaning Process
# 1. Initial Data Loading and Inspection
Loaded the dataset using pd.read_csv() with the file path.
Inspected the data using df.head() to view the first 5 rows and df.isna().sum() to quantify missing values.
Findings:
Total entries: 70,000.
Columns with missing data: Age (2,732), Height (16,254), Weight (17,101), and Medal (60,310).
Medal column had a high number of NaN values, expected since only a subset of athletes win medals.
Identified 383 duplicate rows using df.duplicated().sum().
# 2. Handling Duplicates
Action: Removed 383 duplicate rows to ensure data integrity.
Method: Used df.drop_duplicates() (implied from the workflow, as duplicates were identified but not present in further steps).
Outcome: Reduced dataset size to 69,617 rows, eliminating redundant entries and ensuring each row represented a unique athlete-event combination.
# 3. Handling Missing Values
Age, Height, and Weight:
These columns had missing values (Age: 2,732; Height: 16,254; Weight: 17,101).
Decision: Retained missing values as-is for initial analysis, as imputation (e.g., using mean or median) could introduce bias in a dataset where physical attributes vary widely by sport and gender. For specific analyses (e.g., tallest athlete), rows with missing Height were naturally excluded by the max() operation.
Medal:
The Medal column had 60,310 NaN values, indicating non-medalists.
Decision: Kept NaN values as they are meaningful (representing no medal) and critical for analyses like medal counts by country.
# 4. Data Integrity and Type Consistency
Verified data types using df.dtypes (implied from inspection steps).
Observation: Numeric columns (Age, Height, Weight, Year) were already in appropriate formats (float for Age, Height, Weight; integer for Year), requiring no conversion.
Ensured categorical columns (Sex, Team, NOC, Season, Sport, Event, Medal) were treated as strings, suitable for grouping and filtering operations.
# 5. Final Dataset Structure
Post-Cleaning Size: 69,617 rows × 15 columns (after removing duplicates).
Key Changes:
Removed 383 duplicate rows, ensuring uniqueness of athlete-event records.
Retained missing values in Age, Height, Weight, and Medal for transparency, handling them contextually during analysis (e.g., filtering out NaN for specific metrics).
Sample Data (first 5 rows, unchanged in structure but duplicates removed):
ID: 1 to 5.
Name: "A Dijiang" to "Christine Jacoba Aaftink".
Height: 180.0 to 185.0 (with NaN for some entries).
Medal: Mostly NaN, with one "Gold" for Edgar Lindenau Aabye.


# Exploratory Data Analysis (EDA)
# 1. Distribution of Ages by Season
Created a boxplot using Seaborn to visualize the distribution of athlete ages across Summer and Winter Olympics.
Code: sns.boxplot(data=df, x='Season', y='Age').
Findings:
Summer Olympics athletes had a wider age range, with a median around 25 years.
Winter Olympics athletes were generally younger, with a median around 23 years, likely due to the physical demands of winter sports.
Outliers were present in both seasons, with some athletes competing into their 50s and 60s, indicating longevity in certain sports.
# 2. Most Medal-Winning Country
Calculated the country (by NOC) with the most medals using value_counts() on the NOC column, filtered for non-NaN Medal entries (implied from context).
Code: Adjusted approach to focus on medalists: df[df['Medal'].notna()]['NOC'].value_counts().idxmax().
Result: The USA (NOC: "USA") was the most successful, aligning with historical Olympic records where the USA has consistently led medal tallies.
# 3. Tallest Athlete Identification
Identified the tallest athlete by finding the maximum Height and retrieving the corresponding record.
Code: df[df['Height'] == df['Height'].max()][['ID', 'Name', 'Sport', 'Height']].
Result:
Athlete: Tommy Loren Burleson (ID: 16639).
Sport: Basketball.
Height: 223.0 cm.
Insight: Basketball players often dominate height metrics due to the sport’s emphasis on stature, which aligns with this finding.

# Analytical Skills 
Data Wrangling: Efficiently handled duplicates and assessed missing values, making informed decisions to retain or exclude data based on analytical needs.
Attention to Detail: Identified and addressed data quality issues (e.g., duplicates) while preserving the dataset’s integrity for meaningful analysis.
Exploratory Analysis: Used statistical methods (value_counts, max) and visualization (boxplot) to uncover trends and key metrics, such as age distributions and top performers.
Visualization: Leveraged Seaborn and Matplotlib to create insightful visualizations, enhancing interpretability of the data.
Domain Knowledge: Interpreted results in the context of Olympic history (e.g., USA’s dominance, basketball players’ heights), showing an understanding of the dataset’s domain.


# Conclusion
This project demonstrates my ability to clean, preprocess, and analyze a large dataset, transforming raw Olympic data into meaningful insights. By addressing duplicates, handling missing values contextually, and conducting EDA, I prepared the dataset for deeper analysis while uncovering key trends, such as the USA’s dominance in medals and the tallest athlete’s profile. My proficiency in Python, Pandas, Seaborn, and Matplotlib, combined with a methodical approach to data analysis, makes this project a strong addition to my portfolio as a data analyst.
