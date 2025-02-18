# Supervised ML & Sentiment Analysis

## Supervised ML
> Given input features X and labels Y, train and predict correct label on new data by reducing the cost of the prediction function.


## Sentiment Analysis
> to predict if a test is positive or negative. 

- Process raw tweets in the training sets and extract features
- Train classifier on the features and predict

### Vocabulary 

Tweets -> [tweet 1, tweet 2, tweet 3]
Vocabulary -> List of unique words from the list of tweets.

### Feature Extraction

For every tweet, create a feature vector that shows whether word in the vocabulary appears in the tweet

V = [I, am, happy, because, learning, NLP, ... , hated, the, movie]
Tweet = "I am happy learning"
Feature vector = [1,1,0,1,0, ... ,0,0,0]

In large dataset or large vocabulary, this representation of features will have small relative number of non-zero values called `sparse representation`

**Problem with sparse representation**

- In this representation, feature vector is the size of vocabulary i.e. `n = |V|` - with lot of insignificant feature i.e. 0
- In supervised ML, model will learn `n + 1` parameters. So, unnecessarily more training time and prediction time.

### Negative and Position Frequencies
> Using word counts as features

- Given a word, mark frequency of the word appearing in positive class or negative class.

Corpus
1. I am happy because I am learning NLP - Positive
2. I am happy - Positive
3. I am sad because I am not learning NLP - Negative
4. I am sad- Negative

V = [I, am, happy, because, learning NLP, sad, not]
PosFreq = [3,3,2,1,1,1,0,0]
NegFreq = [3,3,0,0,1,1,2,1]

In practice, above is coded as dictionary where key as word and frequency is values

### Feature as Frequencies

freqs: dictionary mapping from (word, class) to frequency

$X_m = [1, \sum_{w}freqs(w,1), \sum_{w}freqs(w,0)]$
where $X_m$ is the feature of a tweet

$freqs(w,1)$ is sum of positive frequencies

$freqs(w,0)$ is sum of negative frequencies

**Example**: Feature vector of the tweet "I am sad, I am not learning NLP"


$X_m = [1, 8, 11]$

## Preprocessing


1. Stop words and punctuation
2. Stemming

**Stop words and punctuation**

Stopwords and punctuation can be eliminated because it doesn't add any significance to sentiment analysis.

**Stemming**
> Transforming any word to its stem.

- Base stem of word tuning, tuned, tune is `tun`

## Putting all together

- Preprocess tweets
- Build frequencies dictionary
- Extract features and form matrix

## Logistic Regression

To make prediction of labels based on data, you use a function with some parameters to map your features to labels  - by minimizing cost function.

For logistic regression, this function is sigmoid function

$$h(x^i,\theta) = \frac{1}{1 + e^{-\theta^Tx^{(i)}}}$$



## Training

1. Initialize parameters
2. Predict - $h = h(X,\theta)$
3. Get gradient - $\nabla = \frac{1}{m}X^T(h-y)$
4. Update parameters - $\theta = \theta - \alpha\nabla$
5. Get Loss = $J(\theta)$
   
   
