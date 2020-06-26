[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>> REPLACE THIS TEXT WITH YOUR RESPONSE
```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np
import matplotlib.pyplot as plt
from collections import defaultdict

import nsfg
import first
import thinkstats2
import thinkplot
```


```python
resp = nsfg.ReadFemResp()
u18 = resp.numkdhh
```


```python
u18list = list(u18)
u18pmf_d = dict(sorted({k:(u18list.count(k)/len(u18list)) for k in u18list}.items()))
u18pmf = pd.Series(u18pmf_d)
```


```python
plt.bar(range(0, 6), u18pmf)
plt.title('Children Under 18 at Home')
plt.xlabel('Number of Kids')
plt.ylabel('Probability')
plt.show()
```


![png](output_3_0.png)



```python
import pandas as pd
new = {}
for k, v in u18pmf.items():
    new_prob = k * v
    new[k] = new_prob
bias_pmf = pd.Series(new)
bias_pmf = bias_pmf / bias_pmf.sum()
plt.bar(range(0, 6), bias_pmf)
plt.title("Bias PMF of Children at Home")
plt.xlabel("Number of Children")
plt.ylabel("Probability")
plt.show()
```


![png](output_4_0.png)



```python
difference = u18pmf - bias_pmf
difference
```




    0    0.466178
    1    0.005059
    2   -0.186982
    3   -0.168099
    4   -0.074509
    5   -0.041647
    dtype: float64




```python
ind = np.arange(6)
width = .35
plt.bar(ind, u18pmf, width, label="Unbiased")
plt.bar(ind + width, bias_pmf, width, label="Biased")
plt.ylabel("Probability")
plt.xlabel("Children at home")
plt.title("Bias vs Unbias")
plt.xticks(ind+width / 2, ("0", "1", "2","3", "4", "5"))
plt.legend(loc="best")
plt.show()
```


![png](output_6_0.png)



```python
u18pmf
```




    0    0.466178
    1    0.214052
    2    0.196258
    3    0.087139
    4    0.025644
    5    0.010729
    dtype: float64




```python
bias_pmf
```




    0    0.000000
    1    0.208993
    2    0.383240
    3    0.255238
    4    0.100153
    5    0.052376
    dtype: float64




```python
unbias_mean = sum([k*v for k, v in u18pmf.items()])
unbias_mean
```




    1.024205155043831




```python
bias_mean = sum([k*v for k, v in bias_pmf.items()])
bias_mean
```




    2.403679100664282



The bias mean is more than twice the mean of the unbias data. According to this data, if you ask children the number of people under 18 in their house hold they are more likely to double the actual amount. 
