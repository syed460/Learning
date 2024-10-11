## Friday OCT 4 | DSA: Recursion 1

> A SMOOTH SEA NEVER MADE A SKILLED SAILOR

### Revision

### Recursion Intro
1. Function calling itself
2. Solving a problem by solving a subproblem using same logic

> Why Recursion:
1. It is required in BackTracing, DP, Trees, Grapsh
2. Sotring Alogrithm like 'Merge Sort' and 'Quick Sort' uses it.

### Example Problem 1
> Sum of first 5 natural numbers using recursion

`Idea`\
sum(5) = sum(4) + 5\
sum(N) = sum(N-1) + N

```python
def sum_(N):
  if N == 1:
    return 1
  return N + sum_(N-1)
```
> Steps to handle in Recursion:
1. Exceptation from the function
2. breaking problem into sub-problems
3. Handling Base case: how recursion has to stop
   
### Function Call Tracing
1. FILO
2. Child function returns ans to parent function
3. once the function return answer it is going to be removed from stack

### Time and Space Complexity of Recurtion funciton

**Time**: O(number of funciton calls * Time taken per function call)\
**Space**: O(number of function calls * Space taken per function calls)


### Problem 2: Factorial of N (N!)
Given int N return factoral of N

`Note`: 0! = 1 and 1! = 1 
`3! = 3*2*1 (multiplication of natural numbers)`

`Idea`:
fac(5) = fac(4) * N
fac(N) = fac(N-1) * N

```python
def fac(N):
  if N == 1:
    return 1
  return (fac(N-1) * N)
```
**Time Complexity:**\
T(N) = T(N-1) + 1
T(N-1) = T(N-2) + 2
T(N-k) = T(N-k) + K

T(0) = 1 => T(N-k) = T(0) => N-K = 0 => K=N
Hence,

=> T(N) = T(N-N) + N => **T(N) = N**

TC: O(N)

**Space Complexity:**\
N -> function calls happens\
constant time per function call\
=> N*1
=>O(N)

### Problem 3: Print 1 to N in increment order

inc(5) = inc(4) then print(N)
inc(N) = inc(N-1) then print(N)

```python
def inc(N):
  if N == 0:
    return
  inc(N-1)
  print(N)
```
### Problem 4: Wirlpool's countdown timer
Given int N, print it in decresing order until 0

dec(5) = print(N) then dec(5-1)
dec(N) = print(N) then dec(N-1)

```python
def dec(N):
  if N == 0:
    print(N)
  else:
    print(N)
    dec(N-1)
```

### Find Fibunachi Number of N
0,1,1,2,3,5,8,13,21...

fib(5) = fib(5-1) + fib(5-2)
fib(N) = fib(N-1) + fib(N-2)

```python
def fib(N):
  if N == 1:
    return 1
  if N == 0:
    return 0
  return fib(N-1) + fib(N-2)
```
Time Complexity:

                    fib(5) ------------------------------>2^0 = 1
              fib(4)  +   fib(3) ------------------------>2^1 = 2
        fib(3)  +   fib(2)          fib(2)    +  fib(1)-->2^2 = 4
    fib(2)+fib(1) fib(1)+fib(0)  fib(1)+fib(0) ---------->2^3 = 8

=> 2^0+2^1+2^3...+2^n
=> sum of this serise = a(r^n -1)/r-1 and n=(1+N)
=> 1(2^n -1)/1-1 => (2^n -1)
=> 2^N+1 -1 => **O(2^N)**

**Space Complexity:**
Number of function calls = N
space per funciton = 1
=> N+1 => **O(N)**