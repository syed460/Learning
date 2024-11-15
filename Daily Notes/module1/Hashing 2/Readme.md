# Hashing 2

> Agenda:
1. First Non Repeating Element
2. Pair Sum
3. Count of Pair Sum
4. Check if there exists a subarray With Sum Zero
5. Check if There Exists a Subarray With Sum k

## Problem 1: First Non Repeating Element

1. First lets create frequency count of array A in HashMap
2. Iterage over A again and check in hashmap if frequency count that that element is equal to One

`Time`: O(N)
`Space`: O(N)

```python
A = [...]
N = len(A)
freqMap = {}
for i in range(N):
  freqMap[A[i]] = freqMap.get(A[i], 0) + 1
for i in range(N):
  if freqMap[A[i]] == 1:
    return A[i]
```

## Problem 2: Pair with sum is equal to k
Given int[] A and int k. Find if thre is a pair (i,j) such that A[i] + A[j] = k and i!j

> Approch 1: BF O(N^2) time, constant space
1. Create all the pairs and check if condition meats

```python
def findPairSumK(A):
  for i in range(N):
    for j in range(i, N):
      length = j-i+1
      if length == 2:
        if A[i]+A[j] == k:
          return True
  return false
```

> Approch 2: Using set
```
#Formula to be used:
a + b = k
# subtract both sides with a
a + b - a  = k - a
# after simplified
b = k - a
```
1. Create set with element of A. 
2. iterate over the elements of A and using `b=k-a` formula k-A[i] and check if b is present in set or not
3. return True if found

`time`: O(N)
`space`: O(N) beause of using the set to store elements

```python
def findPairSumK(A, k):
  elements = set()
  for a in A:
    elements.add(a)
  # b = k - A[i] and check if b is in elements set or not
  for i in range(N):
    b = k - A[i]
    if b in elements:
      return True
  return False
``` 
> Approch 3: Using set on the go
Same time and space complexity

```python
def findPairSumK(A,K)
  elements = set()
  for i in range(N):
    b = K-A[i]
    if b in elements:
      return True
    else:
      elements.add(A[i])
  return False

```
> Approch 3:
1. As the above approch will not work to satisfy i!=j condition.
2. We need to use hashmap to store the frequency of the elements.
3. and keep the condition if frequency is more than 1 only reutrn true
   
```python
def findPairSumK(A, K):
  freq_ofele = {}
  for a in A:
    freq_ofele[a] = freq_ofele.get(a, 0) + 1
  
  for i in range(N):
    # get the b with formula
    b = K-A[i]
    # get the frequency of element
    value = freq_ofele.get(b, 0)
    # check if frequency is more than 1
    if value > 1:
      return True
  return False    
```

## Problem 3: subarray with sum is equal to zero
Given int [] A, Find the subarray its sum is equal to zero

> Approch 1: BF `time`: O(N^3), `space:` Constant
1. going through all the subarray will take O(N^2)
2. iterating each subarray to find its sum and check the condition is meeting.

> Approch 2: using prefix sum `time`: O(N^2), `space`: O(N)
1. by creating Prefix sum array out of array A
2. and in constant time check the subarray sum which will reduce O(N) time.
3. which will also cost Linear time in space by using extract space for prefix sum array

```python
def subarrSum0(A):
  # create prefix array
  pf = []
  N = len(A)
  pf.append(A[0])
  for i in range(1, N):
    pf.append(pf[i-1]+A[i])
  # create all subarray
  for i in range(N):
    for j in range(i, N):
      value = 0
      if i == 0:
        value = pf[j]
      else:
        value = pf[j] - pf[i-1]
      if value == 0:
        return True
  return False
```

> Approch 3: using Carry forward `time`: O(N^2) `space`: constant
1. we can maintain the subarray sum by carrying the previous subarray sum
2. It cancels the pf sum requirement hence space will be constant.
   
```python
def subarrSum0(A):
  # create all subarray
  N = len(A)
  for i in range(N):
    subArrSum = 0 # which will carry the subarray Sum
    for j in range(i, N):
      subArrSum += A[j]
      # check if subArrSum is equal to Zero
      if subArrSum == 0:
        return True
  return False
```

> Approch 4: Using prefix sum with hashmap

```
sum(i,j) = 0
# means subarray from i to j = 0
# if we impliment prefixSum formula
pf[j] - pf[i-1] = 0
# Adding pf[i-1] in both sides
pf[j] - pf[i-1] + pf[i-1] = 0 + pf[i-1]
# After simplifing it
`pf[j] = pf[i-1]`
```

1. Hence, if we have element of prefixSum array appears more than once. they will make subarray = zero
2. Creating prefixsum array from array A
3. iterate the prefix sum array and insert each element in set and check if it already exist in set.

