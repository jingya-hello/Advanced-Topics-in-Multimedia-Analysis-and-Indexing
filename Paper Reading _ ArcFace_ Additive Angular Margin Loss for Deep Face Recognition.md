# Paper Reading : ArcFace: Additive Angular Margin Loss for Deep Face Recognition

## Problem Discription
both softmax-loss-based methods and triplet-loss-based methods for face recognition:
- softmax:
    1. the size of the linear transformation matrix increases linearly with the identities
    2. not discriminative enough for open-set face recognition problem
- triplet loss:
    1. explosion in large-scale datasets
    2. semi-hard sample mining problem

## Methods

Most used softmax loss does not explicity optimise the feature embedding to enforce higher similarity for intra-class samples and diversity for inter-class diversity

the most used softmax loss
![](https://i.imgur.com/eK3xP2H.png)
### Arface Loss
* fix bias b~j~=0
![](https://i.imgur.com/wrGeJkJ.png)
* fix ||W~j~||=1 by l2 norm
* fiz ||x~i~|| by l2 norm
* add angular margin penalty m between x~~i~~ and W~~yi~~ to enhance tnrea-class compactness and inter-class discrepancy.

the learned embedding can be represent as
![](https://i.imgur.com/DxlYL5y.png)
angular margin loss can enforce gap between  class(as below)
![](https://i.imgur.com/NiI5LaQ.png)

![](https://i.imgur.com/V0XYfVh.png)
![](https://i.imgur.com/CKAj2vK.png)

### Comparison with SphereFace and CosFace
#### Numerical Similarity
different margin penalty
* multiplicative angular margin
* additive angular margin
* additive cosine margin
![](https://i.imgur.com/wF94QKl.png)

#### Geometric Difference
decision boundary boundaries under binary classification.
* Arcface has constant linear angular margin
![](https://i.imgur.com/ailnobj.png)

### Experiment Result
![](https://i.imgur.com/Q1r7i0Z.png)
![](https://i.imgur.com/69QwGUg.png)

## Conclusion
Additive Angular Margin Loss can effectively enhance the discriminative power of feature wmbeddings.
