

# Sliding Window Approach
Iterating over array in fixed size window

`Google` `Microsoft` `Facebook` `Amazon` `Uber`

Given an array A and a number K. Find sum of all subarrays of length K.


```java
int s = 0;
int e = K-1; // range of e : e[K-1,N-1]
int sum = 0;
while(e < N){
    sum = 0;

    for(int i = s; i <= e; i++){
        sum = sum + A[i];
    }

    System.out.println(sum);
    s++;
    e++;

}

```

Number of iterations: K(N-K+1)
if K = 1, Number of iterations = N
if K = N, Number of iterations = N
if K = N/2, Number of iterations = $N^2$
TC: O($N^2$)
SC: O(1)

**Using PS**

Number of iterations = N (Prefix Sum) + N-K+1 (Iterating over subarrays of K)

TC: is same as above
SC: O(N)

**Implementing Sliding Window Approach**

- Sliding two pointers in the array

1. Find the sum of first K elements in the array
2. Minus the leaving number and add the new incoming number.
3. Do 2 untill end of the array

```java
int sum =0;
for(int i =0; i < K; i++){
    sum = sum + A[i];
}

int s = 1;
int e = K;
while(e < N){
    sum = sum - A[s-1] + A[e];
    System.out.println(sum);
    s++;
    e--;
}

```
Total Iterations: K + N - K 
TC:O(N)
SC:O(1)

**Related Question**

Given an array A and a number K. Find max sum of all subarrays of length K.


Given an array A and a number K. Find min sum of all subarrays of length K.


Given an array A and a number K. Find average of every window of size K.

-----


`Amazon` `Media.net` 

Given an array of size N & a number B. Return the minimum number of swaps required to bring all elements less than or equals to B together.

| 1 | 12 | 10 | 3 | 14 | 10 | 5 |
|---|----|----|---|----|----|---|

Expected Output:

| 14 | 12 | 10 | 3 | 1 | 5 | 10 |
|----|----|----|---|---|---|----|

where 3,1,5 are together

B = 8

1. Count the number of elements less than or equal to B (for instance, 3)
2. Slide the fixed window and calculate minimum swaps (numbers in the window not less than or equal to B)

```java
// finding number of elements less than 8
int countUnderB = 0;
for(int i = 0; i < N; i++){
    if(A[i] <= B)
        countUnderB++;
}
s = 0;
e = countUnderB;

// calculate minimum number of swaps 
int noOfSwaps = 0;
for(int i = s; i < e; i++){
    if(A[i] > B)
        noOfSwaps++;
}

s = 1;
e = countUnderB + 1;
while(e < N){

    noOfSwaps = noOfSwaps - (A[s-1] <= 8 ? 1 : 0) + (A[e] <= 8 ? 1 : 0);
    s++;
    e++;
}
```

----

`Amazon` `Microsoft` `DPWorld`
Given a matrix of size N x N. Print it in spiral form.

1. Define row window and column window.
2. Iterate and print the elements in the window.
3. Decrease the window size after each spiral.

TC:O($N^2$)
SC:O(1)


