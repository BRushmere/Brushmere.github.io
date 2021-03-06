# Bollinger-Band

So this is an example of generating technical analysis to price stocks over a time frame. This method can be adapted to suit any technical analysis that suits you (e.g  Moving averages, Relative Strength Indicators, Stochastic Oscillators etc.).


Gather the daily prices for Apple over the period 2015-2018

```python

import pandas as pd

import pandas_datareader.data as web

import matplotlib.pyplot as plt

from datetime import datetime

start = datetime(2015, 1, 1)
end = datetime(2018, 1, 1)

Symbols = ['AAPL']


df = pd.DataFrame()


for sym in Symbols:
    df[sym] = web.DataReader(sym,'iex', start, end)['open']
rolling =df.rolling(window = 21)  

rollingMean =rolling.mean()
std = rolling.std()

upperBand = rollingMean+std*2
lowerBand = rollingMean-std*2


plt.plot(df)
plt.plot(upperBand)
plt.plot(lowerBand)
plt.show()
```
Produces the following:
![bb](bb.png)

*Bollinger Band Interpretation*

Closing prices above the upper Bollinger band may indicate that currently the stock price is too high and price may decrease soon. The market is said to be overbought.

Closing prices below the lower Bollinger band may be seen as a sign that prices are too low and they may be moving up soon. At this point the market for the stock is said to be oversold.
