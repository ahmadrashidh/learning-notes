# Bit Manipulations

## Number System

### Decimal
> Base 10

$0,1,2,3,4,5,6,7,8,9$

$
8734 = 8000 + 700 + 30 + 4 = (8 * 10^3) + (7 * 10^2) + (3 * 10^1) + (4 * 10^0)
$

### Octal
> Base 8

$0,1,2,3,4,5,6,7$

$
0132 = (0 * 8^3) + (1 * 8^2) + (3 * 8^1) + (2 * 8^0) = (90)_8
$

### Ternary
> Base 3

$0,1,2$

$
1120 = (1 * 3^3) + (1 * 3^2) + (2 * 3^1) + (0 * 3^0) = (42)_3
$

### Binary
> Base 2

$0,1$

$
10110 =  (1 * 2^4)+ (0 * 2^3) + (1 * 2^2) + (1 * 2^1) + (0 * 2^0) = (22)_2
$


### Decimal to Binary


| 2 | 28 | 0 |
|---|----|---|
| 2 | 14 | 0 |
| 2 | 7  | 1 |
| 2 | 3  | 1 |
| 2 | 1  | 1 |
|   | 0  |   |

$(28)_{10} = (11100)_2$



## Logical Operations

| Symbol | Gate        |
|--------|-------------|
| &      | AND         |
| \|     | OR          |
| ^      | XOR         |
| ~      | NOT         |
| <<     | LEFT-SHIFT  |
| >>     | RIGHT-SHIFT |

### Observations

**OR**
a | 1
- a + 1 if a is even
- a if a is odd

**AND**
a & 1
- 0 if a is even
- 1 if a is odd

**XOR**
a ^ 0 = a
a ^ a = 0

**LEFT-SHIFT**

Powers of 2:
$1 << 2 = 2^2 = 4$
$1 << 4 = 2^4 = 16$

Checking if i-th bit is set
N & (1 << i)
- $2^i$ if i-th bit iset
- 0 if not

N | (1 << i)
- N if i-th bit is set
- N + $2^i$ if not

Flipping i-th bit
N ^ (1 << i)


**Sample Problem**

`Amazon` `Microsoft` `Adobe` `Google` `Oyo` `Ola`

Given an array where all elements appear even times except only one. What is that element which appears odd number of times?

A: 2 | 8 | 3 | 1 | 2 | 2 | 3 | 2 | 8 | 1 | 1 | 8 | 8 | 100 | 100

2 ^ 2 = 0
2 ^ 2 ^ 1 = 1

**Approach**
- when all elements cancels out each other using XOR, odd numbered element stands out

2 ^ 8 ^ 3 ^ 1 ^ 2 ^ 2 ^ 3 ^ 2 ^ 8 ^ 1 ^ 1 ^ 8 ^ 8 ^ 100 ^ 100 = 1

```java
int ans = 0
for(int i = 0; i < A.length; i++){
    ans = ans ^ A[i];
}
```

TC:O(N)
SC:O(1)

----------

`Google` `Scaler` `CodeNations`

Given an array where every number appear twice except exactly two number. Find & return the two single number.

**HashMap Approach**
1. Add elements to Map with frequency
2. Return elements in 1 frequency

TC:O(N)
SC:O(N)

**Bit approach**

1. Find XOR of the complete array.
2. Find position of any set bit of array and XOR with elements which has set bit on that position that gives one number in the answer.
3. XOR with elements which has unset bit on that position, that gives another number.
(as S1 and S2 will different value at this point)

```java
// find xor of complete array
int xor = 0;
for(int i = 0; i < A.length; i++){
    xor ^= A[i];
}

// find set bit of the xor
int findSetBit(int number){
    int numberWithSetBit = 1;
    int i = 0;
    while(numberWithSetBit & number){
        numberWithSetBit = numberWithSetBit << i;
    }

    return numberWithSetBit;
}
```

TC:O(N)
SC:O(1)

-------

`Amazon` `Google`

Given an array where every number appear thrice except exactly one number. Find & return single number.          

Hint: Can we find if the ith bit in single number will be set or unset?   



--------

`Google`

Given an array of N non-negative integers. Calculate the sum of XOR of all possible pairs (i,j) such that (i,j) != (j,i)

A: 3|5|6|8






