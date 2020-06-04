## Statistical Testing

You are working for a TexMex restaurant that recently introduced queso to its menu.

We have random samples of 1000 "no queso" order check totals and 1000 "queso" order check totals for orders made by different customers.

In the cell below, we load the sample data for you into the arrays `no_queso` and `queso` for the "no queso" and "queso" order check totals. Then, we create histograms of the distribution of the check amounts for the "no queso" and "queso" samples. 


```python
# import the necessary libraries

#data manip
import numpy as np
import pandas as pd 
from scipy import stats

#viz
import matplotlib.pyplot as plt

#object import / export
import pickle

%matplotlib inline
```


```python
# load the sample data 
no_queso = pickle.load(open("data/no_queso.pkl", "rb"))
queso = pickle.load(open("data/queso.pkl", "rb"))

# plot histograms

fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))

ax1.set_title('Sample of Non-Queso Check Totals')
ax1.set_xlabel('Amount')
ax1.set_ylabel('Frequency')
ax1.hist(no_queso, bins=20)

ax2.set_title('Sample of Queso Check Totals')
ax2.set_xlabel('Amount')
ax2.set_ylabel('Frequency')
ax2.hist(queso, bins=20)
plt.show()
```


![png](index_files/index_3_0.png)


### 1. Hypotheses and Errors

The restaurant owners want to know if customers who order queso spend **significantly more *or* significantly less** than customers who do not order queso.

1a) Describe the null $H_{0}$ and alternative hypotheses $H_{A}$ for this test.


```python

print("""
Null hypothesis: Customers who order queso spend the same as those who do not order queso. 

Alternative hypothesis: Customers who order queso do not spend the same as those who do not order queso. 
""")
```

    
    Null hypothesis: Customers who order queso spend the same as those who do not order queso. 
    
    Alternative hypothesis: Customers who order queso do not spend the same as those who do not order queso. 
    


1b) What does it mean to make `Type I` and `Type II` errors in this specific context?


```python
print("""
Type I: (Rejecting the null hypothesis given it's true): Saying queso customers' total check amounts are different 
than non-queso customers' total check amounts when they are the same.

Type II: (Failing to reject the null hypothesis given it's false): Saying queso customers' total check amounts are 
the same as non-queso customers' total check amounts when they are different.
""")

# Give partial credit to students who describe what type I and type II errors are. 
```

    
    Type I: (Rejecting the null hypothesis given it's true): Saying queso customers' total check amounts are different 
    than non-queso customers' total check amounts when they are the same.
    
    Type II: (Failing to reject the null hypothesis given it's false): Saying queso customers' total check amounts are 
    the same as non-queso customers' total check amounts when they are different.
    


### 2. Sample Testing

2a) Run a statistical test on the two samples. Use a significance level of $\alpha = 0.05$. You can assume the two samples have equal variance. 

_Hint: Use `scipy.stats` (imported as `stats` above)._


```python

# Run a two-tailed t-test
print(stats.ttest_ind(no_queso, queso))
print()
# Students may compute the critical t-statistics for the rejection region
critical_t = (stats.t.ppf(0.025, df=999), stats.t.ppf(0.975, df=999))
print(critical_t)
```

    Ttest_indResult(statistic=-45.16857748646329, pvalue=1.29670967092511e-307)
    
    (-1.962341461133449, 1.9623414611334487)


2b) Can you reject the null hypothesis at a significance level of $\alpha = 0.05$?  

Why or why not?


```python
'''
We have enough evidence to reject the null hypothesis 
at a significance level of alpha = 0.05. We obtain a p-value
much smaller than 0.025 (two-tailed test). 

Alternatively: 
our t-statistic is smaller than the critical t-statistic.

Both answers (p-value or critical t-statistic) are valid. 
'''
```
