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

## What does VIX signal/mean?

The VIX is a good indicator of the expectation of market volatility. This is a very important point; it is just a general assumption based on the [premiums](https://www.investopedia.com/terms/o/option-premium.asp#toc-what-is-an-option-premium) investors are willing to pay for the right to buy or sell stock.

This premium in options can be loosely defined as risk. Just like other forms of insurance, the greater the risk the higher the premiums, and the lower the risk the lower the premiums. When the options premium fall the VIX falls and when premiums rise the VIX rises. The buyers and sellers move the option prices, more buyers and the premiums go up, more sellers and the premiums go down.

A high VIX means that traders expect the underlying futures index, in this case the S&P 500, to see choppy trading going forward. When the VIX is rising, this means that traders are paying more for the average monthly S&P 500 put or call option. Traders pay more because they expect bigger price swings. 

A low VIX means that traders aren't willing to pay too much for put and call options on the S&P 500. This usually happens during periods of quiet market trading where the S&P 500 forms small average trading ranges each day. During this sort of period, traders aren't willing to pay much for protection against market swings, and thus prices of S&P 500 calls and puts are muted.

The above explanation can be found at [here](https://seekingalpha.com/article/4493104-cboe-volatility-index-vix).

## Empirical/Historical chart of VIX

Historically, the VIX tends to settle in the 15-25 range during an average market. VIX between 0-15 usually indicates optimism in the market and very low volatility. However, if the VIX falls too low it reflects complacency and that is dangerous accroding to the shoeshine boy theory - if everyone is bullish, there are no buyers left and the market comes tumbling down. VIX between 25-30 indicates some market turbulence, that volatility is increasing and investor confidence is likely declining. VIX over 30 typically indicate some extreme swings in the market coming up.

In general, VIX exhibits a spike pattern with bottom, or [mean-reverting](https://www.investopedia.com/terms/m/meanreversion.asp). A high VIX is often associated with a falling stock market. This is because stock investors often prefer bull market. Highest VIX readings are seen during major market panics such as the 2008 Financial Crisis and the Covid-19 shock of March 2020. Sometimes, VIX also spikes ahead of upcoming events that could lead to market turmoil, such as presidential elections.

## How traders can leverage VIX

### Use VIX as a signal

VIX serves as a market timing signal. Since VIX is a mean-reverting index that doesn't trend over time, centain numbers always tend to hold importantce. Some traders like to buy stocks when the VIX hits historically high numbers such as 30 or 40. Likewise, when the VIX hits unusually low levels such as 10 or 12, it might be a good time to take profits on the stock market.

### Trade VIX future and options

CBOE offers VIX options (VIX, VIXW) and futures (VX01 through VX53), enabling investors to trade volatility independent of the direction or the level of stock prices. Notable example includes story of the ["50 cent"](https://www.yahoo.com/entertainment/mystery-trader-50-cent-made-133000978.html) and the [LTCM fiasco](https://www.amazon.com/When-Genius-Failed-Long-Term-Management/dp/0375758259).

With the rise of [ETF](https://www.investopedia.com/terms/e/etf.asp) and [ETN](https://www.investopedia.com/terms/e/etn.asp), there are ETF longing VIX (e.g. VXX, UVXY) and shorting VIX (e.g. XIV). Such ETFs do not track VIX exactly, and ["correlation does not imply causation"](https://en.wikipedia.org/wiki/Correlation_does_not_imply_causation). We will introduce them in later posts.