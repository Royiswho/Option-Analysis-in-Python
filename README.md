# European-Option-Analysis-in-Python

## Use market data to analyze options including computing implied volatity, verifying put-call parity and volatility smile, calculating Greeks

#### author: Yi Rong
#### update on 12/30/20

---
### 1. Introduction to Tools:

* Python 3.5

* Packages

<img src="media/image1.png" align="center">
---
### Part 1: Data Processing

### 2. Data from Yahoo and Bloomberg

#### 1)  Bloomberg

DATA1 is downloaded at 4:00 PM on 9/5 and DATA2 is downloaded at 4:00 PM
on 9/6. Because it is hard to download all the data simultaneously, only
close prices are obtained here. AMZN call data expired on September is
attached as below:

<img src="media/image2.png"  align="center">

#### 2)  Yahoo Finance

For data retrieval and pre-processing, I created two functions.

The first one is used to download option data of multiple assets and
save them in local.

<img src="media/image3.png" align="center">

<img src="media/image4.png" align="center">

The second one is used to read data and modify them to a concise format
based on symbol, type and expiration date.

<img src="media/image5.png" align="center">

### 3. OPtion Data Description

AMZN is the NASDAQ stock exchange symbol for Amazon. SPY is the
abbreviation for the SPDR S&P 500. It is an exchange-traded fund (ETF)
in NYSE Arca, which is designed to track the S&P 500 stock market index.
VIX, or the Volatility Index, is an index created by the Chicago Board
Options Exchange (CBOE), which shows the market's expectation of 30-day
volatility.

For a monthly expired option, AMZN and SPY are expired the third Friday
on the month, which are 9/21, 10/19, 11/16 and so on. And the expiration
dates for VIX are the third Wednesday on the month, which are 9/19,
10/17, 11/21 and so on.

### 4. Underlying Price / Short-term Interest rate / Time to Maturity

DATA1 is downloaded at 3:28 PM on 9/4 and DATA2 is downloaded at 9:40 AM
on 9/5. The underlying prices and short-term interest rate are shown in
the chart below:

<img src="media/image27.png" align="center">

The time to maturity is calculated based on year. In this assignment,
there are 365 days in 1 year.

### Part 2: European Option Analysis

### 5. Black-shores Formulas

Two functions below are created for pricing European call and European
put:

<img src="media/image6.png" align="center">

### 6. Computing Implied Volatility using Bisection Method

<img src="https://latex.codecogs.com/gif.latex?10^{-6}" title="10^{-6}" />

<img src="media/image7.png" align="center">

With the pricing functions and Bisection method above, I create a
function to calculate all the implied volatilities based on different
strike prices and bid and ask prices.

<img src="media/image8.png" align="center">

The implied volatilities for AMZN put expired on 9/21 and the average
value are shown as below:

<img src="media/image9.png" align="center">

The average value can be calculated as 0.2566. Then, with this method,
we can compute all the volatility values and their average.

### 7. Comparing Call's and Put's Implied Volatilities

All the volatility values are calculated through the same functions.

It is not necessary to show all the results, so I attach the result for
AMZN with expiration in November and SPY with expiration in October.

<img src="media/image11.png" align="center">

<img src="media/image12.png" align="center">

With all the volatility values above, a table for average volatilities
can be obtained as below:

<img src="media/image13.png" align="center">

**Comment:** Compared with SPY, the volatilities for AMZN are much
higher and it makes sense for the current market. As the maturity
increases, AMZN shows a higher volatility, but SPY doesn't change a lot.
From question 9, it is known that when the strike prices go up,
volatility values are decreasing then increasing, like a smile. And this
rule is followed by both put and call.

### 8. Verifying Put-Call Parity

With Put-Call Parity, I create a function to compute the theoretical
price for an option.

<img src="media/image14.png" align="center">

Then, I use the function to calculate the theoretical prices. For AMZN,
I calculate the call price for options expired in 9/21. Then, I make a
comparation with real prices. The results are shown:

<img src="media/image15.png" align="center">

For SPY, I calculate the call price for options expired in 9/21 as well.
Then, I make a comparation with real prices. The results are attached as
below:

<img src="media/image16.png" align="center">

**Comment:** From the two results, it can be found that the theoretical
prices and real prices are quite close. Hence, the Put-Call Parity can
be used to calculate an option price. However, the theoretical prices
and real prices are not exactly the same and I came up with two reasons.
Firstly, the market is not totally efficient, so there are some
opportunities for arbitrage. Secondly, Yahoo Finance gives data with
delay. So, the times for the two prices don't definitely match.

### 9. Volatility Smile

Because only three maturities are considered here, so I show them all
directly and the option expired in September is the one closest to
maturity. The implied volatility values versus strike for AMZN Call,
AMZN Put and SPY are shown as below:

<img src="media/image17.png" align="center">

<img src="media/image18.png" align="center">

**Comment:**

Firstly, the AMZN volatility values are smaller than SPY volatility
values. And this makes sense for a stock and an ETF.

Secondly, for both AMZN and SPY options expired in September, with the
strike prices increasing, the volatility values decrease then reverse,
like a smile.

Thirdly, at the beginning, as the strike price increases, the AMZN
volatility values drops slowly but SPY volatility values drop faster.

Fourthly, for AMZN, the volatility values are higher with further
maturity. However, for SPY, the rule is followed only by options expired
in October and November. The September-expired options show abnormally
high volatility values.

<img src="media/image19.png" align="center">

<img src="media/image20.png" align="center">

**Comment: Call versus Put**

The first picture shows implied volatility for AMZN Call and the second
one shows those for AMZN Put.

Firstly, for both call and put, the volatility values decrease then
reverse, which is like a smile.

Secondly, the trend of SEP-expired lines is the same, crossing down the
blue line then crossing up.

### 10. Greeks

#### 1) Delta

The data applied here is SPY call options expired in September. The
code and result for two methods are shown as below:

<img src="media/image21.png" align="center">

<img src="media/image22.png" align="center">

**Comment:** From the table, it is known that two lists are almost the
same. Hence, the two methods are equivalent as well.

#### 2) Vega

The same data is applied here. The code and result are attached as
below:

<img src="media/image23.png" align="center">

<img src="media/image24.png" align="center">

**Comment:** The two lists are quite close, indicating that the two
methods are equivalent as well.

#### 3) Gamma

*  The same data is used here as well. The code and result are attached:

<img src="media/image25.png" align="center">

<img src="media/image26.png" align="center">

**Comment:** The two lists are quite close, showing that the two methods
are equivalent as well.
