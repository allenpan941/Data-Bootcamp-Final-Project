# Quarter-Level Profit Prediction for Delta Airline Using Macroeconomic Indicators

**Authors:** Zilin Pan, Billy Zhang  
**Study Period:** 2003 – 2025

---

## 1. Introduction

### Overview
This study analyzes a comprehensive dataset spanning from 2003 to 2025, integrating internal airline operational metrics—such as `Total_Passengers`, `Total_Fuel_Cost`, and `Delay`—with external macroeconomic indicators including `GDP_Growth` and `Oil_Price`. The data was standardized to a quarterly frequency using a `PeriodIndex` to ensure temporal consistency for time-series modeling.

### Predictive Task
The primary objective is to forecast **Total_Profit**. By employing multivariate time-series modeling, this research investigates how exogenous variables influence airline profitability and captures the seasonality and inertia of profit fluctuations through historical look-back windows.

### Summary Findings
* **Strongest Predictors:** Oil Prices and GDP Growth are the most significant drivers of profitability.
* **Model Characteristics:** The optimized model exhibits a "short-term memory" characteristic, with an optimal `window_length` of 2 quarters, suggesting that aviation profits are highly sensitive to immediate environmental shifts.

---

## 2. Data Description & Processing

### 2.1 Internal Operational Metrics
Data was aggregated from multiple sources, including BTS (Bureau of Transportation Statistics) web scraping:
* **Passenger Volume:** Aggregated from monthly data into quarterly `Total_Passengers`.
* **Fuel Costs:** Extracted from BTS fuel tables using `pd.read_html` and aggregated into `Total_Fuel_Cost`.
* **Operational Delays:** Statistical count of quarterly delay incidents.
* **Load Factor:** Measuring the efficiency of seat utilization across the fleet.

### 2.2 Macroeconomic Indicators
External data was fetched via the **FRED (Federal Reserve Economic Data) API**:
* **GDP Growth:** Reflecting the overall health of the economy and travel demand.
* **Oil Price:** A primary driver of operational expenditure and fuel cost volatility.

---

## 3. Modeling Approach

### 3.1 Feature Engineering
The model incorporates historical dependencies using a specialized technical pipeline:
* **Standardization:** `StandardScaler` to ensure all features are on a comparable scale.
* **Polynomial Expansion:** `PolynomialFeatures` to capture complex, non-linear interactions between economic indicators and operational costs.

### 3.2 Machine Learning Framework
As implemented in the `code.ipynb`, the study utilizes:
* **Primary Model:** `RandomForestRegressor`.
* **Optimization:** `GridSearchCV` for hyperparameter tuning (optimizing `n_estimators`, `max_depth`, etc.).
* **Architecture:** Scikit-Learn `Pipeline` to automate data transformation and prevent data leakage during training.

---

## 4. Results and Analysis

The research demonstrates that external economic conditions provide substantial predictive power beyond historical profit data alone:
1.  **Fuel Sensitivity:** Oil price fluctuations have a nearly immediate and significant impact on quarterly profit margins.
2.  **Economic Correlation:** GDP fluctuations serve as a robust leading indicator for passenger demand and premium travel volume.
3.  **Model Performance:** The Random Forest approach successfully captured the cyclicality and volatility inherent in the aviation sector.

---

## 5. Conclusion and Next Steps

### Conclusion
This framework confirms that tree-based ensemble methods are highly suitable for capturing the non-linear relationships in industries characterized by cyclical demand and cost volatility.

### Future Improvements
* **Lagged Variables:** Incorporating lagged oil-price variables to better capture delayed effects arising from fuel hedging contracts.
* **Efficiency Metrics:** Introducing "Profit per Available Seat Mile" (CASM/RASM) to control for airline scale expansion.
* **Scenario Analysis:** Developing stress-testing tools for extreme market conditions, such as sudden oil price spikes or recessionary demand collapses.


