# Paper Reading : Deep Learning for Understanding Faces

## Introduction
This paper introduce many methods for facial detection
###  Three modules for automatic face identification and verification systems
1. A face detector to localize faces
2. A fiducial point detector is used to localize the important facial landmarks
3. A feature descriptor that encodes the identity information is extracted from the aligned face.

## Face Detection in Unconstrained Image
### Region Based
Region-based approach generates a pool of object proposals then use a DCNN classify whether the proposal contain face.
* drawback:
    hard to capture difficult face 
### Sliding-window based
Sliding-window based computes a face detection score and bounding-box coordinates at every location in a feature map at a given scale.

![](https://i.imgur.com/gEBCQan.png)

#### Single-shot detector
* The SSD is a sliding-window-based detector, but instead of creating image pyramids at different scales, it utilizes the inbuilt pyramid structure present in DCNNs. 

* Features are pooled from the intermediate layers of DCNN at different scales that are used for object classification and bounding-box regression.

![](https://i.imgur.com/vIK37nl.png)

a comparative performance evaluation of different face detectors on the FDDB data set.

## Finding crucial facial keypoints and head orientation
### Model based
Such as AAM, ASM, and CLM, learn a shape model during training and use it to fit new faces aduring testing.
![](https://i.imgur.com/2SAR1xP.png)
### Cascaded regression based
Cascaded regression based methods learn a model that directly maps the image appearance to the target output.

## Face identification and verification
### Robust feature learning for faces using deep learning
Learning invariant and discriminative feature representations is a critical step in a face recognition system.
![](https://i.imgur.com/D0JEPga.png)

### Discriminative metric learning for faces
Discriminative metric learning approaches have been proposed in the literature that essentially exploit the label information from face images or face pairs.

## Implementation
###  Similarity metrics
 1. L2 distance
 2. cosine similarity( features in the angular space)
### Dataset
![](https://i.imgur.com/mDghO0b.png)

### Accuracy
![](https://i.imgur.com/Ij4tYgP.png)

## Open issues
1. Face detection: The wide range of variations in the appearance of faces make this task more chalenging.
2. Fiducial detection: Most data sets contain only a few thousand images.
3. Face identification/verification: How to choose informative pairs or triplets and train the network end to end using online methods on large-scale data sets is still an open problem, due to memory constraints limited by graphics cards.
