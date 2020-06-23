# Model Compression and Acceleration for Deep Neural Networks
DNN have achieved many successness but it is also time-consuming and needs high computation resources. In this paper, they review recent works on compressing and accerlerating DNNs, these works can be caterize into four types :
![](https://i.imgur.com/tuUUkwZ.png)

## Parameter pruning and sharing
remove parameters that are not crucial to model performance
#### Quantization and binarization
* k-mean scalar quantization to the parameter values
* 8-bit quantization to parameters
* 16-bit fixed point representation in stochastic rounding-based CNN training
* SOTA among parameter quatization-based method: pruned the unimportant connection and retrained the sparsely connected network
![](https://i.imgur.com/68onU6N.png)
* minimize Hessian-weighted quantization errors on average for clustering network parameters
* novel quantization framework
* train CNN with binary weight

##### Drawbacks
* low accuracy in large network
* these binarization schemes are based on simple matrix approximations and ignore the effect of binarization on the accuracy loss

#### Pruning and sharing
* biased weight decay
* reduced the numbe of connections based on the Hessian of the loss function
* prune redundant, noninformative weights in a pretrained CNN model
* training compact CNNs with sparsity constraints.
##### Drawbacks
 1. pruning with l1 or l2 regularization requires more iterations to converge
 2. all pruning criteria require manual setup of sensitivity for layers

#### Designing the structural matrix
Imposed structured matrix which is an m*n matrix that can be described using much fewer parameters than mn. It resuced the memory and accelerate the inference and training stage via fast matrix-vector multiplication and gradient computations

##### Drawbacks
1. the structural constraint will cause loss in accuracy since the constraint might bring bias to the model
2. it is difficult to find a proper structural matrix

## Low-rank factorization and sparsity
![](https://i.imgur.com/c7aLyoq.png)
there might be redundancy in the convolution kernels tensor, then use low-rank filter to compress 2-D convolutional layers
* learning separable 1-D filters
* few low-rank approximation and clustering schemes for convolutionsal kernals
* tensor decomposition schemes
* canonical polyadic decomposition of the kernal
* compute low-rank tensor decomposition and a new method for training low-rank constrained CNNs from scratch
* reduced the number of dynamic parameters in deep models
* low-rank matrix factorization of the final weight layer
![](https://i.imgur.com/S6XPwE0.png)

### Drawbacks
* difficult implementation and computationally expensive
* cannot perform global parameter compression since current methods perform low-rank approximation layer by layer
* factorization requiresextensive model retraining to achieve convergence

## Transferred/compact convolutional filteres
equivariance: 
![](https://i.imgur.com/RfQ4I8R.png)
apply transform to layers or filters to compress the network.
* build a convolutional layer from a set of base filters
![](https://i.imgur.com/Gx3ujtw.png)
### Drawbacks
1. not good in narrow/special architecture (ex. GoogleNet and ResNet).
2. transfer assumptions sometimes are too strong to guide the algorithm, making the results unstable on some data sets.

## KD(knowledge distillation)
To distill knowledge from a large teacher model into a small model by learning the class distributions output by the  teacher via softened softmax
* eased the training of deep networks by following a student teacher paradigm
* FitNets train thin and deep networks compress wide and shallower (but still deep) networks.
* parametric student model to approximate a Monte Carlo teacher
* represented the knowledge by using the neurons in the higher hidden layer
* instantaneously transferring the knowledge from a previous network to each new deeper or wider network
* attention transfer to relax the assumption of FitNet.

### Drawbacks
1. can only be applied to classification tasks with softmax loss function
2. the model assumptions sometimes are too strict

## Benchmarks, evaluation, and databases
the basele mehtod used in compression methods
![](https://i.imgur.com/U3DYcJv.png)

## Discussion adn challenges
### General suggestions
* Compacted models from pretrained model: pruning and sharing or low-rank factorization-based methods
* End-to-end solutions: low-rank and transfered convolution filters
* app in specific domains: transferred convolutional filters and structural matrix
* require stable model accuracy: pruning and sharing
* small or medium size datasets: KD


