# 📦 Pricing Optimisation & Sales Forecasting
### Supporting Market Entry Strategy with Data-Driven Pricing Decisions

---

## 📌 Project Overview

This project was developed as part of a case study for **Storio Group's new market entry strategy**, with the goal of building a data-driven pricing and promotional framework to achieve **10% market share within 3 years**.

The analysis is split into two topics:

| Topic | Goal | Method |
|---|---|---|
| **Topic 1** | Find the optimal product price to maximise revenue | Log-Log OLS Regression |
| **Topic 2** | Forecast sales volume for September 2021 | SARIMA Time Series Model |

---

## 🔑 Key Results

### Topic 1 — Pricing Optimisation
- **Optimal Price: €47.34** — derived from demand elasticity modelling
- **Price Elasticity of Demand: -2.12** — demand is elastic; a 1% price increase reduces volume by ~2.12%
- **Model R² = 0.955** — the model explains 95.5% of variation in sales volume
- **Recommendation:** Test the optimal price point via A/B experiment; re-estimate elasticity periodically as market conditions shift

### Topic 2 — Sales Volume Forecasting
- **September 2021 Forecast: 53,196 units**
- **95% Confidence Interval: [33,846 – 72,545 units]**
- Forecast aligns closely with September 2020 actuals (~54,645 units), validating model reliability
- Identified strong yearly seasonality: peaks in Nov/Dec (~70,000 units), lows in Jul/Aug (~40,000–50,000 units)

---

## 🗂️ Repository Structure

```
├── Pricing_analysis_Topic_1_Final.ipynb   # OLS regression for optimal pricing
├── TimeSeriesForecasting_Topic2_Final.ipynb  # SARIMA forecasting model
├── Case_Study_Presentation.pdf            # Executive summary slide deck
├── question1_dataset.csv                  # Pricing dataset (price, volume, visitors)
├── question3_dataset.csv                  # Daily sales volume (Jan 2016 – Aug 2021)
└── README.md
```

---

## 🛠️ Methods & Tools

### Topic 1 — Log-Log OLS Regression (Demand Elasticity)

**Why Log-Log?**
The relationship between price and volume is non-linear. Taking the natural log of both variables linearises the relationship and allows the regression coefficient to be interpreted directly as price elasticity.

**Model:**
```
ln(Volume) = β₀ + β₁·ln(Price) + β₂·ln(Visitors) + ε
```

**Model Validation:**
- Residuals vs. Fitted plot — checked for homoskedasticity
- Breusch-Pagan test — confirmed constant variance (p > 0.05)
- VIF check — confirmed no multicollinearity between predictors
- Actual vs. Predicted plot — confirmed strong model fit

**Optimal Price Formula:**
```
p* = Marginal Cost / (1 + 1/Price Elasticity)
p* = 25 / (1 + 1/(-2.12)) = €47.34
```

---

### Topic 2 — SARIMA Time Series Forecasting

**Why SARIMA over ARIMA?**
Seasonal decomposition of the daily data revealed a strong yearly seasonality pattern. SARIMA captures both the overall trend and recurring seasonal cycles, producing more accurate forecasts than standard ARIMA.

**Steps:**
1. Aggregated daily data to monthly sums — reduces noise, aligns with monthly forecast target
2. Seasonal decomposition (additive, period=12) — confirmed trend + yearly seasonality
3. Stationarity check — ADF test (p = 0.98) confirmed non-stationary; applied differencing
4. ACF / PACF analysis — identified AR and seasonal MA components
5. `auto_arima` parameter selection — optimised based on lowest AIC
6. Final model: **SARIMA(1,1,0)(0,1,1,12)**
7. Forecast: 1-step ahead (September 2021)

---

## 📚 Libraries Used

```python
pandas
numpy
matplotlib
statsmodels          # OLS regression, SARIMAX, seasonal decompose, ADF test
pmdarima             # auto_arima for SARIMA parameter selection
scipy
```

---

## 💡 Strategic Recommendations

Based on the analysis, a **3-phase pricing glidepath** was recommended for Storio's market entry:

**Phase 1 — Year 1: Entry & Disruption**
- Penetration pricing 10–20% below competitors
- A/B test multiple price points early to build elasticity data
- KPIs: Customer Acquisition Cost (CAC), conversion rate

**Phase 2 — Year 2: Scaling & Value Demonstration**
- Shift to tiered "Good-Better-Best" pricing structure
- Use Year 1 elasticity models to refine pricing scenarios dynamically
- KPIs: ARPU, upsell rate, Customer Lifetime Value (LTV)

**Phase 3 — Year 3: Optimisation & Profitability**
- Transition to value-based pricing with segmentation by customer type
- Reduce reliance on discounting; introduce loyalty-led promotions
- KPIs: Gross margin %, Net Revenue Retention (NRR), market share

---

## ▶️ How to Run

1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/pricing-demand-forecasting.git
cd pricing-demand-forecasting
```

2. Install dependencies
```bash
pip install pandas numpy matplotlib statsmodels pmdarima
```

3. Run the notebooks in order:
   - `Pricing_analysis_Topic_1_Final.ipynb`
   - `TimeSeriesForecasting_Topic2_Final.ipynb`

---

## 👤 Author

**Rupinder Kaur**
Data Analyst | Rotterdam, Netherlands
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/kaur-rupinder/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:rupinderkaur.nl@gmail.com)
