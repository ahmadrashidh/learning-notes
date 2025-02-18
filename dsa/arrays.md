# Arrays


```
Given an array  of size N. Find number of elements that has atleast one element greater than itself
```
Brute Force Solution:
i. Find max. number
ii. Find count of max. numbers in the array, cmax
iii. N - cmax is the answer

Iterations = N + N + 1 = 2N + 1
TC = O(N)
SC = O(1)

PRACTICE: In One Loop

---------

```
Given an array of size N. Return true if there exists a per A[i], A[j] such that A[i] + A[j] = k where i != j. 
```

Brute Force Solution:
i. Check all pairs and compare the sum.
   
Iterations = $N^2$
TC = $O(N^2)$
SC = $O(1)$

Optimized Solution: 
i. Iterate through i and subsequent i+1 elements as pairs only

Iterations = N(N+1)/2
TC = $O(N^2)$
SC = $O(1)$
Same time complexity, but lesser iterations

---------

```
Given an array, reverse it using no extra space (or SC=O(1))
```

Solution:
i. Swap the element between two pointers - one from 0 and another from N-1 until i < j



Iterations = N/2
TC = $O(N)$
SC = $O(1)$

----------------

```
Given an array of size N, and two indices s and e. Reverse the elements of the array from index s to e
```

Iterations = (e - s + 1) / 2 = N / 2
TC = $O(N)$
SC = $O(1)$

-----------------

```
Given an array of size N and a number K. Rotate the array in clockwise direction [right to left] K times. (with SC=O(1))
```

Brute Force:
i. Reverse the whole array
ii. Reverse the first k elements
iii. Reverse the remaining elements

If the value of k can be more than N, number of rotations is N % K


Iterations = N/2 + K/2 + (N-K)/2 = N/2
Worst case is K can be N
TC = $O(NK)$
SC = $O(1)$


