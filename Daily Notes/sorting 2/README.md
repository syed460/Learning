# Sorting 2: Quick & Comparator Problem

## Agenda:
1. Pivot Partition
2. Quick Sort
3. Comparator Problems
   1. It is about custom method of sorting
  
### Find Pivot Point
Given int[] A,Consider first element as pivot and re-arrange the elements such that 
if A[i] < P (smalest element than pivot value into LHS) if A[i] > P and highest elements in RHS. Return the current index of pivot element

```python
def swap(A, i, j):
  temp = A[i]
  A[i] = A[j]
  A[j] = temp

def partitionArr(A, s, e):
  # e = N-1
  N = len(A)
  p = A[s] # pivot element 
  i = s+1 # start of loop
  while(i<=e):
    if A[i] < p:
      i+=1
    elif A[e] > p:
      e+=1
    else:
      swap(A, i, e)
  # in the end e < i, we swap p and A[e]
  swap(A, s, e)
  return e # current index of pivot element
```

`TC:` O(N) # we visit each element once
`SC:` O(1) # no extra space used

### Quick Sort
1. It is a sorting Algo
2. Tacking pivit value from (front, back or random index value) array
3. re-arranging the array by placing smalest element in LHS and largest element in RHS of pivit element
4. performing above process in recursion
5. base case, when the array left with single element return as it is already sorted

```python
def quickSort(A, s, e):
  if e-s+1 == 1:
    return A
  # assuming the s as first pivit point and calculating its index after processing
  pivit = partitionArr(A, s, e)
  # process LHS of pivit ele
  quickSort(A, s, pivit-1)
  # process RHS of pivit ele
  quickSort(A, pivit+1, e)

def partitionArr(A, s, e):
  pivit = A[s] # currenly we are taking first element
  i = s+1
  while(i<=e):
    if A[i] < pivit:
      i+=1
    elif A[e] > pivit:
      e-=1
    else:
      swap(A, i, e)
  swap(A, s, e)
  return e # new pivit element to split array
```
`TC: `
`In Best and Average case:` O(NlogN)

```
N + N/2 + N/4.. 1
sumation of above sequence is:
=> logN
num of function calls = logN
time taken per function = N iteration
```
`in Worst CASE:` O(N^2)
```
if the array is already sorted, the first element is always minimum value.
Hence all the element will stay in RHS of pivit
so, 
num of function calls = N, N-1, N-2 => N times
time per funciton = N iteration
=> N*N => N^2
```

`SC: ` same as TC

### Randamized Quick Sort
`To avoid the Worst case senario of Quick Sort` we can use the Math.random() to pick the pivit element instead of first element always

This brings the TC NlogN

But what if think, we get minimum element always from random() funciton?

```
The probablity of getting smalest element in N is 1/N
The probablity of getting smalest element in N-1 is 1/N-1
The probablity of getting smalest element in N-2 is 1/N-2

The over all sequence
1/N* 1/N-1 * 1/N-2 ...1/1
can write it as,
1/(N * N-1 * N-2 * N-3...1)
So the summation of this sequence,
1/N!
As N! is very very large number, getting the minimum element always is rare, can be ignorable

```
```python
import random
def partitionArr(A, s, e):
  pIndex = random.randint(s,e) # random pivit index
  p = A[pIndex]
  swap(A, s, pIndex)
  i = s+1
  while(i<=e):
    if A[i] <= p:
      i+=1
    elif A[e] > p:
      e-=1
    else:
      swap(A, i, e)
  swap(A, s, e)
  return e
```

### Comparator
used to apply the custom sorting logic.
we can pass custom logic into sort() function which will hanle logic against two arguments

Conditions while handling logic:
```
if first arg to come before second return -ve value like -1
if second arg to come before first return +ve value like 1
if any argument to come return 0
```

### problem: 1
Given int[] A, sort the data in acending order of based on count of factors of each element. if factors are same then arrange basis of value

Code to calculate factors
`TC: ` O(sqrt(N))
`SC: ` O(1)
```python
def count_factor(N):
  count = 0
  n = int(N**.5)
  for i in range(1, (n + 1)):
    if N%i == 0:
      count+=2
  # Handling avoding double counting if N is perfect square
  # perfect squire num factors count = odd hence
  if N% n == 0:
    count-=1
  return count
```

```python
A = int[]
def custom_func(x, y): # It taks only two arg
  if count_factor(x) == count_factor(y):
    # lets compare values since the factors are same
    if x < y:
      return -1 # to return x
    elif x > y:
      return 1 # to return y
    else:
      return 0 # to return any since the x and y are same
  elif count_factor(x) < count_factor(y):
    return -1 # to return x
  else:
    return 1 # to return y

from functools import cmp_to_key
return sorted(A, key=cmp_to_key(custom_func))
```

### Largest Number
Given int[] A. arrange and return such that they form the largest number.

A = [10, 2]
ans = [2, 10]

`idea: `102 < 210

```python
def largestNum(A):
  # After converting the each integer into string
  def custom_func(x, y):
    if x+y > y+x:
      return -1
    elif x+y < y+x
      return 1
    else:
      return 0
  nums = [str(num) for num in A]
  A.sort(nums, key=cmp_to_key(custom_func))
  if A[0] == 0:
    return 0
  return "".join(A)
```

`time`: logn
`space`: O(N) because we are using nums array to store integers in string format

