## Wed OCT 9 | DSA: Maths: Moduler Arithmetic & GCD

### Agenda
1. Introduction & Properties of % wrt [+,-,* and power]
   1. Mod on power function
   2. Pair sum divisible by m
2. Find GCD(a,b)
   1. Properties of GCD
   2. GDD Optimizer code

#### Moduler Operation %
1. It gives the reminder
    (A % B) = to get the rminder of A/B
2. The output of the Moduler operation is going to be `0 to m-1` range only.
3. Moduler is used to restrict the output within the 0 to m-1 range.

> Addition with %
1. `(a+b) % M` can be opened as `((a%m) + (b%m)) % m`

> multiplication with %
1. `(a*b)%m` can be opend as `((a%m)*(b%m))%m`

> NOTE
1. `(a+m)%m` is equal to `(a%m)`

> Subtraction with %
1. `(a-b)%m` can be opend as `((a%m)-(b%m) + m) %m`
   1. Because the output of `((a%m)-(b%m)` can be -ve value hence adding m will keep the output +ve value.

> Power with %
1. `a^b %m` is equal to `(a%m)^b`

```
=> a*a*a*a..bth times
=> (a%m)*(a%m)*(a%m)...bith times
=> (a%m)^b
```

#### Problem 1: Fast power with mod 
perform the `a^n%m` using recursive

power(a,n) = power(a, n/2) * power(a, n/2)

```python
def power(a,n,m):
  if n==0:
    return 1
  p = power(a,n//2,m)
  if n%2 == 0:
    return (p%m)*(p%m)
  else:
    return (((a%m)*(p%m))%m)*(p%m)
```
#### Problem 2: Pair Sum Divisible By M
Given array A and int m. Find the count of pairs (i,j), such that (arr[i]+arr[j])%m = 0

Note:(arr[i]+arr[j])%m to be writen as `(arr[i]%m+arr[j]%m)%m ` 

> Brute force method: TC: O(N^2) SC: Constant
1. Iterate over array A with i and nested loop for j from i+1 to N.
2. if `(arr[i]%m+arr[j]%m)%m == 0` count++  

```python
count = 0
for i in range(N):
  for j in range(i+1, N):
    if (A[i]  %m+ A[j] %m)%m == 0:
      count+=1
return count
```
> Hasnmap method

> Optimized approch:
1. using the frequency map
2. As the moduler opertion output is range between 0 to m-1.
3. We perform modulo operation on each element in A and keep the track of frequency of each moduler output.
4. Handle the zerorth index and Middle index of feqArr using NCR formula to find the possible pairs

```math
ncr = n(n-1)/2
```

```python
ans = 0
N = len(A)
feqArr = [0]*m # to keep track of modulo output
for i in range(N):
  a = A[i]%m
  feqArr[a] += 1
# Handling Zeoro
ans += feqArr[0] * (feqArr[0]-1)//2
# handle middle value if m i even value
if m%2 == 0:
  ans += feqArr[m//2] * (feqArr[m//2]-1)//2
# handle the other values
i = 1, j= m-1
while(i<j):
  ans+= feqArr[i]* feqArr[j]
return ans
```
#### GCD | Greate Common Divisor | Hightest Common Factor

```math
GCD(a,b) = x
```
1. here x is the highest common factor for both a and b 

> Properties of GCD
1. GCD of -ve values, output will be +ve only
2. GCD(a,b) = GCD(b,a) [commutative_property]
3. GCD(0,b) = |b| [Obsolute_value_of_b]
4. GCD(a,b,c) = GCD(GCD(a,b),c), GCD(GCD(b,c),d), GCD(GCD(d,a),c) [Associative_Property]
5. if a,b > 0 and a>b
  `GCD(a,b) => GCD(a-b,b) => GCD(a%b,b) => GCD(b, a%b)`


```python
def gcd(a,b):
  if b == 0:
    return a
  return gcd(b, a%b)
```
`Time complexity`: O(log max(a,b))
`space Complexity`: O(log max(a,b))

### Find the greate common divisor of entier array
given int [] A

```python
a = A[0]
for i in range(1, N)
  b = A[i]
  a = gcd(a, b)
return a
```
`TC` = N*(log max(a,b))
`SC` = N


### Find if there is a pair that output to gcd(a,b) = 1

### Problem 1: Mod Sum 
Given int[] A, calculate sum of A[i]%A[j] for all possible i,j pairs and return it

> Brute fource `time` O(n^2)
1. Iterate over A with nested loop i and j, calculate and add it to sum

