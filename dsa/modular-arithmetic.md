# Modular Arithmetic

## Intuition of Modulo

Dividend / Divisor = Quotient + Reminder<br />

Dividend = Divisor * Quotient + Reminder<br />

Dividend - (Divisor * Quotient) =  Reminder<br />

Divisor * Quotient => Largest multiple of divisor which is smaller than or equal to Dividend.

Dividend % Divisor = Reminder

**100 % 7**

100 / 7 = 14 + 2

100 = 7 * 14 + 2

100 - (14 * 7) = 2

So, 100 % 7 = 2

**-40% 9**

-40 - (largest multiple of 9 smaller than or equal to -40)

-40 - (-45)

= 5

So, -40 % 9 = 5

**-40 % 7**

-40 - (largest multiple of 7 smaller than or equal to -40)

-40 - (-42)

= 5

So, -40 % 7 = 2

--------

**a % m = [0,m-1]**

### Application of Modulo Operation

- Hash Maps, Hash Table
- Consistent Hashing
- Cryptography
- Blockchain (BitCoin)

## Modular Arithmetic Rules - I

(a + b) % M =((a % M ) + (b % M)) % M<br />
(a * b) % M =((a % M ) * (b % M)) % M<br />

controls overflow<br />

Implement a power function $pow(a,n,p) = (a^n) \mod p$

```java
int power(int a, int n, int p){
    int ans = 1;
    for(i = 1; i <= n; i++){
        ans = ((ans % p) * (a % p)) % p;
    }
    return ans % p;
}
```

TC:O(N)
SC:O(1)

### Divisibility Rules

**Divisible by 3** - if sum of the digits is divisible by 3, then the number is divisible by 3<br />
**Divisible by 4** - if last two digits of the number is divisible by 4, then the number is divisible by 4<br />


Given the number A is given in the form of array of size N. Given another number p, return A % p

```java
int ans = 0;
int n = A.length;
int tens = 1;
for(int i = n-1; i >= 0; i--){
    ans = (ans + (A[i]%p * tens)%p);
    tens = (tens * 10) % p;
}
```

TC:O(N)
SC:O(1)

--------

## Modular Arithmetic Rules - II

(a-b) % M = (a % M - b % M + M) % M<br />
M is added to avoid negative number<br />

`Amazon` `Adobe` `Oyo`

Given a number N. Count the number of trailing zeros in the number N! <br />



**Idea**
1. 0 depends on number of `2x5` in the N!
2. It is enough to calculate number of 5 present in the N!
3. It can be calculate by counting number of multiples of 5,25,125 etc in the N!

For 30,
number of multiples of 5 = 30/5 = 6
number of multiples of 25 = 30/25 = 1
number of multiples of 125 = 30/125 = 0

So, number of zeros is 7.

```java
int ans = 0;
int fives = 5;
while(N/fives!=0){
    ans += (N/fives);
    fives *= 5;
}

return ans;
```
Number of iterations: $log_5 N$
TC:O($logN$)
SC:O(1)

------

`Medianet`

Given N,M & N>M. Find the count of number A > 0 such that N % A = M % A

N % A = M % A
N % A - M % A = 0

N % A - M % A + A = A

(N % A - M % A + A) % A = A % A
(N % A - M % A + A) % A = 0 

from the above said, modular arithmetic rule
(N - M) % A = 0 

count of factors of N-M is the answer

TC:O($\sqrt{N}$)
SC:O(1)




























