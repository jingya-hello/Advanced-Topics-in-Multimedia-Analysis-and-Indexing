# A Bayesian Hierarchical Model for Learning Natural Scene Categories

### Goal
use intermediate representations (ex.textons or codewords) to imporove performance but avoid manually labeled or segmented images

### Contribution
1. a principled approach to learning relevant intermediate representations of scene automatically and without supervision
2. a principled probabilistic framework for  learning models of textures via codewords (or textons)
3. Our model is able to group categories of images into a sensible hierarchy

## Our approach
![](https://i.imgur.com/WcWRUHl.png)
### Model structure
![](https://i.imgur.com/BuZlv70.png)
Theme Model 1 is a hierarchical representation of the scene category model.
#### the process that generates an image i formally from the model
1. Choose a category label c ∼ p(c|η) for each image, where c = {1, . . . , C}. C is the total number of categories. η is a C-dimensional vector of a multinomial distribution;
2. 
    * Draw a parameter that determines the distribution of the intermediate themes (e.g. how “foliage”, “water”, “sky” etc. are distributed for this scene). 
    * Choose π ∼ p(π|c, θ) for each image(π is the parameter of a multinomial distribution for choosing the themes. θ is a matrix of size C×K, where θc· is the K-dimensional Dirichlet parameter conditioned on the category c. K is the total number of themes.)
3. for each N patches xn in the image
    * Choose a theme zn ∼ Mult(π). zn is a K-dim unitvector.  zkn = 1 indicates that the kth theme is selected (e.g. “rock” theme)
    * Choose a patch xn ∼ p(xn|zn, β), where β is a matrix of size K × T. K is again the number of themes and T is the total number of codewords in the codebook. Therefore we have βkt = p(xtn = 1|zkn= 1).
#### Generative quation of the model
![](https://i.imgur.com/gvMqqYj.png)

### Bayesian decision
compute the probability of each scene class
![](https://i.imgur.com/I9i4LiQ.png)
where θ, β and η are parameters learnt from a training set

the decision of the category is made by comparing the likelihood of x given each category: c=argmax_c p(x|c,θ,β)
![](https://i.imgur.com/5JYJ5Ea.png)

### Features & codebook
#### Local region detection and representation
Compared to the global features, local regions are more robust to occlusions and spatial variations, the paper have tested 4 ways of extracting local regions:
1. evely smapled grid
2. random sampling
3. kadir&bradly saliency detector
4. lowe's DoG detector
![](https://i.imgur.com/qgBrAZ6.png)

#### Codebook formation
![](https://i.imgur.com/OguXhND.png)

## Results
![](https://i.imgur.com/Aev2XKv.png)
* the highest block of errors occurs among the 4 categories:bedroom, livingroom, kitchen and office. 
* Using he best and second best choices, the mean categorization result increases to 82.3%.
![](https://i.imgur.com/D6il8Mm.png)
![](https://i.imgur.com/GFHQXy9.png)
![](https://i.imgur.com/U7BhuN2.png)

## Summary and discussion
![](https://i.imgur.com/PR8RNxV.png)

