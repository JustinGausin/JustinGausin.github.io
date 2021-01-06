---
title: "Numerical Methods-Matlab"
categories:
  - project
tags:
  - Numerical
  - programming
  - matlab
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS_CHTML"> </script> <script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true}, jax: ["input/TeX","input/MathML","input/AsciiMath","output/CommonHTML"], extensions: ["tex2jax.js","mml2jax.js","asciimath2jax.js","MathMenu.js","MathZoom.js","AssistiveMML.js", "[Contrib]/a11y/accessibility-menu.js"], TeX: { extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"], equationNumbers: { autoNumber: "AMS" } } }); </script>
# Bulding this page now....

# In this page is a collection of Matlab codes and numerical method theories.
> For more info see: Numerical Analysis, 2nd Edition by Sauer, Timothy

## Root finding

### Fixed Point Iteration
``` matlab
function fixed(g, x0, tol, n)
% inputs: g = function g, x0 = starting value, tol = tolerance, n= number of iterations
iter = 0;
u=g(x0);
err = abs(u-x0);
fprintf(' i xn error\n');
fprintf(' ----- ------------------ ----------\n');
fprintf(' %4d %18.16g %12.6g\n', iter, x0, err);
while(err>tol)&(iter<=n)
  x1 = u;
  err = abs(x1-x0);
  x0 = x1;
  u = g(x0);
  iter = iter+1;
  fprintf(' %4d %18.16g %12.6g\n', iter, x0, err);
end

if(iter>n)
  disp('Method failed to converge')
end

end
```
##  Differentiation
### Composite Midpoint Rule / Open Newton-Cottes Formula
#### General Theory:
$$ \int_{a}^{b} f(x) dx = h \sum_{l=1}^{m} f(x_{l}) - \frac{h^2}{24}(b-a)f''(c) $$

<br>

### Composite Trapezoidal Rule
#### General Theory:
$$ \int_{a}^{b} f(x) dx = \frac{h}{2}(f(a) + f(b) + 2 \sum_{l=1}^{m-1} f(x_{l})) - \frac{h^2}{12}(b-a)f''(c) $$

<br>

### Composite Simpson's Rule
#### General Theory:
$$ \int_{a}^{b} f(x) dx = \frac{h}{2}(f(a) + f(b) + 4 \sum_{j=1}^{m} f(x_{2j-1}) + 2 \sum_{j=1}^{m-1} f(x_{2j}) ) - \frac{h^4}{180}(b-a)f^{4}(c)  $$

#### Code:

``` matlab
Composite Simpson's Rule
% Program 5.2x Calculation of Trapezoidal Rule
% Input: function,
% a,b integration interval, n=number of rows
% Output: Approximation
function csr=SimpsonsRule(f,a,b,n)
h=(b-a)./(2*n);
fa = f(a);
fb = f(b); %endpoints
subtotal_Even = 0;
subtotal_Odd = 0;
for j=1:(2*n)-1
  x = a + (j*h);
  if(mod(j,2) == 0) %if even
    subtotal_Even = subtotal_Even + f(x);
  else %if odd
    subtotal_Odd = subtotal_Odd +f(x);
  end
  
end
csr = (h/3)*(fa+fb + 4*(subtotal_Odd) + 2*(subtotal_Even));

end %requires end for .mlx functions
```
<br>

### Explicit Trapezoidal Method
#### Code:
``` matlab
function [t,y]=etm(inter,y0,n,f)
%inputs: inter= interval [# #],  y0 = initial condition, n= number of panels, f = function to be evaluated

t(1)=inter(1); y(1)=y0;
h=(inter(2)-inter(1))/n;
%t values, approximations, and global truncation error
for i=1:n
  t(i+1)=t(i)+h;
  y(i+1)=trapezoidalstep(t(i),y(i),h);
  %gte(i+1) = abs(y(i+1)-exp(t(i+1)^3/3));
  trueval(i+1) = f(t(i));
end

plot(t,y,'bp--',t,trueval)
legend('Approximated', 'True')
%plot(t,trueval)
fprintf(' Last value: \n');
fprintf(' t approximations \n');
fprintf('----- ------------------- \n');
fprintf('%1d %18.16g %18.16g \n', t(end), y(end));

end
```
<br>

### Predictor-Corrector Method
#### Code:
``` matlab
function [t,y] = predcorrect4(inter, ic, n, s,fexact)
%inputs: inter= interval [# #],  ic = initial condition, n= number of panels, s=4 for 4th order method, fexact = exact solution to the ODE
%prediction and correctness with RK4, AB4, AM3, 
h =(inter(2)-inter(1))/n;
y(1)=ic;
t(1)=inter(1);
for i=1:s-1
  t(i+1) = t(i)+h;
  y(i+1) = rk4(t(i), y(i), h);
  f(i) = ydot(t(i), y(i));
  exact(i+1)= fexact(t(i+1));
end
for i=s:n
  t(i+1)= t(i)+h;
  f(i) = ydot(t(i), y(i));
  y(i+1) = ab4step(t(i), i,y,f,h); %predict
  f(i+1) = ydot(t(i+1),y(i+1));
  y(i+1) = am3step(t(i),i,y,f,h); %correct
  exact(i+1)= fexact(t(i+1));
end

plot(t,y,'bp--',t, exact);
legend('Approximated', 'Exact')

end %last end is required by live scripts
```
<br>
