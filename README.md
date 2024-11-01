# PRICE PREDICTION CAPSTONE README

### Price Prediction capstone's big idea
The project focuses on developing a stock price prediction model for U.S. stocks and ETFs. By leveraging time-series model, linear regression model and advanced machine learning techniques, particularly Recurrent Neural Networks (RNN) and Long Short-Term Memory (LSTM) models. RNN and LSTM are designed to capture the sequential dependencies in time series data. These neural networks can capture non-linear patterns, making them better at modeling complex market dynamics. LSTM is an advanced RNN variant with a built-in memory mechanism, which helps capture long-term dependencies and prevents the model from “forgetting” older information. This is critical for financial data, where historical patterns (even months prior) may influence current trends.
This enhanced price prediction will cater to investors and asset management firms interested in mid- to long-term investments, aiming to identify stocks with high probabilities of price increase. The core innovation is to generate a more data-driven prediction model that combines signals from both financial and technical data.

### Describe your goal
The goal is to build a predictive model for mid- to long-term price movements (at least 3 months) in U.S. stocks and ETFs. By achieving higher prediction accuracy than regression model, this tool can provide value to investors and asset management professionals, improving buy-hold decisions and aiding in efficient capital allocation.
### Describe your data
The primary datasets include:
•	“Huge Stock Market Dataset”: Historical daily stock and ETF data (adjusted for dividends and splits), including columns such as Date, Open, High, Low, Close, Volume, and Open Interest. This dataset will serve as the foundational time-series data for the analysis.
•	Alternative Dataset (“Stock Market Dataset” – optional): Focused on Nasdaq stocks, with similar data features as the primary set, allowing for cross-validation if necessary. The historic data is retrieved from Yahoo finance via yfinance python package.
•	“Financial Statements of Major Companies (2009-2023)” dataset that contains financial statements of certain “major” companies. Financial statements will be added for these stocks, to complement the model. 
•	Financial statement data via the Edgar API for U.S. companies (Optional). Quarterly or annual statements are available. 

### Describe your work (models, analysis, EDA, etc.)
•	Exploratory Data Analysis (EDA): 
	o	Load selected stocks and ETFs for initial inspecting of the Data.
	o	Quick check for duplicates.
	o	Get general understanding of the data structure and basic statistics using .info() and .describe().
	o	Convert “Column” date to datetime
	o	Create charts for prices and daily returns (calculated field)
•	Feature Engineering:
	o	calculate daily returns
	o	(Optionally) Create lagged price features, moving averages, and volatility metrics.
	o	Integrate financial metrics from the financial statement data
•	Modeling:
	o	Traditional Models (optionally): Develop benchmark models using linear regression and ARIMA.
	o	Machine Learning Models: Train an RNN and an LSTM for time-series forecasting.
	o	Ensemble Approach (optional): Combine multiple models' predictions using weighted averages to improve overall prediction robustness.
•	Evaluation: Assess models accuracy using MAE (mean absolute error) or others, focusing on prediction accuracy on 3 months and over longer time windows.

### Describe your results
Expected results will include a model that performs competitively against Simple Moving Average as benchmark, with improved predictive accuracy for mid- to long-term stock price movements. Ideally, the model will highlight how integrating time-series and financial statements can enhance predictive capabilities. Results will include:
•	Performance comparison of various models, demonstrating the most effective approach over different groups of stocks.
•	Key insights into which financial and technical factors are most predictive of stock price movement (optional).
•	Potential strategies for integrating these predictions into an investment framework, showing how this tool could support value-oriented investing strategies (optional).
This project has strong real-world applicability, offering asset managers and investors an advanced tool for mid- to long-term stock analysis.
