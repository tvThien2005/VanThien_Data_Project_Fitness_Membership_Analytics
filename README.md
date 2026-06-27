# 🏋️ Fitness Membership Analytics

A comprehensive data analytics project covering **Exploratory Data Analysis**, **Customer Segmentation (Clustering)**, **Churn Prediction**, and **Geo-Revenue Analysis** on a gym membership dataset of 1,998 members across 10 locations in California.

---

## 📁 Project Structure

```
├── Data/
│   ├── Fitness_Membership_Analytics_Dataset.csv   # Raw dataset
│   └── fitness_cleaned.csv                        # Cleaned dataset (output of EDA)
├── Src/
│   ├── eda.ipynb                                  # Data cleaning & Exploratory Analysis
│   ├── analysis.ipynb                             # In-depth univariate & bivariate analysis
│   ├── analysis_location_for_revenue.ipynb        # Geo-revenue & location growth analysis
│   ├── cluster_models.ipynb                       # K-Means vs Hierarchical Clustering
│   └── gym_churn_model.ipynb                      # Churn Prediction models
├── Output/                                        # Charts, figures, saved models
└── Report/                                        # Power BI dashboard & summary report
```

---

## 📊 Dataset Overview

| Attribute | Detail |
|-----------|--------|
| **Rows** | 1,998 members |
| **Features** | 33 (behavioral + financial + demographic) |
| **Locations** | 10 cities across California |
| **Membership Types** | Basic, Standard, Premium, Elite |

**Key features include:** age, membership type, visit frequency, check-in/check-out time, session duration, personal training hours, group lessons, sauna usage, discount info, subscription price, final price, and gym location (lat/lon).

---

## 🔬 Analysis Modules

### 1. EDA & Data Cleaning (`eda.ipynb`)
- Detected and visualized missing values per column
- Filled missing `discount_type` with `"No Discount"`
- Engineered day-of-week binary columns (Mon–Sun) from the `days_per_week` string field
- Extracted `check_in_hour` from time strings for temporal analysis
- Saved cleaned data to `fitness_cleaned.csv`

### 2. In-Depth Analysis (`analysis.ipynb`)
- Computed **correlation matrix** across all numerical features
- **Univariate analysis**: distributions of age, visit frequency, duration, price, membership type
- **Bivariate analysis**: membership type vs. revenue, check-in hour patterns by card type, tenure analysis
- Custom chart styling with a professional color palette (matplotlib/seaborn)

### 3. Geo-Revenue Analysis (`analysis_location_for_revenue.ipynb`)
- Aggregated **revenue, member count, avg price, visit rate** per city
- Computed **Haversine distance matrix** between all 10 gym locations
- Defined a composite **Growth Score** formula:

```
Growth Score = 0.35 × (avg_price / max) 
             + 0.30 × (avg_visit / max)
             + 0.20 × (1 − members / max)
             + 0.15 × (nearest_km / max)
```

- Identified high-opportunity locations based on pricing power, engagement, market saturation, and geographic isolation

### 4. Customer Clustering (`cluster_models.ipynb`)
- **Features used:** visit frequency, session duration, personal training hours, check-in hour, weekend ratio, final price, discount rate, service usage flags (sauna, group lessons, drink subscription, multi-location access)
- **Feature engineering:** `avg_time_week` (duration × visits), label encoding for categorical fields
- **Dimensionality reduction:** PCA before clustering
- **Algorithms compared:**
  - K-Means (Elbow method + multi-metric selection)
  - Hierarchical Clustering (Ward linkage + Dendrogram)
- **Evaluation metrics:** Silhouette Score, Davies-Bouldin Score, Calinski-Harabasz Score, ARI, NMI

### 5. Churn Prediction (`gym_churn_model.ipynb`)
- **Target:** `churn` (binary label engineered from behavioral signals)
- **Feature engineering:**
  - Join season, join month/year
  - `engagement_volume` = visit_per_week × duration_in_gym_minutes
  - `relative_price` = final_price / subscription_price
  - `weighted_services` (PT ×2, multi-location ×2, others ×1)
  - `discount_amount`, `has_discount`
- **Models trained:** Logistic Regression, Random Forest, XGBoost, CatBoost
- **Validation:** 5-fold Stratified Cross-Validation
- **Tuning:** GridSearchCV with F1-macro scorer
- **Metrics reported:** Accuracy, Precision, Recall, F1-macro, AUC-ROC

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python 3 |
| Data manipulation | pandas, NumPy |
| Visualization | matplotlib, seaborn, Power BI |
| Machine Learning | scikit-learn, XGBoost, CatBoost |
| Clustering | KMeans, AgglomerativeClustering (scipy, sklearn) |
| Dimensionality Reduction | PCA (sklearn) |
| Geo-computation | Haversine formula (math) |
| Environment | Jupyter Notebook, Google Colab, Kaggle |

---

## 📈 Key Insights

- **Revenue concentration:** A small number of locations drive disproportionate total revenue, while isolated cities show high growth-score potential due to lower competition and strong per-member value.
- **Engagement patterns:** Members with higher `engagement_volume` (frequent + long sessions) and more add-on services (PT, multi-location) exhibit significantly lower churn risk.
- **Clustering:** Distinct member segments emerge — budget casual users vs. premium high-engagement members — enabling targeted retention and upsell strategies.
- **Churn drivers:** Discount dependency, low visit frequency, and short session duration are the strongest predictors of churn.

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/tvThien2005/VanThien_Data_Project_Fitness_Membership_Analytics.git
cd VanThien_Data_Project_Fitness_Membership_Analytics

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn xgboost catboost

# Run notebooks in order:
# 1. Src/eda.ipynb
# 2. Src/analysis.ipynb
# 3. Src/analysis_location_for_revenue.ipynb
# 4. Src/cluster_models.ipynb
# 5. Src/gym_churn_model.ipynb
```

---

## 👤 Author

**Truong Van Thien**  
Third-year Computer Science student — Saigon University  
📧 truongthien1334@email.com  
🔗 [github.com/tvThien2005](https://github.com/tvThien2005)
