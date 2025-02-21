# Problems

Given an array of size N. Pick a total for B integers from the left to right with the maximum sum.

1. Sort Descending
2. Sum first B elements.


TC:O(nlogn)
SC:O(depends on Sorting algorithm)

----

**Alien's Dictionary**

Given an array of strings A, sort it based on alphabetical order given in String B

A: |hello|scaler|interviewbit|
B: abhbcfegskjlponmirqtxwuvy

**Approach**

1. Add character and their index to HashMap
2. Use custom comparator, use the index value from HashMap to compare strings instead of default ASCII values.

```java
HashMap<Character, Integer> alphabetSet = new HashMap<>();

for(int i = 0; i < B.length(); i++){
    alphabetSet.put(B.charAt(i), i);
}

Comparator<String> stringComparator = new Comparator<String>(){
    public int compare(String s1, String s2){
        int i = 0, j = 0;
        while( i < s1.length() && j < s2.length()){
            if(alphabetSet.get(s1[i]) < alphabetSet.get(s2[j])){
                return -1;
            } else if(alphabetSet.get(s1[i]) > alphabetSet.get(s2[j])){
                return 1;
            } else {
                i++,j++;
            }
        }
        i == s1.length() ? -1 : 1;
    }
}

Arrays.sort(A, stringComparator);
```
TC:O(NxM)
SC:O(1)

---------


**Kth Character**

Given N & K. Find Kth character in Nth row.
- Each row is generated by replacing all elements from previous row from 0 -> {0 1} & 1 -> {1 0}




