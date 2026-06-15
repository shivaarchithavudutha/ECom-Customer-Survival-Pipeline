# ECom-Customer-Survival-Pipeline
An end-to-end customer survival engine and behavioral analysis pipeline designed to optimize conversion funnels and predict e-commerce churn.

## Phase 1: Advanced Business Diagnostics (What Happened?)

### Funnel Conversion Bottlenecks
Our tracking engine exposed a critical vulnerability at the checkout phase, featuring a platform-wide **66.71% cart-to-purchase drop-off rate**. Deep segmentation isolated the absolute worst-performing inventories:
* **Books:** 69.08% cart abandonment
* **Pet Supplies:** 67.99% cart abandonment
* **Clothing:** 67.95% cart abandonment

### Demographic Risk Distributions
While the checkout drop-off remained systemically high across all cohorts (all above 65%), users identifying as **Other** demonstrated the steepest drop-off at **68.06%**. 

### Behavioral Cohorts & RFM Segmentation
Users were anchored into chronological monthly cohorts to evaluate interaction decay. Relational data mapping revealed that **13.65% of all signups** represent window-shoppers who never completed a single transaction, allowing us to isolate a baseline risk group labeled *"Non-Purchasing Signups"*.

---

## Phase 2: Predictive Machine Learning Framework

* **The Architectural Shift:** Standard Random Forest classifiers maxed out at a PR-AUC of 0.52 due to extreme class imbalances. To build a robust, enterprise-ready model, the project was pivoted into a continuous-time **Stratified Cox Proportional Hazards Model** stratified across our custom RFM customer segments.
* **Leakage-Proof Validation:** The processing engine encapsulates all feature scaling, categorical tracking, and imputation layers within a strict scikit-learn preprocessing pipeline, achieving an honest, defensible **Concordance Index (C-Index) of 0.67** with zero data leakage.

---

## Phase 3: Product Strategy & Actionable Engineering

### 3.1 Model Interpretability (The Primary Drivers)
The stratified survival analysis conclusively proved that **`Orders_Per_Tenure_Day`** is the most statistically significant behavioral metric ($p < 0.005$) with an experimental hazard coefficient of **6.46**. This mathematically demonstrates that a customer's purchasing *velocity* relative to their time on the platform dictates their lifespan. If their transaction momentum drops early, their hazard risk spikes exponentially.

### 3.2 Strategic Interventions (The 2-Step Nudge Playbook)
When the survival engine flags an individual user with a **High Hazard Risk Score** who belongs to an **"At-Risk"** RFM segment, the platform triggers an automated, two-tier retention loop:

#### Step 1: The Friction-Reduction UX Nudge
* **Trigger:** The high-risk user adds an item from an underperforming category (Books or Pet Supplies) to their cart.
* **Action:** The application dynamically modifies the cart UI to surface a **1-Click Express Checkout via Saved Payment Methods** paired with urgency micro-copy (*"Items in this category sell out fast. Reserve yours in one click."*). This directly targets the structural cognitive friction causing our 66.71% checkout drop-off.

#### Step 2: The Velocity-Recovery Promotion
* **Trigger:** The high-risk user abandons the cart despite the express checkout nudge.
* **Action:** Within 3 hours, a programmatic webhook fires a personalized, time-decayed incentive via push notification. The system dynamically reads the average item price from our engineered feature layers and issues a value-optimized credit (*"We've saved your cart! Complete your order in the next 24 hours for free shipping + $10 off"*), protecting business margins while artificially forcing the user's transaction velocity back into a healthy pattern.

---

## 🛠️ Tech Stack & Skills Demonstrated
* **Languages & Core Tooling:** Python (Jupyter Notebooks)
* **Data Engineering & Analytics:** Pandas, NumPy
* **Statistical Modeling & Machine Learning:** Lifelines (Cox Proportional Hazards, Stratification), Scikit-Learn (Pipelines, ColumnTransformers, Robust Scalers)
* **Data Visualization:** Matplotlib, Seaborn
* **Domain Frameworks:** RFM Customer Segmentation, Cohort Retention Analysis, Survival Econometrics
