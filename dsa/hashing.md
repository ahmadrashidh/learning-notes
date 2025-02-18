# Hashing

## Searching Value
Given an array of size N & Q queries. In every query, we get a number K. Return true if K is present in the array

A: 3|15|6|2|7|8|1|9
Q: 1|13|27|9|3

**Brute Force Approach**
1. For every K in Query Q, iterate over the array A, and find if its there.

```java
boolean[] result = new result[Q.length]
for(int i = 0; i < Q.length; i++){
    for(int j = 0; j < A.length; j++){
        if(A[j] == Q[i])
            result[i] = true;
    }
}
```

TC:O(QN)
SC:O(N)

- Without changing the order, it is impossible to search K with lesser time-complexity. Lesser time-complexity can be achieved by changing the order of elements.
- Array datastructure is not suitable for searching a value.

**Set Approach**

Time Complexity of `Set.insert(x)` and `Set.contains(x)` is average O(1) but Space complexity is O(N).

1. Iterate over array A, and add all elements in Set.
2. Iterate over Queries Q, and find if K exists

TC: O(Q+N)
SC: O(N)

## Hash Set
> datastructure that stores only distinct elements

Given an array of size N. Count number of distinct elements in the array.

A: 7,3,2,1,3,7,0,5

**Bruteforce Approach**
1. For every element in the array, iterate the array to find if it has duplicate.

TC:O($N^2$)
SC:O(1)

**Set Approach**
1. Add elements in the array A to Set.
2. Result is the size of the Set as Set only stores distinct elements.

TC:O(1)
SC:O(N)

------------

`Microsoft` `Amazon` `Adobe`

Given an array of size N. Find the first non-repeating element in the array.

**Bruteforce Approach**
1. For every element, iterate through array to check if its repeating. If its repeating, continue the loop.
2. If its not repeating, it is the answer.

TC:O($N^2$)
SC:O(1)

**Set Approach**
1. Create two Sets S1 and S2
2. Add all elements in the array to Set S1.
3. For every element, add to S2 if its not present in S1., else in S2.
4. For every element, elements those present in S1 but not in Set 2 are non-repeating elements.

TC:O(N)
SC:O(N)
 
**Map Approach**
1. Add all elements to the Map with value as frequency initializing to 0.
2. If key is already present, increase the value.

TC:O(N)
SC:O(N)

## HashMap
> datastructure that stores key value pair where only entries with distinct keys are stored

`Amazon` `Microsoft` `Facebook` `Google`

Given an array of size N. Return true if there exist a subarray with sum = 0.

**Approach**
Using Prefix sum approach with slight understanding,

SUM[S,E] = PS[E] - PS[S-1]
if we need to find, SUM[S,E] = 0;
Then find, PS[E] = PS[S-1]

- Any query where PS[E] = PS[S-1] is subarray with sum  = 0;


**Variation of Problems**

1. Count of subarrays with sum 0
2. Max-length subarray with sum 0
3. Min-length subarray with sum 0
4. First subarray with smallest index with sum 0

TC:O($N^2$)
SC:O(N)

-------------

**2-Sum Problem**

`Facebook` `Google`

Given an array of size N and number K. Return true if there exists a pair of elements A[i] & A[j] such that A[i] + A[j] = K  and i!=j

A: |2|7|11|15|7|

K=18 -> True
K=14 -> True
K=22 -> True
K=30 -> True

**Bruteforce Approach**
1. Iterate over all elements in the array except itself.
2. Return true at chance you found one.

TC: O($N^2$)
SC: O(1)

**Optimized Approach**
K - A[i] = A[j]

- Iterate over array and add elements where K - A[i] is not found in array to Set if it doesn't exist there.
- In that way, if there is two element in the array that add up to K, it will cause duplicate in Set, so it is found out.

**Implementation**
1. Create a Set S1.
2. Iterate over array, check if it K - A[i] is present in Set.
3. If it isn't, add to Set
4. If it doesn't, pair is found.


