# Technical-Indicators-on-Top-Volatility-Decile-Strategy
In this notebook, we will apply technical analysis not to individual stocks or market indices, but to a custom portfolio which is based on the volatility deciles, i.e. splitting the stocks according to their volatility in 10 equal subsets. The highest volatility decile would be selected for creating a trading strategy. We would then apply the moving average indicator and breakout indicator to generate trading signals and create a trading strategy. In conclusion, we will create a unique trading signal by merging both indicators, and compare the performance of the three indicator based strategies.

# 1. Import the libraries and read the data
First, we will import the necessary libraries and then, we will read the csv file witht the price data for the stocks in the S&P500 using the pandas 'read_csv' function.

We will use the pct_change() method to retrieve the daily returns of all the stocks in the S&P 500.

# 2. Calculate the standard deviation
We will calculate the standard deviation of the daily percentage change using the std() function. Standard deviation is the spread of data distribution in the given data set. To avoid look-ahead bias, we will use the stock data till December 2018 only. In this manner, volatility calculation and strategy returns calculations will have different time periods.

We will annualize the standard deviation and express it as a percentage to help us compare the stocks' volatility.

# 3. Top volatility decile portfolio
1. Sort the stocks by volatility
2. Select the top 10% of the stocks

The following methods/properties are used.

1. sort_values(): The function to sort the stocks according to the standard deviation of the daily percentage returns
2. len: Returns the number of rows in dataframe
3. plot.bar: Plots the bar chart
4. ylim: To set the values of the y-axis
5. show: To display the graph

# 3. Form the portfolio
1. Get the stock data from 2019 onwards. We want to separate the period used for volatility calculation and strategy returns calculations. This is done to avoid look-ahead bias.

2. Calculate the daily percentage change of each stock.

3. Compute mean returns for each day. This will be the portfolio returns.

4. Then, compute the cumulative returns. This will indicate how the portfolio value has changed over the period.

Note: Cumulative returns is the total change in the price of our portfolio over the set time period. Thus, we use the cumprod() method on our portfolio. Also, we are adding 1 to the portfolio as we assume that we started trading with $1 and not $0.

# 5. Trading signals and performance analytics: Moving Average
1. Moving average: Calculate the 10 days simple moving average of the portfolio value.

2. Trading signal: Set the signal as 1 when the portfolio value is more than the simple moving average. If this condition is not satisfied, the signal will return 0, which means no position. If we are already long, then 0 would imply an exit.

3. Strategy returns: Multiply the strategy returns with portfolio returns.

The following methods/properties are used.

1. numpy.where(): It can be used to generate the trading signal.

Parameters:

Condition: Condition to check

value_if_true: Value if the condition is satisfied

value_if_false: Value if the condition is not satisfied

2. dropna: to remove missing values

3. rolling: this method is used to provide a consecutive calculation of a group of numbers. Here, rolling function with a window size of 10 is used to calculate moving average of 10 values sequentially.

For the plotted portfolio:

1. The blue line indicates the portfolio value.

2. The grey dashed line indicates the signal. The value of 1 indicates long and 0 indicates no position. If we are already long, then 0 would imply an exit. Refer to y-axis on right.

3. The green shaded area represents the period when we are long on the portfolio stocks.

Cumulative strategy returns

We use cumprod() function to calculate cumulative strategy returns.

Drawdowns

Drawdown can be defined as the percentage loss from the highest cumulative historical point. The formula to calculate drawdown:

Drawdown = (cumulative returns/running maximum) - 1

To calculate the running maximum, we can use maximum() and accumulate() functions. The matplotlib.pyplot library and plot() function is used to plot both the returns as well as the drawdowns.

# 6. Trading signals and performance analytics: Breakout
1. Breakout: The maximum value of the portfolio from the current and previous two days.
2. Trading signal: Create a trading signal, which returns the value 1 when the current day's portfolio value is more than the maximum value computed in step 1. If this condition is not satisfied, the signal will return 0, which means no position. If we are already long, then 0 would imply an exit.
3. Compute the strategy returns.

# 7. Trading signals and performance analytics: Moving average and breakout
We will only take position when the signal returned is 1, by moving average as well as breakout. If this condition is not satisfied, the signal will return 0, which means no position. If we are already long, then 0 would imply an exit.
