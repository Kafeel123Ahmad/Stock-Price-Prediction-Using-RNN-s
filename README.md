# Stock-Price-Prediction-Using-RNN-s

## Objective
The objective of this assignment is to try and predict the stock prices using historical data from four companies IBM (IBM), Google (GOOGL), Amazon (AMZN), and Microsoft (MSFT).

We use four different companies because they belong to the same sector: Technology. Using data from all four companies may improve the performance of the model. This way, we can capture the broader market sentiment.

The problem statement for this assignment can be summarised as follows:

> Given the stock prices of Amazon, Google, IBM, and Microsoft for a set number of days, predict the stock price of these companies after that window.

## Business Value
Data related to stock markets lends itself well to modeling using RNNs due to its sequential nature. We can keep track of opening prices, closing prices, highest prices, and so on for a long period of time as these values are generated every working day. The patterns observed in this data can then be used to predict the future direction in which stock prices are expected to move. Analyzing this data can be interesting in itself, but it also has a financial incentive as accurate predictions can lead to massive profits.

### **Data Description**
You have been provided with four CSV files corresponding to four stocks: AMZN, GOOGL, IBM, and MSFT. The files contain historical data that were gathered from the websites of the stock markets where these companies are listed: NYSE and NASDAQ. The columns in all four files are identical. Let's take a look at them:

- `Date`: The values in this column specify the date on which the values were recorded. In all four files, the dates range from Jaunary 1, 2006 to January 1, 2018.

- `Open`: The values in this column specify the stock price on a given date when the stock market opens.

- `High`: The values in this column specify the highest stock price achieved by a stock on a given date.

- `Low`: The values in this column specify the lowest stock price achieved by a stock on a given date.

- `Close`: The values in this column specify the stock price on a given date when the stock market closes.

- `Volume`: The values in this column specify the total number of shares traded on a given date.

- `Name`: This column gives the official name of the stock as used in the stock market.

There are 3019 records in each data set. The file names are of the format `\<company_name>_stock_data.csv`.
### Sample Data Head:
| Date       | Open  | High  | Low   | Close | Volume    | Name |
| ---------- | ----- | ----- | ----- | ----- | --------- | ---- |
| 2006-01-03 | 47.47 | 47.85 | 46.25 | 47.58 | 7582127   | AMZN |
| 2006-01-04 | 47.48 | 47.73 | 46.69 | 47.25 | 7440914   | AMZN |
| 2006-01-05 | 47.16 | 48.20 | 47.11 | 47.65 | 5417258   | AMZN |
| 2006-01-06 | 47.97 | 48.58 | 47.32 | 47.87 | 6154285   | AMZN |
| 2006-01-09 | 46.55 | 47.10 | 46.40 | 47.08 | 8945056   | AMZN |


