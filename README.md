# Agentic AI-Based Dynamic Tariff Optimization for EV Charging Networks

An AI-driven framework for predicting EV charging demand, estimating congestion, and recommending dynamic electricity tariffs to improve charging-network utilization and revenue.

## Project Overview

This project was developed for the **Open Project 2026 – Society of Business**. It combines demand forecasting, congestion classification, rule-based dynamic pricing, and a monitoring feedback loop to explore how intelligent pricing can improve electric vehicle charging infrastructure management.

The analysis uses two datasets:

* **ACN-Data:** Workplace EV charging sessions from Caltech/JPL.
* **UrbanEV (ST-EVCDP):** High-frequency EV charging data from Shenzhen, with measurements recorded at five-minute intervals.

The datasets are analyzed separately because they represent different locations and temporal scopes.

## System Architecture

### 1. Demand Prediction Agent

Predicts charging demand and estimates congestion levels using machine learning.

Models evaluated:

* Random Forest
* Extra Trees
* Gradient Boosting
* XGBoost
* LightGBM
* Ridge Regression for demand prediction
* Logistic Regression for congestion classification

### 2. Tariff Pricing Agent

Recommends price adjustments based on charging demand and occupancy.

* **High demand and occupancy:** Apply a 15% price increase.
* **Low demand and occupancy:** Apply a 10% discount.
* **Other conditions:** Retain the existing tariff.

The ACN-Data analysis also evaluates a baseline tariff of ₹15/kWh.

### 3. Monitoring and Learning Agent

Evaluates the simulated pricing policy using revenue, utilization, and queue-related metrics. A feedback rule adjusts the surge and discount multipliers when the revenue target is not achieved.

The feedback mechanism is a rule-based, episodic simulation rather than a continuously trained reinforcement-learning system.

## Methodology

1. Data loading and preprocessing
2. Feature engineering and exploratory data analysis
3. Demand regression and congestion classification
4. Dynamic tariff recommendation
5. Revenue and utilization comparison
6. Simulated congestion-response analysis
7. Evaluation summary and CSV export

## Selected Results

Results recorded in the notebook include:

| Metric                                                    |           Result |
| --------------------------------------------------------- | ---------------: |
| Best demand regression model                              |      Extra Trees |
| Demand regression R²                                      |           0.9936 |
| Best congestion classifier                                |      Extra Trees |
| Congestion classification accuracy                        |           99.61% |
| UrbanEV revenue change under the simulated tariff policy  |          +0.222% |
| ACN-Data revenue change under the simulated tariff policy |          +3.588% |
| Simulated average utilization                             | 77.00% to 77.99% |

**Interpretation:** These are notebook-specific evaluation results. The revenue, utilization, and queue-related improvements rely partly on simulation assumptions and should not be interpreted as measured real-world outcomes. The congestion dataset is also heavily imbalanced, so accuracy alone does not establish performance on rare high-congestion cases.

## Technology Stack

* Python
* Pandas and NumPy
* Matplotlib and Seaborn
* Scikit-learn
* XGBoost
* LightGBM
* Jupyter Notebook / Google Colab

## Repository Structure

```text
agentic-ai-ev-tariff-optimization/
├── README.md
├── requirements.txt
└── agentic_ai_ev_tariff_optimization.ipynb
```

## Running the Notebook

1. Clone or download this repository.
2. Install the required Python packages.
3. Obtain the ACN-Data and ST-EVCDP datasets from their respective sources.
4. Configure the dataset and output paths in the notebook.
5. Run the notebook cells in order.

The raw datasets are not included in this repository. The notebook currently uses Google Drive paths, which must be updated to match your environment.

## Assumptions and Limitations

* Charger availability is assumed to be 24 hours per day for ACN-Data.
* Grid procurement cost is modeled using an assumed rate of ₹8/kWh.
* Demand uplift and queue reduction are simulated using predefined pricing-response assumptions.
* The two datasets are analyzed in parallel rather than joined row by row.
* The congestion classes are imbalanced, and high-congestion samples are rare.
* The monitoring agent uses a single-episode feedback simulation.

## Future Scope

* Incorporate time-series forecasting for demand prediction.
* Test pricing policies against real observed customer responses.
* Evaluate fairness and affordability alongside revenue.
* Develop a multi-episode adaptive pricing policy.
* Validate the framework using live charging-network data.

## Author

Chirag Kumar
