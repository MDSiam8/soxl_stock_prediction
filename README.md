# soxl_stock_prediction
I have created a machine learning model for one of my favorite stocks (or rather, ETFs): SOXL. This takes various different things as input, such as the percent gain of the ETF and its RSI (Relative Strength Indicator), to provide a prediction of what tomorrow's trading day will look like. This is the first ever "real world" model I have made.
The link to the site may be accessed here: https://mdsiam8.github.io/soxl_stock_prediction/.
Future plans are to:
- use more inputs for the model, in anticipation of more accuracy
- expand library of stocks that I cover
- achieve greater accuracy in general for the predictions
- create and publish a field test and my overall performance when using this model
- create a webpage that allows a user to train their own ML model on their given stock, given that they have their own data

# How is this "different"?
Unlike most Machine Learning attempts at the stock market, this one uses categorical data and outputs a categorical prediction. So, rather than giving a prediction for how much a given stock may go up the following day, this instead gives you a prediction of whether or not the next day will be profitable. Also, this is an ETF, so it's price performance isn't dependent on just one company's stock performance, but rather multiple across the same sector. Lastly, it's data is used in coordination with the percent change of the SPY ETF, to anticipate any potentially large moves based on the general condition of the market, because the performance of both of these ETFs are related from my experience with them. 

# How was this made?
TL;DR at the bottom.

First, I downloaded the historical data (ranging back 1 year) for this ETF from the Yahoo Finance database, and opened it up in Google Sheets.

I then used the GOOGLEFINANCE function in coordination with the dates in each row to calculate the percent gain for one trading day ahead of the given date. After this, I created a filter view in that spreadsheet, where I first filtered all the data in the spreadsheet by the values in this column that were greater than 0 (this will bring up only the rows that have a value in this column greater than 0). I then replaced all the filtered values in this column with the label "profit." Then, I reset the filter view and filtered for values less than or equal to 0 and replaced all filtered values in this column with "loss." Then, I turned off the filter view, having done perhaps the most important task in this entire project.

Then, I used the closing price column to calculate the percent gain on the given date from the previous day's close.

Next up is the calculation for RSI. I copied all the data I currently had in the spreadsheet and opened up a blank new spreadsheet, where I pasted the original data. It was important to do this because it's a somewhat messy process that takes up many, many columns to calculate the RSI. After getting the RSI calculation, I pasted the VALUES of them (not FORMULA) back to the original spreadsheet under a column titled RSI.

After that, I copied all the contents of the spreadsheet, and pasted only the VALUES over the current data (important because you do not want to paste the formulas, or else you'll get reference errors when you clean up the data). Then, I cleaned up the data by getting rid of all columns except for next day's gain, RSI, and percent change today.

Up next is the data for SPY. In a new spreadsheet, I obtained SPY data and used it to calculate the percent change from previous day's close to the given date's close, as described above for the SOXL ETF. Then I copied these values and pasted them into a new column into the spreadsheet will all the other data. And with this, I completed my training dataset. 

After collecting all the necessary data, it was time to export it. I exported it as a CSV, and imported it into my training file. I designed a multilayer neural network to train it, using tensorflow.js and used regularization techniques to reduce the risk of overfitting. Previously, I ran into severe overfitting issues, so it was a very important task to make sure not to overfit it. After about 60,000 epochs, the model had been created and it was time to make the complementing webpage. With a few HTML, CSS, and Javascript, the webpage had been completed and the site was ready to publish.

TL;DR: I used Google Sheets and Yahoo Finance to form my training data, consisting of:
- a column consisting of the categorical indicators of "profit" and "loss" which describe the next trading day's performance of any given date. This column was used as the labels in the ML model.
- two columns of the percent change on the given date for SOXL ETF and the SPY ETF
- a column for the RSI for SOXL
I then trained it using tensorflow.js.

# Field testing
I am currently in the process of testing it, running the model under each day's conditions and updating my observations of the model's efficacy. Once I have a considerable amount of data ready, I will publish it in this section.


