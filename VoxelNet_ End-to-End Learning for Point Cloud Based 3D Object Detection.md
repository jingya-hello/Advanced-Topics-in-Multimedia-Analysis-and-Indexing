# VoxelNet: End-to-End Learning for Point Cloud Based 3D Object Detection


### Contributions
* end-to-end deep architecture that directly operates on sparse 3D points and avoids information bottlenecks
* efficient method to implement VoxelNet
* experiments on KITTI benchmark

## Architecture
![](https://i.imgur.com/yzR12T9.png)
### Feature Learning Network

#### Voxel feature encoding layer
![](https://i.imgur.com/YzXWI7n.png)
compute the local mean as the centroid of all points ->  each point with the relative offset -> each point is tranformed through the FCN into feature space (FCN linear layer + batch norm + ReLU)-> element-wise maxpooling -> argument each f to form point-wise concatenated feature

#### Convolution Middle Layers
add more context to the shape description
layer : 3D conv + BN + ReLU

#### Region Proposal Network
![](https://i.imgur.com/yvDcEsm.png)
3 blocks of fcn
1. downsample the feature map 
2. BN ReLU
3. upsample the output

### Efficient Coding
![](https://i.imgur.com/92CSTPq.png)
use voxel coordinate as hash key to O(1) access hash table

## Experiment
![](https://i.imgur.com/NHcyuk6.png)
performance comparison on 3D detection