### Analysis and Visualisation
![image](https://github.com/user-attachments/assets/3d5d85b0-018e-4cf4-afc6-1337dcb7e77f)

![image](https://github.com/user-attachments/assets/b546004e-6209-4c25-88cf-7a96b17416e0)

![image](https://github.com/user-attachments/assets/7da3445e-817a-48f5-b3da-ac3ccbbb0c9a)

### Stock Closing Prices for AMZN, GOOGL, MSFT, and IBM Over Time
![image](https://github.com/user-attachments/assets/a158afa2-4a2d-49b0-ab11-dcef18894c26)

![image](https://github.com/user-attachments/assets/4c39a216-083a-4682-a056-e64c6c30da47)

![image](https://github.com/user-attachments/assets/5954daf9-c380-4b3f-87fc-2c01228765f5)

![image](https://github.com/user-attachments/assets/cebb72f5-71be-476e-b94e-a36e07fdf045)

### Simple RNN Model
Model: "sequential"
| Layer (type)                     | Output Shape         | Param #   |
| -------------------------------- | -------------------- | --------- |
| simple_rnn (SimpleRNN)           | (None, 256)          | 66,816    |
| dropout (Dropout)                | (None, 256)          | 0         |
| dense (Dense)                    | (None, 1)            | 257       |
 
 **Total params:** 67,073 (262.00 KB) <br/>
 **Trainable params:** 67,073 (262.00 KB) <br/>
 **Non-trainable params:** 0 (0.00 B) <br/>

### Plotting the actual vs predicted values for Simple RNN Model

![image](https://github.com/user-attachments/assets/21f5d2d6-e030-4990-9a83-d4ac7866e042)

## Performance Metrics of Simple RNN Model
| Stock | Model | MAE (↓) | MSE (↓) | RMSE (↓) | R² Score (↑) |
| ----- | ----- | ------- | ------- | -------- | ------------ |
| AMZN | SimpleRNN | 6.6196 dollars | 175.5124 dollars² | 13.2481 dollars | 0.9971 |
| GOOGL | SimpleRNN | 6.0805 dollars | 68.0952 dollars² | 8.2520 dollars | 0.9989 |
| IBM | SimpleRNN | 2.6742 dollars | 10.1586 dollars² | 3.1873 dollars | 0.9917 |
| MSFT | SimpleRNN | 4.6353 dollars | 32.5400 dollars² | 5.7044 dollars | 0.8428 |

![image](https://github.com/user-attachments/assets/481b0801-3ad6-4387-b2eb-2ae88870f6c2)

#### Observations from the performance metrics:
- The Simple RNN model demonstrates varying levels of performance across the four stocks.
- It performs best (lowest errors, highest R²) in predicting the stock price of Google and IBM.
- Amazon's stock price prediction has the largest errors, while Microsoft's stock price variance is the least explained by this model.

### LSTM RNN Model
Model: "sequential_1"
| Layer (type)   | Output Shape | Param #  |
| -------------- | ------------ | -------- |
| lstm (LSTM)    | (None, 160)  | 105,600  |
| dropout_1 (Dropout) | (None, 160)  | 0      |
| dense_1 (Dense)  | (None, 1)    | 161      |

 **Total params**: 105,761 (413.13 KB)
 **Trainable params:** 105,761 (413.13 KB)
 **Non-trainable params:** 0 (0.00 B)

 ### Plotting the actual vs predicted values for LSTM RNN Model

 ![image](https://github.com/user-attachments/assets/0290d492-9974-4611-b190-64844828d2da)

 ## Performance Metrics of LSTM RNN Model
| Stock | Model | MAE (↓) | MSE (↓) | RMSE (↓) | R² Score (↑) |
| ----- | ----- | ------- | ------- | -------- | ------------ |
|   AMZN | LSTM | 6.0419 dollars | 178.9548 dollars² | 13.3774 dollars | 0.9971 |
|    GOOGL   | LSTM | 5.6887 dollars | 64.0564 dollars² | 8.0035 dollars | 0.9990 |
|  IBM   | LSTM | 2.0563 dollars | 7.6153 dollars² | 2.7596 dollars | 0.9938 |
|    MSFT  | LSTM | 4.9509 dollars | 32.2751 dollars² | 5.6811 dollars | 0.8441 |

 ![image](https://github.com/user-attachments/assets/dea2ee36-a0a3-4f93-8111-43b1730864b7)

#### Observations from the performance metrics:
- The LSTM model demonstrates a similar pattern of performance across the stocks as the Simple RNN model.
- It generally performs best (lowest errors, highest R²) in predicting the stock price of Google and IBM. Amazon's stock price prediction has the largest errors, while Microsoft's stock price variance is the least explained by this LSTM model compared to the others.
- The LSTM model, however, tends to have slightly lower error metrics (MAE, RMSE) and comparable or slightly better R² scores compared to the Simple RNN model for most stocks, suggesting a marginal improvement in predictive capability.

### Comparing performance metrics for Simple and LSTM RNN Model in a Tabular Format
| Stock | Model | MAE (↓) | MSE (↓) | RMSE (↓) | R² Score (↑) |
| ----- | ----- | ------- | ------- | -------- | ------------ |
| AMZN | SimpleRNN | 6.6196 dollars | 175.5124 dollars² | 13.2481 dollars | 0.9971 |
|      | LSTM | 6.0419 dollars | 178.9548 dollars² | 13.3774 dollars | 0.9971 |
| GOOGL | SimpleRNN | 6.0805 dollars | 68.0952 dollars² | 8.2520 dollars | 0.9989 |
|       | LSTM | 5.6887 dollars | 64.0564 dollars² | 8.0035 dollars | 0.9990 |
| IBM | SimpleRNN | 2.6742 dollars | 10.1586 dollars² | 3.1873 dollars | 0.9917 |
|     | LSTM | 2.0563 dollars | 7.6153 dollars² | 2.7596 dollars | 0.9938 |
| MSFT | SimpleRNN | 4.6353 dollars | 32.5400 dollars² | 5.7044 dollars | 0.8428 |
|      | LSTM | 4.9509 dollars | 32.2751 dollars² | 5.6811 dollars | 0.8441 |

## Conclusion and Final Insights
In this assignment, we successfully designed, trained, and evaluated both SimpleRNN and LSTM models to predict stock prices for four major companies: AMZN, GOOGL, IBM, and MSFT.

### Model Development
- SimpleRNN and LSTM models were built using windowed time series input data.
- Hyperparameter tuning was conducted for the LSTM model using Keras Tuner, optimizing the number of layers, units per layer, dropout rates, and learning rates.
- Models were evaluated using standard metrics: Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R² Score.

### Quantitative Performance Overview

| Stock | Best Model | MAE (↓) | RMSE (↓) | R² Score (↑) |
|:-----:|:----------:|:-------:|:--------:|:------------:|
| AMZN  | LSTM       | 6.04 dollars | 13.38 dollars | 0.9971 |
| GOOGL | LSTM       | 5.69 dollars | 8.00 dollars | 0.9990 |
| IBM   | LSTM       | 2.06 dollars | 2.76 dollars | 0.9963 |
| MSFT  | LSTM       | 4.95 dollars | 5.68 dollars | 0.8441 |

### Key Insights
- **LSTM Model Superiority:** The analysis consistently demonstrates that the LSTM (Long Short-Term Memory) model generally outperforms the Simple RNN model in predicting stock prices. This is evident across most stocks, with the LSTM achieving lower Mean Absolute Error (MAE), lower Root Mean Squared Error (RMSE), and higher R-squared (R²) scores in many cases.
- **Stock-Specific Predictability:** For **Amazon (AMZN) and Google (GOOGL)**, the models achieve a high level of accuracy, suggesting a strong ability to capture the underlying patterns in their stock price movements. For **IBM (IBM)**, the model also demonstrates good predictive power. **Microsoft (MSFT)** presents a greater challenge, with predictions showing more variability, indicating that its stock price is potentially influenced by factors beyond the scope of historical price data alone.

### Final Outcomes
- Successfully scaled, windowed, and processed multi-stock time series data.
- Designed dynamic RNN architectures with hyperparameter tuning.
- Achieved very high R² scores (~0.999 for AMZN and GOOGL), confirming excellent predictive performance.
- Demonstrated clear evidence of model superiority depending on stock characteristics (volatility, trend stability).

### Final Remarks
- For stocks with higher predictability (e.g., AMZN, GOOGL), the models can potentially assist in identifying entry and exit points or in making short-term trading decisions.
- For stocks with lower predictability (e.g., MSFT), the models can still offer insights into general trends but should be used with caution and in conjunction with other forms of analysis.
- Future work could involve exploring stacked LSTM layers, Bidirectional LSTMs, or even Transformer-based architectures for enhanced results.
- Regularization techniques like Dropout and careful hyperparameter tuning were essential in avoiding overfitting.

##### In summary, while the stock price prediction models offer valuable insights and demonstrate promising predictive power, they should be used as a component of a comprehensive investment strategy rather than a sole determinant of trading decisions.
