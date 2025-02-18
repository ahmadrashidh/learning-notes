# Autocorrect
> application that suggests correct words for misspelled words

## Steps of autocorrection
1. Identify misspelled word
2. Find string that are `n` edit distance away
3. Filter candidates
4. Filter word probabilities corresponding to the context


### Identifying misspelled word
> simply, if the word is not in vocabulary, it is misspelled word

### Finding strings n edit distance away

Edits can be:
1. Insert (to: top, two, etc)
2. Delete (hat: ha, at, ht, etc)
3. Switch or swap adjacent letters (eta: eat, tea, etc)
4. Replace (jaw: jar, paw)

Edit distance just means number of edits can be made.

### Filtering candidates
> finding real words i.e. thats in the vocabulary.
Consider the above examples, ha,ht are not real world

### Calculating word probabilities
> find a word that is more probable to appear in the sentence

$$P(w) = \frac{C(w)}{V}$$
where P(w) is the probability of a word in a corpus,
C(w) is the frequency of the word in the corpus,
V is the size of the corpus.

## Minimum Edit Distance
> minimum number of edits needed to transform one word(source) to another(target)

**Applications**
- Spelling correction
- Document Similarity
- Machine Translation
- DNA Sequencing and more

For example, minimum edit distance between play and stay is 2.

replace: p -> s
replace: l -> t

### Edit cost
> Until now, we considered cost of all edits to be 1. In advanced cases, cost of each type of edit is different which alters the minimum edit distance.

For example, if cost of replace is 2, then minimum edit distance between play and stay is `2 + 2 = 4`

The algorithm is time consuming if the word is very long using brute force approach. The alternate way is using tabular approach along with dynamic programming.

## Minimum Edit Distance Algorithm using Dynamic Programming
 



 



 




