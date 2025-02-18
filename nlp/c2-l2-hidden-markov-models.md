# Part of Speech Tagging using Viterbi Algorithm

- Tagging a word to a part of speech for better contextualisation using Viterbi Algorithm
- Viterbi Algorithm is an optimization technique that used dynamic programming to break down bigger problems to smaller problems and utilises optimal solution of the mini problem to solve the whole one.

## Part of Speech Tagging

Why(adverb) not(adverb) learn(verb) something(noun)?(punctuation mark/sentence closer)


### Part of speech(POS) tags

| Lexical term | Tag | Example            |
|--------------|-----|--------------------|
| noun         | NN  | something, nothing |
| ver          | VB  | learn, study       |
| determiner   | DT  | the,a              |
| w-adverb     | WRB | why,where          |
| ...          | ... |                    |

For example, Why(WRB) not(RB) learn(VB) something(NN)?(.)

Part of speech of the next word depends on part of speech of previous word. For example, probability of noun word after verb word is higher than that of verb word.

**Applications POS tagging**
- POS tagging is used for named entities like Eiffel Tower
- It is used for coreference resolution i.e. Consider two sentences: Eiffel tower is in Paris, It is a tourist spot - Here `it` need to  be inferred to` Eiffel tower`
- Speech recognition

## Markov Chains
> Stochastic(randomness) model that describes sequence of possible events. It can be used to learn sequence of words.

- It takes only state of previous event to get the probability of next event.
- It can be depicted as directed graph. Directed graph is datastructure where different states are connected using directed arrow describing the flow.
 - States are mathematical depicted as $Q = \{q1,...,q_N\}$

## Markov Chains & POS tags
> Using markov chain to determine POS tag of next word

**Transition Probabilities**
> Considering POS tags as states, the probability that certain tag can occur next another tag is defined by `transitional probability`

**Transition matrix**
> Transition probabilities of more than POS tag can be tabulated - known as `transition matrix`

| #         | NN  | VB  | O   |
|-----------|-----|-----|-----|
| NN        | 0.2 | 0.2 | 0.6 |
| VB        | 0.4 | 0.3 | 0.3 |
| O(other)  | 0.2 | 0.3 | 0.5 | 

- Transition matrix is nxn matrix where n being the number of POS tags(states).
- Sum of all transitional probabilities in  a matrix is 1.

Why do we do about initial word where there is no previous word (such as beginning a sentence)? Initiate random probability known as $`\pi`$

| #         | NN  | VB  | O   |
|-----------|-----|-----|-----|
| $\pi$     | 0.4 | 0.1 | 0.5 |
| NN        | 0.2 | 0.2 | 0.6 |
| VB        | 0.4 | 0.3 | 0.3 |
| O(other)  | 0.2 | 0.3 | 0.5 | 

## Hidden Markov Models
> used to decode hidden statesof a word

- In our case, hidden states are just parts of speech of word.
- Hidden states also mean the states that are not directly observable.
- When machine counter text like jump, run, fly, it doesn't know it is verb. Those words are known `observables` and part of speech of the words are known as `hidden states`.

 Hidden Markov Model have an additional probabilities known as `emission probabilities`.

 **Emission probabilities**
 > describes transition from hidden states to the observables

 - For instance, consider observables for the hidden state VB are the words: going,to,eat and emission probability from the hidden state VB to the observable eat is 0.5. It means when the model is currently at the hidden state VB, there is 50% percentage chance that the observable the model will emit is the word, eat. 
 - There is emission probability for `n` hidden states to `m` words in the corpus - representing part of speech tag.
 - This can be represented in table known an `emission matrix`
  

| #         | going  | to  | eat   |...|
|-----------|--------|-----|-------|---|
| NN        | 0.5    | 0.1 | 0.02  |
| VB        | 0.3    | 0.1 | 0.5   |
| O(other)  | 0.3    | 0.5 | 0.68  | 

## Computing probabilities 

To calculate probabilities, you will only use part of speech tags used in your corpus.

1. Calculate occurrences of tag pairs.
   $$ C(t_{i-1}, t_i) $$
2. Calculate probabilities using the counts
   $$ P(t_i|t_{i-1}) = \frac{C(t_{i-1}, t_i)}{\sum_{j=1}^{N}C(t_{i-1}, t_j) }$$



### Preparation of the corpus
- Consider each line of the corpus as separate sentence.
- Add start token to each sentence to calculate initial probability.
- Transform all words to lowercase.

### Transition Matrix
> matrix describing probabilities between two pos tag

Consider the corpus,
```
<s> in(O) a(O) station(NN) of(O) the(O) metro(NN)
<s> the(O) apparition(NN) of(O) these(O) faces(NN) in(O) the(O) crowd(O)
<s> petals(NN) on(O) a(O) wet(NN), black(O) dough(NN)
```

