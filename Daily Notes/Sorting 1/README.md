# Sorting 1: Count sort & Merge Sort

## Agenda:
1. Smallest Number
2. Merge two sorted arrays
3. merge sort

## count sort
Find the smallest Number that can be formed by rearranging the digits of the given numbers in array.Return the smallest number in the form of an array.

Approch 1: BF nlogn time
1. sorting the array and returning it in assending order

sorting the array taks nlogn time

Approch 2: using array
1. Creating the frequency array with 0 to length of the digits possible.
   1. 0 to 9 array
   2. 1 to 26 for ABC..
   3. (max - min + 1)
2. updte the array or create one with sorted array from frequency

`Time` O(N)
`space` O(N) because of storing the frequency in an array


```python
def countSortApproch(A):
  # creating freq array
  N = len(A)
  freqArr = [0]*10 # 0 to 9
  for a in A:
    freqArr[a]+=1 
  # iterate over freqArr and update original array A
  M = len(freqArr)
  k = 0
  for i in range(M):
    # i = 0....9
    value = freqArr[i]
    if value > 0:
      while (k < value):
        A[k] = value
        k+=1
  return A
```
`Note:` If the constrain says the element can be more than 10^6 the cont sort is not suitable. As we can not create array more than 10^6 or 10^7 due to the memory utilzation
```
int = 4 bytes
10^6 = 4 MB
10^9 = 4 GB
```
### handling -ve numbers in count sort
A = [-2 3 8 3 -2 3]

1. get the min and max of the array A
2. create freqArr of (max-min+1) length

```python
def countSortOptimized(A):
  # know min and max of A
  min_ele = float(inf)
  max_ele = float(-inf)
  for a in A:
    if min_ele > a:
      min_ele = a
    if max_ele < a:
      max_ele = a
  length = max_ele-min_ele+1
  freqArr = [0]*(length)
  # update the freq array
  for a in A:
    index = a-(min_ele) # get the proper index number for -ve values
    freqArr[index] += 1
  # update te sorted array 
  k = 0
  for i in range(length):
    element = i + min_ele # element
    count = freqArr[i] # element frequency
    if count > 0:
      while(k<count):
        A[k] = element
        k+=1
  return A
```

`time` O( element range)
`space`: O(element range)

## Merge two sorted array
Given two sorted array A and B, merge them and return one array
A = [2 4 7 8 12]
B = [3 5 6 7]

> Approch 1: using the count sort, which only can hanle 10^6 or 7 of 0 <= A[i] <= 10^7=6

> Approch 2: two pointer approch
1. using two pointers one on A[i] and another on B[j] iterate over the both array at a time and create new output array.


```python
def mergeTwoArray(A, B):
  # Create array of size A+B length
  N, M = len(A), len(B)
  ans = [0] * (N+M)
  # iterate over A & B, update smaller value
  i, j, k = 0, 0, 0
  while (i<N and j<M):
    if A[i] <= B[j]:
      ans[k] = A[i]
      i+=1
    else:
      ans[k] = B[j]
      j+=1
    k+=1
  # iterate over A & B seperately if remaing is there
  while (i<N):
    ans[k] = A[i]
    i+=1
    k+=1
  while(j<M):
    ans[k] = B[j]
    j+=1
    k+=1
  return ans  
```

`time`: O(N+M) Because we are vising each element on time
`space: ` O(N+M)

## Merge Sort
Uses devide, conquer, combine points
Uses recursion

Teacher correcting student papers by dividing it into two and assigning the task to two other teachers example

`time: ` 
number function calls + time per function
1. every time we devide the N by 2, hence, 
```
N + N/2 + N/4... N/k
means,
2^0+2^1+2^2+...2^k
1. sum of all this serese = logN
2. base funciton taks: constant time
3. every level taks N iterations to merge the two array
Hence the time complexity = O(N logN)
```

`space: `
```
Depth of function calls + space per function
1. depth of function calls = logN
2. space per funciton = N
O(logN + N)
```

```python
# A = array
# l = left index
# r = right index
def mergeSort(A,l,r):
  if l == r:
    return # base case
  middle = (l+r)/2
  # sort the left to mid array
  mergeSort(A, l, middle)
  # sort the mid+1 to end of array
  mergeSort(A, middle+1, r)
  # sort the two parts and update A
  mergeTwoArray(A, l, middle, r)
  return A

def mergeTwoArray(A, l, middle, r):
  # create two arrays
  P = A[l:middle+1]
  Q = B[middle+1:r+1]
  # itterate P and Q with two pointers and update A
  i, j, k = 0, 0, l # k starts from l
  while(i<N and j<M):
    if P[i]<= Q[j]:
      A[k] = P[i]
      i+=1
    else:
      A[k] = Q[j]
      j+=1
    k+=1
  # update A with the remaining element in P
  while(i<N):
    A[k] = P[i]
    i+=1
    k+=1
  # update A with the remaining element in Q
  while(j<M):
    A[k] = Q[j]
    j+=1
    k+=1
  return A
```

### stable sort
when the order of same element in array not changed

### un-stable sort
when the order of same element in array gets changed

Merge sort is un-stable sort if we use P[i] < Q[j]
Merge sort is stable sort if we use P[i] <= Q[j]

### in-place sort
When a algo do not take extra space apart from the stack space.

Merge sort is not in-place sort as we are using P and Q temprarily to store the array elements

### sort subarray with left to right index
Given int[]A, int B and C

> Using merge Sort:
1. we can use mergeSort to perform the sorting between two indicies

```python
def mergeSort(A, l, r):
  if l==r:
    return A
  m = (l+r)//2 # Dividing the array by halfe
  # handle the left part of array
  mergeSort(A, l, m)
  # handle the right part of the array
  mergeSort(A, m+1, r)
  # sort both the sides by sorting
  merge(A, l, m, r)
  return A

def merge(A, l, m, r):
  P = A[l:m+1]
  Q = A[m+1:r+1]
  N, M = len(P), len(Q)
  i, j, k = 0, 0, l
  while(i<N and j<M):
    if P[i] <= Q[j]:
      A[k] = P[i]
      i+=1
    else:
      A[k] = Q[j]
      j+=1
    k+=1
  while(i<N):
    A[k] = P[i]
    i+=1
    k+=1
  while(j<M):
    A[k] = Q[j]
    j+=1
    k+=1
  return A
```

TC: NlogN
recursion time complexity calculation:
number of function calls = nlogn
Time taken per function = N iteration in each level of function calls

SC: NlogN
depth of the funciton calls = NlogN
space taken per funciton = N lengh of space is taken in every level

### max chunk to make sorted
Given an array of integers A of size N that is a permutation of [0, 1, 2, ..., (N-1)], if we split the array into some number of "chunks" (partitions), and individually sort each chunk. After concatenating them in order of splitting, the result equals the sorted array.

What is the most number of chunks we could have made?

To find the chunk that can be sperated from array.
1. from the array starting every time we meet i = max element that found till now, increase the count
2. the total count is answer

```python
def maxChunkNumber(A):
  N = len(A)
  ma = 0 # to maintain the max element found
  ans = 0 # to maintain num of chunks possible
  for i in range(N):
    ma = max(ma, A[i])
    if ma == i:
      # found the possible sub array
      ans += 1 # increment the ans count
  return ans
```

