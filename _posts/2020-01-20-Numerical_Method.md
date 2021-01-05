---
title: "Numerical Methods-Matlab"
categories:
  - projects
tags:
  - Numerical
  - programming
  - matlab
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

# Bulding this page now....

### PREDICTION AND CORRECTNESS
``` matlab
function [t,y] = predcorrect4(inter, ic, n, s,fexact)
%prediction and correctness with RK4, AB4, AM3, s=4 for 4th order method
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

