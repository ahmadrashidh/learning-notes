# Sorting
> Arranging data in a specific order

**Built-in functions**
`sort()`
TC: O($NlogN$)
SC: Depends on Algorithm

---

## Understanding Sorting Problem

`Zomato` 

**Element Removal**

Given an array of N elements. Remove all elements one-by-one. Cost to remove one element is equal to sum of all the elements in the array before the removal. Find the minimum cost of removing all the elements from the array.

**Approach**
1. Sort the array in descending order
2. Iterate and remove as you calculate the cost

TC: O(NlogN)
SC: O(1)

----

**Noble Integer**

`Amazon` `Directi`

Given an array of size N having distinct elements. Count the number of nobile integers in that array.

`Noble Integer`: Count of elements smaller than it are equal to element itself.

**Approach**
1. Sort the array in ascending order
2. If number of elements before the number is same as it, it is noble integer

TC:O(NlogN)

*What if the elements are not distinct?*

- An subtitute array to track distinct

-------

**Noble Integer**

`Amazon` `Zeta`

Given N elements without repetition. Count the number of Noble Integers present in the array. Noble integers are integers in the array for which number of elements less than number is equal to number

**BruteForce Approach**
1. For every ith element, count number of elements less than ith element.
2. If count is less than ith element, it is counted as noble integer

TC:O($N^2$)
SC:O(1)

**Sorting Approach**
1. Sort the array
2. If the index of the ith element is equal to the number, it is noble integer.

```java
Array.sort(A);
int ans = 0;
for(int i =0; i < N; i++){
    if(A[i] >= i){
        ans++;
    }
}

return ans;
````

Given N elements with repetition. Count the number of Noble Integers present in the array.

1. Sort the array
2. If the index of the ith element is equal to the number, it is noble integer.
3. If the previous number is same and its noble integer, the ith element will also be noble integer

```java
Array.sort(A);
int ans = 0;
boolean isNobleInteger = false;
for(int i =0; i < N; i++){
    if(A[i] >= i){
        ans++;
        isNobleInteger = false;
    } else if(A[i] == A[i-1] && isNobleInteger) {
        ans++;
    }
}
```
TC:O(nlogn + n) = O(nlogn)
SC:O(depends on sorting algo)

------

Sort an array in ascending order based on the number of factors. If those number of factors are same, then sort by value.

The sorting can be customized with `Comparator` function. 

```java
Comparator<Integer> factorComparator = new Comparator<Integer>(){
                                public int compare(a,b){
                                    int f1 = countFactors(a);
                                    int f2 = countFactors(b);

                                    if(f1 < f2){
                                        return -1;
                                    } else if(f1 == f2){
                                        if(a < b){
                                            return -1;
                                        } else {
                                            return 1;
                                        }
                                    } else {
                                        return -1;
                                    }
                                }
                            }

Arrays.sort(A, factorComparator);
```



------

## Bubble Sort


**Approach**
- In every iteration, compare the consecutive elements and move the largest position to farthest position
- At max, N iterations

```java
for(int i = 0; i < N; i++){
    for(int j = 0; j < N-1; j++){
        if(A[j] > A[j+1]){
            swap(A[j],A[j+1])
        }
    }
}
```

where `A[j] > A[j+1]` is condition for ascending order

To facilitate code reusability of `sort()` function, you can use additional `compare()`

```java
void sort(int A[]){
    for(int i = 0; i < N; i++){
        for(int j = 0; j < N-1; j++){
            if(compare(A[j],A[j+1])){
                swap(A[j],A[j+1])
            }
        }
    }
}

boolean compare(int a, int b){
    if(a < b){
        return true;
    }

    return false;
}

```

- Java allows you to pass custom compare method to sort method.
- In custom comparator, return -1 to order a before b, 1 to order b before a, 0 if a and b are equals.

 







