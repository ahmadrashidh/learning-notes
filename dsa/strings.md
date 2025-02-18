# Strings

- Computers work with character with identifying integers knows ASCII.
- 65 refers to 'A', 97 refers to 'a'

## Toggling case of characters in string

**Observation**
- Upper case alphabets are from 65 to 90
- Lower case alphabets are from 97 to 122
- 'A' is 32 characters before 'a'

**Arithmetic Approach**
- If its lowercase, subtract 32
- If its uppercase, add 32

```java
for(int i = 0; i < A.length; i++){
    if(A[i] >= 65 && A[i] <= 91){
        A[i] = A[i] + 32;
    } else {
        A[i] = A[i] - 32;
    }
}
```

TC:O(N)
SC:O(1)

**Bitwise Approach**

A = 65 = 1000001
a = 97 = 1100001

- Take XOR with $324$ or $2^5$ or $1 << 5$ to toggle case of character

```java
for(int i = 0; i < A.length; i++){
    A[i] = A[i] ^ 32;
}
```

-----


Given a character array with lowercase alphabets (may have duplicate), sort the characters in the array.

**Approach**
- An array of size 26 (0 as a, 25 as z) to store frequency of a letter in array to corresponding position.
- Nested ifs to find which character doesn't work, so subtracting character from 'a' will give index.

```java
int[] freq = new int[26];

for(int i = 0; i < A.length; i++ ){
    freq[A[i] - 'a']++;
}

// use freq array to generate sorted array
```

TC:O(N)
SC:O(1)

----

Given string which consists of words separated by _. Reverse the string word by word. No Extra Space.

S: love_hate_data_structure
Output: structure_data_hate_love

**Approach**
1. Reverse the whole string
2. Reverse each word in the string.

 





