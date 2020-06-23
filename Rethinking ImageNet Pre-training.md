# Rethinking ImageNet Pre-training
### Questions
results on object detection and instance segmentation training from random initilazation are no worse than the pre-training counterparts.
### Introduction
This paper questions the paradigm of pre-training: report competitive result when training from random initialization(**from scratch**)

### Observation from experiment
1. ImageNet pre-training speeds up convergence;however the duration of training from scratch is comparable to tht total pre-training + fine-tuning 
2. ImageNet pre-training does not automatically give better regularization.
3. ImageNet pre-training show no benefit  when target tasls/metrics are more sensitive to spatially well-localizaed presictions.

## Methodology
goal: abalate the role of ImageNet pre-training
two modifications for training from scratch

### Normalization
Batch Normalization is a popular method but the accuracy drops when using small batches. Training from scratch usually constrained with small batch due the limit of memory.

Two strategies to help:
1. Group normalization: independent of the batch dimension
2. Synchrinized batch normalization: BN with batch statistics computed across multiple devices.

### Convergence
![](https://i.imgur.com/Z9IfVOV.png)

from-scratch case trained more iteration but the total image than fine-tuned case but sees fewer samples in images, instances and pixels level

### Results and analysis
#### Training from scratch to match accuray
COCO train2017
#### baselines with GN and SyncBN
![](https://i.imgur.com/x3HeOtM.png)
![](https://i.imgur.com/UTOhlul.png)

![](https://i.imgur.com/4TxFcLI.png)

![](https://i.imgur.com/WlRkvPW.png)
![](https://i.imgur.com/WVQaORW.png)

#### training with fewer data
![](https://i.imgur.com/aPqhEkK.png)
![](https://i.imgur.com/1xdVK7g.png)

### Discussion
* Training from scratch on target tasks is possible without architectural changes.
* Training from scratch requires more iterations to sufficiently converge.
* Training from scratch can be no worse than its ImageNet pre-training counterparts under many circumstances, down to as few as 10k COCO images.
* ImageNet pre-training speeds up convergence on the target task.
* ImageNet pre-training does not necessarily help reduce overfitting unless we enter a very small data regime.
* ImageNet pre-training helps less if the target task is more sensitive to localization than classification.
