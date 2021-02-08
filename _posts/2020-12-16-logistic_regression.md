---
title: "Logistic Regression Introduction"
categories:
  - project
  
tags:
  - python
  - machine learning 
  - ODU

---

<script type="text/javascript"
        src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML">
</script>

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {
inlineMath: [['$','$'], ['\\(','\\)']],
processEscapes: true},
jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"],
extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"],
TeX: {
extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
equationNumbers: {
autoNumber: "AMS"
}
}
});
</script>
# Building this page....
# Intro
Logistic Regression is a Machine Learning classification algorithm that is used to predict the probability of the dependent variable. In logistic regression, the dependent variable is a binary value of either 1 or 0. 

# Dataset
We will use the pre-existing IRIS data set from the sklearn package. The iris data set consists of 150 data points, each point a 4 dimensional vector. For more <a href="https://en.wikipedia.org/wiki/Iris_flower_data_s"> info </a> 

We can load up the data usig the following command:
``` python
import numpy as np
from sklearn import datasets
iris = datasets.load_iris()
```

The class label (iris.target) for the data set is 0, 1, 2 (which signifies whether it classifies as either Iris setosa, Iris virginica, or Iris versicolor). Hence, we need to reformulate the class labels 0,1,2 in iris.target to (1,0,0), (0,1,0), (0,0,1) as following:
``` python
Y_old = iris.target # original class labels of 0,1,2 
Y_new=np.zeros([len(Y_old),3]) # store new labels 
for i in range(len(Y_old)):
    if Y_old[i]==0: 
        Y_new[i,:]=[1,0,0]
    elif Y_old[i]==1: 
        Y_new[i,:]=[0,1,0]
    else: 
        Y_new[i,:]=[0,0,1]
```
