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
#### Problem 2: 
Given array A and int m. Find the count of pairs (i,j), such that (arr[i]+arr[j])%m = 0

Note:(arr[i]+arr[j])%m to be writen as `(arr[i]%m+arr[j]%m)%m ` 

> Brute force method: TC: O(N^2) SC: Constant
1. Iterate over array A with i and nested loop for j from i+1 to N.
2. find the 

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

