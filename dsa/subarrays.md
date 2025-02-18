# Subarrays

> Contiguous part of an array

- Single element within the array as well as whole array is a part of subarray 
- Empty subarray is also subarray but it is not considered so in competitive coding

------

Print all values of subarray from s to e


```java
void printSubarray(int[] arr, int s, int e){
    for(i = s;i <= e ; i++){
        print(i);
    }
}
```

TC: O(N)

-----

Print all subarrays of given array A.

```java

for(int s = 0; s < A.length; s++){
    for (int e = s; e < A.length; e++){
        printSubarray(A, s,e);
    }
}
```


TC: $O(N^3)$



`Amazon`
Print sum of all  subarrays of array A of size N.

**Brute Force**
- Iterate through every subarrays as said above

TC: $O(N^3)$
SC: O(1)


**Prefix Sum**
- Apply Prefix Sum Array technique in place of finding sum in range queries

```java

// Create Prefix Sum Array - PS
sum = 0
for(int s = 0; s < A.length; s++){
    for (int e = s; e < A.length; e++){
        if(s==0){
            sum += PS[0]
        } else {
            sum += (PS[e] - PS[s-1])
        }
    }
}

```

TC:$O(N^2)$
SC:$O(N)$

**Optimized**
- Without prefix sum array

```java
int sum = 0;
for(i = 0;i < A.length; i++){
    sum = 0;
    for(j=i; j < A.length; j++){
        sum = sum + A[j];
    }

}

```

TC: $O(N^2)$
SC: O(1)

----

Element at index i will be present in all sub arrays whose start >= i and end <= i

- mathematically, number of elements starting before i => |s| = (i+1)
- number of elements end after i => |e| = (N-i)


Element at index i will be present in (i+1) * (N-i) number of sub arrays

