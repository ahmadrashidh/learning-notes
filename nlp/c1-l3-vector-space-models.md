# Vector Spaces
> Representing word and documents as vectors

## Vector Space Models

- General Idea
- Advantages
- Applications

### General Idea

**Why learn vector space models?**

Consider two examples,

Where are heading? , Where are you from? - identical words, but different meaning

But? What is your age? , How old are you? - distinct words, but same meaning 

### Advantages

- Vector Space models allows us to identify sentences despite this variety
- They can be used to identify similarity for question-answering, paraphrasing, etc
- Overall, helps in capturing relationships between words.
  
### Applications

- Information extraction i.e. who, what, where, when from a text
- Machine Translation
- Chatbots

## Encoding Word or Document to vector

- Making co-occurrence matrix and extracting vector representation out of it
- discovering relationships between words/document i.e. similarity

### Word-by-word
> number of times they occur together within distance k

- Values in Co-occurrence matrix corresponds to the number of times words occur together within distance k.

|      | simple | raw | like | I |
|------|--------|-----|------|---|
| data | 2      | 1   | 1    | 0 |

### Word-by-document
> number of times a word occurs within a certain category

Let's say we have documents or corpus across many categories. word by document co-occurrence matrix is as follows:

|      | entertainment | economy | machine learning |
|------|---------------|---------|------------------|
| data | 500           | 6620    | 9320             |
| film | 7000          | 4000    | 1000             |


### Vector Space
> Space (like Cartesian plane) where dimensions is the number of words and markings are number of times.

- In the above example, dimension of vector space is 2 (i.e. there is 2 data) and three coordinate for three categories under comparison. 
- This space or cartesian graph depicts the similarity of words or documents.
- The similarity can be valued using cosine similarity or euclidean distance

## Euclidean Distance
> a similarity metrics that allows to compute how two vectors are similar to each other

Consider a vector space for above example, where two coordinates A and B corresponding to entertainment and economy are marked. 

  Euclidean distance is length of the straight line between two coordinates. It is calculated as:
  $$(B,A) = \sqrt{(B_1-A_1)^2 + (B_2-A_2)^2}$$

  where $B_1-A_1$ is horizontal distance between the points, $B_2-A_2$ is the vertical distance between the points


### Euclidean distance for multi-dimensional vectors
> compute distance between one and other coordinates

It is calculated as:

$$d(\vec{v},\vec{w}) = \sqrt{\sum_{i=1}^{n}(v_i - w_i)^2}$$

where v, w are vectors and n is the number of word i.e dimensions.

In python, it can coded as:
```python
d = np.linalg.norm(v-w)
```

## Cosine Similarity Intuition
> cosine of the angle between two vectors

### Problems of the Euclidean Distance

- In vector space for document of varying sizes , vector deviating drastically can have smallest distance between their coordinates. 

In the same case, cosine angle will show deviation as it is based on angle between vectors.


## Cosine Similarity

Some formulae to recall,

**Norm vector:**
$$\lVert \vec{v} \rVert = \sqrt{\sum_{i=1}^{n}v_i^2}$$

**Dot Product:**

$$\vec{v}.\vec{w} = \sum_{i=1}^{n}v_i.w_i$$

### Calculating cosine similarity

Let's say v,w are two vectors in the space and $\beta$ is the angle between them. The dot product between them is,

$$\hat{v}.\hat{w} = \lVert \hat{v} \rVert\lVert \hat{w} \rVert cos{\beta}$$

Therefore,
$$cos{\beta} = \frac{\hat{v}.\hat{w}}{\lVert \hat{v} \rVert\lVert \hat{w} \rVert}$$

### What does this tell about similarity?

When two vectors are orthogonal (perpendicular to each other), angle between them is $90^{\circ}$. In this case,

$\beta = 90^{\circ}$

$cos(\beta) = 0$

This means they are maximally dissimilar.

When two vectors have same direction, angle between them is $0^{\circ}$. In this case,

$\beta = 0^{\circ}$

$cos(\beta) = 1$

This means they are maximally similar.

Therefore, cosine similarity score is between 0 and 1.

## Manipulating words in vector spaces
> manipulating vectors using simple vector arithmetic

Let's consider an example of vector space with countries and their capital cities. With similarity between country and capital city vector whose data is known, we can predict for the other vectors of countries and capital cities using simple vector algebra.

```
This is great example of how vector spaces are used to capture relationships between words and predict other relationships.
```

## Principle Component Analysis(PCA)
> Visualising vector representations in higher dimensions in lower dimensions - called as Dimensionality Reduction

1. Find a set of uncorrelated features.
2. Project data in required lower dimension plane trying to retain as much as information as possible.

## PCA Algorithm

Recall that matrices have eigen vectors and eigen values.

Eigen Vector: uncorrelated features of the data</br><br>
Eigen Value: amount of information retained by each feature.










