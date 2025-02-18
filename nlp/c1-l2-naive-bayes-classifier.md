# Naive Bayes Classifier

## Probabilities

Consider corpus of tweets:

A -> Positive Tweet
$P(A) = P(Positive) = N_{pos}/N$
$P(Negative) = 1 - P(Positive)$

B -> Tweets contains word 'happy'
$P(B) = P(contains word 'happy') = N_{happy}/N $

## Bayes Rule

**Conditional Probabilities** - Probability of something given conditions i.e. probability of B given A happened.

Consider only the tweets those contains the word 'happy'.

P(Positive|contains word 'happy') = Probability of positive tweets given that it contains word 'happy'

$P(Positive|'happy') = P(Positive \cap 'happy') / P('happy')$

$P('happy'|Positive) = \frac{P('happy' \cap Positive)}{P(Positive)}$

But, 
$P(Positive \cap 'happy') = P('happy' \cap Positive)$

so, 
$P(Positive|'happy')  = P('happy'|Positive) \frac{P(Positive)}{P('happy')}$

Bayes Rule is:

$P(X|Y)  = P(Y|X) \frac{P(X)}{P(Y)}$

## Naive Bayes Rule

Consider two corpora - one for positive tweets and one for negative tweets.

1. Count occurence of word in positive corpus & negative corpus and tabulate
2. Calculate total counts in each corpus - called as $N_{class}$ for each corpus
3. Calculate conditional probability of each word by given class i.e. $P(w_i | N_{class} )$ and tabulate.
4. Words having same conditional probability value is insignificant others are necessary.

$$P(w_i|class) = \frac{freq(w_i|class)}{N_{class}}$$
where $N_{class}$ is frequency of all words in class

**Naive Bayes Inference for Binary Classification**

$$\prod_{i=1}^{m}\frac{P(w_i|pos)}{P(w_i|neg)}$$

where $w$ is set of $m$ words in tweet.

If the result is more than 1, it is positive otherwise its negative.

## Laplacian Smoothing

Sometimes, we need to calculate probability of word occurring after another word. For this we calculate, number of times two words occur together divided by the number of times first word appear alone. What if two words never show up together in training corpus - so the probability becomes zero. How to tackle? 

$$P(w_i|class) = \frac{freq(w_i|class) + 1}{N_{class} + V_{class}}$$

where $N_{class}$ is frequency of all words in class,
$V_{class}$ number of unique words in class

- +1 avoids 0
- $V_{class}$ normalizes/to account for +1

## Log Likelihood

### Ratio of Probabilities

Consider table of laplacian-smoothed conditional probabilities of each word

$$ratio(w_i) = \frac{P(w_i|Pos)}{P(w_i|Neg)}$$

ratio as:
- $\infty$ is positive
- 1 is neutral
- 0 is negative

Above can be known as sentiment of the words.

**Applying to Naive Bayes Inference for Binary Classification**

$$\frac{P(pos)}{P(neg)}\prod_{i=1}^{m}\frac{P(w_i|pos)}{P(w_i|neg)} > 1$$

where class $\exist$ {pos, neg}, w -> set of m words in a tweet
 
**Pros**
- A simple, fast, and powerful baseline
- probabilistic model used for classification

**Cons**
- Risk of underflow

it can be fixed by using below mathematical formula:

$log(a*b) = log(a) + log(b)$

Applying a and b:

$$log(\frac{P(pos)}{P(neg)}\prod_{i=1}^{m}\frac{P(w_i|pos)}{P(w_i|neg)}) = log(\frac{P(pos)}{P(neg)}) +  \sum_{i=1}^{m}log(\frac{P(w_i|pos)}{P(w_i|neg)}) $$

where $log(\frac{P(pos)}{P(neg)})$ is log prior, $\sum_{i=1}^{m}log(\frac{P(w_i|pos)}{P(w_i|neg)})$ is log likelihood.

## Training Naive Bayes Classifier

Steps:
1. Collect and annotate corpus
2. Preprocess
    - Lowercase
    - Remove punctuations, urls, names, stopwords.
    - Stem
    - Tokenize
3. Tabulate word count followed by conditional probabilities of words
4. Get lambda or log of the ratio of conditional probabilities
5. Get the log prior - $log(P(pos) / P(neg))$

    