# Recursion

Usecases of recursion in programming:
1. Merge Sort and Quick sort are recursive sorting algorithm
2. Tree, heap and graph are recursively implemented datastructure
3. Dynamic programming heavily dependent on recursion


## Steps to write recursive code

1. Assumption
2. Main logic - equation to solve bigger problem with smaller subproblem
3. Exit Condition - base condition to exit/stop the recursion

### Time Complexity

Simply, Time Complexity of recursive function = (Total number of function calls * time complexity of one function call) + (Time complexity of base operation)

TC = O(N)

**Recurrence Relation**

Time complexity of N function calls = Time of complexity of (N-1) functional call + Time complexity of Base operation

*Solving by Substitution method,*

$T(N) = T(N-1) + 1$<br />
$T(N)= [T(N-2) + 1] + 1 = T(N-2) + 2$  <br />
....<br />
Therefore after K steps, $T(N)= T(N-K) + K$ <br />

### Space Complexity

- Height of the recursive tree
  
------

## Fibanacci Series

| Index (N)    | 0 | 1 | 2 | 3 | 4 | 5 | 6  | 7  | 8  |
|--------------|---|---|---|---|---|---|----|----|----|
| Fibonacci No | 1 | 1 | 2 | 3 | 5 | 8 | 13 | 21 | 34 |

<br >

$Fibonacci(N) = Fibonacci(N-1) + Fibonacci(N-2)$

<br >

**Main Logic**:
```java
fibonacci(N-1) + fibonacci(N-2);
```
**Exit Condition**: iteration starts from N and decreases, so it must be greater than or equal to 1 at all times.

```java
int fibonacci(int N){
    if(N == 0 || N == 1)
        return 1;
    
    return fibonacci(N-1) + fibonacci(N-2);
}
```

**Time Complexity Computation**:

- Each function invoke other two function calls, so total number of function call  is $2^N$
- Calculating GP, $2(2^N - 1) = 2^{(N+1)} - 1 = O(2^N)$
- TC = Number of function call * TC of each function call
- TC = $O(2^N) * O(1)$
- aka Exponential Time Complexity


## Towe of Hanoi