```java
HashSet<Integer> tempSet = new HashSet<>();

for(int i = 0; i < A.length; i++){
    int aOfJ = K - A[i];
    if(tempSet.contains(aOfJ)){
        return true;
    }

    tempSet.add(A[i]);
}
```

TC:O(N)
SC:O(N)

------------

Given an array of size N and number K. Return true if there exists a pair of elements A[i] & A[j] such that A[i] - A[j] = K  and i < j.


**Bruteforce Approach**
1. Iterate over all elements in the array except itself.
2. Return true at chance you found one.

TC: O($N^2$)
SC: O(1)

**Optimized Approach**

A[i] = K + A[j]

- Iterate over array and check if K + A[j] exists in the Set, otherwise add it
- In that way, if there is two element in the array that add up to K, it will cause duplicate in Set, so it is found out.

**Implementation**
1. Create a Set S1.
2. Iterate over array, check if it K + the element is present in Set.
3. If it isn't, add to Set
4. If it doesn't, pair is found.

```java
HashSet<Integer> tempSet = new HashSet<>();

for(int i = 0; i < A.length; i++){
    int aOfJ = K + A[i];
    if(tempSet.contains(aOfJ)){
        return true;
    }

    tempSet.add(A[i]);
}
```

TC:O(N)
SC:O(N)

--------

`Google`

Given an array of size N. Return true if there exist a subarray with sum = K.

**Bruteforce** 
- Iterate over all subarrays, calculate sum and compare
TC:O($N^3$)
SC:O(1)
**Prefix Sum**
- Create a prefix sum array
- Iterate over subarray indexes
- Calculate sum and compare
TC: O($N^2$)
SC: O(N)
**Formula Approach**
- Create contribution formula
- Iterate over array, calculate contribution and total sum and compare
TC:O($N^2$)
SC:O(1)

----

`Facebook`

Given an array of size N & number K. Return an array containing the count of distinct elements in every window of size K.

A: |1|1|2|2|
K: 2

Output: |1|1|1|2|1|

**Bruteforce Approach**

1. Iterate through every subarray of window K, and
2. Compare each element in the window to find count of distinct elements

TC: O($N^3$)
SC: O(1)

**Set Approach**
1. Iterate every subarray of window K
2. Using sliding window approach, add elements in the Set.
3. Size of the set is the count of distinct elements

It is not correct solution as the middle elements in the window are not considered for count - because sliding-window approach and distinctness trait of Set. We need datastructure to keep track of frequency of all elements in the window.

**HashMap Approach**
1. Iterate every subarray of window K.
2. Using Sliding Window approach, add elements in the Map if it doesn't exist, update frequency if it does and remove if it doesn't
3. Record total frequency of elements in HashMap and record it as size.

```java
HashMap<Integer,Integer> countMap = new HashMap<>();

for(int i = 0; i < K; i++){
    countMap.put(A[i],1);
}

int s = 1;
int e  = K;
while(e < N){
    // leaving element
    int freq = countMap.get(A[s-1]) - 1;
    if(freq = 0){
        countMap.remove(A[s-1])
    } else {
        countMap.put(A[s-1], freq);
    }

    // incoming element
    if(countMap.contains(A[e])){
        countMap.put(A[e], countMap.get(A[e])+1);
    } else {
        countMap.put(A[e], 1);
    }
}
```
TC:O(N)
SC:O(N)

## Implementation of Hash

- Need for categorising the data based on key data.
- Therefore, need for function that categorise the data within specified key data

### Hash Function
> Functions that distribute data within limited range is known as Hash Function

- Example of Hash Function: Sin, Cos, Mod

Mod Hash function:
$f(x) = x \mod 10$

- A good hash function distributes elements across all buckets uniformly and avoid O(N) time complexity.
- A number is categorised/bucketed as per the output value of the Hash function for the input value.
- A same number passed into Hash Function will always give same output.
- Even if all the data is mapped to same category, the worst case time complexity is O(N).
- In Java 7, the elements of same bucket are arranged in Balance Binary Search Tree instead of array, so worst-case time-complexity is O(log N)
- 









