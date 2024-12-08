# PRICE PREDICTION CAPSTONE README

### Price Prediction capstone's big idea
The project focuses on developing a stock price prediction model for U.S. stocks and ETFs. By leveraging time-series model, linear regression model and advanced machine learning techniques, particularly Recurrent Neural Networks (RNN) and Long Short-Term Memory (LSTM) models. RNN and LSTM are designed to capture the sequential dependencies in time series data. These neural networks can capture non-linear patterns, making them better at modeling complex market dynamics. LSTM is an advanced RNN variant with a built-in memory mechanism, which helps capture long-term dependencies and prevents the model from “forgetting” older information. This is critical for financial data, where historical patterns (even months prior) may influence current trends.
This enhanced price prediction will cater to investors and asset management firms interested in mid- to long-term investments, aiming to identify stocks with high probabilities of price increase. The core innovation is to generate a more data-driven prediction model that combines signals from both financial and technical data.

### Describe your goal
The goal is to build a predictive model for mid- to long-term price movements (at least 3 months) in U.S. stocks and ETFs. By achieving higher prediction accuracy than regression model, this tool can provide value to investors and asset management professionals, improving buy-hold decisions and aiding in efficient capital allocation.
### Describe your data
The primary datasets include:
*	“Huge Stock Market Dataset”: Historical daily stock and ETF data (adjusted for dividends and splits), including columns such as Date, Open, High, Low, Close, Volume, and Open Interest. This dataset will serve as the foundational time-series data for the analysis.
*	Alternative Dataset (“Stock Market Dataset” – optional): Focused on Nasdaq stocks, with similar data features as the primary set, allowing for cross-validation if necessary. The historic data is retrieved from Yahoo finance via yfinance python package.
*	“Financial Statements of Major Companies (2009-2023)” dataset that contains financial statements of certain “major” companies. Financial statements will be added for these stocks, to complement the model. 
*	Financial statement data via the Edgar API for U.S. companies (Optional). Quarterly or annual statements are available. 

### Describe your work (models, analysis, EDA, etc.)
*	Exploratory Data Analysis (EDA): 
	-	Load selected stocks and ETFs for initial inspecting of the Data.
	-	Quick check for duplicates.
	-	Get general understanding of the data structure and basic statistics using .info() and .describe().
	-	Convert “Column” date to datetime
	-	Create charts for prices and daily returns (calculated field)
*	Feature Engineering:
	-	calculate daily returns
	-	(Optionally) Create lagged price features, moving averages, and volatility metrics.
	-	Integrate financial metrics from the financial statement data
*	Modeling:
	-	Traditional Models (optionally): Develop benchmark models using linear regression and ARIMA.
	-	Machine Learning Models: Train an RNN and an LSTM for time-series forecasting.
	-	Ensemble Approach (optional): Combine multiple models' predictions using weighted averages to improve overall prediction robustness.
*	Evaluation: Assess models accuracy using MAE (mean absolute error) or others, focusing on prediction accuracy on 3 months and over longer time windows.

### Describe your results
Expected results will include a model that performs competitively against Simple Moving Average as benchmark, with improved predictive accuracy for mid- to long-term stock price movements. Ideally, the model will highlight how integrating time-series and financial statements can enhance predictive capabilities. Results will include:
*	Performance comparison of various models, demonstrating the most effective approach over different groups of stocks.
*	Key insights into which financial and technical factors are most predictive of stock price movement (optional).
*	Potential strategies for integrating these predictions into an investment framework, showing how this tool could support value-oriented investing strategies (optional).
This project has strong real-world applicability, offering asset managers and investors an advanced tool for mid- to long-term stock analysis.

### Sprint 2
Built an RNN model for pure price prediction (prediction based only on prices) for almost all 46 stocks and etfs I chose initially for analysis. I had to throw out 2 stocks (Paypal and Google) because available data for them was too short. In the beginning the model converts daily data to quarterly data because I found that the forecast can only be done for 1 cell, consecutively if I want to forecast for at least 90 days, I need to build the whole forecast on quarters. Then doing the train-test split manually, as the function train_test_split cannot maintain the sequence of data, because of it's randomization parameter. I have done 75%/25% split. I would prefer to have 80/20 split as longer training period presumably does affect positively the accuracy of the forecast, but in this case I would have to throw away significantly more stocks. 
Next I apply MinMaxScaler to normalise the datasets, to prepare the data  for modeling. For each prediction (forecast) I created a sliding window of historical data points - Lookback - to predict the next value. Next, I set the model itself: 4 layers of SimpleRNN units equal in number to Lookback, with dropout=0.2 to prevent overfitting and other parameters. Then I visulize the results: first train set only, then train and test together, then train,test and SMA that I add as a baseline prediction. The code calculates MSE, Mean Squared Error for train, test and SMA. Comparison analysis of MSE didn't produce any meaningful results.

Also I integrated financial metrics from the financial statement data by merging it with price data.

### Sprint 3
Built 4 comparable models based on the model from Sprint 2: 2 RNN models (univariate and multivariate) and 2 LSTM models (univariate and multivariate). All models were built on the same data: same monthly data from 2009 to 2017, same 9 stocks - the data that is present for . All 4 models also had the same specifications of the models: 75%/25% train/test split, MinMax scaler, 4 layers of Simple RNN/ LSTM units equal in number to lookback, dropout = 0.2, 50 epochs. The differences were: the model being used - RNN or LSTM and different number of variables: 1 - for univariate model (prices only), and 23 for multivariate model (prices plus financial statements).
Added calculation of MSE and saving it into csv and reading it from csv to compare 4 models' MSE across in one chart. Made a relative comparison of models' MSE. Results show that by and large model 1 - univariate RNN model with prices only - is the most attractive model in terms of accuracy. Other models deserve additional attention in the conditions outside of this comparison (more on that below).

To further develop project in the future, I define the following areas of research:
- Explore bigger number of nodes, especially in models 2 and 4 - multivariate models.
- Add variables stepwise, little by little, especially in models 2 and 4 the multivariate models. 