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

## Problems

### sort the array
given array A of 0s and 1s. Sort the array
A = [0,1,1,0,1]

> Approch 1 BF: (NlogN)
using built in sorting method

> count sort: `time: O(N)` `space: O(N)`
1. creating freqArr of size 2 for 0 and 1 `sapce: O(2)`
2. updating the frequency by iterating A `time: O(N)`
3. iterating freqArr and updating original Array `time: 2 * N`

> using two pointer: `time: O(N)` `space: constant`
1. using the i and j. i from the 0th index and j from N-1 index.
2. we increment i and decrement j based on condition.
3. It taks Linear time complexity only.

```python
N = len(A)
i, j = 0, N-1
while(i<=j):
  if A[i] == 0:
    i+=1 # valid at A[i] is in correct place
  elif A[j] == 1:
    j-=1 # value at A[j] is in correct place
  else:
    # swapping i and j values
    A[i], A[j] = A[j], A[i]
return A
```
### Tens digit sorting
Given int[] A, sort the array in increasing order based on the element tens value. if the elements tens value are same, arrange it in decresing order basis of element value.

A = [15, 11, 7, 19]

> BF: `space: O(1)` `time: O(nlogn)`
1. Iterate throu the array to find the tens digit
2. and sorting the array.

```python
def custom_sorting(x,y):
  a = (x//10) % 10
  b = (y//10) % 10
  if a>b:
    return 1
  elif a<b:
    return -1
  else:
    # handling if the tens digit is same
    if x>y:
      return -1
    elif x<y:
      return 1
    else:
      return -1

from functools import cmp_to_key

return sorted(A, key=cmp_to_key(custom_sorting))
```

### closet points to origin
Given list of restorent locations in x and y coordinates, and int B represening the num of closet restarent user to see. The user current locaiton is assumed to (0,0). Find the ecludiean distance between two points and return the B locations.

A [[1,3][-2,2]], B = 1

> BF:  `time: O(NlogN)`
1. Iterate over array A and calculate the ecludiean distanc.
2. Sort the array using built in functionality
3. return the first B elements

```
Ecludian Distance is distance between two points.
points are coordinate in x and y

Formula:
d = sqrt((x1-x2)**2 + (y1-y2)**2)

We can ignore sqrt and compare the ((x2-x1)**2 + (y2-y1)**2) value
As the origin is 0,

((x2)**2 + (y2)**2) only is enough

```

```python
def customFunc(x, y):
  a = ((x[0])**2 + (x[1])**2)
  b = ((y[0])**2 + (y[1])**2)
  if a>b:
    return 1
  elif a<b:
    return -1
  else:
    return -1

from functools import cmp_to_key

A = sorted(A, key=cmp_to_key(customFunc))
return A[0:B]
```

### wave array
Given int[] A, sort the array into wave-link array and return it.
a1>=a2<=a3>=a4<=a5 is the wave link format.

A = [1,2,3,4]
ans = [2,1,4,3]

Note: return lexicographically smallest if more possible answers

> BF: `time: NlogN`
1. Sort the array
2. swap every two elements in the array to get the answer

```python
def waveArray(A):
  N = len(A)
  A.sort()
  for i in range(N):
    if i+1 <N: # To handle if the N is odd value
      # swapping the two elements
      A[i], A[i+1] = A[i+1], A[i]
  return A
```



### quick sort
### partition given arry assuming the last element as pivot point