# PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation

# problem discription
Most deep learning architectures require highly regular input data, therefore most researchers transform point net into images or 3D voxel grids which resulting data unneccessarily voluminous.

# Method : Deep Learning on Point Sets

## Propreties of Point Sets in R^n
the three main properties of the input subset
1. Unordered: input without specific order, so the network that having N 3D point set should be invariant to N! permutations of the input feeding order.
2. Interaction among points: neighbor point is meaningful. the model should be able to capture local structures from nearby points and the combinatorial interactions among local structures.
3. Invariance under transformations : should be rotating and translating invariance

## Architecture
![](https://i.imgur.com/p4foaNL.png)

### Symmetry Function for Unordered Input
traditional stratergies:
1. sorting : does not exist an ordering that is stable to high dimensional space
2. RNN : it's hard to scale to thousands of input elements
3. symmetric function :
![](https://i.imgur.com/oiqJP9r.png)


![](https://i.imgur.com/jSgjegC.png)
we approximate h by multi-layer perceptron network and g by a composition of a single variable function and a max pooling function.

### Local and Global Information Aggregation
after compputing the global point cloud feature vector, we feed it back to per point features by concatenating the global feature with wach of the point features.

### Joint Alignment Network
predict affine transformation matrix by a mini-network and directly apply this tranformation to the coordinates of input points.
add a regularization term to the softmax training loss 
![](https://i.imgur.com/TvwQR1o.png)
where A is the feature alignment matrix predicted by the mini-network.

### Theoretical Analysis
#### Univeral approximation
given enough neurons at the max pooling layer, function can be arbitrarily approximated.

#### Bottleneck dimension and stability
* the expressiveness of our network is strongly affected by the dimension of the max pooling layer
* small corruptions or extran noise points are not licklt to change the output
## Experiment
#### Classification result
![](https://i.imgur.com/5zILd0z.png)

#### Qualitative results for semantic segmentation
![](https://i.imgur.com/G8vdKnA.png)





