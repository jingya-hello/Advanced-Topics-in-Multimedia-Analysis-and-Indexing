# Bi-directional Attention Flow For Machine Comprehension

### Task
machine comprehension which answers a query about given context paragraph

### Contribution
Bi-directional Attention Flow
    * a multi-stage hierarchical process that represents the context at different levels of granularity
    * uses bidirectional attention flow mechanism to obtain a query-aware context representation without early summarization
 
### Improvement of the proposed attention mechanism
1. Instead of being used to summarize the context paragraph, the attention vector is allowed to flow through to the subsequent layer which can reduce the information loss caused by early summarization.
2. Use a memory-less attention mechanism: the attention at each time step is a function of only the query and the context paragraph at the current time step and does not directly depend on the attention at the previous time step.
    * It forces the attention layer to focus on learning the attention between the query and the context
    * It enables the modeling layer to focus on learning the interaction within thequery-aware context representation (the output of the attention layer)
    * It allows the attention at each time step to be unaffected from incorrect attendances at previous time steps.
3. Use attention mechanisms in both directions which provide complimentary information to each other.

## Model
![](https://i.imgur.com/2m9GpAB.png)

1. Character Embedding Layer
    matching each word to high-dimensional vector space using CNN
3. Word Embedding Layer
    maps word to high-dimensional vector space: pre-trained GloVe
5. Contextual Embedding Layer
    use LSTM on top of the embeddings previded by the previous layer to capture the temporal interactions between words.
7. Attention Flow layer
    link and fuse the information from the context and the query, the attention vector at each time step are allowed to **flow** through to the subsequent layer
    * Contect-to-qeury Attention: signifies which query words are most relevant to each context word
    * Query-to-context Attention: signifies which context  have the closest similarity to one of the query words
9. Modeling Layer
    use two layers of bi-directional LSTM to encode the query-aware representations of context words.
11. Output Layer
    spplication-specific to answer the query
    
## Question Answering Experiments

### Dataset
SQuAD with 100000 questions.
evaluation metrics: Exact Match(EM), F1 score
### Results and ablations
![](https://i.imgur.com/mLFdTe6.png)

### Visualizations
![](https://i.imgur.com/yX27ka0.png)

## Cloze Test Experiments
### Dataset
Cloze-style comprehension dataset consisting 300k/4k/3k and 879k/65k/53k examples from CNN and DailyMail

### Results
![](https://i.imgur.com/kiVgi5t.png)
