---
layout: single
title: "Leveraging Volatility in Trading"
tags: finance
author-profile: true
comments: true
published: true
---

VIX is a volatility index that measures the volatility of S&P500 Index returns [implied](https://www.investopedia.com/terms/i/iv.asp#toc-what-is-implied-volatility-iv) in the next 30 days and priced (implied) in S&P500 options. The VIX gauges the level of fear or stress in the stock market and hence enjoys an vivid nickname as the “Fear Index.”

## How to compute VIX?

The components of the VIX Index are near- and next-term [put and call options](https://www.investopedia.com/options-basics-tutorial-4583012#toc-what-are-options) with more than 23 days and less than 37 days to expiration. They are computed in the same way, hence we focus on the generalized formula. The time to expiration is given by the following expression:

$$T = (M_c + M_s + M_o) / M_{365}$$

where $M_c$ is the minutes remianing until midnight of the current day, $M_s$ is minutes from midnight until 9:30 am ET for "standard" SPX expirations; or minutes from midnight unitl 4:00om ET for "weakly" SPX expirations; $M_o$ total minutes in the days between current day and expiration day; $M_{365}$ is the minutes in a year.

The risk-free interest rates, $R_1$ and $R_2$, are yields based on [U.S. Treasury yield curve rates](https://www.investopedia.com/terms/c/cmtindex.asp) (commonly referred to as “Constant Maturity Treasury” rates or CMTs), to which a [cubic spline](https://mathworld.wolfram.com/CubicSpline.html) is applied to derive yields on the expiration dates of relevant SPX options. As such, the VIX Index calculation may use different risk-free interest rates for near- and next-term options.

The selected options are [out-of-the-money](https://www.investopedia.com/ask/answers/042715/what-difference-between-money-and-out-money.asp) SPX calls and out-of-the-money SPX puts centered around an at-the-money [strike](https://www.investopedia.com/terms/s/strikeprice.asp#toc-what-is-a-strike-price) price, $K_0$. Only SPX options quoted with non-zero bid prices are used in the VIX Index calculation.  For each contract month, one determine the forward SPX level, F, by identifying the strike price at which the absolute difference between the call and put prices is smallest

$$F = \text{Strike Price} + e^{RT} \times (\text{Call Price} - \text{Put Price}).$$

Next, one determine $K_0$ - the strike price equal to or otherwise immediately below the forward index level, $F$ - for the near- and next-term options. Then one select out-of-the-money put options with strike prices $< K_0$. Start with the put strike immediately lower than $K_0$ and move to successively lower strike prices. Exclude any put option that has a bid price equal to zero (i.e., no bid). Likewise, one select out-of-the-money call options with strike prices $> K_0$. Start with the call strike immediately higher than $K_0$ and move
to successively higher strike prices, excluding call options that have a bid price of zero.

Finally, select both the put and call with strike price $K_0$. The VIX Index uses the midpoint of quoted bid and ask prices for each option selected. The $K_0$ put and call prices are averaged to produce a single value. 

Now we are ready to apply the generalized formula of raw VIX index

$$\sigma^2 = \frac{2}{T} \sum_{i}\frac{\Delta K_i}{K_i^2} e^{RT}Q(K_i) - \frac{1}{T}\Big(\frac{F}{K_0}-1\Big)^2$$

where $\sigma = VIX/100$, $T$ is the time to expiration, $F$ is the forward index level derived from index option prices, $K_0$ is the first strike below the forward index level $F$, $K_i$ is the strike price of $i$th out-of-the-money option; a call if $K_i > K_0$ and a put if $K_i < K_0$; both put and call if $K_i=K_0$, $\Delta K_i$ is the interval between strike prices -  half the difference between the strike on either side of $K_i$: $\Delta K_i = \frac{K_{i+1} - K_{i-1}}{2}$, $R$ is the risk-free interest rate to expiration and $Q(K_i)$ is the midpoint of the bid-ask spread for each option with strike $K_i$.

Going through the above process, one calculate the 30-day weighted average of $\sigma_1^2$ and $\sigma_2^2$, for near- and next-term, respectively. Then take the square root of that value and multiply 100 to get the VIX index value.

$$\text{VIX} = 100 \times \sqrt{\Big(T_1\sigma_1^2 \frac{M_{T_2} - M_{30}}{M_{T_2} - M_{T_1}} + T_2\sigma_2^2 \frac{M_{30} - M_{T_1}}{M_{T_2} - M_{T_1}}\Big) \times \frac{M_{365}}{M_{30}}}$$

where $M_{T_1}$ is the  number of minutes to settlement of the near-term options; $M_{T_2}$ is the  number of minutes to settlement of the next-term options; $M_{30}$ is the  number of minutes in 30 days and $M_{365}$ is the  number of minutes in a 365-day year. 

The inclusion of SPX Weeklys in the VIX Index calculation means that the near-term options will always have more than 23 days to expiration and the next-term options always have less than 37 days to expiration, so the resulting VIX Index value will always reflect an interpolation of $\sigma_1^2$ and $\sigma_2^2$ ; i.e., each individual weight is less than or equal to 1 and the sum of the weights equals 1.

A concrete exmaple is given from [CBOE white paper](https://cdn.cboe.com/resources/vix/vixwhite.pdf) or [OIC](https://www.optionseducation.org/referencelibrary/white-papers/page-assets/vixwhite.aspx).

For those interested in what the number mathematically represents, here it is in the most simple of terms. The VIX represents the S&P 500 index $\pm$ percentage move, annualized for one standard deviation. Example, if the VIX is currently at 15. That means, based on the option premiums in the S&P 500 index, the S&P is expected to stay with in a $\pm 15\%$ range over 1 year, $68\%$ of the time (which represents one standard deviation). 

Historically, the VIX tends to settle in the 15-20 range during an average market. VIX below 20 means that the market is forecasting a rather healthy and low risk environment. However, if the VIX falls too low it reflects complacency and that is dangerous, implying everyone is bullish. Remember the story of the "Shoe Shine Boy", if everyone is bullish there are no buyers left and the market comes tumbling down. If the VIX heads higher than 20, then fear is starting to enter into the market and it is forecasting a higher risk environment. If it goes too high, then everyone is singing the "chicken little" song.


## What does VIX signal?

The VIX is a number derived from the prices of options [premium](https://www.investopedia.com/terms/o/option-premium.asp#toc-what-is-an-option-premium) in the S&P 500 index (which is an index comprising 500 large cap stocks).

It is a good indicator of the expectation of market volatility, note I said "expectation", it is not representative of the actual volatility or what will happen. This is a very important point; it is just a general assumption based on the premiums investors are willing to pay for the right to buy or sell stock.

This premium in options can be loosely defined as risk. Just like other forms of insurance, the greater the risk the higher the premiums, and the lower the risk the lower the premiums. When the options premium fall the VIX falls and when premiums rise the VIX rises. The VIX is not set by any one person, but rather the results of millions of transactions by millions of traders from around the world. The buyers and sellers move the option prices, more buyers and the premiums go up, more sellers and the premiums go down. The VIX takes a weighted average of all these options prices in the S&P 500 index and derives a single number that is called the VIX.

This one VIX number gives us a general idea if investors are paying more or less for the right to buy or sell the S&P 500 index.

A high VIX means that traders expect the underlying futures index, in this case the S&P 500, to see choppy trading going forward. When the VIX is rising, this means that traders are paying more for the average monthly S&P 500 put or call option. Traders pay more because they expect bigger price swings. 

In general, a high VIX is associated with a falling stock market. Generally, the highest VIX readings are seen during major market panics such as the 2008 Financial Crisis and the Covid-19 shock of March 2020. Sometimes, VIX also spikes ahead of upcoming events that could lead to market turmoil, such as presidential elections.

A low VIX means that traders aren't willing to pay too much for put and call options on the S&P 500. This usually happens during periods of quiet market trading where the S&P 500 forms small average trading ranges each day. During this sort of period, traders aren't willing to pay much for protection against market swings, and thus prices of S&P 500 calls and puts are muted.


