---
title: "Geometric Brownian Motion on Stock and Option Price Discovery"
excerpt: ""
classes: wide
header:
  overlay_image: /assets/images/chromaAnalysis/cleopatraforPython1second.png
  overlay_filter: 0.2 # same as adding an opacity of 0.5 to a black background
  caption: "Photo credit: Random Walk using Matlab"
---

## Summary
Quantitative Finance is a field of applied mathematics that employs mathematical and statistical
methods to analyze assets. One of the main concepts of quantitative finance is Brownian motion,
more specifically Geometric Brownian Motion used in stock price prediction. In this project, GBM
was used to model and forecast option contract prices of an asset (specifically Microsoft) with a
week-long option contract. Results showed accuracy close to the actual prices albeit to two data
points. The probable cause for the inaccuracy may be due to: dividends, examples used were
American-style options, and volatility and drift may have been calculated differently. GBM forms
the basis of the Black-Scholes equation, the current standard of options pricing today.


## Introduction 

Brownian Motion is first credited to botanist Robert Brown and decades later, was used by Louis Bachelier to model stock speculation and Albert Einstein to indirectly prove the existence of atoms. Brownian Motion, or specifically Geometric Brownian Motion (logarithmic quantity that follows Brownian Motion), is one of the main concepts of quantitative finance for asset price prediction. 
The log of the Geometric Brownian motion is as follows:
$$
log(S_t) = log(S_0) + (\mu - \frac{\sigma^2}{2})t + \sigma W_t
$$
where:

$ \mu = $ drift of the stock.  

$ \sigma = $ volatility. 

$ S_0 = $ initial value/price. 

$ S_t = $ forecast price. 

$ t = $ small interval time. 

$ W_t = $ Wiener process.

The drift of the stock, $\mu $, and volatility, $ \sigma $, are the unknown parameters for the equation. The drift of the stock is the mean of the returns, which can be calculated by a simple equation: $\frac{1}{T} \sum_{i}^{T} R_t$ where $R_t = \frac{S_t - S_{t-1}}{S_{t-1}}$, such that $S_t$ is the next day log-price, and $S_{t-1}$ is the current day log-price. For volatility, the variance-covariance matrix is calculated from the log returns and subsequently using Cholesky Decomposition. Since the variance-covariance is always symmetric and semi-positive definite, Cholesky Decomposition, $LL^T$, can be used. To get the volatility, we take the diagonal of the resulting $L$.

 
For this project, 14 Tech companies' stock prices were used. Since the companies are in the same sector (Tech), the prices will be correlated. While data are already adjusted for stock splits and stock consolidation, they do not adjust for dividends. Hence, we will assume that dividends are relatively small and do not affect the overall price of the stock. 

Using the GBM formula with the calculated drift, $\mu $, and volatility, $ \sigma $, we can forecast the price of stocks using multiple simulations as shown in Figure(4) - Figure(6). However, the use of GBM is not directly implemented in stocks but on \textit{options}. Options is a financial derivative that gives the buyer the right, but not the obligation, to buy an asset for a given price before a predetermined time (expiry). For this project, we take on a \textit{Risk Neutral Position} (RNP), a position where we ignore the risks, of European-style Options, options that can only be \textit{exercised} on the expiry date. In an RNP, the drift rate of the stock becomes a risk-free interest rate. Using the same GBM, we can forecast the price of the options per strike price. 


The forecast price was relatively close to the actual price, albeit for two data points (strike price at $ \$342.5$ and $ \$347.5)$ as shown in Figure(1). Probable cause for this error may be due to: 


1. Volatility and Drift may have been calculated differently. For example, drift and volatility may have been calculated using a much bigger data set. 
    
2. We modeled the price using a European-style option but the options in question were American-style options. As each option could have been exercised, the price of the option would have changed.
    
3. Dividends were assumed to be small. However, in the Black-Scholes model and GBM, assets are assumed to have no dividends. 


GBM forms the basis of the Black-Scholes equation, the current standard of options pricing today. GBM and Black-Scholes are a simplification of a complex financial system. For example, stock prices are non-stationary time series, with changing volatility and drift. Likewise, GBM and Black-Scholes are incapable of forecasting unpredictable events in the real world. Lastly, with the increased use of High-Frequency Trading (HFT) for price discovery, quantitative finance is becoming more dominant in the current market, increasing speculation. The recent increase in speculation has likewise increased volatility, which has been considered to be one cause of the recent recessions. The current state of quantitative finance is the application of machine learning, however, whether it improves the state of the market is still questionable.


![image](/assets/images/chromaAnalysis/Picture3.png){: .align-center}
*Figure 3: 1/11 clip used for training. As seen, the clip was deconstructed to the average values of its frames per 5 seconds. When visualized, the framelines is seen at (C)*


``` Matlab
% calculatde the return
score = diff(YTD)./YTD(1:end-1,:);

%calculate the drift
meanx = mean(score,1);

%calculate variance
variance = cov(score);
L = chol(variance);
diag_L = diag(L);
diag_L;
```

