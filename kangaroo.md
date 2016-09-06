# Kangaroo


## Problem:

There are two kangaroos on an x-axis ready to jump in the positive direction (i.e, toward positive infinity). The first kangaroo starts at location $$x_1$$ and moves at a rate of $$v_1$$ meters per jump. The second kangaroo starts at location $$x_2$$ and moves at a rate of $$v_2$$ meters per jump. Given the starting locations and movement rates for each kangaroo, can you determine if they'll ever land at the same location at the same time?

**Input Format**

A single line of four space-separated integers denoting the respective values of $$x_1$$, $$v_1$$, $$x_2$$, and $$v_2$$.

**Constraints**
* $$0 <= x_1 < x_2 <= 10000$$
* $$1 <= v_1 <= 10000$$
* $$1 <= v_2 <= 10000$$

**Output Format**

Print *YES* if they can land on the same location at the same time; otherwise, print *NO*.

**Note:** The two kangaroos must land at the same location after making the same number of jumps.

**Sample Input 0**

`0 3 4 2`

**Sample Output 0**

`YES`

**Explanation 0**

The two kangaroos jump through the following sequence of locations:
1. $$0->3->6->9->12$$
2. $$4->6->8->10->12$$

Thus, the kangaroos meet after  jumps and we print *YES*.

**Sample Input 1**

`0 2 5 3`

**Sample Output 1**

`NO`

**Explanation 1**

The second kangaroo has a starting location that is ahead (further to the right) of the first kangaroo's starting location (i.e., $$x_2 > x_1$$). Because the second kangaroo moves at a faster rate (meaning $$v_2>v_1$$) and is already ahead of the first kangaroo, the first kangaroo will never be able to catch up. Thus, we print *NO*.

**Solution:**
```python
#!/bin/python

import sys

x1,v1,x2,v2 = raw_input().strip().split(' ')
x1,v1,x2,v2 = [int(x1),int(v1),int(x2),int(v2)]
if (x1 < x2 and v1 <= v2) or (abs(x2-x1) % abs(v2-v1) != 0):
    print 'NO'
else:
    print 'YES'
```