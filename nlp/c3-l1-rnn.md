# Recurrent Neural Network (RNN)

## Traditional Language Models

- N-grams need to capture dependencies between distant words
- For large N-grams, it requires extremely lots of space and RAM

**Outline**

- In autocompletion task, N-gram model computer probability of the next word based on the couple of previous words. To account for appropriate completion for longer sentences, it needs longer N-grams which impractical.


- A plain RNN propagates information from the beginning to end of  sentences to find completing word. 
- Computation ($W_x$) made to find completing word includes information from all previous words and it is propagated as ($W_h$) to find final computation ($W$)

## Applications of RNN
> Many types of RNN - chosen based on nature of inputs and outputs


- For tasks like predicting score of a football based previous scores - one to one, RNN is not of much use than Conventional NN.
- For task like caption generation for a image - which takes one input to give many outputs, RNN is helpful.
- Also, for task like sentiment analysis for a tweet, where many inputs should result in one output, 
- For translation - many inputs to many output task, RNN do well as it propagates information to end. Propagating information to extract representation that capture overall meaning of the sentences - called as `Encoder`. On the other hand, `Decoder` utilisizes the representation to retrieve information.

## Vanilla RNN

- At each step, it takes $x$, a hidden state $H$ and make prediction $\hat{y}$
- It propagates new hidden state to next time step.
- The hidden states at every time $t$, is computed with an activation function $g$ of products between a parameter  matrix $W_h$ and the previous hidden states $h^{<t-1>}$. These are concatenated with the input variable $x^{<t>}$, plus the bias term $b$.
    $$h^{<t>} = g(W_h[h^{<t-1>},x^{<t>}] + b_h)$$
- The complete equation looks like this, where $x^{<t>}$ and $h^{<t-1>}$, are multiplied
by different parameters, and the resulting vectors are summed up element twice.
    $$h^{<t>} = g(W_{hh}h^{<t-1>} + W_{hx}x^{<t>} + b_h)$$
- After computing the hidden state at time $t$, it's possible to get the prediction $\hat{y}$ by using an activation function $g$, with arguments equal to the product between the hidden state $h$, and some parameters $W$ plus a bias trim
    $$\hat{y}^{<t>} = g(W_{yh} h^{<t>} + b_{y})$$

**Observation**
- Hidden states propagate information through time
- Basic recurrent units have two inputs at each time: $h^{<t-1>}, x^{<t>}$

### Cost function of RNN

**Cross Entropy Loss**

Looking at single example $x,y$ in Sequential model,

$J = -\sum_{j=1}^K y_j log \hat{y}_j$ where $K$ is number of classes

Same for vanilla RNN looks like,

$$J = -\frac{1}{T} \sum_{t=1}^T\sum_{j=1}^K y_j^{<t>} log \hat{y}_j^{<t>}$$ 
where $K$ is number of classes
where $T$ is the number of time steps

The above just means that its averaging w.r.t time.

### Implementation of RNN

**tf.scan()**
> nothing but abstract RNN

- Used to do forward pass
- takes in a function `fn` and apply it to all the elements in `elems` from the beginning to end.
- where fn is $F_w$, elems is $x^T$ and initializer is $h^T_0$
```python
def scan(fn, elems, initializer=None,...):
    cur_val = initializer
    ys = []

    for x in elems:
        y, cur_val = fn(x, cur_value)
        ys.append(y)
    
    return ys, cur_val
```
### Advantages of RNN
- Captures dependencies within short range
- Takes up less RAM than other n-gram models

### Limitation of RNN
- While processing long sequence of words, prior information might disapper in the network i.e. RNN struggles to capture long-term dependencies
- prone to vanishing gradients
  
Because

## Gated Recurrent Units(GRU)
> Complex RNN to handle long sequences of words

- Its just vanilla RNN with additional computation - that relevance and update gates to remember important prior information
- Takes two inputs at every timestep - $x^{t}$ and $h$ passed from previous step $h^{<t-1>}$.
- Two computations made are relevance gate $\Gamma_r$ and update gate $\Gamma_u$ - sigmoid activations that squeeze vector of values between 0 and 1
  $$\Gamma_r = \sigma(W_r[h^{<t_0>},x^{<t_1>}]+b_r)$$
  $$\Gamma_u = \sigma(W_u[h^{<t_0>},x^{<t_1>}]+b_u)$$
- Gates to keep/update relevant information in the hidden state i.e. its output determines which information from previous hidden states is relevant and which values should be updated with current information
- After the relevance gates is computed, a candidate's h prime for the hidden states is found. Its computation takes as parameters the previous hidden state times the relevant gates, and the variable X for the current sign.
  $$h'^{<t_1>} = tanh(W_h[\Gamma_r * h^{<t_0>},x^{<t_1>} + b_h])$$
- This value stores all the candidates for information thus could override the one contained in the previous hidden states.
- After that, a new value for the hidden states is calculated using the information from the previous hidden states, the candidates' hidden states, and the updates gates. The updates gate determines how much of the information from the previous hidden state will be overwritten.
  $$h^{<t_1>} = (1-\Gamma_u) * h^{<t_0>} + \Gamma_u * h'^{<t_1>}$$
- Finally, prediction $\hat{y}$ is computed using current hidden states.
  $$\hat{y}^{<t_1>} = g(W_yh^{<t_1>} + b_y)$$


## GRU vs Vanilla RNN
- In Vanilla RNN, hidden state is updated at every step. In long sequence models, the information will vanish due to vanishing gradients problem
- In GRU, relevance gate and update gate controls what information to keep and forgotten.

## Bidirectional RNN
> Information flows from the future and from the past independently

- Calculate hidden states for both that flows from back to front as well as front to back at each time step.
- Based on calculated hidden states, calculate prediction at each step - then computing overall prediction

## Deep RNN
> multiple RNNs stacked together as layers

**How Deep RNN works**
1. Get hidden states for current layer
    $$h^{[l]<t>} = f^{[l]}(W_h^{[l]}[h^{[l]<t-1>},a^{[l-1]<t>}] + b_h^{[l]})$$
2. Pass the activations to next layer
   $$a^{[l]<t>} = f^{[l]}(W_a^{l}h^{[l]<t>}+b_a^{[l]})$$

