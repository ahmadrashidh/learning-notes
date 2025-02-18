# Word Embeddings Neural Networks

**Applications of word embeddings**:
- Semantic anologies and similarity
- Sentiment Analysis
- Machine Translation
- Information Extraction
- Question Answering
  
**Learning Objectives**
- Key concepts of word representations
- Generate Word Embeddings
- Prepare text for machine learning
- Implement continuous Bag-of-words model

## Basic Word Representation
> building matrix to represent all the words in the vocabulary

**Integers**
> Assigning unique integer to each word in the vocabulary

Pros:
+ simple

Cons:
- Ordering doesn't make sense
- Why head has to be denoted with less integer than happy or vice versa

**One-hot vectors**
> encode bit corresponding to word 1 out of V elements vector akin to V word in the vocabulary

Pros:
+ simple
+ no implied ordering
Cons:
- huge vectors
- no embedded meaning

**Word Embedding Vectors**
> Way of encoding words into lower dimension (i.e. <V)

Consider a real number line:
-  words are represented with the negative number amounting to their negativity. Likewise, positive number for positivity - along the number line.
- This can be extended by adding another vertical real number line. Word more concrete are on positive side while more abstract on their negative side. 

Pros:
+ Low dimension
+ Embed meaning e.g. semantic, analogies

## Word Embedding Process

To work embed, we need two things:
1. Corpus (esp. words in context)
   - Shakespeare corpus are very limited
   - General purpose (e.g. Wikipedia)
   - Specialized (e.g. contract books, law books)
2. Embedding method
   - Self-supervised Machine Learning Model (e.g. learning task to find a word based on surrounding words)
   - One of the important hyperparameter is `word embedding size`

### Word Embedding Methods

1. word2vec(Google,2013)
   - Uses Shallow NN to learn word embeddings
   - Proposes two archs - Continuous Bag-of-word model(CBOW) & Continuous skip-gram/skip-gram with negative sampling (SGNS)
2. Global Vectors or GloVe(Stanford,2013)
   - close to Vertibi algorithm
3. fastText (Meta,2016)
   - Based on skip-gram
   - Supports out-of-vocabulary(OOV) words i.e. synthesize new words based on similar words in the vocabulary.
   - Word embeddigs could be added together for phrase representations

**Advanced Methods**
> Uses Advanced Deep Learning to refine word meanins according to their context 

That is, same words assume different embedding based on their meaning e.g. plant as biological plant, plant as industry

1. BERT (Google,2018)
2. ELMo (Allen Instiute for AI, 2018)
3. GPT-2 (OpenAI,2018)


## Continuous Bag-of-word Model Embedding Process

**Objective** is to predict missing(center) word based on the surrounding words
**Rationale** if two words are often surrounded by similar meaning words, then those two words are related semantically

Embedding process needs:
1. Corpus
2. Embedding method
3. Way to transform corpus into representation that suits for machine learning

### Creating a training example

Consider an example corpus - I am happy because I am learning

- `happy` is the center word
-  `I am` & `because I` are context words. Number of context words is referred by hyper-parameter c(i.e. 2). C is known as **half-size** in this case.
-  In whole, `I am happy because I` is called the **window**. In this case, window size is 5.
-  Every training example will have context words to predict center word. 

In CBOW model, window is slided across the sentence to collect continuous words in training examples

| #   | context words  | center word |
|-----|----------------|-------------|
| 1   | I am because I | happy       |
| 2   | am happy I am  | because     |
| ... | ...            | ...         |

 
### Cleaning and tokenisation

**Practical advice**

- Make corpus case-insensitive
- Handle punctuations (trim redundant, remove meaningless)
- Handle numbers (keeping numbers like 3.14, 2023)
- Handle special characters (safe to drop)
- Handle special words (transforming emoji to meaningful words.)

```python
corpus = 'Who ❤️ "word embeddings" in 2020? I do!!!'
data = re.sub(r'[,!?;-]+','.',corpus)
```
-> Who ❤️ "word embeddings" in 2020. I do.

```python
data = nltk.word_tokenize(data)
```
-> ['Who','❤️','``','word','embeddings','""','in','2020','.','I','do','.']
```python
data = [ch.lower() for ch in data
        if ch.isalpha()
        or ch == '.'
        or emoji.get_emoji_regexp().search(ch)
        ]
```
-> ['Who','❤️','word','embeddings','in','2020','I','do','.']


### Sliding window of words

```python
def get_windows(words,C):
    i = C # hyperparameter context size
    while i < len(words) - C:
        center_word = words[i]
        context_words = words[(i-C):i] + words[(i+1):(i+C+1)]
        yield context_words, center_word
        i += 1

for x,y in get_windows(['I','am','happy','because','I','am','learning'],2):
    print(f'{x}\t{y}')

```
-> ['I','am','because','I']/'happy'
['am','happy','I','am']/'because'
['happy','because','am','learning']/'I'

### Transforming words into vectors

1. Collect corpus
2. Prepare vocabulary
3. One-hot encode all words
    | #        | am | because | happy | I | learning |
    |----------|----|---------|-------|---|----------|
    | am       | 1  | 0       | 0     | 0 | 0        |
    | because  | 0  | 1       | 0     | 0 | 0        |
    | happy    | 0  | 0       | 1     | 0 | 0        |
    | I        | 0  | 0       | 0     | 1 | 0        |
    | learning | 0  | 0       | 0     | 0 | 1        |
4. For context words - average the individual one-hot vector of context words
    - For center word 'learning', averaged context-word vector looks like [0.25,0.25,0,0.5,0]

### Architecture of CBOW model
> Shallow Dense Neural Network

**Architecture**
Context-words vector(X) -> `Input Layer` -> (ReLU) -> `Hidden Layer` -> (Softmax) -> `Output Layer` -> Center word vector($\hat{y}$)

**Dimensions**
N - Hyperparameter Word Embedding Size
V - Size of vocabulary

Input layer =  V x 1
Weights-1 = N x V
Bias-1 = N x 1

Hidden Layer = N x 1
Weights-2 = V x N
Bias-2 = V x 1

Output Layer = V x 1

The above archicture is for one training example. Passing multiple training example makes the training process quicker - the process known as `Batch Processing`.

**Dimensions with Batch Processing**

N - Hyperparameter Word Embedding Size
M - Batch Size
V - Vocabulary Size

Input layer =  V x M
Weights-1 = N x V
Bias-1 = N x M

Hidden Layer = N x M
Weights-2 = V x N
Bias-2 = V x M

Output Layer = V x M

**Activation Function**

ReLU - Rectifier Linear Unit
- Input and output are real number
- Flattens negative value at zero

Softmax
- Input(X) is vector of real numbers
- Output($\hat{y}$) is vector of real numbers in the interval [0,1] - which sum upto 1 - describing probabilities of being center word.

$$\hat{y}_i = \frac{e^{z_i}}{\sum_{j=1}^V e^{z_j}}$$
where $z_i$ is the input to softmax
$e^z$ transforms $z$ to positive and
$\sum_{j=1}^V e^{z_j}$ normalises the input.


**Cost Function**
> Cross-entropy loss - predominantly used with classification

**Training Progress**
- Forward Propagation
- Backward Propagation
- Gradiest Descent

---Skipped---

## Extracting Word Embedding Vectors

Option 1:
Stacking output word vectors as row of a matrix
Option 2:
Just opposite of previous option - stacking vertically
Option 3:
Averaged addition of all element in option 1 and option 2.
For eg, $W_3 = 0.5(W_1 + W_2^T)$


## Intrinsic Evaluation

