```
| Smile Offten
| Think Positively
| Give Thanks
| Laugh Loudly
| Love Others
| Dream Big
```
Agenda:
1. Intro to hash mapping
2. Given Q quireis, find frequency of an element.
3. No. of distinct element.
4. Longest substring without repeat

Arryas:
Cons: we can not declare array with size more than 10^6 or 10^7
Pros: Quich access the element with thir index

HashMap:
HashSet:

### Problem 1:\
Given int[] A and int[] Q,
Find the frequency of elements in the Q in array A.

> Brutefource: O(N^2)
1. Iterate over the array Q and check if element count in array A with nested loop.

> Using HashMap
1. Store the frequency of elements of A O(N) in freqMap
2. iterate over Q and check the frequency in freqMap
`time`: O(N)
`space`: O(N) due to the space we use in freqMap

```python
freqMap = {} # to store the ele freq
for a in A:
  value = freqMap.get(a, 0)
  freqMap[a]  = value +1
N = len(Q)
ans = []
for i in range(N):
  value = freqMap.get(A[i], 0)
  ans.append(value)
return ans
```

### Problem 2: count of distinct elemetns
Given  int[] A return count of distinct elements.

> Using Hashmap:

> Using Set:

### Problem 3: Longest Substring without repeat
Given string A, find the longest substring that doest not have duplicate element

> BruteFource approch: 
1. going through all the substring of the A O(N^2)
2. Check if the substring has no duplicate O(N)
`time`: O(N^3), `space`: O(N) because of Set we use to count lengh of substring.

> Dynamic Sliding Window Approch:
1. Keeping i and j pointers.
2. move j and count the length of the current string.
3. if duplicate char is found, update the length to ans
4. reset i = j-1

```python
i = 0, j = 1
ansCount = 1
current_substring = Set()
while(j<N):
  if A[j] in current_substring:
    # then we have found the duplicte element
    length = (j-1) - i + 1
    ansCount = max(ansCount, length)
  else:
    current_substring.add(A[i])
ansCount = max(ansCount, ((j-1)  - 1+1))
```

### Problem: First non-repeating element
Given  int [] A. Find first non repeating element

??

### Distinct Numbers in Window int B
given intp[] A and int B. Find the elements count in all window B and return in array.

> Brute Fource:
1. going through each substring and if substirng length equal to B.
2. Count the distcint elements and add to ans array.
3. using Set to keep get count.

> Sliding Window approch: `time:` O(N) `space`: O(B)
1. iterate over first window and count the distcint elemnts count and update ans array.
2. while i = 1 < N-B+1, and j = B add and remove i-1 and add j element.
3. using hashmap or Set to keep the track of elements count.

```python
freqSet, ans = set(), []
for i in range(B):
  freqSet.add(A[i])
ans.append(len(freqSet))

i, j, d = 1, B, (N-B+1)
while(i<d):
  # remove i-1
  freqSet.remove(A[i-1])
  freqSet.add(A[j])
  ans.append(len(freqSet))
  i+=1
  j+=1
return ans
```

