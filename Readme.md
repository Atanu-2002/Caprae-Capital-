# AI Lead Enhancement Tool: Lead Scoring & Duplicate Detection

---

## Project Overview

This project is a prototype developed as part of the Caprae Capital AI-Readiness Pre-Screening Challenge. It aims to enhance a typical lead generation scraping tool, such as `saasquatchleads.com`, by implementing two crucial features: **Automated Duplicate Lead Detection** and **Machine Learning-Powered Lead Scoring/Prioritization**.

The goal is to demonstrate how AI and machine learning can transform raw, unorganized lead data into actionable insights, enabling sales and business development teams to operate more efficiently and effectively.

---

## Features

This prototype includes the following key features:

1.  **Sample Data Generation**: Creates a synthetic dataset that simulates typical scraped lead data, including intentional duplicates and varying lead "qualities."

2.  **Duplicate Lead Detection**:
    * Utilizes **fuzzy string matching** (`fuzzywuzzy`) on company names and websites to identify similar, near-duplicate entries that might result from different scraping sources or minor data entry variations.
    * Marks and effectively de-duplicates the lead list, providing a cleaner, more accurate dataset for outreach.

3.  **Lead Scoring/Prioritization**:
    * Applies a **Logistic Regression machine learning model** to assign a numerical "Lead Score" to each unique lead.
    * The model is trained on **heuristic rules** (e.g., industry, employee count, job title of contact) to simulate what a "good" or "high-potential" lead would look like for a firm like Caprae Capital.
    * Allows leads to be sorted by their score, enabling prioritization of sales and M&A outreach efforts.

---

## How It Works (Technical Overview)

1.  **Data Simulation**: A Pandas DataFrame is programmatically created and saved as `sample_leads.csv`, serving as the input for the enhancement process.

2.  **Data Loading**: The `sample_leads.csv` is loaded into a Pandas DataFrame.

3.  **Preprocessing**: Company names and websites are standardized using regular expressions for robust fuzzy matching.

4.  **Duplicate Identification**: A custom function leverages `fuzzywuzzy.fuzz.token_sort_ratio` to compare pairs of leads and identify groups of duplicates based on a similarity threshold.

5.  **De-duplication**: The DataFrame is filtered to retain only unique leads, effectively removing the marked duplicates.

6.  **Heuristic Labeling**: For the purpose of demonstration and due to the absence of real historical conversion data, a heuristic function assigns a binary `is_good_lead` label (0 or 1) to each de-duplicated entry based on predefined business rules. This acts as the target variable for the ML model.

7.  **Feature Engineering**: Relevant columns (`Industry`, `Employee Count`, `Revenue`, `Job Title`) are selected. Categorical features like `Industry` are one-hot encoded, and a boolean feature `is_decision_maker` is extracted from `Job Title`.

8.  **Model Training**: A `LogisticRegression` model from `scikit-learn` is trained on the prepared features and the heuristic `is_good_lead` labels.

9.  **Lead Scoring**: The trained model predicts the probability of each lead being a "good lead," and this probability is assigned as the `Lead_Score`.

10. **Output**: The final de-duplicated and scored lead list is displayed, sorted by `Lead_Score`, demonstrating the immediate business utility.

---

## Setup and Installation (Google Colab)

This project is designed to run seamlessly in **Google Colab**.

1.  **Open Google Colab**: Go to [colab.research.google.com](https://colab.research.google.com/) and click on "New notebook."

2.  **Copy Code**: Copy the entire Python code from the provided `.ipynb` notebook file into the first cell of your new Colab notebook.

3.  **Run Cells**: Execute the cells sequentially. The first cell will handle all necessary package installations.

### Dependencies

The script automatically installs the required libraries:

* `pandas`: For data manipulation and analysis.
* `scikit-learn`: For machine learning models (Logistic Regression, `train_test_split`).
* `fuzzywuzzy`: For fuzzy string matching (requires `python-Levenshtein` for speed).
* `python-Levenshtein`: For faster Levenshtein distance calculations used by `fuzzywuzzy`.

---

## Running the Code

1.  **Execute the first cell** in your Colab notebook. This will install dependencies and import libraries.

2.  **Continue running each subsequent cell** in the notebook.
    * The notebook will first generate `sample_leads.csv`.
    * Then, it will load this data.
    * It will perform duplicate detection and print the identified duplicate groups.
    * Next, it will apply the heuristic labeling and train the lead scoring model.
    * Finally, it will display the de-duplicated and prioritized list of leads.

---

## Output Demonstration

The final output will show:

* The initial sample dataset created.
* A report on the number of duplicate groups found and the reduction in lead count after de-duplication.
* The `deduplicated_leads_df` showing the cleaner dataset.
* A summary of the heuristic labels assigned to leads.
* The top 10 leads from the de-duplicated list, sorted by their calculated `Lead_Score` in descending order, showcasing the prioritization capability.

---

## Business Value & Alignment with Caprae Capital

This prototype directly addresses critical challenges in lead generation for businesses and aligns with Caprae Capital's vision:

* **Improved Efficiency**: By automating duplicate detection, sales teams save valuable time that would otherwise be spent manually cleaning lead lists.
* **Enhanced Focus & Conversion**: Lead scoring allows teams to prioritize outreach to the most promising prospects, leading to higher conversion rates and more effective resource allocation.
* **Data Quality**: De-duplication contributes to a cleaner, more reliable lead database, reducing wasted effort and improving overall CRM health.
* **Actionable Insights**: The project transforms raw data into actionable intelligence, showcasing how AI can move beyond simple scraping to drive strategic decision-making. This directly supports Caprae Capital's "M&A as a Service" model by helping identify high-value acquisition targets more effectively.
* **Scalability**: The modular approach demonstrates how these ML-powered enhancements can be integrated into existing lead generation workflows to handle larger volumes of data more intelligently.
