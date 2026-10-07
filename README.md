# 📊 Financial Market Analysis & Stock Price Drivers

A data analysis and statistical modeling project that explores the financial characteristics of publicly traded companies and investigates which financial indicators are statistically associated with stock prices.

The project combines **Exploratory Data Analysis (EDA), data preprocessing, correlation analysis, hypothesis testing, Pearson correlation, and Ordinary Least Squares (OLS) regression** using Python.

---

## 🎯 Project Objective

The primary objective of this project is to answer:

> **Which financial indicators have a statistically significant relationship with a company's stock price?**

The analysis examines financial metrics such as:

* Stock Price
* Price/Earnings (P/E)
* Dividend Yield
* Earnings per Share (EPS)
* 52-Week Low
* 52-Week High
* Market Capitalization
* EBITDA
* Price/Sales
* Price/Book

The project also investigates whether there is a significant linear relationship between **Market Capitalization and EBITDA**.

---

## 📁 Dataset

The analysis uses a financial dataset containing information about approximately **500 publicly traded companies** across different sectors.

### Dataset Features

| Feature          | Description                                                    |
| ---------------- | -------------------------------------------------------------- |
| `Symbol`         | Company's stock ticker                                         |
| `Name`           | Company name                                                   |
| `Sector`         | Industry sector                                                |
| `Price`          | Current/observed stock price                                   |
| `Price/Earnings` | Price-to-Earnings ratio                                        |
| `Dividend Yield` | Dividend yield percentage                                      |
| `Earnings/Share` | Earnings per share                                             |
| `52 Week Low`    | Lowest stock price over 52 weeks                               |
| `52 Week High`   | Highest stock price over 52 weeks                              |
| `Market Cap`     | Total market capitalization                                    |
| `EBITDA`         | Earnings before interest, taxes, depreciation and amortization |
| `Price/Sales`    | Price-to-Sales ratio                                           |
| `Price/Book`     | Price-to-Book ratio                                            |
| `SEC Filings`    | SEC filing reference                                           |

---

## 🛠️ Technologies & Libraries

### Programming Language

* Python

### Data Analysis

* Pandas
* NumPy

### Data Visualization

* Matplotlib
* Seaborn

### Statistical Analysis

* SciPy
* Statsmodels

### Machine Learning / Data Preprocessing

* Scikit-learn

### Environment

* Jupyter Notebook
* Kaggle Notebook

---

# 🔍 Project Workflow

```text
Dataset
   ↓
Data Loading
   ↓
Data Understanding
   ↓
Missing Value Analysis
   ↓
Data Cleaning & Preprocessing
   ↓
Descriptive Statistics
   ↓
Exploratory Data Analysis
   ↓
Correlation Analysis
   ↓
Hypothesis Testing
   ↓
Pearson Correlation
   ↓
OLS Regression
   ↓
Statistical Interpretation
```

---

# 1️⃣ Data Loading & Understanding

The financial dataset is loaded using Pandas.

Initial inspection includes:

* `head()`
* `columns`
* `info()`
* Missing-value identification
* Descriptive statistics

The original dataset contains **505 companies** and **14 variables**.

---

# 2️⃣ Data Cleaning

The notebook performs several preprocessing operations before analysis.

### Missing Values

Missing values were identified in:

* `Price/Earnings`
* `Price/Book`

The notebook applies `KNNImputer` to the `Price/Book` column and subsequently removes remaining incomplete observations.

After preprocessing, the analytical dataset contains **503 observations**.

The `SEC Filings` column is also removed because it is a URL/reference field and is not directly required for the numerical analysis.

---

# 3️⃣ Exploratory Data Analysis

Several statistical and visual techniques are used to understand the dataset.

### Descriptive Statistics

The analysis examines:

* Mean
* Median
* Standard deviation
* Minimum
* Maximum
* Quartiles

For example, the average stock price in the cleaned dataset is approximately:

```text
$103.98
```

while the median is approximately:

```text
$73.92
```

The difference indicates that stock prices are strongly influenced by high-value observations.

---

## 📈 Stock Price Distribution

The distribution of stock prices is visualized using a histogram.

The calculated skewness is approximately:

```text
7.29
```

This indicates a **strong right-skewed distribution**, meaning a relatively small number of companies have substantially higher stock prices than the majority.

---

## 📦 Outlier Analysis

The notebook uses the **Interquartile Range (IQR)** approach to calculate:

* Q1
* Q3
* Lower bound
* Upper bound

This helps identify potential outliers in stock prices.

---

# 4️⃣ Sector Analysis

The project compares financial performance across different market sectors.

Visualizations are used to investigate:

* Earnings per Share by sector
* Sector-level differences
* Distribution of financial metrics

This provides a high-level view of how company financial characteristics differ across industries.

---

# 5️⃣ Correlation Analysis

A correlation matrix is generated to examine relationships between numerical financial variables.

A heatmap is used to visualize the correlation structure.

The analysis helps identify:

* Strong positive relationships
* Strong negative relationships
* Weak relationships
* Potential multicollinearity between explanatory variables

---

# 6️⃣ Pearson Correlation Hypothesis Test

The project specifically tests the relationship between:

```text
Market Capitalization
        vs.
EBITDA
```

### Hypotheses

**Null Hypothesis (H₀):**

> There is no linear correlation between Market Capitalization and EBITDA.

**Alternative Hypothesis (H₁):**

> There is a linear correlation between Market Capitalization and EBITDA.

Using Pearson's correlation test:

```text
Correlation coefficient (r) ≈ 0.7712
p-value ≈ 2.56 × 10⁻¹⁰⁰
```

