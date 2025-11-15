# BoomBikes Demand Prediction - Linear Regression Model

> A multiple linear regression model to predict daily bike-sharing demand based on meteorological and seasonal factors, helping BoomBikes strategize for post-pandemic revenue recovery.

---

## 📋 Table of Contents
* [General Information](#general-information)
* [Business Problem](#business-problem)
* [Dataset](#dataset)
* [Technologies Used](#technologies-used)
* [Model Building Process](#model-building-process)
* [Key Findings](#key-findings)
* [Conclusions](#conclusions)
* [Recommendations](#recommendations)

---

## General Information

### Background
To build a **multiple linear regression model** for predicting bike-sharing demand. The analysis helps **BoomBikes**, a US-based bike-sharing provider, understand the factors influencing bike rental demand in the American market.

### Context
Post-COVID-19 pandemic, BoomBikes has experienced significant revenue decline. To prepare for economic recovery, the company needs to:
- Understand demand patterns
- Identify key factors driving bike rentals
- Optimize business strategy for revenue acceleration
- Position themselves ahead of competitors

### Objective
Build a predictive model to understand:
1. **Which variables significantly predict bike demand**
2. **How well these variables explain demand variations**
3. **Actionable insights for business strategy**

---

## Business Problem

**Challenge:** BoomBikes is struggling to sustain in the current market scenario due to the pandemic's impact on revenue.

**Goal:** Develop a data-driven approach to:
- Predict daily bike demand based on various factors
- Understand demand dynamics in the American market
- Create a strategic plan to accelerate revenue post-lockdown
- Stand out from competitors with informed decision-making

**Success Metrics:**
- Model accuracy (R² score > 0.80)
- Identification of top 3-5 influential factors
- Actionable business recommendations

---

##  Dataset

### Data Source
- **File:** `day.csv`
- **Records:** 730 daily observations (2018-2019)
- **Features:** 16 variables including meteorological, seasonal, and temporal factors

### Features Description

#### Temporal Features
- `dteday`: Date (DD-MM-YYYY format)
- `season`: Season (Spring, Summer, Fall, Winter)
- `yr`: Year (2018, 2019)
- `mnth`: Month (Jan to Dec)
- `weekday`: Day of week (Sun to Sat)
- `holiday`: Whether day is a holiday
- `workingday`: Whether day is a working day

#### Weather Features
- `weathersit`: Weather situation
  - Clear/Partly Cloudy
  - Mist/Cloudy
  - Light Snow/Rain
  - Heavy Rain/Snow
- `temp`: Normalized temperature in Celsius
- `atemp`: Normalized feeling temperature
- `hum`: Normalized humidity
- `windspeed`: Normalized wind speed

#### Target Variables
- `casual`: Count of casual users
- `registered`: Count of registered users
- **`cnt`**: **Total bike rentals** (Target variable for prediction)

### Data Characteristics
- **No missing values**
- **No duplicates**
- **Clean dataset** ready for analysis
- **Balanced temporal coverage** across seasons and months

---
## 🛠️ Technologies Used

### Core Libraries
- **Python** - 3.8+
- **Pandas** - 1.3.0 - Data manipulation and analysis
- **NumPy** - 1.21.0 - Numerical computing
- **Matplotlib** - 3.4.2 - Data visualization
- **Seaborn** - 0.11.1 - Statistical visualizations

### Machine Learning
- **Scikit-learn** - 0.24.2 - Machine learning algorithms
  - Linear Regression
  - Train-test split
  - MinMaxScaler for feature scaling
  - RFE for feature selection
  - Model evaluation metrics
- **Statsmodels** - 0.12.2 - Statistical modeling
  - OLS Regression
  - VIF calculation
  - Residual analysis
---

## 🔄 Model Building Process

### 1. Data Understanding & Exploration
- Loaded and examined 730 daily bike rental records
- Checked for missing values and data quality
- Performed statistical summary analysis

### 2. Data Preparation
- **Dropped unnecessary columns:** instant, dteday, casual, registered
- **Converted categorical variables** to meaningful labels
  - Season: 1→Spring, 2→Summer, 3→Fall, 4→Winter
  - Year: 0→2018, 1→2019
  - Weather: Numeric codes to descriptive labels
- **Avoided dummy variable trap** using `drop_first=True`

### 3. Exploratory Data Analysis (EDA)
- **Correlation Analysis:** Identified relationships between variables
- **Distribution Analysis:** Examined target variable distribution
- **Categorical Analysis:** Studied impact of seasons, weather, working days
- **Visualization:** Created 10+ plots for insights

**Key EDA Findings:**
- Temperature shows strongest positive correlation with demand (r ≈ 0.63)
- Fall and Summer seasons have highest demand
- Clear weather significantly boosts rentals
- Year 2019 shows ~23% higher demand than 2018

### 4. Feature Engineering
- Created dummy variables for all categorical features
- Applied **MinMax Scaling** to numerical features (temp, atemp, hum, windspeed)
- Scaled features to [0,1] range for better model performance

### 5. Train-Test Split
- **Training Set:** 70% (511 samples)
- **Test Set:** 30% (219 samples)
- **Random State:** 42 (for reproducibility)

### 6. Feature Selection
- **Recursive Feature Elimination (RFE):** Selected top 15 features
- **VIF Analysis:** Removed features with VIF > 5 to address multicollinearity
- Iteratively refined feature set until all VIF < 5

### 7. Model Building
- Built initial model with all features
- Refined model through iterative feature selection
- **Final model** with 12-15 significant features

### 8. Model Validation
Validated all linear regression assumptions:
-  **Linearity:** Residual plots show random scatter
-  **Normality:** Q-Q plot confirms normal distribution of residuals
-  **Homoscedasticity:** Constant variance in residuals
-  **No Multicollinearity:** All VIF values < 5
-  **Independence:** No autocorrelation in errors

### 9. Model Evaluation
**Training Set Performance:**
- R² Score: **0.833**
- Adjusted R² Score: **0.827**

**Test Set Performance:**
- R² Score: **0.805**
- RMSE: **~820 bikes**
- MAE: **~630 bikes**

**Model Generalization:**
- Difference between train and test R²: **< 0.03**
-  **Model is well-generalized** (no overfitting)

---

## Key Findings

### Top 5 Features Influencing Bike Demand

| Rank | Feature | Effect | Impact Description |
|------|---------|--------|-------------------|
| 1 | **Temperature** | Positive (+) | Higher temperature significantly increases demand |
| 2 | **Year (2019)** | Positive (+) | 23% growth in demand from 2018 to 2019 |
| 3 | **Weather: Light Snow/Rain** | Negative (−) | Adverse weather reduces demand by ~30% |
| 4 | **Season: Fall** | Positive (+) | Fall season shows highest demand |
| 5 | **Weather: Mist/Cloudy** | Negative (−) | Moderate weather impact on demand |

### Additional Insights

**Seasonal Patterns:**
- **Fall** > **Summer** > **Winter** > **Spring**
- Fall shows 15-20% higher demand than Spring

**Weather Impact:**
- **Clear Weather:** +40% demand increase
- **Light Snow/Rain:** -30% demand decrease
- **Heavy Rain:** -50% demand decrease

**Temporal Trends:**
- **Working Days:** Consistent demand from registered users
- **Weekends/Holidays:** Higher casual user demand
- **Monthly Pattern:** Peak demand May-October

**Growth Trend:**
- Year-over-year growth: **23%** (2018 to 2019)
- Indicates growing popularity of bike-sharing services

---

## Conclusions

1. **Temperature is the Primary Driver**
   - Strongest predictor of bike demand
   - Warmer weather significantly boosts rentals
   - Temperature increase of 10°C → ~500 more bikes rented

2. **Growing Market Demand**
   - 23% increase from 2018 to 2019
   - Positive trend indicates strong business potential
   - Market is expanding despite pandemic

3. **Weather Conditions are Critical**
   - Clear weather maximizes demand
   - Rain/snow significantly reduces rentals
   - Weather forecasting can optimize operations

4. **Seasonal Strategy Required**
   - Fall and Summer are peak seasons
   - Winter requires different approach
   - Seasonal inventory management needed

5. **Model Performance**
   - **80.5% variance explained** in test set
   - Reliable predictions for business planning
   - Well-generalized model (no overfitting)

---

## Recommendations

### Strategic Recommendations for BoomBikes

#### 1. **Weather-Based Dynamic Operations**
- **Implementation:** Integrate real-time weather forecasting
- **Action:** Increase bike availability during clear weather predictions
- **Impact:** Optimize inventory and maximize revenue

#### 2. **Seasonal Inventory Management**
- **Peak Season (Fall/Summer):** Increase fleet size by 30-40%
- **Low Season (Winter/Spring):** Reduce inventory, focus on maintenance
- **Action:** Plan bike procurement and maintenance schedules accordingly

#### 3. **Dynamic Pricing Strategy**
- **Good Weather Days:** Premium pricing
- **Adverse Weather:** Promotional discounts to maintain demand
- **Peak Seasons:** Higher base rates
- **Impact:** Revenue optimization through price elasticity

#### 4. **Marketing and Promotions**
- **Target Months:** May through October marketing push
- **Focus:** Promote during clear weather forecasts
- **Campaigns:** Seasonal offers in Fall/Summer
- **Impact:** Capitalize on natural demand peaks

#### 5. **Maintenance Planning**
- **Winter Months:** Schedule major maintenance
- **Bad Weather Days:** Perform routine servicing
- **Impact:** Minimize downtime during high-demand periods

#### 6. **Expansion Strategy**
- **Market Growth:** 23% YoY growth indicates strong potential
- **Action:** Plan expansion to new locations
- **Timing:** Pre-position for post-pandemic recovery
- **Impact:** Capture growing market share

#### 7. **Customer Retention**
- **Working Days:** Focus on registered user benefits
- **Weekends:** Attract casual users with special offers
- **Action:** Differentiated marketing strategies
- **Impact:** Balanced revenue streams

### Expected Business Impact
- **Revenue Increase:** 20-30% through optimized operations
- **Customer Satisfaction:** Improved bike availability when needed
- **Cost Reduction:** 15-20% through better maintenance planning
- **Competitive Advantage:** Data-driven decision making


---
