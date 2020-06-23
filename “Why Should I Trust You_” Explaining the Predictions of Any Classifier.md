# “Why Should I Trust You?” Explaining the Predictions of Any Classifier

While machine learning models remain black boxex, it is important to understand the reason behind th prediction which make the users "trust the prediction" and also " trust the model".
In this paper, they provide explanations for predictions as a solution to the “trusting a prediction” problem, and selecting multiple such predictions (and explanations) as a solution to the “trusting the model” problem.
### Contribution
1. LIME: an algorithm that can explain the predictions of any classifier or regressor by approximating it locally with an interpretable model
2. SP-LIME: select a set of representative instances with explanations via submodular optimization
3. Comprehensive evalution with simulated and human subjetcs, where we measure the impact of explanations on trust and associated tasks.

## The case for explanation
![](https://i.imgur.com/3pXlluV.png)
![](https://i.imgur.com/xPGWPbW.png)


### Desired Characteristics for Explainers
* Interpretable
* Local Fidelity
* Model-Agnostic
* Global Perspective

## Local Interpretable Model-agnostix Explanations(LIME)
to identify an interpretable model over the interpretable representation that is locally faithful to the classier

### Interpretable data representation
* interpretable: a representation which is understandable to humans
* binary vector indicating the presence or absence of a word(for text) or image patch(for image)
### Fidelity-interpretability trade-off

* omega(g): a measure of complexity of the explanation
* L(f, g, pi_x): local fidelity function
![](https://i.imgur.com/JrBn5Mh.png)
![](https://i.imgur.com/W5MbsNg.png)

### Sampling for local exploration
model-agnostic: minimize the locality-liss L(f, g, pi_x) without making assumption
### Sparse linear explanations
![](https://i.imgur.com/xAZOeli.png)


## Submodular Pick for explaining models
* **should** pick a diverse, representative set of explanations to show the user and avoid to select redundent explanation to the user
![](https://i.imgur.com/ndJ3I4s.png)

* non-redundant coverage intuition:
![](https://i.imgur.com/wtl0rLl.png)
to maximize a weighted coverage function

## Simulated User Experiments
### Are explanations faithful to the model?
![](https://i.imgur.com/eUzp1zf.png)
### Should I trust this prediction?
![](https://i.imgur.com/twGRLK7.png)

## Evaluation with human subjects
![](https://i.imgur.com/FiilFZ7.png)