> Optimized approch: `time`: O(range^2), `space`: O(range)
1. Create freqArr for the range 1001
2. Iterate through the array and store the frequency of the elements in freqArray.
3. Iterate through the range 1 to 1001 with nested loop i and j
4. calculate i%j and multiply with freqArr[i] and freqArr[j] to get value for all the possible pairs
5. update ans

```python
freqArr = [0]*1001
N = len(A)
for ele in A:
  freqArr[ele]+=1
mod = 10**9+7
for i in range(1,1001):
  for j in range(1,1001):
    value = i%j
    temp = (value*freqArr[i]*freqArr[j])%mod
    ans = (ans%mod) * (temp%mod)
return ans
```

### Problem 2: A, B modulo C
Given int A and B, Find Greatest Possible Positive Int 'M'. Such that `A%M = B%M`

> Brute Fource: `time`: O(N) `space`: O(1)
1. Iterate from 1 to max(A, B) and check the condition and keep the max element in ans

> Optimized: `time` Constant
1. by looking at the examples, possible A & B are
```
A>B 
B> A
A = B means A = M

if A> B
B = B
B = A - A + B => A - (A - B)
B % (A- B) = (A - (A-B)) % (A-B) => A % (A-B) - (A-B) % (A-B)
B % (A- B) =>  A % (A-B)
B % m = A % m
m = A - B
if B> A
A = A
A = B - B + A => B - (B-A)
A % (B-A) = B % (B-A) - (B-A)% (B-A) 
A % (B-A) = B % (B-A)
A %m  = B % m
m  = B - A

Ans  m = abs(A - B)
```

### Problem 3: Delete one Elemenet to get max GCD of int [] A
Given int [] A. Delete one element such that the GCP of the all element remaining in array A is Maximum

> Brute Fource: O(N^2) `time`
1. Iterating throug array A and nested loop to calculate gcp of the array ignoring ith element.
2. maintaining max output

> Optimized approch (Using Prefix Sum):
1. if we remove ith element calculate gcd of left and right side of the i.
2. To have the left and right hand side elements GCD ready by using prefix Sum approch
3. calculate prefix and Suffix gcd of the array.
4. iterate through the array A and calucate left and right of ith element maintain the max GCD output.

```python
N = len(A)
# calculate GCD of the array in prefArr
prefArr = [0]*N
prefArr[0] = A[0]
for i in range(1, N):
  prefArr.append(gcd(prefArr[i-1], A[i]))
# calculate GCD of the array A in sufArr
sufArr = [0]*N
sufArr[N-1] = A[N-1]
for i in range(N-2, -1, -1): # in reverse order
  sufArr[i] = gcd(sufArr[i+1], A[i])
ans = 0*
for i in range(N):
  if i == 0:
    value = sufArr[i+1]
  elIf i == N-1:
    value = prefArr[i-1]
  else:
    value = gcd(prefArr[i-1], sufArr[i+1])
  if value > ans:
    ans = value
return ans
```
`time Complexity` = O(N * log max(a,b))
`space Complexity` = O(N)

#### problem 4: Divisor Game
Given A, B, C
Find number of X found in A, such that x%B = 0, x%C = 0 and that x is <= A.
1. do the prime factorization of A, B, C
2. Write the 1 to A numbers
3. from the examples, we can see the answer is LCM(B,C)

`Relation BetwenLCM & GCD`

```math
lcm(a,b) * gcd(a,b) = (a*b)\\
lcm(a,b) = (a*b)/gcd(a,b)
```

4. Find the GCD(B,C)
5. Find LCM(B,C)
6. we can see the output of LCM and its multiple are the one meets the condtion `x%B = 0, x%C = 0`.
7. Hence (A//LCM(a,b)) is the answer

```python
gcdValue = gcd(b,c)
lcmValue = (b*c)/gcdValue
ans = (A//lcmValue)
```
`Time`: O(log max(b,c))
`space`: O(log max(b,c))

#### problem 5: Larger Co-Prime Divisor
Given int A,B. Find number X such that A%X = 0, B%X=0 and gcd(x,b) = 1

`gcd(x,b) = 1` means x and b are co-prime having only one common factors

1. To solve this write down the prime factorization of A,B.
   1. Because prime factorization output are prime numbers, where ans x is a prime number too.
2. Buy elimiating the common factors we will be left with one value which is ans.
3. To achive this, we use A//gcd(a,b) untill we get output 1

```python
gcdValue = gcd(a,b)
while(gcdValue != 1):
  a = a//gcdValue
  gcdValue = gcd(a,b)
return a
```
`Time`: O(log max(a,b))
`space`: also same

