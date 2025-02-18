# Matrices

Given a matrix of size N * M.. Print the sum of every row.

- For every row, iterate over the columns and save th sum

```java
void printRowSum(int A[][]){
    int N = A.length;
    int M = A[0].length;
    int sum = 0;

    for(int i = 0; i < N; i++){
        sum = 0;
        for(int j = 0; j < M; j++){
            sum += A[i][j];
        }
        System.out.println("Sum of row "+ i + ":" + sum);
    }

}
```

TC: O(N*M)
SC: O(1)

-------

Given  a sq. matrix of size N x N. Print the diagonal elements. (Left-top to Bottom-right)


```java
void printDiagonal(int A[][]){
    int N = A.length;

    for(int i = 0; i < N; i++){
        System.out.println(A[i][i])
    }
}
```

TC: O(N)
SC: O(1)

-----


Given a matrix of size NxN. Print all elements about the diagonal.

```java
int N = A.length;


for(int i = 0; i< N; i++){
    for(int j = i + 1; j<  N; j++){
        System.out.println(A[i][j])
    }
}
```

Number of Iterations: N(N-1)/2
TC: $O(N^2)$
SC: $O(1)$

-----

`Paytm` `ServiceNow`
Given a square matrix of size NxN. Convert it to its transpose.

```java

void transpose(int A[][]){
    int N = A.length

    for(int i = 0; i < N; i++){
        for(int j = i+1; j < N; j++){
            swap(A[i][j], A[j][i]);
        }
    }
}


```

TC: $O(N^2)$
SC: $O(1)$

-----

`Amazon` `Adobe` `Microsoft` `VMware`

Given a square matrix. Rotate the matrix by 90 degree in clockwise direction without using extra space i.e. SC: O(1)

1. Convert matrix into its transpose
2. Reverse each row of the matrix


Total TC: $O(N^2)$
SC: $O(1)$

----


















