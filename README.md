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
https://www.dropbox.com/s/pqqz49xlqgit4h9/X_new.csv?dl=0 (factor exposures)
https://www.dropbox.com/s/0z51jj6xfy1ndsn/Y_new.csv?dl=0 (stock returns)

The actual symbols have been remapped and the factors have been normalized in each period. The stocks are characterized by GICS and use dummy variables to represent the four difference catergories:

industry=[10, 20, 30 ,40 ,50, 60, 70]
subindustry=[10, 15, 20, 25, 30 ,35, 40 ,45, 50, 60, 70 ,80]
sector=[10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60]
indgroup=[10, 20, 30 ,40, 50]

Note that the first element in each list is dummatized as 1 0 0 0 .. and the next as 0 1 0 0 ... etc.




