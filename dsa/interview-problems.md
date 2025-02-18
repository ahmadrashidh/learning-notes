# Interview Problems - Arrays

`Amazon` `Microsoft` `Adobe` `etc`

Given an array of 1 & 0. We can replace one of the 0 with 1. Return the count of maximum consecutive 1s in the array

A: 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 1 |

Output: 6

**Brute Force**
1. Find 0 in the array and count the number of consecutive 1s on the either side of the 0.
2. Count the maximum count.

```java
// find number of 1s
for(int i = 0; i < N; i++){
    if(A[i] == 0)
        countOf1s++;
}

// for edge case if all elements are 1
if(countOf1s == A.length)
    return countOf1s;

int z = 0;
int maxCount = 0;
while(z < N && A[z] == 0){
    int count = 1;
    int l = z-1;
    while(A[i] == 1){
        i++;
        count++;
    }

    i = z+1;
    while(A[i] == 1){
        i++;
        count++;
    }

    if(count > maxCount)
        maxCount = count;


    z++;
    
}

return maxCount;
```
Number of Iterations:N (iterating 1s) + N (find 0) + N (iterating 1 on either side)
TC:O(N)
SC:O(1)

------

`Amazon` `Directi` `Microsoft` `Adobe`

Given an array of 1 & 0. We can swap one of the 0 with 1. Return the count of maximum consecutive 1s in the array

A: 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 1 |

Output: 6

**Brute Force**
1. Find 0 in the array and count the number of consecutive 1s on the either side of the 0.
2. If the count of 1s is equal to total 1s, there is no 1 to swap. If its valid count.
3. Calculate the maximum count

---------


`Amazon` `VMware`

**Number of Triples**

Given an array. Count the number of triplets i,j,k such that i < j < k & A[i] < A[j] < A[k]

A: 2 | 6 | 9 | 4 | 10

**Brute Force**
1. Iterate over all possible triplets by nested iteration

TC: O($N^3$)
SC: O(1)

**Observation**

- A element will be in triplet, if it has smaller number before its index and larger number after its index.
- Number of triplet it exist in middle is number of smaller number before it multiplied by number of larger number after it.

Number of times element is in triplet =  number of smaller numbers before it * number of larger numbers after it.

**Approach using Carry Forward**
1. Iterate from index 0 to N-1, find the number of elements smaller on left of every element.
2. Iterate from index N-1 to 0, find the number of elements greater on right of every element.
3. Number of triplets can be counted by summing the product of element in triplet.

**Implementation**
```java
int[] smallerBeforeIt = new int[A.length];
int[] largerAfterIt = new int[A.length];
int N  = A.length;

// finding number of smaller element before every element
smallerBeforeIt[0] = 0;
for(int i = 1; i < N; i++){
    if(A[i] > A[i-1])
        smallerBeforeIt[i] = smallerBeforeIt[i-1] + 1;
}

// finding number of larger element before every element
largerAfterIt[N-1] = 0;
for(int i = N-2; i >= 0; i--){
    if(A[i] > A[i+1])
        largerAfterIt[i] = largerAfterIt[i+1] + 1;
}

int numOfTriplets = 0;
for(int i =0; i < N; i++){
    numOfTriplets += smallerBeforeIt[i] + largerAfterIt[i];
}
```

TC:O(N)
SC:O(N)

------

**Josephus Problem**

- K is Nearest Power of N
- Ans is 1 + N=K * 2

------

`Google` `Directi` `CodeNatives`

Given an array of size N and Q queries of s & e. For every query, return the sum of all even indexed elements in the range from s to e.

**Approach**
1. Create Prefix Sum of the array with only even indexed elements
2. For every query, subtract from prefix sum array of corresponding e index from s-1 index.

```java
int N = Q.length;

// create prefix sum array PS
int[] sum = new int[N];
for(int i = 0; i < M; i++){
    if(Q[i][0]-1 == 0){
        sum[i] = PS[Q[i][0]]
    } else {
        sum[i] = PS[Q[i][1]]  - PS[Q[i][0]-1]
    }
}
```

TC:O(N)
SC:O(N)

-----

`Google` `CodeNations` `Directi` `JPMorgan`

Given an array. Count the numbers of special index in the array. Special Index, after removing which index, sum of even-indexed elements == sum of odd-indexed elements.

A: 4 | 3 | 2 | 7 | 6 | -2

**Approach**
1. Calculate two prefix sum array - one for even-indexed elements $PS_e$ and one for odd-indexed elements $PS_o$
2. Iterate over array, check if sum of odd-indexed elements and sum of even-indexed elements equals if element at current index is removed.
3. Consider when element at current index is removed, the elements after index shifts place such sum of even-indexed become sum of odd-indexed and vice versa.

After removal of index i,

$S_E = S_e[0,i-1] + S_o[i+1, N-1]$
$S_O = S_o[0,i-1] + S_e[i+1, N-1]$

$S_e[0,i-1] = PS_e[i-1]$
$S_o[0,i-1] = PS_o[i-1]$

$S_o[i+1, N-1] = PS_o[N-1] - PS_o[i]$
$S_e[i+1, N-1] = PS_e[N-1] - PS_e[i]$

TC:O(N)
SC:O(N)

------

`Google` `Facebook`

**Majority Element**

Given an array of +ve members. Return if there exists an element with frequency > N/2 (N is length of the array). Condition: SC must be O(1).

A: | 1 | 6 | 1 | 1 | 2 | 1 |
N = 6, |ME| = 3

Output: 1

A: | 3 | 4 | 3 | 6 | 1 | 3 | 2 | 5 | 3 | 3 | 3 |
N = 11, |ME| = 5

Output: 3

A: | 4 | 6 | 5 | 3 | 4 | 5 | 6 | 4 | 4 | 4 |
N = 10, |ME| > 5

Output: -1

**Observation**
- There can be only one majority element
- If we remove two distinct element from array, finally, only majority element remains.


This algorithm is known as `Moore Volting Algorithm`
-----


Given an array of positive numbers. Return if there exists an element with frequency > N/3







