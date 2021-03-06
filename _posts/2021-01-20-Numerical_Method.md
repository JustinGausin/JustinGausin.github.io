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


# In this page is a collection of Matlab codes and numerical method theories.
> For more info see: Numerical Analysis, 2nd Edition by Sauer, Timothy

## ROOT FINDING 
### Fixed Point Iteration
#### General Theory:

$$ x_0 \text{ initial guess} \\ x_{n+1} = g(x_{n}) $$

#### Code:
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
### Newton's Method
#### General Theory:

$$ x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} $$

Modified Newton's Method: $ x_{n+1} = x_n - \frac{m f(x_n)}{f'(x_n)} $

where m is the multiplicity.(To achieve quadratic convergence)

#### Code:
``` matlab
%If not modified m =1, if it is modified newton m is the multiplicity
function Newton(f, f1, x0, tol, r, n, mod)
iter = 0;
u=x0;
err = abs(u-r);
m = mod;
%linear convergent error
linerr = 0;
fprintf(' i xn |xn-r| en/e_n-1 \n');
fprintf(' -- ---------------- ----------- -------- \n');
fprintf(' %4d %18.16g %12.6g %12.6g \n', iter, u, err, linerr);

while(err>tol)&(iter<=n)
  xi = u;
  en_minus1 = err;
  xi_plus1 = xi - m*((f(xi))/(f1(xi)));
  u = xi_plus1;
  iter = iter+1;
  err = abs(u-r);
  linerr = err/en_minus1;
  fprintf(' %4d %18.16g %12.6g %12.6g \n', iter, u, err, linerr);
end
```

### Secant Method
#### General Theory:

$$ x_{n+1} = x_n - f(x_n) \frac{x_n - x_{n-1}}{f(x_n) - f(x_{n-1})} $$

#### Code:
``` matlab
function Secant(f, x0, x1, n)
iter = 0;
u0 = x0;
u = x1;
fprintf(' %4d %18.16g \n', iter , u);

while(iter<=n)
  xi = u;
  xi_minus1 = u0;
  xi_plus1 = xi - ((f(xi)*(xi - xi_minus1))/(f(xi)-f(xi_minus1)));
  u0 = u;
  u = xi_plus1;
  iter = iter+1;
  fprintf(' %4d %18.16g \n', iter, u);
end

end
```
<br>

##  DIFFERENTIATION
### Composite Midpoint Rule / Open Newton-Cottes Formula
#### General Theory:

$$ \int_{a}^{b} f(x) dx = h \sum_{l=1}^{m} f(x_{l}) - \frac{h^2}{24}(b-a)f''(c) $$

<br>

### Composite Trapezoidal Rule
#### General Theory:

$$ \int_{a}^{b} f(x) dx = \frac{h}{2}(f(a) + f(b) + 2 \sum_{l=1}^{m-1} f(x_{l})) - \frac{h^2}{12}(b-a)f''(c) $$

#### Code:
``` matlab 
% Program 5.2x Calculation of Trapezoidal Rule
% Input: function,
% a,b integration interval, n=number of rows
% Output: Approximation
function trapz=trapezoidal(f,a,b,n)
h=(b-a)./n;
fa = f(a);
fb = f(b); %endpoints
subtotal = 0;
for j=1:n-1
  subtotal = subtotal + f(a+(j*h));
end

trapz = (h/2)*(fa+fb + 2*(subtotal));
end
```


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
## INITIAL VALUE PROBLEMS - ODE

### Euler's Theorem (One Step)
#### General Theory:

$$ w_{i+1} = w_i + h f_i, \text{ where }, f_i = f(t_i,w_i) $$

LTE: $\mathcal{O}(h^2)$

GTE: $\mathcal{O}(h) $, making it a 1st order method.

