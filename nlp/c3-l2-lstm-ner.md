# Named Entity Recognition(NER) using Long Short Term Memory(LSTM)

## Limitations of RNN
- struggles to capture long-term dependencies
- prone to vanishing gradients & exploding gradients

**Solving for vanishing or exploding gradients**
- Identity RNN i.e. initializing weights with identity matrix and using ReLU activation. This works only for vanishing gradients.
- For exploding gradients, we can use gradient clippings. Any value greater than 25, will be clipped to 25.
- Skip connections

## LSTM
> A special variety of RNN designed to handle entire sequence of data by learning when to remember and when to forget - more like GRU

**Basic Anatomy**
- Cell State i.e. local memory
- Hidden State
- Multiple Gates - allow gradients to avoid vanishing and exploding

### Intuition of LSTM

As your friend rings, you might about thinking about irrelevant things. But as your pick the call, you discard those information and involve relevant information. Your friend may added new information, which on discussion - at the end of call, you have the memory with the most relevant information.

Irrelevant information may be in cell and hidden states, new information and gates retain relevant information in memory.

### Gates in LSTM

1. **Forget gate**: In this gate, inputs and previous hidden states are used to decide which information is no longer important and discard from previous cell state
2. **Input gate**: This gate, decided which information is relevant from input and previous hidden states and to be added to the cell state.
3. **Output gate**: This gate determines information from the cell state that is stored in the hidden state and used to construct output at the given time step.

### Application of LSTM

- Language Models i.e. character prediction, chatbots, music composition, image captioning, speech recongnition

### Architecture

**Candidate Cell State** - information from previous cell state and current input using hyperbolic activation that shrinks value between -1 and 1.
**New Cell State** - Add information from the candidate cell state using `forget` and `input gates`
**New Hidden State** - Select information from new cell state using the `output gate`.


 # Named Entity Recognition
> scanning text to locate and extract predefined entities e.g. places,organisations,names,time and dates

## Types of Entities
1. Geographical entity e.g. Thailand
2. Organisation e.g. Google
3. Geopolitical entity e.g. Indian
4. Time Indicator e.g. December
5. Artifact e.g. Egyptian statue
6. Person e.g. Barack Obama

Example for a sentence: Sharon flew to Miami last Friday

Sharon:B-per
Miami:B-geo
Friday:B-tim
flew,to,last:O aka fillers

`B-` denotes entity of some kind - used for content classification

## Applications of NER
- Search Engine Efficiency - millions to websites are searched for entities and then matched based on queries.
- Recommendation Engines - products mentions extracted from user history to recommend
- Customer Service - matching customers to appropriate service person
- Automatic trading

## NER data preprocessing

1. Assign each class a unique number i.e. B-per to 1, B-geo to 2, B-tim to 3
2. Assign each word a number that corresponds to its assigned entity class

**Token Padding**
> Making all word sequences to be the same size

1. Set sequence length to certain number
2. Use the `<PAD>` token to fill empty spaces

## Training the NER

1. Create a tensor for each input and its corresponding number
2. Put them in a batch with batch size 64,128,256,12
3. Feed it into LSTM unit
4. Run the output through dense layer
5. Predict using log softmax over K classes

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(),
    tf.keras.layers.LSTM(),
    tf.keras.layers.Dense(),
    ])
```
## Evaluate Model
1. Pass test set through the model
2. Get arg max across the prediction array
3. Mask padded tokens to compute correct accuracy
4. Compare the output against test labels

