[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

>> REPLACE THIS TEXT WITH YOUR RESPONSE

```python
from __future__ import print_function, division

%matplotlib inline

import numpy as np
import matplotlib.pyplot as plt

import nsfg
import first
```


```python
resp = nsfg.ReadFemPreg()
live = resp[resp['outcome']==1]
```


```python
firstborn = live[live['birthord']==1]
other = live[live['birthord']!=1]
```


```python
first_mean = firstborn['totalwgt_lb'].mean()
first_mean
```




    7.201094430437772




```python
others_mean = other['totalwgt_lb'].mean()
others_mean
```




    7.325855614973262




```python
mean_difference = first_mean - others_mean
mean_difference
```




    -0.12476118453549034




```python
cohens_d = mean_difference/np.std(live['totalwgt_lb'])
cohens_d
```




    -0.08859523385261187



A value below .01 is considered to be very small. The difference is not significant between first born weights and babies that come afterwards. This is consistent with the effect size for the difference in pregnancy length which was small as well with a value of .0289. 
