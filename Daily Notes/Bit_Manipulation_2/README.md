# Class: 30 Sep 2024: Bit Manipulation 2

## Assigenets Summary

### Problem 1: Single Number II

Given int[] A, every ele is appearing thrice except 1 element. Find it.

> Brutefource approch:
> TC: O(N^2)
> SC: Constant space
1. Iterate the array A and for every element
2. check if it is repeating thrice by iterating the A again in innerloop.
3. if not return it

> sorting approch: TC: O(nlogn), SC: Constant time

> Hashmap approch: TC: Linear time, SC: Linear time

> Bitwise contribution techniqe: TC: , SC: Constant time
1. for every bit in the element, count the set bits
2. if the setbits count is multiple of 3 or not
3. if not means, uniqe element has this bit set. else unset
```python
A = [...]
N = len(A)
ans = 0
for i in ragne(32):
  setBitCount = 0
  for j in range(N):
    if (A[i]&(1<<i)) > 0 # bit is set
      setBitCount+=1
  if setBitCount % 3 != 0: # setbits multiple of 3
    # hence the answer is having 1 in this bit
    ans = ans | (1<<i)
return ans
```
### Problem 2 Single Number III
Given int[]A, two int appears only once, all other elements appears twice. Find the two elements

> Bit wise contribution techniqe: TC= O(32*N), SC=Constant
1. If the problem is solving the multiple of 2 we can use BITWISE XOR to elminate duplicate elements.
2. It will resulting with uniqe elements. We need to extract the two integers from the result.
3. we will make use of XOR property of SAME SAME PUPPY SAME, the result number bits 0 means both uniqe numbers has 1 or 0 in the bit index.
4. if bit is 1, then both values have different bits. Get the index of set bit.
5. split the array A into two groups setBitGroup and unSetBitGroup and XOR it.

```python
N = len(A)
xorOfAllEle = 0
for i in range(N):
  xorOfAllEle = xorOfAllEle ^ A[i]
indexOfSetBit = 0 # find the set bit index of xorOfAllEle
for i in range(32):
  if (xorOfAllEle & (1<<i)) > 0: # bit is set
    indexOfSetBit = i
    break
setBitGroup = 0
unSetBitGroup = 0
for i in range(N):
  if(A[i] & (1<<indexOfSetBit)) > 0: # bit is set
    setBitGroup = setBitGroup ^ A[i]
  else:
    unSetBitGroup = unsetBitGroup ^ A[i]
return [setBitGroup, unSetBitGroup]
```
## Problem 3: Sum of XOR of all pairs
Given int[] A. Find sum of bitwise XOR of all pairs in the A.

```math
Number of Pairs Can Be Formed By N integers = N(N-1)/2
```
> Bitwise contribution techniqe: TC=O(32*N), SC=Constant
1. Iterate over range 32, and for every element in array A
2. count the setBits and unsetBits counts
3. calculate the number of paris that ith bit contributes for by multipling both bits count.
4. Matintain the sum by adding (result * 2^i)
5. return sum

```python
N = len(A)
for i in range(32):
  setBits = 0
  unsetBits = 0
  for j in range(N):
    if (A[j] & (1<<i)) > 0: # set bit
      setBits +=1
    else:
      unsetBits +=1
  numOfPairs = setBits * unsetBits
  ans += (numOfPairs * (1<<i))
return ans
```
### Problem 4: Min XOR value
Given int[] A, find the pair of int, which has min XOR value.

> Sorting approch: TC: O(nlogn), SC: contant
1. Sort the array. Because the closer values only produce the pair with min XOR value.
2. Iterate over array A and find XOR of i and i+1 element
3. Maintain the min value in ans

```python
N = len(A)
for i in range(N-1):
  xorResult = A[i] ^ A[i+1]
  ans = min(ans, xorResult)
return ans
```
### Problem 5: Strange Equality
Given in A, Find X and Y
X = is the gratest number smaller than A, such that the sum of X and A equal to XOR of X and A
Y = is the Smallest number grater than A, such that the sum of Y and A equal to XOR of Y and A.
```
Relation Between Arithmatic Sum of A, B and Bitwise XOR of A, B
(A ^ B) = (A + B) + (2 * (A & B))
```
1. X<...A...>Y
2. Hence the condition we need to check is (X & A) == 0
3. Y = The Smallest number grater than A:
   1. Find the bits count of A
   2. (1<<count) provides the smallest number Grater than A

```Y
A = 5 => 
101 & 1000 = 0
Y = 1000 => 
```
4. X = The Gratest number smaller than A
   1. by unsetting the bits that are set and wise versa of A. provides the expected X
```X
A = 5 => 101
101 & 010 = 0
X = 010 = 2
```
```python
X = 0
Y = 0
N, bitsCount = A, 0 # count the bits in A
while(N > 0):
  bitsCount +=1
  N = (N>>1)
Y = (1<<bitsCount)
X = 0
for i in range(bitsCount):
  if (A & (1<<i)) == 0: # Bit is unset
    X = X | (1<<i)
return [X,Y]
```
### Problem 6: Subarray OR
Given int[] A.
The value of subarray is defined by Bitwise OR of all the element.
Return sum of all value of all subarray.

> Bitwise Operation approch: TC=O(32*N), SC=Constant

1. Find the number of subarray of A (totalSubarrayCount)
2. Iterate over range(32), and trawarse through A
3. Lets find the unset bits hence we can sum the set bits and add to ans
   1. For every element, count the unsetBits. Makesure to handle possible pairs if bits are continuous
   2. Suptract the unsetBitcount with totalSubarrayCount which we can multiply with (1<<i) = 2^i
4. add the each value into ans and return

```python
ans, N = 0, len(A)
totalSubarrayCount = (N(N+1))//2
for i in range(32):
  unsetBitCount = 0
  zeroscount=0
  for j in range(N):
    if (A[j] & (1<<i)) == 0: # bit is unset
      zeroscount += 1
    else: # bit is set
      unsetBitCount += (zeroscount *(zeroscount+1))//2
  unsetBitCount += (zeroscount *(zeroscount+1))//2
  setBits = (totalSubarrayCount - unsetBitCount)
  value = (setBits * (1<<i))
  ans += value
return ans
```
### Problem 7: Find Two Missing Numbers
Given int[] A, where all the ele are distinct and are in range [1, N+2]
Find the two numbers that are missing in array A

> By using Bitwise XOR: TC: O(N), SC=Constant
1.  Find XOR of all the element in A
2.  Find the xOR of all the element from 1 to N+2
3.  Keep them in X variable, we will have two distinct element in the result now.
4.  We need to extract the two number from X
5.  Find the first set bit index of X number, since XOR propertiy is 1^0 = 1. Means both missiong element has different bits in this index position.
6.  Find setBitGroup and unsetBitGroup in this index, from array A and [1,N+2]. Return [setBitGroup,unsetBitGroup] 