# Robust Sparse Coding for Face Recognition

## Contribution
proposed RSC which is a more robust and efficient of sparse representation model

## Previous work
* Sparse representation based classification sceme (SRC)
    * codes a query image as a sparse linear combination of the training samples via l1-norm minimization. 
    * classify by evaluating which class has the minimal reconstuction error with its coding coefficients.
    * Two issues about SRC
        1. whether l1-norm is good enough to characterize the signal sparsity.
        2. whether the l2-norm term is effective enough to  chracterize the signal fidelity then y is noisy or has many outliers.


## Robust Sparse Coding (RSC)
#### Traditional sparse coding(SRC)
![](https://i.imgur.com/6ksfyzd.png)
d_j is the training face
Is is true only if the residual follow the Gaussian distribution.

##### A more robust model for face images (RSC)
* rewrite D = [𝒓1; 𝒓2; ⋅ ⋅ ⋅ ; 𝒓𝑛]
* rewrite 𝒆 = 𝒚 − 𝐷𝜶 = [𝑒1; 𝑒2; ⋅ ⋅ ⋅ ; 𝑒𝑛]
* Then, then MLE aims to minimize 
    ![](https://i.imgur.com/fbYWvO1.png)
* Assumption:
    * 𝑓𝜽(𝑒𝑖) is symmetric
    * 𝑓𝜽(𝑒𝑖) < 𝑓𝜽(𝑒𝑗) if ∣𝑒𝑖∣ > ∣𝑒𝑗 ∣
    * 𝜌𝜽(0) is the global minimal of 𝜌𝜽(𝑒𝑖)
    * 𝜌𝜽(𝑒𝑖) = 𝜌𝜽(−𝑒𝑖)
    * 𝜌𝜽(𝑒𝑖) < 𝜌𝜽(𝑒𝑗) if ∣𝑒𝑖∣ > ∣𝑒𝑗 ∣
* Do not dtermine the 𝜌𝜽, but iteratively reweighted sparse coding problem

### The distribution induced weights
![](https://i.imgur.com/Sjn6Uyh.png)
![](https://i.imgur.com/6WInenk.png)
![](https://i.imgur.com/k8GQlBu.png)
![](https://i.imgur.com/4xiTCSX.png)
(please refer to the original paper)


## Algorithm of RSC
![](https://i.imgur.com/3E3j9WZ.png)

#### Iteratively reweighted sparse codeing
iinitialize 𝒆 = 𝒚-𝒚ini , yini is mean of all training samplesfor the first face y

#### convergence of IRSC
The convergence is achieved when the difference of the
weight between adjacent iterations is small enough.
![](https://i.imgur.com/iMpcqnz.png)
stop for some small enough positive scalar 𝛾

#### Complexity analysis
in sparse coding process 𝑂(𝑚^𝜀) with 𝜀 ≈ 1.5
RSC higher than SRC since it needs several iterations

In occlusion or corruption cases, SRC = 𝑂((𝑚 + 𝑛)^𝜀)
RSC = 𝑂(𝑘(𝑚)^𝜀) where k is the number of iteration

### Experimental Results
##### Face recognition
* Extended Yale B database
![](https://i.imgur.com/XiIBhHp.png)
* AR database
![](https://i.imgur.com/oeE54EE.png)
* Multi-PIE database
![](https://i.imgur.com/mf56A4Q.png)

#### with different corruption rate
![](https://i.imgur.com/1JOC1GN.png)
#### with different level of block occlusion
![](https://i.imgur.com/3ISmDd4.png)

#### ollusion with sumgalss or scarf
![](https://i.imgur.com/keAzOqr.png)


