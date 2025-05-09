## Model Prediction Task II


---

### Purpose

The goal of building an in-house predictive model is to enable tailored, cost-effective, and efficient decision-making. For example, predicting HDB resale prices helps inform public policy, housing supply planning, or citizen advisory services.

---

###  Key Considerations

#### 1. **Data Availability & Quality**
- **Structured Data**: We assume access to structured CSV files with features like `flat_type`, `town`, `lease_commence_date`, etc.
- **Data Cleaning**: Handle missing fields (`storey_range`, `remaining_lease`) and standardize formats (`month`, categorical labels).
- **Assumption**: All historical resale transaction data is collected and consistently formatted.

#### 2. **Model Objective**
- Define the use case clearly: In this example, the goal is to **predict resale prices** based on features such as location, flat attributes, and lease remaining.

#### 3. **Feature Engineering**
- Derived variables like:
  - `storey_avg` from `storey_range`
  - `remaining_lease_years` from textual `remaining_lease`
  - Categorical encodings for `town`, `flat_type`, `flat_model`
- Additional external data (e.g. MRT proximity, amenities) could enhance predictions.

#### 4. **Model Selection**
- **Random Forest Regressor** is used due to:
  - Good performance on tabular data
  - Handles nonlinear relationships well
  - Doesn't require GPU
- Simpler models (e.g. Linear Regression) may be used for speed; complex ones (e.g. XGBoost) for accuracy.

#### 5. **Infrastructure & Tooling**
- Assumed setup does **not** use GPUs.
- Deployment can be local (e.g. scheduled Python script), containerized (e.g. Docker), or exposed via API.
- Tooling stack includes `pandas`, `scikit-learn`, `matplotlib`, `seaborn`.

#### 6. **Interpretability**
- Important for stakeholders to trust and use the model.
- Techniques include:
  - Feature importances
  - SHAP values
  - Visualizations (e.g. Partial Dependence Plots)

#### 7. **Governance & Ethics**
- Avoid bias against certain towns or flat types.
- Transparency in how the model is trained, updated, and used.
- Document assumptions and limitations clearly.

#### 8. **Monitoring & Maintenance**
- Regular evaluation to detect model drift (e.g., policy changes, market fluctuations).
- Periodic retraining (e.g. every quarter).
- Track performance metrics: MAE, RMSE, R², and others.

---

###  Assumptions
- Access to full HDB resale transaction data from a reliable source (e.g., data.gov.sg).
- Model is used internally by government analysts, planners, or digital services.
- Model deployment is CPU-based, with minimal infrastructure needs.

---

###  Application: HDB Example

Using the HDB resale dataset:
- Trained model predicts `resale_price` using engineered features.
- Insights generated:
  - Towns with highest median resale prices
  - Price impact of lease remaining
  - Growth trends across years

These findings help guide housing policy, pricing strategy, and citizen engagement.

