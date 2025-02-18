# Locality Sensitive Hashing
> Using word vectors to align words of two different languages (translation)

## Overview of translation

1. Calculating word embeddings(word vectors) associated with both languages, say English & French.
2. Finding some way to transform word vector of one language into other.
3. Finding most similar vector to the transformed vector is aligned vector (aka translation).

You need to find a matrix that can do this transformation

## Transforming word vectors

It can be coded in python as,
```python
R = np.array([[2,0],[0,-2]])
x = np.array([[1,1]])
np.dot(x,R)
```
denoted as,
$$XR \approx Y$$

where R is the transformation matrix and x is a vector to give transformed vector i.e. Y

### Align word vectors

If you have subset of vocabulary from different language as aligned word vectors, you can train a supervised learning model to translate many other words.

Aligned word vectors meant as,
English - [cat,...,zebra],
French - [chat,...,zebresse]

### Solving for R

1. Initialize random tranformation matrix, R
2. In a loop, find loss and update transformation matrix with gradient
    $Loss = \lVert RX - Y\rVert _F^2$
    $g = \frac{d}{dR}Loss$
    $R = R - \alpha g$
3. Breakout from a loop, when loss under certain threshold.

**What does $\lVert \rVert$ means**
> Forbenius Norm

$A = \begin{pmatrix} 2 & 2\\\ 2 & 2 \end{pmatrix}$
$\lVert A_F\rVert = \sqrt{2^2 + 2^2 + 2^2 + 2^2}$
$\lVert A_F\rVert = 4$
$\lVert A_F\rVert = \sqrt{\sum_{i=1}^m\sum_{j=1}^n |a_{ij}^2}$

It can be coded as,

```python
A = np.array([[2,2],[2,2]])
A_sq = np.square(A)
A_frobenius = np.sqrt(np.sum(A_sq))
```

**Finding Gradient**

Find $Loss = \lVert RX - Y\rVert _F^2$ - is nothing but Frobenius Norm Squared

$g = \frac{d}{dR}Loss = \frac{2}{m}(X^2(XR-Y))$
where m is number of words in the subset of vocabulary in training

Having figured out transforming vector and transformation matrix, we need to find a way to find most similar word vector with this transformed vector

## K-nearest neighbours
> a way to find similar word vectors in other language with the transformed vector.

### Hashing & Hash Table
> allows you to group and lookup similar word vector in much faster way than simple linear search

- Word vector -> Hash function -> Hash value(for vector) -> Hash Table
- Hash value = vector % no. of buckets
  
Basic Hash Table can be coded as,
```python

def basic_hash_table(vector_vals, n_buckets):
    def hash_function(val, n_buckets):
        return int(val) % n_buckets
    hash_table = {i:[] for i in range(n_buckets)}
    for val in vector_vals:
        hash_val = hash_function(val, n_buckets)
        hash_table[hash_val].append(val)
    return hash_table
```

We need to define hash function that group similar word vectors in the same bucket - known as `locality sensitive hashing`

## Locality Sensitive Hashing Intuition
> key hashing method to reduce computational cost of using k-nearest neighbours in high-dimensional space.

- If vectors are plotted in space, a plane can separate vectors that belongs together.
- In geometrical terms, consider a plane, which actually represents all the vectors in the plane. In that, consider a vector which is perpendicular to the plane - known as `normal vector` to the plane.
- Output of dot product of any vector and normal vector specifies on which side of plane the vector exist. It can be positive depicting one side, negative for other side or even 0 if the vector is on the plane. 
- This allows us to find out points that belong together

### Multiple Planes
> combining several planes to identify a hash value.

1. For every plane, find whether vector is in positive or negative side of the plane.
2. Find a way to combine all of them into a single hash value.

**General Formula**

$hash_value = \sum_{i}^{H} 2^i * h_i$
where H is number of planes
$h_i$ is output for the vector corresponding to that plane.

It is coded as,
```python
def hash_multiple_plane(P_l,v):
    hash_value = 0

    for i,P in enumerate(P_l):
        sign = side_of_plane(P,v)
        h_i = 1 if sign >= 0 else 0
        hash_value += 2**i * h_i
    
    return hash_value

```

## Approximate Nearest Neighbours

But, what is best location of multiple planes in the vector space?

A:Have multiple independent set of planes(aka hash tables)

This can approximate most similar vector known as `approximate nearest neighbours`.

Making one set of random planes can be coded as,
```python
num_dims = 2
num_planes = 3

random_planes_matrix = np.random.normal(size=(num_planes, num_dims))

# for example, v = [2,2]
v = np.array([[2,2]])

def side_of_plane_matrix(P,v):
    dotProd = np.dot(P,v.T)
    return np.sign(dotProd)

num_planes_matrix = side_of_plane_matrix(random_planes_matrix,v)

```

## Searching Docs
> Fast way using k-nearest neighbours to search pieces of text related to a query in a large collection of docs.

```python

word_embedding = {"I":np.array([1,0,1]),"love":np.array([-1,0,1]),"learning":np.array([1,0,1])}

words_in_doc = ['I','love','learning']
doc_embedding = np.array([0,0,0])

for w in words_in_doc:
    doc_embedding += wod_embedding.get(word,0)




```












