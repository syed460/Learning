# Arrays 1D
## Max subarray sum
1. brute fource approch
2. using prefix sum approch
3. carry forward approch
4. Kadane's algo

![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)
![alt text](image-3.png)

prefix sum Explanation:
![alt text](image-4.png)
![alt text](image-5.png)

carry forward:
![alt text](image-6.png)
![alt text](image-7.png)

Kadan's algorithem:
 -> maxsum subarray

 ![alt text](image-8.png)
## queris from i to last index
![alt text](image-9.png)
Brute fource:
![alt text](image-10.png)
![alt text](image-11.png)
## queries from index i to j

![alt text](image-12.png)

Brute fource: iterate the query for i to j iterate A and increment the each elements.

TC: O(Q*N) SC: O(1)
i.e
![alt text](image-13.png)

Optimized Approch:
for every query,
    update A[i] += value
    update A[j+1] -= value

Calculate the prefix sum and return

![alt text](image-14.png)

## merge intervals

![alt text](image-15.png)

IMPORTENT: Start time <= End time

2, 6 and 3, 7 
Point: both intervals over lapping hence we can merge them.
How to find if overlapping or not?
interval1: 2,5
interval2: 8,10
s1=2, s2=8, e1=5, e2=10

```python
#Possible Non-overlapping Intervals
#s1|-----|e1  
#    s2|-----|e2
#s2-----e2  
#    s1-----|e1
# if e1<s2 or e2<s1: or
if s2 > e1 or s1 > e2
    #No Over lapping
    pass
else:
    #Over lapping hence merge it
    mergedInterval = (min(2, 3), max(6, 7))
```

![alt text](image-16.png)

## merge sorted overlapping Intervals

![alt text](image-17.png)
![alt text](image-18.png)

i.e
![alt text](image-19.png)

Code:
![alt text](image-20.png)

## senario based problems: TODO

![alt text](image-21.png)
![alt text](image-22.png)

![alt text](image-23.png)