`time: ` O(N)
`space: ` O(N) because of using the set to store uniqe elements

```python
def subArrSum0(A):
  # create prefix sum array
  N = len(A)
  pf = []
  pf.append(A[0])
  for i in range(1, N):
    pf.append(pf[i-1]+A[i])
  # iterate over pf array and check if any appears more than 1
  pfElement = set()
  for i in range(N):
    if pf[i] in pfElement:
      return True
    else:
      pfElement.add(pf[i])
  return False
```

## Problem 4: subarray with sum is equal to k
given int [] A and int k.Find if any subarray exist with sum k

> approch 1: BF O(N^3)
1. going through all the subarray and check the subarray sum is equal to k

> approch 2: using prefixSum `time: ` O(N^2), `space: `O(N)
1. having prefixSum array of A
2. for every subarray get the sum from prefix sum in constant time
   
> approch 3: Carry forward techniqe: O(N^2)
1. going through all the subarray and maintaing the sum of subarray and carry forward it

> approch 4: using prefix sum with set: O(N) time and O(N) space
1. as we need to find sum(i,j) = k
2. we can use formula of prefix sum `pf[j] -k = pf[i-1]`
3. we will create prefix sum array from A
4. for every element check if output of the formula is present in set.

```
sum(i,j) = k
# if we apply prefixSum formula
pf[j] - pf[i-1] = k
# by adding  pf[i-1] in both sides
pf[j] - pf[i-1] + pf[i-1] = k + pf[i-1]
# after simplifying it
pf[j] = k +  pf[i-1]
# as we need find p[i-1], subtract k from both sides
pf[j] -k = k + pf[i-1] -k
# after simplifying it
pf[j] -k = pf[i-1]
```

```python
def subArrSumk(A):
  N = len(A)
  # creat prefix sum array
  pf = []
  pf.append(A[0])
  for i in range(1, N):
    pf.append(pf[i-1] + A[i])
  # iterate pf array and check if output is present in set
  pfElement = set()
  for i in range(N):
    b = pf[i] - k
    if b in pfElement:
      return True
    else:
      pfElement.add(pf[i])
  return False
```

> approch 5: using set only
1. as we can keep adding the each element into prefixSum variable and perform the required check

`time & space`: are same as above approch

```python
def subArrSumk(A):
  N = len(A)
  prefixSum = 0
  pfElement = set()
  for i in range(N):
    prefixSum += A[i]
    b = prefixSum - k
    if b in pfElement:
      return True
    else:
      pfElement.add(prefixSum)
  return False
```

## Problem 5: Count pair difference
Given int[] A, int B. Find count of pairs (i,j) such that `A[i]-A[j] = B & i!=j`

```
a - b = k
a - b + b = k + b # added b both sides
a = k+b # after simplified

A[i] = B + A[j] # to use to find the pair
```

```python
def countPairDif(A, B):
  hashMap = {}
  for a in A:
    hashMap[a] = hashMap.get(a, 0) +1
  ans = 0 # the number of pairs count
  for i in range(len(A)):
    b = A[i] + B
    if b in hashMap: # we have a pair that can be counted
      ans += hashMap[b]
    
  return ans
```

## Problem 6: count pair sum
given int[] A, int B. count the number of pair (i,j) such that `A[i]+ A[j] = B and i!=j`

```
a + b = k # we have k value and b
a + b - b = k - b # subtracting b from both sides
a = k - b

A[i] = B - A[j] # to find the pair that can make value B
```

```python
def countPairSumB(A, B):
  hm = {}
  ans = 0 # count of pairs
  for i in range(len(A)):
    b = B - A[i]
    if b in hm:
      ans += hm[b]
    # adding current into hm
    hm[A[i]] = hm.get(A[i], 0) +1
  return ans

```

## Problem 7: Largest subarray with sum zero
Given int [] A, and int B. Find the length of longest subarray length.

```                 
                    subarray with sum 0
------------|(sum)|---------------------|
----------------------------------------|(sum)
```

```python
def largSubarrLen(A):
  ans = 0 # length of maximum subarray
  s, e = -1, -1 # initial start and end index
  hm = {0: -1} # 0 to handle the case where subarray zero from the start
  curr_sum = 0 # to maintain prefix sum values
  for i in range(len(A)):
    curr_sum += A[i]
    if curr_sum in hm:
      s = hm[curr_sum] +1 # next index of the value
      e = i
      length = e - s +1 # length of subarray
      ans = max(ans, length)
    else: # if curr_sum is not present previously
      hm[curr_sum] = i
  return ans
```

`TC`: O(N)
`SC`: O(N)