Since:

```text
p-value < 0.05
```

the null hypothesis is rejected.

### Interpretation

There is **strong positive and statistically significant evidence of a linear relationship between Market Capitalization and EBITDA** in this dataset.

---

# 7️⃣ OLS Regression Analysis

An Ordinary Least Squares regression model is built to investigate which financial variables are statistically associated with stock price.

### Dependent Variable

```text
Price
```

### Independent Variables

```text
Dividend Yield
52 Week Low
52 Week High
Earnings/Share
EBITDA
Price/Sales
```

The dataset is divided into:

```text
70% Training Data
30% Testing Data
```

An OLS regression model is then fitted using Statsmodels.

---

# 📊 Regression Results

The model produced an:

```text
R² ≈ 0.994
Adjusted R² ≈ 0.994
```

This means the selected variables explain a very large proportion of the variation in the observed stock price **within this dataset**.

However, the high R² should **not** be interpreted as proof that the model can predict future stock prices accurately. Several explanatory variables, particularly the 52-week price measures, are inherently closely related to stock price, and the model also shows signs of multicollinearity and non-normal residuals.

---

## 🧪 Hypothesis Testing Results

Using a significance level of:

```text
α = 0.05
```

the regression coefficients were tested.

| Variable       | Coefficient | P-value | Result          |
| -------------- | ----------: | ------: | --------------- |
| Dividend Yield |     -0.1880 |  0.6727 | Not Significant |
| 52 Week Low    |      0.8606 | < 0.001 | Significant     |
| 52 Week High   |      0.0136 |  0.6768 | Not Significant |
| Earnings/Share |     -0.0810 |  0.5651 | Not Significant |
| EBITDA         |          ~0 |  0.8255 | Not Significant |
| Price/Sales    |     -0.5748 |  0.0027 | Significant     |

### Key Findings

At the 5% significance level:

**Statistically significant variables:**

* `52 Week Low`
* `Price/Sales`

**Statistically insignificant variables:**

* `Dividend Yield`
* `52 Week High`
* `Earnings/Share`
* `EBITDA`

---

# 💡 Key Insights

### 1. Market Cap and EBITDA have a strong relationship

The Pearson correlation of approximately **0.77** indicates a strong positive linear relationship between Market Capitalization and EBITDA.

---

### 2. Stock prices are highly right-skewed

The stock-price skewness is approximately **7.29**, indicating substantial influence from high-priced stocks.

---

### 3. 52-Week Low is statistically significant

The regression indicates a strong positive association between the 52-week low and the observed stock price.

---

### 4. Price/Sales is statistically significant

The model identifies Price/Sales as another statistically significant variable, with a negative coefficient in the fitted regression.

---

### 5. Not every financial metric is statistically significant

Dividend Yield, Earnings/Share, EBITDA, and 52-Week High do not show statistically significant coefficients in this particular regression specification.

---

# ⚠️ Important Statistical Limitations

This project is primarily an **exploratory and statistical analysis**, not a production-grade stock prediction system.

The regression output contains several warning signs:

* Very high R²
* Large condition number
* Evidence of multicollinearity
* Highly non-normal residuals
* Strongly skewed financial variables
* Cross-sectional rather than time-series analysis

Therefore:

> **Statistical association should not be interpreted as causation or as an investment recommendation.**

The results describe relationships present in this particular dataset and model specification.

---

# 📂 Project Structure

```text
Financial-Market-Analysis/
│
├── finance-analysis.ipynb
├── README.md
└── data/
    └── financials.csv
```

If the dataset is not redistributed with the repository, users can download it separately and update the notebook's input path.

---

# ▶️ How to Run

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/Financial-Market-Analysis.git
cd Financial-Market-Analysis
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels jupyter
```

### 3. Launch Jupyter Notebook

```bash
jupyter notebook
```

### 4. Open

```text
finance-analysis.ipynb
```

### 5. Update the dataset path

Change the Kaggle-specific path:

```python
/kaggle/input/datasets/adityamullick/financials/financials.csv
```

to the location of your local dataset.

---

# 📌 Skills Demonstrated

This project demonstrates practical experience with:

* Python for data analysis
* Pandas data manipulation
* NumPy numerical analysis
* Data cleaning
* Missing-value handling
* KNN imputation
* Descriptive statistics
* Exploratory Data Analysis
* Data visualization
* Correlation analysis
* Pearson correlation testing
* Null and alternative hypothesis formulation
* P-values and statistical significance
* OLS regression
* Regression coefficient interpretation
* Financial data analysis
* Outlier detection using IQR
* Statistical reasoning

---

# 🚀 Future Improvements

Possible extensions to make this project more robust:

* Add feature scaling and transformation
* Investigate multicollinearity using VIF
* Apply log transformation to highly skewed variables
* Perform residual diagnostics
* Compare Linear Regression, Random Forest and Gradient Boosting
* Use cross-validation
* Evaluate models using MAE, RMSE and R²
* Add sector-wise regression analysis
* Build an interactive financial dashboard
* Add time-series stock data for historical trend analysis
* Compare predicted vs. actual stock prices
* Develop a more rigorous stock valuation framework

---

# 📌 Disclaimer

This project is created for **educational and analytical purposes only**.

The statistical relationships identified in this analysis should not be considered financial advice, investment recommendations, or evidence of future stock-price performance.

---

## 👨‍💻 Author

**Ritik Chauhan**

B.Tech — Computer Science Engineering
Interested in **Data Analytics, AI/ML, Python, Automation and Business Intelligence**.

---

⭐ If you found this project useful, consider giving the repository a star.
