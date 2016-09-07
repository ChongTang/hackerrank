# Divisible Sum Pairs


## Problem:
You are given an array of $$n$$ integers, $$a_0, a_1, ..., a_{n-1}$$, and a positive integer, $$k$$. Find and print the number of $$(i,j)$$ pairs where $$i<j$$ and $$a_i + a_j$$ is evenly divisible by $$k$$.

**Input Format**

The first line contains $$2$$ space-separated integers, $$n$$ and $$k$$, respectively. 
The second line contains $$n$$ space-separated integers describing the respective values of $$a_0, a_1, ..., a_{n-1}$$.

**Constraints**
* $$2<=n<=100$$
* $$1<=k<=100$$
* $$1<=a_i<=100$$

**Output Format**

Print the number of $$(i,j)$$ pairs where $$i<j$$ and $$a_i + a_j$$ is evenly divisible by $$k$$.

**Sample Input**
```
6 3
1 3 2 6 1 2
```

**Sample Output**
```
5
```

**Explanation**

Here are the $$5$$ valid pairs:
* $$(0,2) -> a_0 + a_2 = 1 + 2 = 3$$
* $$(0,5) -> a_0 + a_5 = 1 + 2 = 3$$
* $$(1,3) -> a_1 + a_3 = 3 + 6 = 9$$
* $$(2,4) -> a_2 + a_4 = 2 + 1 = 3$$
* $$(4,5) -> a_5 + a_5 = 1 + 2 = 3$$


## Thoughts:
The naive solution is simple:
```python
#!/bin/python
import sys

n,k = raw_input().strip().split(' ')
n,k = [int(n),int(k)]
a = map(int,raw_input().strip().split(' '))

ans = 0
for i in xrange(n):
    for j in xrange(i+1, n):
        if (a[i]+a[j])%k == 0:
            ans += 1
print ans
```

This solution has **time complexity** of $$O(n^2)$$. Can we do better? Yes!

Suppose we have a pair $$(i,j )$$ meets the constrains. We can tell that the sum of reminders of $$a_i$$ and $$a_j$$ equals $$k$$, say $$a_i \% k + a_j \% k = k$$. With this property, we can count the reminder of each number in the input array first. And then, we can scan the counter array to compute the final number of pairs.

The **time complexity** of this solution is $$O(n+k)$$.


## Solution:
```python
#!/bin/python

import sys

n,k = raw_input().strip().split(' ')
n,k = [int(n),int(k)]
a = map(int,raw_input().strip().split(' '))

# mod_cnt is the counter array, the maximum possible length of this array is k 
mod_cnt = [0]*k
# count the number of each reminder 
for num in a:
    mod_cnt[num%k] += 1

# mod_cnt[0] contains the numbers that have 0 as its reminder when module k 
# In this set, numbers can composite pairs themselves.
# For example, suppose the indies of these numbers are [1, 3, 5, 7]. How many number of pairs are there?
# the answer is 4*3/2 = 6.
ans = mod_cnt[0]*(mod_cnt[0]-1)/2
# Then for reminders from 1 to k-1, we compute the number of pairs they can composite.
for i in xrange(1, (k+1)/2):
    ans += mod_cnt[i]*mod_cnt[k-i]

# At last, if k is an even number, for example 10, 
# the above loop will miss the reminder in the middle, which is 5
# we need to compute the number of pairs which in this set, similar to reminder 0
if k % 2 == 0:
    ans += mod_cnt[k/2]*(mod_cnt[k/2]-1)/2
print ans
```



