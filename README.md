# Startup_Health_scoring_model_project
##  Dataset Features

| Column Name              | Description                                      |
|--------------------------|--------------------------------------------------|
|   startup_id             | Unique ID of the startup                         |
|  team_experience         | Avg years of experience (scale 1–10)             |
|  market_size_million_usd | Addressable market size in million USD           |
|  monthly_active_users    | Current monthly active users                     |
|  monthly_burn_rate_inr   | Monthly expenses in INR (lower = better)         |
|  funds_raised_inr        | Total funding raised so far                      |
|  valuation_inr           | Current valuation in INR                         |


##  Methodology

###  1. Simple Version (Manual Weight-Based Scoring)

- Applied **Min-Max Normalization** to all features:
- Higher is better: market size, users, valuation, etc.
- Lower is better: burn rate (inverted after normalization)
- Assigned manual weights to each feature:

| Feature                  | Weight |
|--------------------------|--------|
|   team_experience        | 10.6%  |
|  market_size_million_usd | 30.9%  |
|  monthly_active_users    | 24.0%  |
|  monthly_burn_rate_inr   | 17.2%  |
|  funds_raised_inr        | 17.4%  |

- Final score = weighted sum of normalized values (scaled to 100)

###  2. Optional ML Enhancement (Random Forest + Clustering)

- Trained a **Random Forest Regressor** to predict `valuation_inr` from features.
- Extracted **feature importances** as data-driven weights:

| Feature                  | ML-Derived Weight|
|--------------------------|------------------|
|  market_size_million_usd | 30.8%            |
|  monthly_active_users    | 23.4%            |
|  funds_raised_inr        | 17.9%            |
|  monthly_burn_rate_inr   | 17.4%            |
|  team_experience         | 10.8%            |

- Compared these with manual weights (found good alignment).
- Recalculated scores using ML-derived weights.
- Applied **KMeans Clustering** to group similar startups (e.g., high-growth, high-burn, low-traction types).

##  Visualizations

| Chart                     | Description                           |
|---------------------------|---------------------------------------|
| Score Distribution        | Histogram of startup scores           |
| Correlation Heatmap       | Correlation between features          |
| Ranked Score Barplot      | Visual of all startups sorted by score|
| Manual vs ML Weights      | Bar chart comparing both approaches   |

##  Results

###  Top 3 Startups
| Startup ID | Score |
|------------|-------|
| S006       | 79.15 |
| S045       | 76.43 |
| S077       | 76.39 |

###  Bottom 3 Startups
| Startup ID | Score |
|------------|-------|
| S084       | 25.84 |
| S023       | 24.23 |
| S055       | 19.17 |


##  Key Insights

- **Market Size** and **User Traction** are the most important indicators for valuation.
- **High Burn Rate** penalizes a startup even if funding is strong.
- Manual and ML-derived weights were closely aligned, validating the initial logic.
- **Clustering** helped identify startup personas for investor strategies.

##  Future Work

- Add **time-based features** (growth rate, CAC, LTV)
- Use **XGBoost** or **SHAP** for interpretability
- Add a classification model to predict success/failure
- Deploy as a **scoring web app** (e.g., Streamlit)

##  Tech Stack

- Python (Pandas, scikit-learn, seaborn, matplotlib)
- Jupyter Notebook
- GitHub (version control)

##  Contact

Made with  by **Alok Upadhyay**  
