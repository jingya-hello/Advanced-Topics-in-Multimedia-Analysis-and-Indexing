# A Survey on Learning to Hash

## Learn to hash
five problems needed to concern of approach:
1. what hash function is adopted
2. what similarity in the coding space in used
3. what similarity is provided
4. loss function
5. what optimization tech

### hash function
1. linear hash function
    ![](https://i.imgur.com/u8z29Uq.png)

    w is projection function, b is the bias

2. kernal hash function
     ![](https://i.imgur.com/I53Fv7y.png)
    s_t is a set of representation, w_t is the weight
    
3. non-parametric function
    ![](https://i.imgur.com/DHaU7zb.png)
### Similarity
defined a function about the distance: 
Hamming distance, Euclidean distance

### Loss function
to preserve the similarity order

#### Optimization
challenges:
1. mixed-binaryinteger optimization problem from the sgn function
2. high time complexity  when processing a large number of data points
handle the problem:
 1. continuous relaxation
 2. two-step scheme

#### Catergorization
different similarity preserving manner:
1. pairwise similarity preserving class
2. multiwise similarity preserving class
3. implicit similarity preserving
4. quantization class

## Pairwise similarity preserving
to align the distances or similarities of a pair of items computed from the input space and the Hamming coding space
1. Similarity-distance product minimization (SDPM):
the distance in the coding space is expected to be smaller if the similarity in the original space is larger.
2.  Similarity-similarity product maximization (SSPM):
the similarity in the coding space is expected to be larger if the similarity in the original space is larger.
3. Distance-distance product maximization (DDPM):
the distance in the coding space is expected to be larger if the distance in the original space is larger.
4. Distance-similarity product minimization (DSPM):
the similarity in the coding space is expected to be smaller if the distance in the original space is larger.
5. Similarity-similarity difference minimization(SSDM): 
the difference between the similarities is expected to be as small as possible.
6. Distance-distance difference minimization (DDDM):
the difference between the distances is expected to be as small as possible.
7. Normalized similarity-similarity divergence minimization(NSSDM)

### Multiwise similarity preserving
formulate the loss function by maximizing the agreement of the similarity orders over more than two items computed from the input space and the coding space.
#### Order preserving hashing
to learn hash functions through aligning the orders computed from the original space and the ones in the coding space.
* Objective:
![](https://i.imgur.com/33RPPDR.png)

#### KNN hashing
maximizes the kNN accuracy of the search result

#### Triplet loss hashing
maximizing the similarity order agreement defined over triplets of items, {(x, x+, x−)}
![](https://i.imgur.com/Nk0RnCr.png)
#### Listwise supervision hashing
* triplet
![](https://i.imgur.com/J8KEQnB.png)
* objective
![](https://i.imgur.com/575K3bB.png)

### Implicit similarity preserving
#### Random maximum margin hashing
learns a hash function with the maximum margin criterion

#### Complementary projection hashing
finds the hash function such that the items are as far away as possible from the partition plane corresponding to the hash function.
#### Spherical hashin
uses a hypersphere to partition the space

### Quantization
The distortion error in the quantization approach is an upper bound (with a scale) of the differences between the pairwise distances computed from the input features and from the approximate representation.
1. hyper cubic wuantization
2. Caetesian quantization

A summary of representative hashing algorithms:
![](https://i.imgur.com/nnfdRpp.png)
