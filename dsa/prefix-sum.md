# Prefix & Carry-forward array

## Prefix Sum Array

- Every index stores the sum of all elements in the array from start (0) till that index [i]
- PS[i] = sum of elements from [0] to [i]

**Usage**
- Range sum queries

## Problems
```
Given an array of size N & Q queries of the format s & e. Return the sum of elements from s to e
```

Original Array:
|0|1|2|3|4|5|6|7|8|9|
|-|-|-|-|-|-|-|-|-|-|
|-3|6|2|4|5|2|8|-9|3|1

Prefix Sum Array:
|0|1|2|3|4|5|6|7|8|9|
|-|-|-|-|-|-|-|-|-|-|
|-3|3|5|9|14|16|24|13|16|17

**Brute Force**:
- Iterate through queries
- Iterate through index in the queries and find sum of elements for each query

Time Complexity - O(QN)

**Optimized**:

```java
// creating prefix sum array
int[] PS = new int[A.length]
PS[0] = A[0]
for(i = 1; i < A.length; i++){
    PS[i] = PS[i-1] + A[i];
}

int[] result = new int[Q.length]
// 
for(i = 0; i < Q.length; i++){
    result[i] = PS[Q[i][1]] - PS[Q[i][0]-1]
}
```

Time Complexity: O(N+Q)
Space Complexity: O(N)

------------
`Directi`

```
Given an array. Return true if there exist an equilibrium index in the array. Equilibrium index is the index where sum of the all the elements on left side = sum of all the elements on right side.
```

**Brute Force**:
For every index, calculate sum of elements before and after the index. If both sum is equal, respective index is called as equilibrium index.


**Optimized**:
Using prefix sum array, for every index, find the sum of elements before and after the index. If both sum is equal, it is equilibrium index.


```java
// creating prefix sum array
int[] PS = new int[A.length]
PS[0] = A[0]
N = A.length
for(i = 1; i < N; i++){
    PS[i] = PS[i-1] + A[i];
}

for(i = 0; i < N; i++){
    sumOfLeft = PS[i]
    sumOfRight = PS[N-1] - PS[i]

    if(sumOfLeft == sumOfRight)
        return true;
}

```
Time Complexity: O(N)
Space Complexity: O(N)

--------

## Prefix Even Array

```
Given an  array of size N & Q queries (s,e). For every query, return count of even elements in the index range from s to e.
```
- Prepare prefix even array and do just like previous problem

```java
int[] PE = new int[A.length]
PE[0] = A[0]
for(i = 1; i < A.length; i++){
    if(A[i] % 2)
        PE[i] += PE[i-1]+1;
}

int[] result = new int[Q.length]
for(i = 0; i < Q.length; i++){
    result[i] = PS[Q[i][1]] - PS[Q[i][0]-1]
}
```