**Calculating occurrences of tag pairs**
| #         | NN | VB| O|
|-----------|----|---|--|
| $\pi$     | 1  | 0 | 2|
| NN        | 0  | 0 | 6|
| VB        | 0  | 0 | 0|
| O(other)  | 6  | 0 | 8| 

**Calculating transition probabilities**

Note that in our case, probability of transition matrix will be 0 as probability of pos tag verb is 0 with this formula. This will affect training the model. So, we need to apply smoothing .

- Apply $\epsilon$ to numerator
- Apply $N + \epsilon$ to the denominator(where N is total number of POS tags.)
  $$ P(t_i|t_{i-1}) = \frac{C(t_{i-1}, t_i) + \epsilon}{\sum_{j=1}^{N}C(t_{i-1}, t_j) + N + \epsilon }$$

The transition matrix for the above corpus is:
| #         | NN      | VB     | O     | 
|-----------|---------|--------|-------|
| $\pi$     | 0.3333  | 0.0003 | 0.6663|
| NN        | 0.0001  | 0.0001 | 0.9996|
| VB        | 0.3333  | 0.3333 | 0.3333|
| O(other)  | 0.4285  | 0.0000 | 0.5713| 

### Emission matrix
> matrix describing probabilities between pos tag and the word.

Consider the same corpus,
```
<s> in(O) a(O) station(NN) of(O) the(O) metro(NN)
<s> the(O) apparition(NN) of(O) these(O) faces(NN) in(O) the(O) crowd(O)
<s> petals(NN) on(O) a(O) wet(NN), black(O) dough(NN)
```
**Calculating occurrences of tag and word pairs**
| #         | in | a |...|
|-----------|----|---|---|
| NN        | 0  | 0 | 0 |
| VB        | 0  | 0 | 0 |
| O(other)  | 2  | 0 | 0 | 

**Calculating emission probabilities**

$$ P(w_i|t_i) = \frac{C(t_i, w_i) + \epsilon}{\sum_{j=1}^{V}C(t_i, w_j) + N + \epsilon }$$

$$ P(w_i|t_i) = \frac{C(t_i, w_i) + \epsilon}{C(t_i) + N + \epsilon }$$

With  the above matrices, it is viable to predict part of speech tagging by looking up the corresponding row and column in the matrices


## Viterbi Algorithm


Let's consider with example:
```<s> i love to learn```
 
 For the above sentence, lets assume transition and emission matrix

Transition matrix:
| #         | NN      | VB     | O     | 
|-----------|---------|--------|-------|
| $\pi$     | 0  | 0 | 0.3|
| NN        | 0 | 0 | 0.2|
| VB        | 0  | 0| 0|
| O(other)  | 0.5  | 0.5 | 0| 

Emission Matrix:
| #         | i | love |to|learn|
|-----------|----|---|---|---|
| NN        | 0  | 0.1 | 0 | 0|
| VB        | 0  | 0.5 | 0 | 0|
| O(other)  | 0.5  | 0 | 0.4 | 0.2|

- From the $\pi$, highest probable POS tag is O i.e. 0.3. With the current state being O, the highest probable word for the tag is I i.e. 0.5. The combined probability is `0.2 * 0.5 = 0.15`
- With the current state being O, both VB and NN has equal probability w.r.t to transition matrix. But the combined probability of word `love` with POS tag `VB` is high i.e. 0.25.
- The next probable state from VB is O with the transition probability 0.2. This is the process of viterbi algorithm
- The total probability for this sequence of hidden states is 0.0003.

### Viterbi Algorithm steps
1. Initialization step
2. Forward pass
3. Backward pass

Viterbi algorithm use two auxiliary matrices:
- one holds the intermediate optimal probabilities and
- other stores indices of the visited states.

### Initialisation

In initialisation step, first column of two auxiliary matrices are initialised. 

Lets consider transition matrix as A, emission matrix as B and other two auxiliary matrices as C and D respectively. First column of both matrices are initialised as described below:

C matrix holds the intermediate optimal probabilities:
| #    | $w_1$   | $w_2$| ... | $w_k$ |
|------|---------|------|-----|-------|
| $t_1$|$C_{1,1}$|      |     |       |
| $t_2$|         |      |     |       |
| ...  |         |      |     |       |
| $t_n$|$C_{N,1}$|      |     |       |

$C_{i,1} = A_{i,1} * B_{i,index(w_1)}$

D matrix stores indices of the visited states:
| #    | $w_1$   | $w_2$| ... | $w_k$ |
|------|---------|------|-----|-------|
| $t_1$|$D_{1,1}$|      |     |       |
| $t_2$|         |      |     |       |
| ...  |         |      |     |       |
| $t_n$|$D_{N,1}$|      |     |       |

$D_{i,1} = 0$

### Forward Pass
> Forward update of the matrices` values

$C_{i,j} = \max_{k} C_{k,j-1} * A_{k,i} * B_{i,index(w_j)}$

$D_{i,j} = \argmax_{k} C_{k,j-1} * A_{k,i} * B_{i,index(w_j)}$

### Backward pass


