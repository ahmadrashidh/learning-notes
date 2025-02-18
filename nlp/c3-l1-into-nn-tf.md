# Neural Networks for Sentiment Analysis

## Sample Architecture of NN for Sentiment Analysis
Input Layer - vector representation of the tweets
Embedding Layer
Hidden Layer - ReLU Activation
Output Layer - Positive or Negative

**Initial Representation**
1. List out all words in the tweets
2. Assign integer to each word in the tweet
3. Create integer vector for each tweet
4. Match size of vector for the longest tweet - called `padding`

**Embedding Layer**
> maps words to embedding and returns matrix of word embeddings

- In NLP, we have set of unique words called vocabulary.
- Embedding layer takes in index assigned to each word from the vocabulary and maps it to a representation in determined dimensions.
- For example, with hyperparameter embedding size as 2, for word `NLP`  embedding layer return vector of two trainable values - -0.009 and 0.050.
- In embedding layer, you will learn representation that gives the best performance for your task.
- For the embedding layer, you'd had to learn matrix of weights of size equal to the vocabulary times the dimension of the embedding.

**Mean Layer**
> Feeding embedding layer to next layer


- Could unroll matrix and feed its values to next layer but might end up in lots of training parameters
- so, alternatively, take mean of each feature from the embedding - resulting in same number as embedding sites for next layer

  
