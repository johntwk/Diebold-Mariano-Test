# Diebold-Mariano Test
This Python function <i>dm_test</i> implements the Diebold-Mariano Test (1995) with modification suggested by Harvey et. al (1997) to statitsitcally identify forecast accuracy equivalance for 2 sets of predictions.

## Description

Suppose that the difference between the first list of prediction and the actual values is e1 and the second list of prediction and the actual value is e2. The length of time-series is T. <br>
Then d can be defined based on different criterion (<i>crit</i>).
<br>
<ol>
  <li>MSE : d = (e1)^2 - (e2)^2</li>
  <li>MAD : d = abs(e1) - abs(e2)</li>
  <li>MAPE: d = abs((e1 - actual)/(actual))</li>
  <li>Poly: d = (e1)^power - (e2)^power</li>
</ol>
The null hypothesis is E[d] = 0.

The test statistics follow the student-T distribution with degree of freedom (T - 1).

## File
|    | File Name  | Description                                               |
|----|------------|-----------------------------------------------------------|
| 1. | dm_test.py | This file contains the function to implement the DM test. |

## Input

|    | Input Parameter | Description                                                                                                                        |
|----|-----------------|------------------------------------------------------------------------------------------------------------------------------------|
| 1. | actual_lst      | The list of actual values                                                                                                          |
| 2. | pred1_lst       | The first list of predicted values                                                                                                 |
| 3. | pred2_lst       | The second list of predicted values                                                                                                |
| 4. | h               | The number of steps ahead of the prediction. The default value is 1.                                                               |
| 5. | crit            | A string specifying the criterion. The default value is MSE.                                                                       |
| 6. | power           | The power for crit equal "poly".  It is only meaningful when crit is "poly". The default value is 2. (i.e. E[d] = (e1)^2 - (e2)^2) |

## Return

|    | Names of Return | Description                       |
|----|-----------------|-----------------------------------|
| 1. | DM              | The DM test statistics            |
| 2. | p-value         | The p-value of DM test statistics |

## Example

Sample Script:
```Python
from dm_test import dm_test
import random

random.seed(123)
actual_lst = range(0,100)
pred1_lst = range(0,100)
pred2_lst = range(0,100)

actual_lst = random.sample(actual_lst,100)
pred1_lst = random.sample(pred1_lst,100)
pred2_lst = random.sample(pred2_lst,100)

rt = dm_test(actual_lst,pred1_lst,pred2_lst,h = 1, crit="MAD")
print rt
rt = dm_test(actual_lst,pred1_lst,pred2_lst,h = 1, crit="MSE")
print rt
rt = dm_test(actual_lst,pred1_lst,pred2_lst,h = 1, crit="poly", power=4)
print rt
```

Output:
```Python
dm_return(DM=1.3275742446369585, p_value=0.18737195617455585)
dm_return(DM=1.2112523589452902, p_value=0.22868210381769466)
dm_return(DM=0.9124498079287283, p_value=0.36374861695187799)
```

## Reference

Harvey, D., Leybourne, S., & Newbold, P. (1997). Testing the equality of 
   prediction mean squared errors. International Journal of forecasting, 
   13(2), 281-291.

Diebold, F. X. and Mariano, R. S. (1995), Comparing predictive accuracy, 
   Journal of business & economic statistics 13(3), 253-264.

## Licence

MIT License

Copyright (c) 2017 John Tsang

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
