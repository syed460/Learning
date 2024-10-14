## Class: Monday OCT 7 | DSA: Recursion 2

### Agenta
1. Power Function
2. Print Array
3. All Indices
4. Check Palindrome

> What is Recursion:
1. A function that calls itself.
2. A function that solves the problem by bracking it into smaller sub-problems and calling itself.
3. Internal data structure used is STACK

> Factorial
1. 0! = 1

> Fibunachi Numbers
1. Nth Fibunatchi = Fn-1 + Fn-2
  
### Problem 1: Power Function
Given int a and n. Find a^2 using recursion

`Idea`:\
pow(2, 3) = 2 * 2 * 2
pow(2, 3) = 2 * pow(2, 2)
pow(a, n) = a * pow(a, n-1)

```python
def power(a, n):
  if n == 0: 
    return 1

  return a * power(a, n-1)
```
`Time Complexity:`:\
Number of function calls = N+1\
Time per function call = Constant\
=> O(N)
`space complexity`:\
Depath of the funciton calls = N\
Space per function = constant\
=> O(N)

## Method 2

`idea`: deviding the function calls by two\
if even, return power(a, n/2) * power(a, n/2)\
if odd, return a * power(a, n/2) * power(a, n/2)

```python
def power(a, n):
  if n == 0:
    return 1

  if ((n & 1) == 0): # even number
    return power(a, n//2) * power(a, n//2)
  else:
    return power(a, n//2) * power(a, n//2) * a

```
`Time Complexity`:

                 n   --------------2^0
             n/2       n/2---------2^1
         n/4   n/4   n/4  n/4------2^2
        0 0    0 0   0 0   0 0-----2^logN

2^0 + 2^1 + 2^3...2^logN (Geomatrically progression)
ratio = 2, First Term = a => 1,
Number of Term = [0, logN] => logN -0 +1 => logN+1
Sum of all the Term = a(r^# of terms - 1)/r-1\
Substitutions:\
=>  1(2^logN)/1-2 => 2^logN\

k = 2^logN, Apply logN in both side.\
log k = logN(2^logN) => logN => k = N `O(N)`
`Space Complexiy`: The Depth of the function calls = `O(logN)`

## Optimized Method:
```python
def power(a, n):
  if n == 0:
    return 1
  p = power(a, N//2)

  if ((n & 1) == 0): # even number
    return p * p
  else:
    return p * p * a

```
`Time complexity`:\
Number of function calls = logN
Time per function is Constant. Hence `O(logN)`\
`Space Complexity`: `O(logN)`

### Problem 2: Print Array using Recursion
Given int[] A, print all element.

`idea`: printAll(A, N) = printAll(A, N-1) then print(A[N])\
```python
def printAll(A, N):
  if N == 0:
    return
  printAll(A, N-1)
  print(A[N])
```
TC: O(N), SC: O(N)

### Problem 3: All indecies of Array
Given in[] A and target int B. Find the indicies of B and return them.

```python
def allIndices(A, B , idx, cnt):
  if N == idx:
    return [0]* cnt
  if A[idx] == B:
    arr = allIndices(A, B , idx+1, cnt+1)
    arr[cnt] = idx
    return arr
  if A[idx] != B:
    arr = allIndices(A, B, idx+1, cnt)
    return arr
```
TC: O(N)
Number of funciton calls = N+1 => O(N)\
SC: O(N)

### Problem 4: Palindrom or Not
Given String A, Check if A is palindrom or not

```python
def checkPalin(A, s, e):
  if s>e:
    return True
  if A[s] != A[e]:
    return False
  return checkPalin(A, s+1, e-1)
```
TC: O(N), SC: O(N)