# Graph Embedding and Extensions: A General Framework for Dimensionality Reduction

previous dimension reduction:
* linear
    * PCA
    * LDA
    * LPP
* non-linear
    *  ISOMAP
    *  LLE
    *  Laplacian Eigenmap

## Graph embedding: a general framework for dimensionality reduction
task: to derive a lower dimensional representation and facilitate the subsequent classification task.
### Graph Embedding
G={X, W} is an undirected weighted parh with vertex set X and similarity matrix W where each element measures the similarity of a pair of vertices.
* Diagonal matrix D of G:
    ![](https://i.imgur.com/OEHu2O4.png)
* Laplacian matrix L of G:
    L = D-W
* Graph embedding of G is to find the desired low-dimensional vector representations
* graph preserving criterion
![](https://i.imgur.com/vG2ox8v.png)
where d is a constant ans B in the constraint matrix defined to avoid a trivial solution of the objective function.
* y: the low-dimesional representation of verteces [y1... yN]^T
#### Linearization
objection function by linear projection
![](https://i.imgur.com/EGgs914.png)

#### Kernelization
to handle nonlinear case
![](https://i.imgur.com/bTRNKaA.png)

#### Tonsorization
to conduct dimensionality reduction with vertices encoded as general tensors of an arbitrary order for the extracted feature that contain higher-order structure (i.e matrix, sequential data)

### General framework for dimensionality reduction
![](https://i.imgur.com/XPuU783.png)
### Related works and discussions
* kernel interpretation and out-of-sample extension
* Brand's work
* laplacian eigenmap and LPP
![](https://i.imgur.com/xori57w.png)

## Marginal Fisher Analysis
previous work usually with gaussian distribution assumption on each class.
![](https://i.imgur.com/9vIvoso.png)
each sample is connected to its k1-nearest neighbors of the same class.
* Intrinsic graph characterizes the intraclass compactness:
![](https://i.imgur.com/RBOrWlm.png)
* Panalty graph characterize the interclass separability:
![](https://i.imgur.com/4lcDP2E.png)
### algorithmic procedure

1. PCA projection: project the dataset into the PCA subspace
2. Constucting the intraclass compactness and interclass separability graphs
    * Intraclass compactness: set W_ij = W_ji = 1 if sample x_i is among the k1-nearest neighbors of x_j
    * interclass separability: set W_ij^p = 1 if the pair(i, j) is among the k2 shortest pairs among the set{(i,j)}
4. Marginal fisher criterion
![](https://i.imgur.com/AH5rTIN.png)
5. Output the final linear projection direction

## Experiments
### Face recognition
### MFA versus Fisherface
![](https://i.imgur.com/naX5x1b.png)
### comprehensive evaluation of graph embedding framework
![](https://i.imgur.com/Xqh3sG9.png)
![](https://i.imgur.com/msqdLGb.png)

1. The kernel trick can improve face recognition accuracy for both KDA and KMFA beyond the corresponding linear algorithms.
2. When the training set adequately characterizes the data distribution,LPP has the potential to outperform Fisherface and PCA;When the data set distribution is complex and the training data cannot represent the data distribution well, LPP appears tobe less effective than Fisherface in these cases.
3. performance can be substantially improved by exploring a certain range of PCA dimensions before conducing LDA or MFA.
4. The Bayesian Face algorithm performs better than PCA, Fisherface, and LPP in most cases and it is comparable to MFA. However, it is consistently worse than PCA + MFA in all cases.
5. The tensor representation brings encouraging performance improvements