#### Code:
``` matlab
6.1 Euler’s Method for Solving Initial Value Problems
%Program 6.1 Euler’s Method for Solving Initial Value Problems
%Use with ydot.m to evaluate rhs of differential equation
% Input: interval inter, initial value y0, number of steps n
% Output: time steps t, solution y
% Example usage: euler([0 1],1,10);
function [t,y]=euler(inter,y0,n)
t(1)=inter(1); y(1)=y0;
h=(inter(2)-inter(1))/n;
for i=1:n
  t(i+1)=t(i)+h;
  y(i+1)=eulerstep(t(i),y(i),h);
end

plot(t,y)
fprintf(' Last value: \n');
fprintf(' t approximations \n');
fprintf('----- ------------------- \n');
fprintf('%1d %18.16g \n', t(end), y(end));

end
```
it calls the Euler one-step function:
``` matlab
function y=eulerstep(t,y,h)
%one step of Euler’s Method
%Input: current time t, current value y, stepsize h
%Output: approximate solution value at time t+h
y=y+h*ydot(t,y);  % ydot is the function we are evaluating, for example:function z=ydot(t,y) z=-y+2*exp(-t)*cos(2*t); 
end
```
<br>

### Explicit Trapezoidal Method (One Step)
#### General Theory:

$$ w_{i+1} = w_{i} + \frac{h}{2}(f_i + f(t_{i+1}, w_i + h f_i) $$

LTE: $\mathcal{O}(h^3)$

GTE: $\mathcal{O}(h^2) $, making it a 2nd order method. 

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

### Runge-Kutta 4th order Method (One Step)
#### General Theory:

$$ w_0 = \alpha \\ w_{i+1} = w_i + \frac{h}{6}(S_1+2S_2 + 2S_3 + S_4) $$ 

where:

$$ \begin{array}{rcl} S_1  &=& f_i \\ S_2  &=& f(t_i + \frac{h}{2}, w_i + \frac{h}{2} S_1) \\ S_3  &=& f(t_i + \frac{h}{2}, w_i + \frac{h}{2}S_2) \\ S_4  &=& f(t_i + h, w_i + h S_3) \end{array}  $$

LTE: $\mathcal{O}(h^5)$

GTE: $\mathcal{O}(h^4) $, making it a 4th order method. 

#### Code:
``` matlab
RK4 FORMULA
function [t,y]=RK4(inter,y0,n)
t(1)=inter(1); y(1)=y0;
h=(inter(2)-inter(1))/n;
%t values, approximations, and global truncation error
for i=1:n
  t(i+1)=t(i)+h;
  y(i+1)=rk4_onestep(t(i),y(i),h);
  gte(i+1) = abs(y(i+1)-exp(t(i+1)^3/3));
end

%plot(t,y)
fprintf(' t approximations GTE \n');
fprintf('----- ------------------- ------\n');
for i=1:n+1
  fprintf('%1d %18.16g %18.16g\n', t(i), y(i), gte(i));
end

end
```
it calls the RK4 one-step function:
``` matlab
function y=rk4(t,y,h)
%one step of RK4 Method
%Input: current time t, current value y, stepsize h
%Output: approximate solution value at time t+h
% ydot is the function we are evaluating, for example:function z=ydot(t,y) z=-y+2*exp(-t)*cos(2*t); 
S1 = ydot(t,y);  
S2 = ydot(t+(h/2),y+(h/2)*S1);
S3 = ydot(t+(h/2), y+(h/2)*S2);
S4 = ydot(t+h, y+(h)*S3);
y= y+(h/6)*(S1+2*S2+2*S3+S4);
end
```

### Multi-Step Methods
> Check for more info: https://en.wikipedia.org/wiki/Linear_multistep_method


#### AB4STEP
``` matlab
function z = ab4step(t,i,y,f,h);
z =y(i)+(h/24)*(55*f(i)-59*f(i-1)+37*f(i-2)-9*f(i-3));
end
```

#### AM3STEP
``` matlab
function z = am3step(t,i,y,f,h);
z =y(i)+(h/24)*(9*f(i+1)+19*f(i)-5*f(i-1)+1*f(i-2));
end
``` 


<br>
### Predictor-Corrector Method
#### General Theory: 
Prediction and correctness with RK4 (one step), AB4(predict-multistep), AM3(correct-multistep),
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
