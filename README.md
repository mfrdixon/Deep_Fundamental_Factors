# Deep_Fundamental_Factors

This repository provides the Python code and data for the study:

@misc{dixon2019deep, title={Deep Fundamental Factor Models},
    author={Matthew F. Dixon and Nicholas G. Polson},
    year={2019},
    eprint={1903.07677},
    archivePrefix={arXiv},
    primaryClass={stat.ML}
}

## Source code
The repository consists of two Python notebooks: 
- DNNs_vs_OLS.ipynb which compares DNNs with OLS factor models
- DNNs_vs_LASSO.ipynb which compares DNNs with LASSO factor models

Each use Tensorflow to implement the deep neural networks together with an ADAM optimizer. LASSO is implemented using Scikit-learn and OLS uses the stats module. The maximum number of epoches is set to 100 and an early stopping criteria based on the mimumim loss and patience=3 is used. Further details are described in the paper.

## Data
The factor data has been collected from a financial data vendor and santized to avoid violation of data licensing agreement and non-commercial utility. The data, for non-commercial use only, can be downloaded from:
https://www.dropbox.com/s/x6mp1n4khxzouex/X.csv?dl=0 (factor exposures)
https://www.dropbox.com/s/cdhv3x4djqlpwhe/Y.csv?dl=0 (stock excess returns)

The actual symbols have been remapped and the factors have been normalized in each period. The stocks are characterized by GICS and use dummy variables to represent the four difference catergories:

industry=[10, 20, 30 ,40 ,50, 60, 70] 

subindustry=[10, 15, 20, 25, 30 ,35, 40 ,45, 50, 60, 70 ,80]

sector=[10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60]

indgroup=[10, 20, 30 ,40, 50]

Note that the first element in each list is dummatized as 1 0 0 0 .. and the next as 0 1 0 0 ... etc.

ID | Symbol  | Value Factors |
| --- | --- | --- |
|1 | B/P | Book to Price|
|2 | CF/P | Cash Flow to Price|
|3 | E/P | Earning to Price|
|4 | S/EV | Sales to Enterprise Value (EV). EV is given by |
||| EV=Market Cap + LT Debt + max(ST Debt-Cash,0), |
|| | where LT (ST) stands for long (short) term|
|5| EB/EV|   EBIDTA to EV |
|6| FE/P | Forecasted E/P. Forecast Earnings are calculated from Bloomberg earnings consensus estimates data. |
|| | For coverage reasons, Bloomberg uses the 1-year and 2-year forward earnings.|
|17| DIV | Dividend yield. The exposure to this factor is just the most recently announced annual net dividends ||  divided by the market price. |
||| Stocks with high dividend yields have high exposures to this factor.|
| --- | --- | --- |
|| | Size Factors|
| --- | --- | --- |
|8 | MC | Log (Market Capitalization)|
|9| S | Log (Sales)|
|10 | TA | Log (Total Assets)|
| --- | --- | --- |
|| |  Trading Activity Factors|
| --- | --- | --- |
|11| TrA | Trading Activity is a turnover based measure. |
|| | Bloomberg focuses on turnover which is trading volume normalized by shares outstanding. |
||| This indirectly controls for the Size effect. |
|||The exponential weighted average (EWMA) of the ratio of shares traded to shares outstanding:| 
||| In addition, to mitigate the impacts of those sharp shortlived spikes in trading volume, |
||| Bloomberg winsorizes the data: |
||| first daily trading volume data is compared to the long-term EWMA volume(180 day half-life), |
||| then the data is capped at 3 standard deviations away from the EWMA average.|
| --- | --- | --- |
||| Earnings Variability Factors|
| --- | --- | --- |
|12 |EaV/TA | Earnings Volatility to Total Assets. |
||| Earnings Volatility is measured |
||| over the last 5 years/Median Total Assets over the last 5 years|
|13 | CFV/TA | Cash Flow Volatility to Total Assets.| 
||| Cash Flow Volatility is measured over the last 5 years/Median Total Assets over the last 5 years|
|14 | SV/TA |  Sales Volatility to Total Assets.| 
||| Sales Volatility over the last 5 years/Median Total Assets over the last 5 year|
| --- | --- | --- |
|| | Volatility Factors|
| --- | --- | --- |
|15 | RV| Rolling Volatility which is the return volatility over the latest 252 trading days|
|16 | CB | Rolling CAPM Beta which is the regression coefficient|
|| | from the rolling window regression of stock returns on local index returns|
| --- | --- | --- |
||| Growth Factors||
| --- | --- | --- |
|7| TAG | Total Asset Growth is the 5-year average growth in Total Assets || divided by the Average Total Assets over the last 5 years|
|18 | EG | Earnings Growth is the 5-year average growth in Earnings ||  divided by the Average Total Assets over the last 5 years|


