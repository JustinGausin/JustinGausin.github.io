---
title: "Building Page....!"
categories:
  - Project
  
tags:
  - Python
  - Machine Learning 
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


This is a testing page

LaTeX? 
\\( a^2 = b^2 \\)



Latex 2.0
$$ \begin{equation} \label{label} 1+1 \end{equation} $$

Logistic Regression is a Machine Learning classification algorithm that is used to predict the probability of the dependent variable. In logistic regression, the dependent variable is a binary value of either 1 or 0. 

Dataset
The data used in this project are simple dimensional inputs for those learning the fundamentals of logistic regression. Suppose we have the data set: inputs X=[-1. -0.8 -0.6 -0.4 -0.2  0 0.2  0.4  0.6  0.8  1] and the corresponding outputs Y=[-5.4 -4.9 -4.5 -3.6 -2.7 -2.  -1.1 -0.1  0.1  1.1  1.5]. Suppose we need to find the linear regression function $y=w_1x+w_0$ according to the regularized least square method. That is, solve the following minimization problem: 
<br>
$$\min_{w_0,w_1}F(w_0,w_1)=\sum_{j=1}^{11} (w_1x_j +w_0 - y_j)^2 + \mu (w_0^2+w_1^2),$$
where $\mu=0.1$.
<br>

We first initialize the inputs and the outputs. 
```python3
X = np.array([-1, -0.8, -0.6, -0.4, -0.2, 0, 0.2, 0.4, 0.6, 0.8, 1])
Y = np.array([-5.4, -4.9, -4.5, -3.6, -2.7, -2, -1.1, -0.1, 0.1, 1.1, 1.5])
N=X.shape[0]
mu = .1

mA=np.array([np.ones(N),X])
mA=np.transpose(mA)
```
The result should be similar to the expected 'A' matrix.
[[ 1.  -1. ]
 [ 1.  -0.8]
 [ 1.  -0.6]
 [ 1.  -0.4]
 [ 1.  -0.2]
 [ 1.   0. ]
 [ 1.   0.2]
 [ 1.   0.4]
 [ 1.   0.6]
 [ 1.   0.8]
 [ 1.   1. ]]
