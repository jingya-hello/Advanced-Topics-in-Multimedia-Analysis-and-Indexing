# A Closer Look At Few-shot Classification

## Introduction

### Few-shot classification

To learn a classifier to recognize unseen classes during training with limited labeled examples("few shot")

### Contribution
1. a consistent comparative analysis
2. a modifieed baseline method 
3. a new experimental setting for evaluating cross-domain generalization ability

### Current Limitations
1. the discrepancy of the implementation details among multiple algorithms makes it difficult to faily estimate.
2. the lack of domain shift between the base and novel classes makes the evaluation scenarios unrealistsic

## Realated Work
### Initialization methods
learn good model initialization or learn a good optimizer
ex. LSTM-based meta-learner for replacing the sgd, weight-update mechanism
* liminitation: difficulty in handling domain shifts

### Distance metric learnign based methods
learning to compare by making prediction conditioned on distance or metric to few labeled instances
ex. cosine similarity, euclidean distance to class-mean representation, CNN-based relation module, ridge regression, GNN

### Hallucination based methods
learned a generator and use the generator to hallucinate new novel class for data augmentation.
 * transfer appearance variations, ex.transfer variance, use GAN to transfer style
 * integrate the generator into meta-learning algorithm

### Domain adaption
reduce domain shifts between source and target domain also novel tasks in a different domain

## Overview of few-shot classification algorithms
![](https://i.imgur.com/POJvpC9.png)

### Baseline
#### Training stage
train a feature extractor f_theta and the classifier C(．|W_b) (which consists of a linear layer and followed by a softmax function) from scratch by minimizing a cross-entropy loss.

#### Fine-tuning stage
fix the pre-trained network parameter in the feature extractor and train a new classifier  using few labeled of example in the novel class. 

### Baseline++
reduce intra-class cariation among features
Classifier: compute cosine similarity to each weight vector and obtain the similarity scroe for all classes, then normalize with a softmax function.

### Meta-learning algorithm
![](https://i.imgur.com/gsRHqw8.png)
* Meta-training stage: randomly select N classes and sample small base support set and a base query sey from these classes.
* Objective: train a classification model that minimizes N-way prediction loss of samples in the query set.
* The classifier is conditioned on the provided support set
* Meta-testing stage: all novel class data X_n are considered as the support set for novel classes S_n, and classification model can be adapted to predict novel classes with the new support set S_n

#### Example methods
* MatchingNet: compare the cosine distance between query feature and support feature
* ProtoNet: compare the euclidean distance between query feature and support feature
* RelationNet: compare with relation module
* MAML: used upport set to adapt the initalization of model parameter

## Experimetal results
### Setup
#### Datasets and scenariots
1. generic object recognition: mini-ImageNet which condists of a subset of 100 classes from ImageNet and contains 600 images for each class.
2. fine-grained classification: CUB-200-2011 which contains 200 classes and 11788 images in total
3. cross-domain: use mini-ImageNet as base class and  the 50 validation and 50 nocel class form CUB.

#### Implemetation details

##### Train
* Baseline&Baseline++: train 400 epoch, batch size 16
* meta-learnign methods: 60000episodes for 1-shot and 40000 episodes for 5-shot task. use the validation set to select the training episodes wuth best accuracy. In each episode, sample N classes to form N-way classification; for each class, pick k labeled instances as support set and 16 instance for the query set for k-shot task

##### Finetune
randomly sample 5 classes from novel classes and k instance and 16 for the wuery set in each class
average result over 600 experiments

##### Others
* trained from scratch
* Adam optimizer with lr 10^-3
* data augmentation: random crop, left-right flip, color jitter

### Evaluation using the standard setting
For standard setting please refer to the original paper

![](https://i.imgur.com/5xbJOXP.png)
Few-shot classification results
Baseline++ improves and show that reducing intra-class variation is an important factor in the current few-shot classification problem setting.

### Effect of increasing the network depth
change the depth of the feature backbone to reduce intra-class variation(Conv-4 -> Conv-6 -> ResNet-1 -> ResNet-18 -> ResNet34)

![](https://i.imgur.com/Evikhoa.png)

#### Results of CUB
* when backbone gets deeper which reduce the intra-class variation, the gap among different methods reduces in CUB dataset
* Protonet improves rapidly as the backbone gets deeper

#### Results of mini-ImageNet
* Baseline and Baseline++ achieve good performance which some meta-learnign methods become worse relatively.
* We can assume that dataset is important in few-shot learning classification that CUB and mini-ImageNet have different domain difference that mini-ImageNet have larger divergence.


### Effect of domain differences between base and novel classes
![](https://i.imgur.com/Udbkitr.png)
In cross-domain scenario, baseline outperforms all meta-learning methods.
* meta-learning are not able to adapt to novel classes that are too different since in training the base support set are within the same dataset.
* baseline allow quick adpation to novel class and is less effected by domain shift since it simply replace and  trained a new classifier on the few given nodel class data

### Effect of further adaption
![](https://i.imgur.com/egwJqtU.png)
* the performance for MathcingNet and MAML imporoves significant which demonstrates that lack of adaption is the reason why they fall behind the Baseline.
* learning to learn adaption in the meta-training state would be an important direction for future meta-learning research in few-shot classification