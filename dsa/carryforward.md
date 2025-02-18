# Carry forward

`Amazon`
```
Given a string of lowercase alphabets. Return count of (i,j) such that i < j, S[i] -> 'a', S[j] -> 'g'
```
S: 
|a|b|e|g|a|g|
|-|-|-|-|-|-|

**Brute Force**
For every element at i, iterate j and find if S[i] is while S[j] is g
```java

int ans = 0;
for(int i = 0; i < A.length; i++){
    if(A[i] == 'a'){
        for(int j = i + 1; j < A.length; j++){
            if(A[j] == 'g'){
                ans++;
            }
        }
    }  
}
```
Time Complexity: $O(N^2)$


**Optimized**
For every g, how many a's are before it

Iteration:
|S|a|b|e|g|a|g|
|-|-|-|-|-|-|-|
|number of a's|1|1|1|1|2|2|
|Ans|0|0|0|1|3|3|


```java
int ans = 0
int countOfAs = 0
for(int i = 0; i < S.length(); i++){

    if(S[i] == 'a'){
        countOfAs = countOfAs + 1;
    } else if(S[i] == 'g'){
        ans = ans + countOfAs; 
    } 
}
```

TC: O(N)
SC: O(1)

-------

## Sub Arrays
any contiguous part of an array within an array

How many sub-arrays is there in array of size N?

Count of sub-arrays from index 0 - N
Count of sub-arrays from index 1 - N - 1
Count of sub-arrays from index 2 - N - 2 and so on
so adding all(arithmetic progression),

Sub-arrays in an array = N(N+1)/2



`Amazon` `Zeta`

Given an array. Return the length of smallest subarray which contains both maximum and minimum of the array.

|0|1|2|3|4|5|6|7|8|9|
|-|-|-|-|-|-|-|-|-|-|
|1|2|3|1|3|4|6|4|6|3|

Array max = 6
Array min = 1

Subarray = (3,6)

|0|1|2|3|4|5|6|7|8|9|10|
|-|-|-|-|-|-|-|-|-|-|-|
|2|2|6|4|5|1|5|2|6|4|1|

Array max = 6
Array min = 1

Sub-array = (8,10)

**Solution**
- Find min and max
- Iterate tracking last min index and last max index and find the smallest gap

```java
// find min and max in the array

int lastMinInd = -1;
int lastMaxInd = -1;

for(int i =0; i < A.length; i++){
    if(A[i] == min){
        lastMinInd = i;
        if(lastMaxInd >= 0){
            ans = Math.min(ans, i - lastMaxInd + 1);
        }
    } else if(A[i] == max){
        lastMaxInd = i;
        if(lastMinInd >= 0){
            ans = Math.min(ans, i - lastMinInd + 1);
        }
    }
}
```

-------
Given an array, , count the no. of leaders. Leader - An element that is greater than all the elements on the left side. A[i] > [0,i-1]

|0|1|2|3|4|5|
|-|-|-|-|-|-|
|2|5|3|4|17|16|

Leaders are 2,5,17.
Count is 3

**Brute Force**
1. Iterate through each element in the array
2. For every element, iterate elements in the left to check whether there is any larger elements
3. Else, count it.

TC: $O(N^2)$

**Optimized**

```java
int max = Integer.MIN_VALUE;
int count = 0;

for(int number : A){
    if(number > max){
        max = number;
        count++;
    }  
}
```


TC: $O(N)$
SC: O(1)
