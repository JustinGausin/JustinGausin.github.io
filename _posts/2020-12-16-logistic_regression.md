---
title: "Building Page....!"
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
``` python
X = np.array([-1, -0.8, -0.6, -0.4, -0.2, 0, 0.2, 0.4, 0.6, 0.8, 1])
Y = np.array([-5.4, -4.9, -4.5, -3.6, -2.7, -2, -1.1, -0.1, 0.1, 1.1, 1.5])
N=X.shape[0]
mA=np.array([np.ones(N),X])
mA=np.transpose(mA)

#The result of mA should be similar to the expected 'A' matrix for our formula:
#[[ 1.  -1. ]
# [ 1.  -0.8]
# [ 1.  -0.6]
# [ 1.  -0.4]
# [ 1.  -0.2]
# [ 1.   0. ]
# [ 1.   0.2]
# [ 1.   0.4]
# [ 1.   0.6]
# [ 1.   0.8]
# [ 1.   1. ]]
```
Next we solve the following equation:
 
$\nabla F(w) = 2A^T(Aw-y) $

Set $ \nabla F(w)=0$ to solve the minimizer $$ (A^T A )w^*=A^T y $$  **or**  $w^* = (A^T A)^{-1}A^T y$ (see How)

``` python
from numpy import linalg as lu
# use x=LA.solve(A,b) to solve Ax=b
mu=0.1
mA_t=np.transpose(mA)
mI=np.eye(2) # generate the 2x2 idenity matrix, or use np.identity(mA.shape[1])
vw_st=lu.solve(mA_t@mA + mu*mI, mA_t@Y)
```

which will give us w* = [-1.94594595  3.59555556] or in other words, w0 = -1.94594595 and w1 = 3.59555556.
Recall:  $F(w)=\|Aw-y\|_{\ell^2}^2 + \mu \|w\|_{\ell^2}^2$
``` python
ssq = np.sum((mA@vw-Y)**2) + mu*(np.sum(vw**2))
print('F(w_0*,w_1*): ',ssq)
```
Should yield: F(w_0*,w_1*):  2.151478678678679

### Using Gradient descent method to find the approximate minimizer.
That is to solve the following equation: 
$(w^{k+1}_0,w^{k+1}_1)=(w^k_0,w^k_1) - \eta \nabla F(w^k_0,w^k_1)$ 

$w^{k+1}=w^k - \eta \nabla F(w^k)${: .align-center}


