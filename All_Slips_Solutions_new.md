# MTC-242-MN-P: All Slips Solutions

S.Y. B.Sc. (Computer Science) — Mathematics Practical Examination (Sem III)

Practical on Mathematics for Computer Science - I (NEP 2025 Pattern)

Solutions by Raj…

> Every question is reproduced in full from the slips. Under each question the matching Lab Book practical/question is named, and the program uses the same function names, variables, loops and print statements as that lab-book program (only the equation, data, limits and iteration counts are changed). Each output shown was produced by actually running the program.


---

## Slip No. 1

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup>−5x−9 = 0, using Regula-Falsi method correct up to five decimal places Or 15 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.1 (same question)*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**3 - 5*x - 9
falsePosition(f,2,3,0.000001,15)
```

Output:

```
Iteration 1 , x2 = 2.78571 and f(x2) = -1.31086 
Iteration 2 , x2 = 2.85087 and f(x2) = -0.08392 
Iteration 3 , x2 = 2.85493 and f(x2) = -0.00513 
Iteration 4 , x2 = 2.85518 and f(x2) = -0.00031 
Iteration 5 , x2 = 2.85520 and f(x2) = -0.00002 
Iteration 6 , x2 = 2.85520 and f(x2) = -0.00000 
Iteration 7 , x2 = 2.85520 and f(x2) = -0.00000 

Required root is : 2.85520 
```


**2)** Write a Python program to evaluate f (1.7) by Newton’s forward difference formula using the given data.

| x | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| y = f(x) | 40 | 60 | 65 | 50 | 18 |

*Lab Book – Practical 6, Q.1 (same question)*

Program:

```python
from math import*
from numpy import *
x = [1, 2, 3, 4, 5]
y = [40, 60, 65, 50, 18]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=1.7
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[  1.  40.  20. -15.  -5.   8.]
 [  2.  60.   5. -20.   3.   0.]
 [  3.  65. -15. -17.   0.   0.]
 [  4.  50. -32.   0.   0.   0.]
 [  5.  18.   0.   0.   0.   0.]]
Newton's Forward interpolated value at xp is:  55.138200000000005
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>3</sup><sub>-3</sub> x<sup>2</sup> dx, using Trapezoidal rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Trapezoidal Q(1) (same question)*

Program:

```python
def f(x):
    return x**2
a = -3
b = 3
n = 12
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", xi,'and', "y =", yi)
# Final answer
print("Approximate integral:", result)
```

Output:

```
x = -3.0 and y = 9.0
x = -2.5 and y = 6.25
x = -2.0 and y = 4.0
x = -1.5 and y = 2.25
x = -1.0 and y = 1.0
x = -0.5 and y = 0.25
x = 0.0 and y = 0.0
x = 0.5 and y = 0.25
x = 1.0 and y = 1.0
x = 1.5 and y = 2.25
x = 2.0 and y = 4.0
x = 2.5 and y = 6.25
x = 3.0 and y = 9.0
Approximate integral: 18.25
```


**2)** Write Python program to find f(10) , using Lagrange’s interpolation formula for the data: f(5) = 12, f(6) = 13, f(9) = 14, f(11) = 16.

*Lab Book – Practical 8, Q.2 (same question)*

Program:

```python
from math import*
from numpy import*
x = [5, 6, 9, 11]
y = [12, 13, 14, 16]
n=len(x)
yp=0 # Initialize the interpolated value
xp=10
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 10 is 14.666666666666668
```


**3)** Write a python program to find y (2.2), for the differential equation dy/dx = −xy<sup>2</sup> by Euler’s Modified Method where y(2) = 1 take h = 0.1.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(1) (same question) – same program, equation dy/dx = −xy², y(2)=1, h=0.1*

Program:

```python
def f(x, y):
    return -x * y**2
x = 2
y = 1
h = 0.1
while x < 2.2:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
print("y(2.2) =", f"{y:.4f}")
```

Output:

```
y(2.2) = 0.7080
```


---

## Slip No. 2

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> – 10x<sup>2</sup> + 5 = 0 in [ 0, 1], using False Position method the program should terminate when relative error is of order 10<sup>−6</sup> or perform 25 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.2 – same equation, interval [0, 1] as given in the slip*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.6f and f(x2) = %0.6f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.6f ' % x2)

def f(x):
    return x**3 - 10*x**2 + 5
falsePosition(f,0,1,0.000001,25)
```

Output:

```
Iteration 1 , x2 = 0.555556 and f(x2) = 2.085048 
Iteration 2 , x2 = 0.707845 and f(x2) = 0.344218 
Iteration 3 , x2 = 0.730994 and f(x2) = 0.047085 
Iteration 4 , x2 = 0.734124 and f(x2) = 0.006270 
Iteration 5 , x2 = 0.734540 and f(x2) = 0.000832 
Iteration 6 , x2 = 0.734595 and f(x2) = 0.000110 
Iteration 7 , x2 = 0.734602 and f(x2) = 0.000015 
Iteration 8 , x2 = 0.734603 and f(x2) = 0.000002 
Iteration 9 , x2 = 0.734603 and f(x2) = 0.000000 

Required root is : 0.734603 
```


**2)** Write a Python program to evaluate f (1.7) by Newton’s backward difference formula using the given data.

| x | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| y = f(x) | 40 | 60 | 65 | 50 | 18 |

*Lab Book – Practical 6, Q.7–Q.12 (Newton’s backward interpolation)*

Program:

```python
from math import*
from numpy import*
x=[1, 2, 3, 4, 5]
y=[40, 60, 65, 50, 18]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=1.7
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  55.13820000000001
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>7</sup><sub>1</sub> (1/x) dx, using Simpson’s (1/3)rd rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
def f(x):
    return 1 / x
a = 1
b = 7
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 1.0000 and y = 1.0000
x = 1.5000 and y = 0.6667
x = 2.0000 and y = 0.5000
x = 2.5000 and y = 0.4000
x = 3.0000 and y = 0.3333
x = 3.5000 and y = 0.2857
x = 4.0000 and y = 0.2500
x = 4.5000 and y = 0.2222
x = 5.0000 and y = 0.2000
x = 5.5000 and y = 0.1818
x = 6.0000 and y = 0.1667
x = 6.5000 and y = 0.1538
x = 7.0000 and y = 0.1429
Approximate integral = 1.9473
```


**2)** Write Python program to prepare divided difference table for the data:

| x | 1 | 2 | 5 | 7 |
|---|---|---|---|---|
| y = f(x) | 6 | 9 | 30 | 54 |

*Lab Book – Practical 5, Q.2 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [1, 2, 5, 7]
y = [6, 9, 30, 54]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

   x   y  Δ^1y Δ^2y Δ^3y
0  1   6   3.0  1.0  0.0
1  2   9   7.0  1.0     
2  5  30  12.0          
3  7  54                
```


**3)** Write a python program to solve the differential equation, dy/dx = (x + y) for x = 0 to x = 0.3 by Runge-Kutta second order Method where y(0) = 1 take h = 0.1.

*Lab Book – Practical 12, (i) RK 2nd order Q(1) (same question)*

Program:

```python
def f(x, y):
    return x + y
x = 0
y = 1
h = 0.1
xn = 0.3
while x < xn:
    k1 = h * f(x, y)
    k2 = h * f(x + h, y + k1)
    y = y + (k1 + k2) / 2
    x = x + h
print("Approximate solution at x =", xn, "is", f"{y:.4f}")
```

Output:

```
Approximate solution at x = 0.3 is 1.3985
```


---

## Slip No. 3

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of equation 3x − cos(x) – 1 = 0, using Bisection method correct up to three decimal places. Plot the graph of function y = f(x), also plot the roots obtained.

*Lab Book – Practical 2, Q.5 (same question) – 3x − cos(x) − 1; 12 iterations are used so that the root is correct to three decimals*

Program:

```python
import matplotlib.pyplot as plt
import numpy as np # Import numpy
def f(x):
    return 3*x-np.cos(x)-1 # Use np.cos instead of math.cos
midpoints = [] # Define midpoints list here
def bisection(f, a, b, max_iteration):
    for i in range(max_iteration):
        print(f"Iteration {i+1}. ",end='')
        mid = (a + b) / 2
        midpoints.append(mid)
        print(f"{mid:.4f}")
        if f(a)*f(mid)<0:
            [a, b]=[a, mid]
        elif f(mid)*f(b)<0:
            [a, b]=[mid, b]
        else:
            return mid
    print("Approximate Root of the equation is:",mid)
root = bisection(f, 0, 1, 12)

x = np.linspace(0, 3, 400)
y = f(x)
plt.plot(x, y, label='f(x) = 3x-cos(x)-1', color='blue')
plt.axhline(0, color='black', linewidth=1)
plt.grid(True)
plt.xlabel("x")
plt.ylabel("f(x)")
plt.title("Bisection Method: Convergence Near the Root")
# Plot all midpoints
y_mid = [f(x) for x in midpoints]
plt.plot(midpoints, y_mid, 'ro-', label='Midpoints')
# Annotate each midpoint
for i, (x_pt, y_pt) in enumerate(zip(midpoints, y_mid), start=1):
    plt.text(x_pt, y_pt ,f"x{i}",fontsize=8,color='red',ha='right',
    va='bottom')
# Zoom in on the root area
plt.xlim(-0.5, 1.5) # Adjusted zoom range to be around ln(2)
plt.ylim(-1, 1)
plt.legend()
plt.show()
```

Output:

```
Iteration 1. 0.5000
Iteration 2. 0.7500
Iteration 3. 0.6250
Iteration 4. 0.5625
Iteration 5. 0.5938
Iteration 6. 0.6094
Iteration 7. 0.6016
Iteration 8. 0.6055
Iteration 9. 0.6074
Iteration 10. 0.6064
Iteration 11. 0.6069
Iteration 12. 0.6072
Approximate Root of the equation is: 0.607177734375
```

Graph:

![Slip 3 graph](Slip3_graph.png)


**2)** Write a Python program to evaluate f (1.7) by Newton’s divided difference formula using the given data.

| x | 1 | 2 | 5 | 7 |
|---|---|---|---|---|
| y = f(x) | 6 | 9 | 30 | 54 |

*Lab Book – Practical 7, Q.1–Q.7 (Newton’s divided difference interpolation)*

Program:

```python
from math import*
from numpy import*
x=[1, 2, 5, 7]
y=[6, 9, 30, 54]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=1.7
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  7.89
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>π</sup><sub>0</sub> sin (x) dx, using Trapezoidal rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Trapezoidal Q(2) (same question)*

Program:

```python
import math

def f(x):
    return math.sin(x)
a = 0
b = math.pi
n = 12
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 0.0000
x = 0.2618 and y = 0.2588
x = 0.5236 and y = 0.5000
x = 0.7854 and y = 0.7071
x = 1.0472 and y = 0.8660
x = 1.3090 and y = 0.9659
x = 1.5708 and y = 1.0000
x = 1.8326 and y = 0.9659
x = 2.0944 and y = 0.8660
x = 2.3562 and y = 0.7071
x = 2.6180 and y = 0.5000
x = 2.8798 and y = 0.2588
x = 3.1416 and y = 0.0000
Approximate integral = 1.9886
```


**2)** Write Python program to prepare forward difference table for the given data:

| x | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| y = f(x) | 40 | 60 | 65 | 50 | 18 |

*Lab Book – Practical 4, Q.1–Q.3 (forward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [1, 2, 3, 4, 5]
y = [40, 60, 65, 50, 18]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        D[i,j] = D[i+1,j-1] - D[i,j-1]

columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)] #'Δ' - Unicode for capital delta
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)

df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Forward Difference Table:\n")
print(df)
```

Output:

```
Newton's Forward Difference Table:

   x   y  Δ^1y  Δ^2y Δ^3y Δ^4y
0  1  40  20.0 -15.0 -5.0  8.0
1  2  60   5.0 -20.0  3.0     
2  3  65 -15.0 -17.0          
3  4  50 -32.0                
4  5  18                      
```


**3)** Write a python program to find y(0.1) and y (0.2), for the differential equation dy/dx = y − x by Runge-Kutta Fourth order Method where y(0) = 2 take h = 0.1.

*Lab Book – Practical 12, (ii) RK 4th order Q(1) (same question)*

Program:

```python
def f(x, y):
    return y - x
x = 0
y = 2
h = 0.1
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 0.1 ) = 2.2052
y( 0.2 ) = 2.4214
```


---

## Slip No. 4

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of algebraic equation x<sup>3</sup>− 2x +1 = 0 in interval [ –1, 0], using Newton Raphson method correct up to five decimal or perform 15 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.3 – same equation*

> Note: the starting value x0 = −1 is taken from the given interval; f(−1) and f(0) have the same sign, so the iteration converges to the nearby root −1.61803.

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.5f and f(x1) =%0.5f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.5f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return x**3 - 2*x + 1

def g(x):
    return 3*x**2 - 2

newtonRaphson(f ,g , -1 ,0.00001 ,15)
```

Output:

```
Iteration 1 , x1=-3.00000 and f(x1) =-20.00000 
Iteration 2 , x1=-2.20000 and f(x1) =-5.24800 
Iteration 3 , x1=-1.78083 and f(x1) =-1.08599 
Iteration 4 , x1=-1.63630 and f(x1) =-0.10858 
Iteration 5 , x1=-1.61830 and f(x1) =-0.00158 
Iteration 6 , x1=-1.61803 and f(x1) =-0.00000 

 Required root is :-1.61803
```


**2)** Write a Python program to evaluate f (97) by Newton’s backward difference formula using the given data.

| x | 80 | 85 | 90 | 95 | 100 |
|---|---|---|---|---|---|
| y = f(x) | 5026 | 5674 | 6362 | 7088 | 7854 |

*Lab Book – Practical 6, Q.8 (same question)*

Program:

```python
from math import*
from numpy import*
x=[80, 85, 90, 95, 100]
y=[5026, 5674, 6362, 7088, 7854]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=97
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  7389.3535999999995
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>1</sup><sub>0</sub> x e<sup>x</sup> dx, using Simpson’s 1/3rd rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
import math

def f(x):
    return x * math.exp(x)
a = 0
b = 1
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 0.0000
x = 0.0833 and y = 0.0906
x = 0.1667 and y = 0.1969
x = 0.2500 and y = 0.3210
x = 0.3333 and y = 0.4652
x = 0.4167 and y = 0.6320
x = 0.5000 and y = 0.8244
x = 0.5833 and y = 1.0453
x = 0.6667 and y = 1.2985
x = 0.7500 and y = 1.5878
x = 0.8333 and y = 1.9175
x = 0.9167 and y = 2.2925
x = 1.0000 and y = 2.7183
Approximate integral = 1.0000
```


**2)** Write Python program to find f(4) , using Lagrange’s interpolation formula for the data: f(1) = 6, f(2) = 9, f(5) = 30, f(7) = 54.

*Lab Book – Practical 8, Q.3 (same question)*

Program:

```python
from math import*
from numpy import*
x = [1, 2, 5, 7]
y = [6, 9, 30, 54]
n=len(x)
yp=0 # Initialize the interpolated value
xp=4
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 4 is 21.0
```


**3)** Write a python program to find y (1), for the differential equation dy/dx = −2xy<sup>2</sup> by Euler’s Modified Method where y(0) = 1 take h = 0.2.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(2) (same question) – program of Q(1)*

Program:

```python
def f(x, y):
    return -2 * x * y**2
x = 0
y = 1
h = 0.2
while x < 1:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
print("y(1) =", f"{y:.4f}")
```

Output:

```
y(1) = 0.5033
```


---

## Slip No. 5

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x log<sub>10</sub>(x) −1.2 = 0, using Bisection method the program should terminate when relative error is of order 10<sup>−4</sup> or perform 25 number of iterations whichever occurs earlier.

*Lab Book – Practical 2, Q.4 (same question)*

> Note: the slip gives no interval; [2, 3] is used (f(2) < 0 and f(3) > 0), as in the lab book.

Program:

```python
from math import *
def f(x):
  return x*log10(x)-1.2

def bisection(f , a, b, tol,max_iteration):
  a = float (a)
  b = float (b)
  tol = float (tol)
  if f(a) * f(b) > 0:
     print("Invalid interval: f(a) and f(b) must have opposite signs")
  else:
      for i in range(max_iteration):
        if (b-a)/2 > tol:
          print(f"Iteration {i+1}. ",end='')
          c = (a + b) / 2
          print(f"{c:.3f}")
          if f(a)*f(c)<0:
             [a, b]=[a, c]
          elif f(c)*f(b)<0:
             [a, b]=[c, b]
          else:
            return c
      print("Approximate Root of the equation is:",f"{c:.3f}")

bisection(f,2,3,0.0001,25)
```

Output:

```
Iteration 1. 2.500
Iteration 2. 2.750
Iteration 3. 2.625
Iteration 4. 2.688
Iteration 5. 2.719
Iteration 6. 2.734
Iteration 7. 2.742
Iteration 8. 2.738
Iteration 9. 2.740
Iteration 10. 2.741
Iteration 11. 2.741
Iteration 12. 2.740
Iteration 13. 2.741
Approximate Root of the equation is: 2.741
```


**2)** Write a Python program to evaluate f (1.7) by Newton’s divided difference formula using the given data.

| x | 0 | 1 | 2 | 5 |
|---|---|---|---|---|
| y = f(x) | 5 | 13 | 22 | 129 |

*Lab Book – Practical 7, Q.3 (same question)*

Program:

```python
from math import*
from numpy import*
x=[0, 1, 2, 5]
y=[5, 13, 22, 129]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=1.7
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  18.7547
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>5</sup><sub>2</sub> (x<sup>2</sup> − 2x + 1) dx, using Trapezoidal rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Trapezoidal Exercise Q(1) (same question)*

Program:

```python
def f(x):
    return x**2 - 2*x + 1
a = 2
b = 5
n = 12
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 2.0000 and y = 1.0000
x = 2.2500 and y = 1.5625
x = 2.5000 and y = 2.2500
x = 2.7500 and y = 3.0625
x = 3.0000 and y = 4.0000
x = 3.2500 and y = 5.0625
x = 3.5000 and y = 6.2500
x = 3.7500 and y = 7.5625
x = 4.0000 and y = 9.0000
x = 4.2500 and y = 10.5625
x = 4.5000 and y = 12.2500
x = 4.7500 and y = 14.0625
x = 5.0000 and y = 16.0000
Approximate integral = 21.0312
```


**2)** Write Python program to prepare backward difference table for the data: f(1) = 40, f(2) = 60 , f(3) = 65, f(4) = 50 , f(5) = 18

| x | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| y = f(x) | 40 | 60 | 65 | 50 | 18 |

*Lab Book – Practical 4, Q.4–Q.7 (backward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [1, 2, 3, 4, 5]
y = [40, 60, 65, 50, 18]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(j, n):
        D[i,j] = D[i,j-1] - D[i-1,j-1]
columns = ['y'] + [f'∇^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(j, n):
        df.loc[i, f'∇^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Backward Difference Table:\n")
print(df)
```

Output:

```
Newton's Backward Difference Table:

   x   y  ∇^1y  ∇^2y ∇^3y ∇^4y
0  1  40                      
1  2  60  20.0                
2  3  65   5.0 -15.0          
3  4  50 -15.0 -20.0 -5.0     
4  5  18 -32.0 -17.0  3.0  8.0
```


**3)** Write a python program to find y (0.6), for the differential equation dy/dx = 1 + y<sup>2</sup> by Runge-Kutta second order Method where y(0) = 0 take h = 0.2.

*Lab Book – Practical 12, (i) RK 2nd order Q(1)*

Program:

```python
def f(x, y):
    return 1 + y**2
x = 0
y = 0
h = 0.2
xn = 0.6
while x < xn:
    k1 = h * f(x, y)
    k2 = h * f(x + h, y + k1)
    y = y + (k1 + k2) / 2
    x = x + h
print("Approximate solution at x =", xn, "is", f"{y:.4f}")
```

Output:

```
Approximate solution at x = 0.6 is 0.6870
```


---

## Slip No. 6

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the algebraic equation x<sup>3</sup> – x<sup>2</sup> – 2 = 0 between 1 and 2, using Newton Raphson method. The program should terminate when relative error is of order 0.000001 or perform n number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.3 / Q.4 (Newton-Raphson)*

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.6f and f(x1) =%0.6f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.6f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return x**3 - x**2 - 2

def g(x):
    return 3*x**2 - 2*x

newtonRaphson(f ,g , 1 ,0.000001 ,20)
```

Output:

```
Iteration 1 , x1=3.000000 and f(x1) =16.000000 
Iteration 2 , x1=2.238095 and f(x1) =4.201706 
Iteration 3 , x1=1.839868 and f(x1) =0.843048 
Iteration 4 , x1=1.709680 and f(x1) =0.074396 
Iteration 5 , x1=1.695773 and f(x1) =0.000796 
Iteration 6 , x1=1.695621 and f(x1) =0.000000 

 Required root is :1.695621
```


**2)** Write a Python program to evaluate f (1.8) by Newton’s forward difference formula using the given data.

| x | 1.5 | 1.7 | 1.9 | 2.1 | 2.3 |
|---|---|---|---|---|---|
| y = f(x) | 1494 | 1691 | 1888 | 2084 | 2279 |

*Lab Book – Practical 6, Q.2 (same question)*

Program:

```python
from math import*
from numpy import *
x = [1.5, 1.7, 1.9, 2.1, 2.3]
y = [1494, 1691, 1888, 2084, 2279]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=1.8
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[ 1.500e+00  1.494e+03  1.970e+02  0.000e+00 -1.000e+00  1.000e+00]
 [ 1.700e+00  1.691e+03  1.970e+02 -1.000e+00  0.000e+00  0.000e+00]
 [ 1.900e+00  1.888e+03  1.960e+02 -1.000e+00  0.000e+00  0.000e+00]
 [ 2.100e+00  2.084e+03  1.950e+02  0.000e+00  0.000e+00  0.000e+00]
 [ 2.300e+00  2.279e+03  0.000e+00  0.000e+00  0.000e+00  0.000e+00]]
Newton's Forward interpolated value at xp is:  1789.5859375
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>2</sup><sub>1</sub> (x<sup>2</sup> − 10) dx, using Simpson’s 3/8th rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3) and Exercise Q(1) (same question)*

Program:

```python
def f(x):
    return x**2 - 10
a = 1
b = 2
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 1.0000 and y = -9.0000
x = 1.0833 and y = -8.8264
x = 1.1667 and y = -8.6389
x = 1.2500 and y = -8.4375
x = 1.3333 and y = -8.2222
x = 1.4167 and y = -7.9931
x = 1.5000 and y = -7.7500
x = 1.5833 and y = -7.4931
x = 1.6667 and y = -7.2222
x = 1.7500 and y = -6.9375
x = 1.8333 and y = -6.6389
x = 1.9167 and y = -6.3264
x = 2.0000 and y = -6.0000
Approximate integral = -7.6667
```


**2)** Write Python program to prepare divided difference table for the data:

| x | 2 | 4 | 9 | 10 |
|---|---|---|---|---|
| y = f(x) | 4 | 56 | 711 | 980 |

*Lab Book – Practical 5, Q.3 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [2, 4, 9, 10]
y = [4, 56, 711, 980]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

    x    y   Δ^1y  Δ^2y Δ^3y
0   2    4   26.0  15.0  1.0
1   4   56  131.0  23.0     
2   9  711  269.0           
3  10  980                  
```


**3)** Write a python program to find y (1.4), for the differential equation dy/dx = y<sup>2</sup> + x<sup>2</sup> by Runge-Kutta Fourth order Method where y(1) = 0 take h = 0.2.

*Lab Book – Practical 12, (ii) RK 4th order Q(1)*

Program:

```python
def f(x, y):
    return y**2 + x**2
x = 1
y = 0
h = 0.2
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 1.2 ) = 0.2463
y( 1.4 ) = 0.6228
```


---

## Slip No. 7

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup>−9x +1 = 0, using Regula-Falsi method correct up to five decimal places Or 15 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.1 (Regula-Falsi)*

> Note: the interval [0, 1] is chosen because f(0) = 1 > 0 and f(1) = −7 < 0.

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**3 - 9*x + 1
falsePosition(f,0,1,0.000001,15)
```

Output:

```
Iteration 1 , x2 = 0.12500 and f(x2) = -0.12305 
Iteration 2 , x2 = 0.11130 and f(x2) = -0.00036 
Iteration 3 , x2 = 0.11126 and f(x2) = -0.00000 

Required root is : 0.11126 
```


**2)** Write a Python program to evaluate f (48) by Newton’s backward difference formula using the given data.

| x | 30 | 35 | 40 | 45 | 50 |
|---|---|---|---|---|---|
| y = f(x) | 0.5 | 0.5736 | 0.5736 | 0.7071 | 0.766 |

*Lab Book – Practical 6, Q.9 (same question)*

Program:

```python
from math import*
from numpy import*
x=[30, 35, 40, 45, 50]
y=[0.5, 0.5736, 0.5736, 0.7071, 0.766]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=48
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  0.7819827199999999
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write a python program to estimate the value of the integral ∫<sup>5</sup><sub>0</sub> (1 + x<sup>3</sup>) dx, using Simpson’s 3/8th rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12 .

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3)*

Program:

```python
def f(x):
    return 1 + x**3
a = 0
b = 5
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 1.0000
x = 0.4167 and y = 1.0723
x = 0.8333 and y = 1.5787
x = 1.2500 and y = 2.9531
x = 1.6667 and y = 5.6296
x = 2.0833 and y = 10.0422
x = 2.5000 and y = 16.6250
x = 2.9167 and y = 25.8119
x = 3.3333 and y = 38.0370
x = 3.7500 and y = 53.7344
x = 4.1667 and y = 73.3380
x = 4.5833 and y = 97.2818
x = 5.0000 and y = 126.0000
Approximate integral = 161.2500
```


**2)** Write Python program to find f(4) , using Lagrange’s interpolation formula for the data: f(1) = 6, f(2) = 9, f(5) = 30, f(7) = 54.

*Lab Book – Practical 8, Q.3 (same question)*

Program:

```python
from math import*
from numpy import*
x = [1, 2, 5, 7]
y = [6, 9, 30, 54]
n=len(x)
yp=0 # Initialize the interpolated value
xp=4
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 4 is 21.0
```


**3)** Write a python program to find y (1), for the differential equation, dy/dx = 2 − xy<sup>2</sup> by Euler’s Method where y(0) = 1 take h = 0.2.

*Lab Book – Practical 11, (i) Euler’s method Q(1) (same question)*

Program:

```python
def f(x, y):
    return 2 - x * y**2
x0 = 0
y0 = 1
h = 0.2
xn = 1
while x0 < xn:
    y0 = y0 + h * f(x0, y0)
    x0 = x0 + h
print("Approximate solution at x =", xn, "is", y0)
```

Output:

```
Approximate solution at x = 1 is 1.7057884740561524
```


---

## Slip No. 8

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write python program to evaluate f(2) by Newton’s divided difference formula using the given data:

| x | -1 | 0 | 3 | 6 | 7 |
|---|---|---|---|---|---|
| y = f(x) | 3 | -6 | 39 | 822 | 1611 |

*Lab Book – Practical 7, Q.4 (same question)*

Program:

```python
from math import*
from numpy import*
x=[-1, 0, 3, 6, 7]
y=[3, -6, 39, 822, 1611]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=2
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  6.0
```


**2)** Write a Python program to estimate a root of the equation x − cos(x) = 0, using Bisection method correct up to four decimal places or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 2, Q.3 (Bisection, correct up to n decimal places)*

> Note: the slip gives no interval; [0, 1] is used (f(0) = −1 < 0 and f(1) > 0).

Program:

```python
from math import *
def f(x):
  return x-cos(x)

def bisection(f , a, b, tol,max_iteration):
  a = float (a)
  b = float (b)
  tol = float (tol)
  if f(a) * f(b) > 0:
     print("Invalid interval: f(a) and f(b) must have opposite signs")
  else:
      for i in range(max_iteration):
        if (b-a)/2 > tol:
          print(f"Iteration {i+1}. ",end='')
          c = (a + b) / 2
          print(f"{c:.4f}")
          if f(a)*f(c)<0:
             [a, b]=[a, c]
          elif f(c)*f(b)<0:
             [a, b]=[c, b]
          else:
            return c
      print("Approximate Root of the equation is:",f"{c:.4f}")

bisection(f,0,1,0.00005,20)
```

Output:

```
Iteration 1. 0.5000
Iteration 2. 0.7500
Iteration 3. 0.6250
Iteration 4. 0.6875
Iteration 5. 0.7188
Iteration 6. 0.7344
Iteration 7. 0.7422
Iteration 8. 0.7383
Iteration 9. 0.7402
Iteration 10. 0.7393
Iteration 11. 0.7388
Iteration 12. 0.7390
Iteration 13. 0.7391
Iteration 14. 0.7391
Approximate Root of the equation is: 0.7391
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare Newton’s forward difference table for following information.

| x | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
|---|---|---|---|---|---|---|---|
| y = f(x) | 18 | 25 | 40 | 70 | 90 | 100 | 110 |

*Lab Book – Practical 4, Q.1–Q.3 (forward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [10, 11, 12, 13, 14, 15, 16]
y = [18, 25, 40, 70, 90, 100, 110]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        D[i,j] = D[i+1,j-1] - D[i,j-1]

columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)] #'Δ' - Unicode for capital delta
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)

df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Forward Difference Table:\n")
print(df)
```

Output:

```
Newton's Forward Difference Table:

    x    y  Δ^1y  Δ^2y  Δ^3y  Δ^4y  Δ^5y  Δ^6y
0  10   18   7.0   8.0   7.0 -32.0  57.0 -72.0
1  11   25  15.0  15.0 -25.0  25.0 -15.0      
2  12   40  30.0 -10.0   0.0  10.0            
3  13   70  20.0 -10.0  10.0                  
4  14   90  10.0   0.0                        
5  15  100  10.0                              
6  16  110                                    
```


**2)** Write a python program to find y(0.1) and y(0.2) for the differential equation dy/dx = y − x by Runge-kutta second order method where, y(0)=2 take h=0.1.

*Lab Book – Practical 12, (i) RK 2nd order Q(2)*

Program:

```python
def f(x, y):
    return y - x
x = 0
y = 2
h = 0.1
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h, y + k1)
    y = y + (k1 + k2) / 2
    x = x + h
    print("y(", f"{x:.1f}", ") =", f"{y:.4f}")
```

Output:

```
y( 0.1 ) = 2.2050
y( 0.2 ) = 2.4210
```


**3)** Write a python program to estimate the value of the integral ∫<sup>1</sup><sub>0</sub> (4x − 3x<sup>2</sup>)dx, using Trapezoidal rule, use n = 10 . Print all values of xi and yi = f(xi), i = 0,1,2,3…10.

*Lab Book – Practical 10, Trapezoidal Q(1) / Q(2)*

Program:

```python
def f(x):
    return 4*x - 3*x**2
a = 0
b = 1
n = 10
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 0.0000
x = 0.1000 and y = 0.3700
x = 0.2000 and y = 0.6800
x = 0.3000 and y = 0.9300
x = 0.4000 and y = 1.1200
x = 0.5000 and y = 1.2500
x = 0.6000 and y = 1.3200
x = 0.7000 and y = 1.3300
x = 0.8000 and y = 1.2800
x = 0.9000 and y = 1.1700
x = 1.0000 and y = 1.0000
Approximate integral = 0.9950
```


---

## Slip No. 9

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> − 4x + 1 = 0 in [ 0, 1], using Regula-Falsi method the program should terminate when relative error is of order 10<sup>−5</sup> or perform 25 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.2 (Regula-Falsi)*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**3 - 4*x + 1
falsePosition(f,0,1,0.00001,25)
```

Output:

```
Iteration 1 , x2 = 0.33333 and f(x2) = -0.29630 
Iteration 2 , x2 = 0.25714 and f(x2) = -0.01157 
Iteration 3 , x2 = 0.25420 and f(x2) = -0.00038 
Iteration 4 , x2 = 0.25410 and f(x2) = -0.00001 
Iteration 5 , x2 = 0.25410 and f(x2) = -0.00000 

Required root is : 0.25410 
```


**2)** Write python program to evaluate f(8) by Newton’s backward interpolation formula using the given data:

| x | 1 | 3 | 5 | 7 | 9 |
|---|---|---|---|---|---|
| y = f(x) | 8 | 12 | 21 | 36 | 62 |

*Lab Book – Practical 6, Q.10 (same question)*

Program:

```python
from math import*
from numpy import*
x=[1, 3, 5, 7, 9]
y=[8, 12, 21, 36, 62]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=8
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  47.15625
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to find f(2) if f(0) = 12, f(3) = 6 and f(4) = 8 by using Lagrange’s interpolation formula.

*Lab Book – Practical 8, Q.5 (same question)*

Program:

```python
from math import*
from numpy import*
x = [0, 3, 4]
y = [12, 6, 8]
n=len(x)
yp=0 # Initialize the interpolated value
xp=2
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 2 is 6.0
```


**2)** Write a python program to find y(0.05) and y(0.1) for the differential equation dy/dx = x<sup>2</sup> + y by using Euler’s modified method where, y(0)=1 take h=0.05.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(1)*

Program:

```python
def f(x, y):
    return x**2 + y
x = 0
y = 1
h = 0.05
while x < 0.1:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
    print(f"y({x:.2f}) = {y:.4f}")
```

Output:

```
y(0.05) = 1.0513
y(0.10) = 1.1055
```


**3)** Write a python program to estimate the value of the integral ∫<sup>1</sup><sub>0</sub> 1/(1+x) dx, using Simpson’s One-Third rule, use n = 8 . Print all values of xi and yi = f(xi), i = 0,1,2,3…8.

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
def f(x):
    return 1 / (1 + x)
a = 0
b = 1
n = 8
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 1.0000
x = 0.1250 and y = 0.8889
x = 0.2500 and y = 0.8000
x = 0.3750 and y = 0.7273
x = 0.5000 and y = 0.6667
x = 0.6250 and y = 0.6154
x = 0.7500 and y = 0.5714
x = 0.8750 and y = 0.5333
x = 1.0000 and y = 0.5000
Approximate integral = 0.6932
```


---

## Slip No. 10

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write python program to evaluate f(1) by Newton’s Forward interpolation formula using the given data:

| x | 2 | 4 | 6 | 8 | 10 |
|---|---|---|---|---|---|
| y = f(x) | 5 | 10 | 17 | 29 | 50 |

*Lab Book – Practical 6, Q.3*

Program:

```python
from math import*
from numpy import *
x = [2, 4, 6, 8, 10]
y = [5, 10, 17, 29, 50]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=1
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[ 2.  5.  5.  2.  3.  1.]
 [ 4. 10.  7.  5.  4.  0.]
 [ 6. 17. 12.  9.  0.  0.]
 [ 8. 29. 21.  0.  0.  0.]
 [10. 50.  0.  0.  0.  0.]]
Newton's Forward interpolated value at xp is:  2.5859375
```


**2)** Write a Python program to estimate a root of the equation 2x<sup>3</sup> − 3x − 6 = 0, using Newton’s Raphson method correct up to five decimal places or perform 15 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.3 / Q.4 (Newton-Raphson)*

> Note: f(1) < 0 and f(2) > 0, so the starting value x0 = 2 is taken.

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.5f and f(x1) =%0.5f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.5f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return 2*x**3 - 3*x - 6

def g(x):
    return 6*x**2 - 3

newtonRaphson(f ,g , 2 ,0.00001 ,15)
```

Output:

```
Iteration 1 , x1=1.80952 and f(x1) =0.42155 
Iteration 2 , x1=1.78420 and f(x1) =0.00693 
Iteration 3 , x1=1.78377 and f(x1) =0.00000 

 Required root is :1.78377
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare divided difference table for following information.

| x | 0 | 1 | 4 | 5 |
|---|---|---|---|---|
| y = f(x) | 8 | 11 | 68 | 123 |

*Lab Book – Practical 5, Q.4 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [0, 1, 4, 5]
y = [8, 11, 68, 123]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

   x    y  Δ^1y Δ^2y Δ^3y
0  0    8   3.0  4.0  1.0
1  1   11  19.0  9.0     
2  4   68  55.0          
3  5  123                
```


**2)** Write a python program to find y(1.1) , y(1.2) and y(1.3) for the differential equation dy/dx = xy by Euler’s method where, y(1)=5 take h=0.1.

*Lab Book – Practical 11, (i) Euler’s method Q(2)*

Program:

```python
def f(x, y):
    return x * y

x0 = 1
y0 = 5
h = 0.1
xn = 1.3

while x0 < xn:
    y0 = y0 + h * f(x0, y0)
    x0 = x0 + h
    print(f"y({x0:.1f}) = {y0:.4f}")
```

Output:

```
y(1.1) = 5.5000
y(1.2) = 6.1050
y(1.3) = 6.8376
```


**3)** Write a python program to estimate the value of the integral ∫<sup>6</sup><sub>0</sub> 1/(1+x<sup>4</sup>) dx, using Simpson’s Three-Eight rule, use n = 6 . Print all values of xi and yi = f(xi), i = 0,1,2,3…6.

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3)*

Program:

```python
def f(x):
    return 1 / (1 + x**4)
a = 0
b = 6
n = 6
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 1.0000
x = 1.0000 and y = 0.5000
x = 2.0000 and y = 0.0588
x = 3.0000 and y = 0.0122
x = 4.0000 and y = 0.0039
x = 5.0000 and y = 0.0016
x = 6.0000 and y = 0.0008
Approximate integral = 1.0193
```


---

## Slip No. 11

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write python program to evaluate f(15) by Newton’s divided difference formula using the given data:

| x | 4 | 5 | 7 | 10 | 11 | 13 |
|---|---|---|---|---|---|---|
| y = f(x) | 48 | 100 | 294 | 900 | 1210 | 2028 |

*Lab Book – Practical 7, Q.5 (same question)*

Program:

```python
from math import*
from numpy import*
x=[4, 5, 7, 10, 11, 13]
y=[48, 100, 294, 900, 1210, 2028]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=15
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  3150.0
```


**2)** Write a Python program to estimate a root of the equation 8x<sup>3</sup> − 2x − 1 = 0 in [ 0, 1], using Regula-Falsi method the program should terminate when relative error is of order 10<sup>−4</sup> or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.2 (Regula-Falsi)*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return 8*x**3 - 2*x - 1
falsePosition(f,0,1,0.0001,20)
```

Output:

```
Iteration 1 , x2 = 0.16667 and f(x2) = -1.29630 
Iteration 2 , x2 = 0.33824 and f(x2) = -1.36691 
Iteration 3 , x2 = 0.48031 and f(x2) = -1.07417 
Iteration 4 , x2 = 0.57221 and f(x2) = -0.64556 
Iteration 5 , x2 = 0.62113 and f(x2) = -0.32520 
Iteration 6 , x2 = 0.64427 and f(x2) = -0.14916 
Iteration 7 , x2 = 0.65457 and f(x2) = -0.06546 
Iteration 8 , x2 = 0.65904 and f(x2) = -0.02817 
Iteration 9 , x2 = 0.66095 and f(x2) = -0.01202 
Iteration 10 , x2 = 0.66176 and f(x2) = -0.00511 
Iteration 11 , x2 = 0.66210 and f(x2) = -0.00217 
Iteration 12 , x2 = 0.66225 and f(x2) = -0.00092 
Iteration 13 , x2 = 0.66231 and f(x2) = -0.00039 
Iteration 14 , x2 = 0.66234 and f(x2) = -0.00017 
Iteration 15 , x2 = 0.66235 and f(x2) = -0.00007 

Required root is : 0.66235 
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare Newton’s forward difference table for following information.

| x | 2 | 3 | 4 | 5 |
|---|---|---|---|---|
| y = f(x) | 8 | 27 | 64 | 125 |

*Lab Book – Practical 4, Q.1–Q.3 (forward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [2, 3, 4, 5]
y = [8, 27, 64, 125]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        D[i,j] = D[i+1,j-1] - D[i,j-1]

columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)] #'Δ' - Unicode for capital delta
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)

df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Forward Difference Table:\n")
print(df)
```

Output:

```
Newton's Forward Difference Table:

   x    y  Δ^1y  Δ^2y Δ^3y
0  2    8  19.0  18.0  6.0
1  3   27  37.0  24.0     
2  4   64  61.0           
3  5  125                 
```


**2)** Write a python program to find y(0.2) and y(0.4) for the differential equation dy/dx = −2xy<sup>2</sup> by Runge-kutta fourth order method where, y(0)=1 take h=0.2.

*Lab Book – Practical 12, (ii) RK 4th order Q(1)*

Program:

```python
def f(x, y):
    return -2 * x * y**2
x = 0
y = 1
h = 0.2
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 0.2 ) = 0.9615
y( 0.4 ) = 0.8621
```


**3)** Write a python program to estimate the value of the integral ∫<sup>6</sup><sub>0</sub> 1/(1+x<sup>3</sup>) dx, using Simpson’s One-Third rule, use n = 6 . Print all values of xi and yi = f(xi), i = 0,1,2,3…6.

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
def f(x):
    return 1 / (1 + x**3)
a = 0
b = 6
n = 6
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 1.0000
x = 1.0000 and y = 0.5000
x = 2.0000 and y = 0.1111
x = 3.0000 and y = 0.0357
x = 4.0000 and y = 0.0154
x = 5.0000 and y = 0.0079
x = 6.0000 and y = 0.0046
Approximate integral = 1.1441
```


---

## Slip No. 12

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>2</sup> + 2x − 1 = 0 in [ 0, 1], using Bisection method the program should terminate when relative error is of order 10<sup>−4</sup> or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 2, Q.1 (same question)*

Program:

```python
def f(x):
  return x**2 + 2*x - 1

def bisection(f , a, b, tol,max_iteration):
  a = float (a)
  b = float (b)
  tol = float (tol)
  if f(a) * f(b) > 0:
     print("Invalid interval: f(a) and f(b) must have opposite signs")
  else:
      for i in range(max_iteration):
        if (b-a)/2 > tol:
          print(f"Iteration {i+1}: ",end='')
          c = (a + b) / 2
          print(f"{c:.4f}")
          if f(a)*f(c)<0:
             [a, b]=[a, c]
          elif f(c)*f(b)<0:
             [a, b]=[c, b]
          else:
            return c
      print("Approximate Root of the equation is:",f"{c:.4f}")

bisection(f,0,1,0.0001,20)
```

Output:

```
Iteration 1: 0.5000
Iteration 2: 0.2500
Iteration 3: 0.3750
Iteration 4: 0.4375
Iteration 5: 0.4062
Iteration 6: 0.4219
Iteration 7: 0.4141
Iteration 8: 0.4180
Iteration 9: 0.4160
Iteration 10: 0.4150
Iteration 11: 0.4146
Iteration 12: 0.4143
Iteration 13: 0.4142
Approximate Root of the equation is: 0.4142
```


**2)** Write python program to evaluate f(80) by Newton’s backward interpolation formula using the given data:

| x | 19 | 39 | 59 | 79 | 99 |
|---|---|---|---|---|---|
| y = f(x) | 41 | 103 | 168 | 218 | 235 |

*Lab Book – Practical 6, Q.11 (same question)*

Program:

```python
from math import*
from numpy import*
x=[19, 39, 59, 79, 99]
y=[41, 103, 168, 218, 235]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=80
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  219.78337499999998
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to f(10) using Lagrange’s interpolation formula for the following information:

| x | 5 | 6 | 9 | 11 |
|---|---|---|---|---|
| y = f(x) | 12 | 13 | 14 | 16 |

*Lab Book – Practical 8, Q.2 (same question)*

Program:

```python
from math import*
from numpy import*
x = [5, 6, 9, 11]
y = [12, 13, 14, 16]
n=len(x)
yp=0 # Initialize the interpolated value
xp=10
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 10 is 14.666666666666668
```


**2)** Write a python program to find y(0.1) and y(0.2) for the differential equation dy/dx = 1 − y by using Euler’s modified method where, y(0)=0 take h=0.1.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(1)*

Program:

```python
def f(x, y):
    return 1 - y
x = 0
y = 0
h = 0.1
while x < 0.2:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
    print(f"y({x:.1f}) = {y:.4f}")
```

Output:

```
y(0.1) = 0.0950
y(0.2) = 0.1810
```


**3)** Write a python program to estimate the value of the integral ∫<sup>5.2</sup><sub>4</sub> log x dx, using Simpson’s Three-Eight rule, use n = 6. Print all values of xi and yi = f(xi), i = 0,1,2,3…6.

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3)*

Program:

```python
import math

def f(x):
    return math.log(x)
a = 4
b = 5.2
n = 6
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 4.0000 and y = 1.3863
x = 4.2000 and y = 1.4351
x = 4.4000 and y = 1.4816
x = 4.6000 and y = 1.5261
x = 4.8000 and y = 1.5686
x = 5.0000 and y = 1.6094
x = 5.2000 and y = 1.6487
Approximate integral = 1.8278
```


---

## Slip No. 13

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> − 2x<sup>2</sup> − 4 = 0 in [ 2, 3], using Newton-Raphson method the program should terminate when relative error is of order 0.00001 or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.4 (same question)*

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.5f and f(x1) =%0.5f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.5f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return x**3 - 2*x**2 - 4

def g(x):
    return 3*x**2 - 4*x

newtonRaphson(f ,g , 2 ,0.00001 ,20)
```

Output:

```
Iteration 1 , x1=3.00000 and f(x1) =5.00000 
Iteration 2 , x1=2.66667 and f(x1) =0.74074 
Iteration 3 , x1=2.59722 and f(x1) =0.02860 
Iteration 4 , x1=2.59432 and f(x1) =0.00005 
Iteration 5 , x1=2.59431 and f(x1) =0.00000 

 Required root is :2.59431
```


**2)** Write python program to evaluate f(45) by Newton’s forward interpolation formula using the given data:

| x | 40 | 50 | 60 | 70 | 80 |
|---|---|---|---|---|---|
| y = f(x) | 35 | 83 | 153 | 193 | 215 |

*Lab Book – Practical 6, Q.4 (same question)*

Program:

```python
from math import*
from numpy import *
x = [40, 50, 60, 70, 80]
y = [35, 83, 153, 193, 215]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=45
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[ 40.  35.  48.  22. -52.  64.]
 [ 50.  83.  70. -30.  12.   0.]
 [ 60. 153.  40. -18.   0.   0.]
 [ 70. 193.  22.   0.   0.   0.]
 [ 80. 215.   0.   0.   0.   0.]]
Newton's Forward interpolated value at xp is:  50.5
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare Newton’s divided difference table for the following information:

| x | 5 | 6 | 9 | 11 |
|---|---|---|---|---|
| y = f(x) | 12 | 13 | 14 | 16 |

*Lab Book – Practical 5, Q.5 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [5, 6, 9, 11]
y = [12, 13, 14, 16]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

    x   y      Δ^1y      Δ^2y  Δ^3y
0   5  12       1.0 -0.166667  0.05
1   6  13  0.333333  0.133333      
2   9  14       1.0                
3  11  16                          
```


**2)** Write a python program to find y(1.1) and y(1.2) for the differential equation dy/dx = x + y<sup>2</sup> by using Runge-kutta second order method where, y(1)=1 take h=0.1.

*Lab Book – Practical 12, (i) RK 2nd order Q(2) (same question)*

Program:

```python
def f(x, y):
    return x + y**2
x = 1
y = 1
h = 0.1
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h, y + k1)
    y = y + (k1 + k2) / 2
    x = x + h
    print("y(", f"{x:.1f}", ") =", f"{y:.4f}")
```

Output:

```
y( 1.1 ) = 1.2270
y( 1.2 ) = 1.5279
```


**3)** Write a python program to estimate the value of the integral ∫<sup>4</sup><sub>0</sub> (x<sup>2</sup> + 2x + 9)dx, using Trapezoidal rule, use n = 8 . Print all values of xi and yi = f(xi), i = 0,1,2,3…8.

*Lab Book – Practical 10, Trapezoidal Q(1) / Q(2)*

Program:

```python
def f(x):
    return x**2 + 2*x + 9
a = 0
b = 4
n = 8
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 9.0000
x = 0.5000 and y = 10.2500
x = 1.0000 and y = 12.0000
x = 1.5000 and y = 14.2500
x = 2.0000 and y = 17.0000
x = 2.5000 and y = 20.2500
x = 3.0000 and y = 24.0000
x = 3.5000 and y = 28.2500
x = 4.0000 and y = 33.0000
Approximate integral = 73.5000
```


---

## Slip No. 14

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> − 5x + 1 = 0 in [ 2, 3], using Bisection method the program should terminate when relative error is of order 0.0001 or perform 25 number of iterations whichever occurs earlier.

*Lab Book – Practical 2, Exercise Q.1 (same question)*

Program:

```python
def f(x):
  return x**3 - 5*x + 1

def bisection(f , a, b, tol,max_iteration):
  a = float (a)
  b = float (b)
  tol = float (tol)
  if f(a) * f(b) > 0:
     print("Invalid interval: f(a) and f(b) must have opposite signs")
  else:
      for i in range(max_iteration):
        if (b-a)/2 > tol:
          print(f"Iteration {i+1}: ",end='')
          c = (a + b) / 2
          print(f"{c:.4f}")
          if f(a)*f(c)<0:
             [a, b]=[a, c]
          elif f(c)*f(b)<0:
             [a, b]=[c, b]
          else:
            return c
      print("Approximate Root of the equation is:",f"{c:.4f}")

bisection(f,2,3,0.0001,25)
```

Output:

```
Iteration 1: 2.5000
Iteration 2: 2.2500
Iteration 3: 2.1250
Iteration 4: 2.1875
Iteration 5: 2.1562
Iteration 6: 2.1406
Iteration 7: 2.1328
Iteration 8: 2.1289
Iteration 9: 2.1270
Iteration 10: 2.1279
Iteration 11: 2.1284
Iteration 12: 2.1287
Iteration 13: 2.1285
Approximate Root of the equation is: 2.1285
```


**2)** Write python program to evaluate f(35) by Lagrange’s interpolation formula for the given data:

| x | 25 | 30 | 40 | 50 |
|---|---|---|---|---|
| y = f(x) | 52 | 67 | 84 | 94 |

*Lab Book – Practical 8, Q.7 (same question)*

Program:

```python
from math import*
from numpy import*
x = [25, 30, 40, 50]
y = [52, 67, 84, 94]
n=len(x)
yp=0 # Initialize the interpolated value
xp=35
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 35 is 77.14999999999999
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare Newton’s Backward difference table for the following information:

| x | 10 | 12 | 14 | 16 |
|---|---|---|---|---|
| y = f(x) | 25 | 50 | 80 | 100 |

*Lab Book – Practical 4, Q.4–Q.7 (backward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [10, 12, 14, 16]
y = [25, 50, 80, 100]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(j, n):
        D[i,j] = D[i,j-1] - D[i-1,j-1]
columns = ['y'] + [f'∇^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(j, n):
        df.loc[i, f'∇^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Backward Difference Table:\n")
print(df)
```

Output:

```
Newton's Backward Difference Table:

    x    y  ∇^1y  ∇^2y  ∇^3y
0  10   25                  
1  12   50  25.0            
2  14   80  30.0   5.0      
3  16  100  20.0 -10.0 -15.0
```


**2)** Write a python program to find y(0.1), y(0.2), y(0.3), y(0.4) and y(0.5) for the differential equation dy/dx = (y−x)/(y+x) by using Euler’s method where, y(0)=1 take h=0.1.

*Lab Book – Practical 11, (i) Euler’s method Q(2) (same question)*

Program:

```python
def f(x, y):
    return (y - x) / (y + x)

x0 = 0
y0 = 1
h = 0.1
xn = 0.5

while x0 < xn:
    y0 = y0 + h * f(x0, y0)
    x0 = x0 + h
    print(f"y({x0:.1f}) = {y0:.4f}")
```

Output:

```
y(0.1) = 1.1000
y(0.2) = 1.1833
y(0.3) = 1.2544
y(0.4) = 1.3158
y(0.5) = 1.3692
```


**3)** Write a python program to estimate the value of the integral ∫<sup>2</sup><sub>-2</sub> (1/(5+2x)) dx, using Simpson’s one-Third rule, use n = 8 . Print all values of xi and yi = f(xi), i = 0,1,2,3…8.

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
def f(x):
    return 1 / (5 + 2*x)
a = -2
b = 2
n = 8
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = -2.0000 and y = 1.0000
x = -1.5000 and y = 0.5000
x = -1.0000 and y = 0.3333
x = -0.5000 and y = 0.2500
x = 0.0000 and y = 0.2000
x = 0.5000 and y = 0.1667
x = 1.0000 and y = 0.1429
x = 1.5000 and y = 0.1250
x = 2.0000 and y = 0.1111
Approximate integral = 1.1050
```


---

## Slip No. 15

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>2</sup> − log (x) − 12 = 0 in [ 3, 4], using False-position method the program should terminate when relative error is of order 10<sup>−4</sup> or perform 25 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.2 and Q.8 (Regula-Falsi with log)*

Program:

```python
import numpy as np
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**2 - np.log(x) - 12
falsePosition(f,3,4,0.0001,25)
```

Output:

```
Iteration 1 , x2 = 3.61061 and f(x2) = -0.24737 
Iteration 2 , x2 = 3.64428 and f(x2) = -0.01240 
Iteration 3 , x2 = 3.64596 and f(x2) = -0.00062 
Iteration 4 , x2 = 3.64604 and f(x2) = -0.00003 

Required root is : 3.64604 
```


**2)** Write python program to evaluate f(48) by Newton’s forward interpolation formula using the given data:

| x | 40 | 45 | 50 | 55 | 60 | 65 |
|---|---|---|---|---|---|---|
| y = f(x) | 210 | 253 | 307 | 381 | 413 | 492 |

*Lab Book – Practical 6, Q.5 (same question)*

Program:

```python
from math import*
from numpy import *
x = [40, 45, 50, 55, 60, 65]
y = [210, 253, 307, 381, 413, 492]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=48
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[ 40. 210.  43.  11.   9. -71. 222.]
 [ 45. 253.  54.  20. -62. 151.   0.]
 [ 50. 307.  74. -42.  89.   0.   0.]
 [ 55. 381.  32.  47.   0.   0.   0.]
 [ 60. 413.  79.   0.   0.   0.   0.]
 [ 65. 492.   0.   0.   0.   0.   0.]]
Newton's Forward interpolated value at xp is:  279.526656
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare Newton’s divided difference table for the following information:

| x | 0 | 1 | 2 |
|---|---|---|---|
| y = f(x) | 40.7 | 38.1 | 39.3 |

*Lab Book – Practical 5, Q.6 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [0, 1, 2]
y = [40.7, 38.1, 39.3]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

   x     y Δ^1y Δ^2y
0  0  40.7 -2.6  1.9
1  1  38.1  1.2     
2  2  39.3          
```


**2)** Write a python program to find y(0.1) and y(0.2) for the differential equation dy/dx = −y/(1+x) by using Euler’s modified method where, y(3)=2 take h=0.1.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(1)*

> Note: the slip prints y(3) = 2; since y(0.1) and y(0.2) are required, the initial condition is read as y(0) = 2.

Program:

```python
def f(x, y):
    return -y / (1 + x)
x = 0
y = 2
h = 0.1
while x < 0.2:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
    print(f"y({x:.1f}) = {y:.4f}")
```

Output:

```
y(0.1) = 1.8182
y(0.2) = 1.6667
```


**3)** Write a python program to estimate the value of the integral ∫<sup>2</sup><sub>-2</sub> (x/(5+2x)) dx, using Trapezoidal rule, use n = 8 . Print all values of xi and yi = f(xi), i = 0,1,2,3…8.

*Lab Book – Practical 10, Trapezoidal Q(1) / Q(2)*

Program:

```python
def f(x):
    return x / (5 + 2*x)
a = -2
b = 2
n = 8
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = -2.0000 and y = -2.0000
x = -1.5000 and y = -0.7500
x = -1.0000 and y = -0.3333
x = -0.5000 and y = -0.1250
x = 0.0000 and y = 0.0000
x = 0.5000 and y = 0.0833
x = 1.0000 and y = 0.1429
x = 1.5000 and y = 0.1875
x = 2.0000 and y = 0.2222
Approximate integral = -0.8418
```


---

## Slip No. 16

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> + 2x<sup>2</sup> + 10x − 20 = 0 in [ 1, 2], using Newton-Raphson method the program should terminate when relative error is of order 10<sup>−5</sup> or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.3 / Q.4 (Newton-Raphson)*

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.5f and f(x1) =%0.5f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.5f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return x**3 + 2*x**2 + 10*x - 20

def g(x):
    return 3*x**2 + 4*x + 10

newtonRaphson(f ,g , 1 ,0.00001 ,20)
```

Output:

```
Iteration 1 , x1=1.41176 and f(x1) =0.91757 
Iteration 2 , x1=1.36934 and f(x1) =0.01115 
Iteration 3 , x1=1.36881 and f(x1) =0.00000 

 Required root is :1.36881
```


**2)** Write python program to evaluate f(63) by Newton’s backward interpolation formula using the given data:

| x | 21 | 31 | 41 | 51 | 61 | 71 |
|---|---|---|---|---|---|---|
| y = f(x) | 20 | 24 | 29 | 36 | 46 | 51 |

*Lab Book – Practical 6, Q.12 (same question)*

Program:

```python
from math import*
from numpy import*
x=[21, 31, 41, 51, 61, 71]
y=[20, 24, 29, 36, 46, 51]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(n-1,j-2,-1):
         D[i,j]=D[i,j-1]-D[i-1,j-1]
xp=63
h=x[1]-x[0]
u=(xp-x[-1])/h
sum=0
pp=1
for i in range(1,n+1):
     sum=sum+(pp*D[-1,i])
     pp=pp*(u+(i-1))/(i)
print("Newton's Backward interpolated value at xp is = ",sum)
```

Output:

```
Newton's Backward interpolated value at xp is =  47.915776
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to find f(2) using Lagrange’s interpolation formula for the following information:

| x | 1 | 3 | 4 |
|---|---|---|---|
| y = f(x) | 10 | 27 | 65 |

*Lab Book – Practical 8, Q.8 (same question)*

Program:

```python
from math import*
from numpy import*
x = [1, 3, 4]
y = [10, 27, 65]
n=len(x)
yp=0 # Initialize the interpolated value
xp=2
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 2 is 8.666666666666668
```


**2)** Write a python program to find y(0.2) and y(0.4) for the differential equation dy/dx = 3x<sup>2</sup>y<sup>2</sup> by using Runge-kutta fourth order method where, y(0)=2 take h=0.2.

*Lab Book – Practical 12, (ii) RK 4th order Q(1)*

Program:

```python
def f(x, y):
    return 3 * x**2 * y**2
x = 0
y = 2
h = 0.2
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 0.2 ) = 2.0325
y( 0.4 ) = 2.2935
```


**3)** Write a python program to estimate the value of the integral ∫<sup>12</sup><sub>0</sub> (3x<sup>2</sup> + 2)dx, using Simpson’s Three-Eight rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12.

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3)*

Program:

```python
def f(x):
    return 3*x**2 + 2
a = 0
b = 12
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 2.0000
x = 1.0000 and y = 5.0000
x = 2.0000 and y = 14.0000
x = 3.0000 and y = 29.0000
x = 4.0000 and y = 50.0000
x = 5.0000 and y = 77.0000
x = 6.0000 and y = 110.0000
x = 7.0000 and y = 149.0000
x = 8.0000 and y = 194.0000
x = 9.0000 and y = 245.0000
x = 10.0000 and y = 302.0000
x = 11.0000 and y = 365.0000
x = 12.0000 and y = 434.0000
Approximate integral = 1752.0000
```


---

## Slip No. 17

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> + x<sup>2</sup> − 1 = 0 in [ 0, 1], using Regula-Falsi method the program should terminate when relative error is of order 10<sup>−5</sup> or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.2 (Regula-Falsi)*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**3 + x**2 - 1
falsePosition(f,0,1,0.00001,20)
```

Output:

```
Iteration 1 , x2 = 0.50000 and f(x2) = -0.62500 
Iteration 2 , x2 = 0.69231 and f(x2) = -0.18889 
Iteration 3 , x2 = 0.74119 and f(x2) = -0.04344 
Iteration 4 , x2 = 0.75197 and f(x2) = -0.00934 
Iteration 5 , x2 = 0.75426 and f(x2) = -0.00198 
Iteration 6 , x2 = 0.75475 and f(x2) = -0.00042 
Iteration 7 , x2 = 0.75485 and f(x2) = -0.00009 
Iteration 8 , x2 = 0.75487 and f(x2) = -0.00002 
Iteration 9 , x2 = 0.75488 and f(x2) = -0.00000 

Required root is : 0.75488 
```


**2)** Write python program to evaluate f(3) by Newton’s divided difference interpolation formula using the given data:

| x | 0 | 1 | 2 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| y = f(x) | 1 | 14 | 15 | 5 | 6 | 19 |

*Lab Book – Practical 7, Q.6 (same question)*

Program:

```python
from math import*
from numpy import*
x=[0, 1, 2, 4, 5, 6]
y=[1, 14, 15, 5, 6, 19]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=3
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  10.0
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare forward difference table for the following information:

| x | -1 | 0 | 1 | 2 |
|---|---|---|---|---|
| y = f(x) | 1 | 1 | 1 | -3 |

*Lab Book – Practical 4, Q.1–Q.3 (forward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [-1, 0, 1, 2]
y = [1, 1, 1, -3]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        D[i,j] = D[i+1,j-1] - D[i,j-1]

columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)] #'Δ' - Unicode for capital delta
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)

df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Forward Difference Table:\n")
print(df)
```

Output:

```
Newton's Forward Difference Table:

   x  y Δ^1y Δ^2y Δ^3y
0 -1  1  0.0  0.0 -4.0
1  0  1  0.0 -4.0     
2  1  1 -4.0          
3  2 -3               
```


**2)** Write a python program to find y(1.1) and y(1.2) for the differential equation dy/dx = (x<sup>2</sup>+y<sup>2</sup>)/x by using Runge-kutta second order method where, y(1)=2 take h=0.1.

*Lab Book – Practical 12, (i) RK 2nd order Q(2)*

Program:

```python
def f(x, y):
    return (x**2 + y**2) / x
x = 1
y = 2
h = 0.1
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h, y + k1)
    y = y + (k1 + k2) / 2
    x = x + h
    print("y(", f"{x:.1f}", ") =", f"{y:.4f}")
```

Output:

```
y( 1.1 ) = 2.5891
y( 1.2 ) = 3.4649
```


**3)** Write a python program to estimate the value of the integral ∫<sup>1/2</sup><sub>0</sub> (1/√(1−x<sup>2</sup>)) dx, using Trapezoidal rule, use n = 5 . Print all values of xi and yi = f(xi), i = 0,1,2,3…5.

*Lab Book – Practical 10, Trapezoidal Q(2)*

Program:

```python
import math

def f(x):
    return 1 / math.sqrt(1 - x**2)
a = 0
b = 0.5
n = 5
h = (b - a) / n
# Trapezoidal rule
result = f(a) + f(b)
for i in range(1, n):
    result += 2 * f(a + i * h)
result = result * h / 2
# Print xi and yi values
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and', "y =", f"{yi:.4f}")
# Final answer
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 1.0000
x = 0.1000 and y = 1.0050
x = 0.2000 and y = 1.0206
x = 0.3000 and y = 1.0483
x = 0.4000 and y = 1.0911
x = 0.5000 and y = 1.1547
Approximate integral = 0.5242
```


---

## Slip No. 18

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>3</sup> + 7x<sup>2</sup> + 9 = 0 in [ -8, -7], using Newton-Raphson method the program should terminate when relative error is of order 10<sup>−5</sup> or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.3 / Q.4 (Newton-Raphson)*

Program:

```python
def newtonRaphson(f ,g ,x0 ,e ,N):
    x0=float(x0)
    e=float (e)
    N=int (N)
    step=1
    flag=1
    condition=True
    while condition:
        if g(x0)==0.0:
            print('Divide by zero error!')
            break
        x1=x0-f(x0)/g(x0)
        print('Iteration %d , x1=%0.5f and f(x1) =%0.5f '% (step ,x1,f(x1)))
        x0=x1
        step=step+1
        if step>N:
            flag=0
            break
        condition= abs(f(x1)) >e
    if flag==1:
        print('\n Required root is :%0.5f' %x1 )
    else:
        print('\n Not convergent.')

def f(x):
    return x**3 + 7*x**2 + 9

def g(x):
    return 3*x**2 + 14*x

newtonRaphson(f ,g , -8 ,0.00001 ,20)
```

Output:

```
Iteration 1 , x1=-7.31250 and f(x1) =-7.71021 
Iteration 2 , x1=-7.17966 and f(x1) =-0.26123 
Iteration 3 , x1=-7.17484 and f(x1) =-0.00034 
Iteration 4 , x1=-7.17483 and f(x1) =-0.00000 

 Required root is :-7.17483
```


**2)** Write python program to evaluate f(0) by Lagrange’s interpolation formula using the given data:

| x | -1 | -2 | 2 | 4 |
|---|---|---|---|---|
| y = f(x) | -1 | -9 | 11 | 69 |

*Lab Book – Practical 8, Q.9 (same question)*

Program:

```python
from math import*
from numpy import*
x = [-1, -2, 2, 4]
y = [-1, -9, 11, 69]
n=len(x)
yp=0 # Initialize the interpolated value
xp=0
for i in range (n):
     L=1 # Initialize the Lagrange basis polynomial for the current 'i'
     for j in range (n):
         if j != i :
             L = L * (xp - x[j]) / (x[i] - x[j])
     yp= yp + y[i]*L
print(f"Lagrange's interpolating polynomial value at x = {xp} is {yp}")
```

Output:

```
Lagrange's interpolating polynomial value at x = 0 is 1.0
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare backward difference table for the following information:

| x | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| y = f(x) | -1 | -1 | 1 | 5 |

*Lab Book – Practical 4, Q.4–Q.7 (backward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [1, 2, 3, 4]
y = [-1, -1, 1, 5]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(j, n):
        D[i,j] = D[i,j-1] - D[i-1,j-1]
columns = ['y'] + [f'∇^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(j, n):
        df.loc[i, f'∇^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Backward Difference Table:\n")
print(df)
```

Output:

```
Newton's Backward Difference Table:

   x  y ∇^1y ∇^2y ∇^3y
0  1 -1               
1  2 -1  0.0          
2  3  1  2.0  2.0     
3  4  5  4.0  2.0  0.0
```


**2)** Write a python program to find y(0.2) and y(0.4) for the differential equation dy/dx = x<sup>2</sup>y<sup>2</sup>/y by using Runge-kutta fourth order method where, y(0)=2 take h=0.2.

*Lab Book – Practical 12, (ii) RK 4th order Q(1) / Q(2)*

Program:

```python
def f(x, y):
    return x**2 * y**2 / y
x = 0
y = 2
h = 0.2
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 0.2 ) = 2.0053
y( 0.4 ) = 2.0431
```


**3)** Write a python program to estimate the value of the integral ∫<sup>6</sup><sub>0</sub> (1/(3x<sup>2</sup>+2)) dx, using Simpson’s Three-Eight rule, use n = 12 . Print all values of xi and yi = f(xi), i = 0,1,2,3…12.

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3)*

Program:

```python
def f(x):
    return 1 / (3*x**2 + 2)
a = 0
b = 6
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}", 'and',"y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 0.0000 and y = 0.5000
x = 0.5000 and y = 0.3636
x = 1.0000 and y = 0.2000
x = 1.5000 and y = 0.1143
x = 2.0000 and y = 0.0714
x = 2.5000 and y = 0.0482
x = 3.0000 and y = 0.0345
x = 3.5000 and y = 0.0258
x = 4.0000 and y = 0.0200
x = 4.5000 and y = 0.0159
x = 5.0000 and y = 0.0130
x = 5.5000 and y = 0.0108
x = 6.0000 and y = 0.0091
Approximate integral = 0.5807
```


---

## Slip No. 19

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>2</sup> + 2x − 1 = 0 in [ -2, -3], using Bisection method the program should terminate when relative error is of order 0.0001 or perform 20 number of iterations whichever occurs earlier.

*Lab Book – Practical 2, Q.2 (same question)*

Program:

```python
def f(x):
  return x**2 + 2*x - 1

def bisection(f , a, b, tol,max_iteration):
  a = float (a)
  b = float (b)
  tol = float (tol)
  if f(a) * f(b) > 0:
     print("Invalid interval: f(a) and f(b) must have opposite signs")
  else:
      for i in range(max_iteration):
        if (b-a)/2 > tol:
          print(f"Iteration {i+1}: ",end='')
          c = (a + b) / 2
          print(f"{c:.4f}")
          if f(a)*f(c)<0:
             [a, b]=[a, c]
          elif f(c)*f(b)<0:
             [a, b]=[c, b]
          else:
            return c
      print("Approximate Root of the equation is:",f"{c:.4f}")

bisection(f,-3,-2,0.0001,20)
```

Output:

```
Iteration 1: -2.5000
Iteration 2: -2.2500
Iteration 3: -2.3750
Iteration 4: -2.4375
Iteration 5: -2.4062
Iteration 6: -2.4219
Iteration 7: -2.4141
Iteration 8: -2.4180
Iteration 9: -2.4160
Iteration 10: -2.4150
Iteration 11: -2.4146
Iteration 12: -2.4143
Iteration 13: -2.4142
Approximate Root of the equation is: -2.4142
```


**2)** Write python program to evaluate f(27) by Newton’s forward interpolation formula for the given data:

| x | 25 | 30 | 35 | 40 | 45 |
|---|---|---|---|---|---|
| y = f(x) | 50 | 67 | 84 | 94 | 101 |

*Lab Book – Practical 6, Q.6 (same question)*

Program:

```python
from math import*
from numpy import *
x = [25, 30, 35, 40, 45]
y = [50, 67, 84, 94, 101]
n = len(x)
D=zeros((n,n+1))
for i in range (0,n): #create forward difference table
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=D[i+1,j-1]-D[i,j-1]
print("Forward difference table:")
print(D)
xp=27
h=x[1]-x[0]
u=(xp-x[0])/h
sum=0
pp=1
for i in range (1,n+1):
     sum=sum+(pp*D[0,i])
     pp=pp*(u-(i-1))/(i)
print("Newton's Forward interpolated value at xp is: ",sum)
```

Output:

```
Forward difference table:
[[ 25.  50.  17.   0.  -7.  11.]
 [ 30.  67.  17.  -7.   4.   0.]
 [ 35.  84.  10.  -3.   0.   0.]
 [ 40.  94.   7.   0.   0.   0.]
 [ 45. 101.   0.   0.   0.   0.]]
Newton's Forward interpolated value at xp is:  55.8944
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare divided difference table for the following information:

| x | 10 | 11 | 14 | 16 |
|---|---|---|---|---|
| y = f(x) | 25 | 50 | 80 | 100 |

*Lab Book – Practical 5, Q.7 (same question)*

Program:

```python
import numpy as np
import pandas as pd
# Sample data
x = [10, 11, 14, 16]
y = [25, 50, 80, 100]
n = len(x)
dt = np.zeros((n, n))
dt[:, 0] = y
for j in range(1, n):
    for i in range(n - j):
        dt[i,j] = (dt[i+1,j-1] - dt[i,j-1])/(x[i+j]-x[i])
columns = ['y'] + [f'Δ^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(n - j):
        df.loc[i, f'Δ^{j}y'] = dt[i,j]
df.insert(0, 'x', x)
print("Newton's Divided Difference Table:\n")
print(df)
```

Output:

```
Newton's Divided Difference Table:

    x    y  Δ^1y  Δ^2y   Δ^3y
0  10   25  25.0 -3.75  0.625
1  11   50  10.0   0.0       
2  14   80  10.0             
3  16  100                   
```


**2)** Write a python program to find y(0.2) and y(0.4) for the differential equation dy/dx = (y+x)/(y−x) by using Euler’s modified method where, y(0)=2 take h=0.2.

*Lab Book – Practical 11, (ii) Euler’s Modified Q(1)*

Program:

```python
def f(x, y):
    return (y + x) / (y - x)
x = 0
y = 2
h = 0.2
while x < 0.4:
    k1 = f(x, y)
    yp = y + h * k1
    k2 = f(x + h, yp)
    y = y + (h / 2) * (k1 + k2)
    x = x + h
    print(f"y({x:.1f}) = {y:.4f}")
```

Output:

```
y(0.2) = 2.2200
y(0.4) = 2.4786
```


**3)** Write a python program to estimate the value of the integral ∫<sup>11</sup><sub>5</sub> (5x<sup>2</sup> + 3x + 2)dx, using Simpson’s one-Third rule, use n = 6. Print all values of xi and yi = f(xi), i = 0,1,2,3…6.

*Lab Book – Practical 10, Simpson’s 1/3 rule Q(1)*

Program:

```python
def f(x):
    return 5*x**2 + 3*x + 2
a = 5
b = 11
n = 6
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 2 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 4 * f(a + i * h)
result = result * h / 3
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.4f}",'and', "y =", f"{yi:.4f}")
print("Approximate integral =", f"{result:.4f}")
```

Output:

```
x = 5.0000 and y = 142.0000
x = 6.0000 and y = 200.0000
x = 7.0000 and y = 268.0000
x = 8.0000 and y = 346.0000
x = 9.0000 and y = 434.0000
x = 10.0000 and y = 532.0000
x = 11.0000 and y = 640.0000
Approximate integral = 2166.0000
```


---

## Slip No. 20

**Time: 3 hours** &nbsp;&nbsp;&nbsp; **Maximum Marks : 30**


### Q.1. Attempt any one of the following. [12×1 = 12 Marks]


**1)** Write a Python program to estimate a root of the equation x<sup>2</sup> − x − 0.1 = 0 in [ 1, 2], using Regula-Falsi method the program should terminate when relative error is of order 0.00001 or perform 15 number of iterations whichever occurs earlier.

*Lab Book – Practical 3, Q.1 / Q.2 (Regula-Falsi)*

Program:

```python
def falsePosition(f,x0,x1,e,N):
 x0 = float (x0)
 x1 = float (x1)
 e = float (e)
 N = int (N)
 if f(x0) * f(x1) >0.0:
  print('Given guess value do not bracket the root .')
  print('Try Again with different guess values .')
 else :
  step =1
  condition =True
  while condition :
   x2 =(x0*f(x1)-x1*f(x0)) / (f(x1) - f(x0) )
   print ('Iteration %d , x2 = %0.5f and f(x2) = %0.5f ' % (step ,x2,f(x2)))
   if f(x0) * f(x2) <0:
    x1 =x2
   else :
    x0 =x2
   step =step+1
   condition = abs(f(x2)) > e
  print ('\nRequired root is : %0.5f ' % x2)

def f(x):
    return x**2 - x - 0.1
falsePosition(f,1,2,0.00001,15)
```

Output:

```
Iteration 1 , x2 = 1.05000 and f(x2) = -0.04750 
Iteration 2 , x2 = 1.07317 and f(x2) = -0.02148 
Iteration 3 , x2 = 1.08353 and f(x2) = -0.00949 
Iteration 4 , x2 = 1.08809 and f(x2) = -0.00416 
Iteration 5 , x2 = 1.09008 and f(x2) = -0.00181 
Iteration 6 , x2 = 1.09094 and f(x2) = -0.00079 
Iteration 7 , x2 = 1.09132 and f(x2) = -0.00034 
Iteration 8 , x2 = 1.09148 and f(x2) = -0.00015 
Iteration 9 , x2 = 1.09155 and f(x2) = -0.00006 
Iteration 10 , x2 = 1.09158 and f(x2) = -0.00003 
Iteration 11 , x2 = 1.09160 and f(x2) = -0.00001 
Iteration 12 , x2 = 1.09160 and f(x2) = -0.00001 

Required root is : 1.09160 
```


**2)** Write python program to evaluate f(7) by Newton’s divided difference interpolation formula for the given data:

| x | 3 | 5 | 8 | 9 | 12 |
|---|---|---|---|---|---|
| y = f(x) | 24 | 120 | 504 | 720 | 1716 |

*Lab Book – Practical 7, Q.7 (same question)*

Program:

```python
from math import*
from numpy import*
x=[3, 5, 8, 9, 12]
y=[24, 120, 504, 720, 1716]
n=len(x)
D=zeros((n,n+1))
for i in range (0,n):
     D[i,0]=x[i]
     D[i,1]=y[i]
for j in range(2,n+1):
     for i in range(0,n-j+1):
         D[i,j]=(D[i+1,j-1]-D[i,j-1])/(x[i+j-1]-x[i])
xp=7
sum=0
pp=1
for i in range(0,n):
     sum=sum+(pp*D[0,i+1])
     pp=pp*(xp-x[i])
print("Newton's Divided interpolated value at xp is = ",sum)
```

Output:

```
Newton's Divided interpolated value at xp is =  336.0
```


### Q.2. Attempt any two of the following. [9×2 = 18 Marks]


**1)** Write python program to prepare backward difference table for the following information:

| x | 15 | 17 | 19 | 21 |
|---|---|---|---|---|
| y = f(x) | 25 | 50 | 80 | 90 |

*Lab Book – Practical 4, Q.4–Q.7 (backward difference table)*

Program:

```python
import numpy as np
import pandas as pd
x = [15, 17, 19, 21]
y = [25, 50, 80, 90]
n = len(x)
D = np.zeros((n, n))
D[:, 0] = y
for j in range(1, n):
    for i in range(j, n):
        D[i,j] = D[i,j-1] - D[i-1,j-1]
columns = ['y'] + [f'∇^{j}y' for j in range(1, n)]
df = pd.DataFrame('', index=range(n), columns=columns, dtype=object)
df['y'] = y
for j in range(1, n):
    for i in range(j, n):
        df.loc[i, f'∇^{j}y'] = D[i,j]
df.insert(0, 'x', x)
print("Newton's Backward Difference Table:\n")
print(df)
```

Output:

```
Newton's Backward Difference Table:

    x   y  ∇^1y  ∇^2y  ∇^3y
0  15  25                  
1  17  50  25.0            
2  19  80  30.0   5.0      
3  21  90  10.0 -20.0 -25.0
```


**2)** Write a python program to find y(0.1) and y(0.2) for the differential equation dy/dx = 1 + y by using Runge-kutta fourth order method where, y(0)=1.1 take h=0.1.

*Lab Book – Practical 12, (ii) RK 4th order Q(1)*

Program:

```python
def f(x, y):
    return 1 + y
x = 0
y = 1.1
h = 0.1
for i in range(2):
    k1 = h * f(x, y)
    k2 = h * f(x + h/2, y + k1/2)
    k3 = h * f(x + h/2, y + k2/2)
    k4 = h * f(x + h, y + k3)
    y = y + (k1 + 2*k2 + 2*k3 + k4) / 6
    x = x + h
    print("y(", round(x, 1), ") =", f"{y:.4f}")
```

Output:

```
y( 0.1 ) = 1.3209
y( 0.2 ) = 1.5649
```


**3)** Write a python program to estimate the value of the integral ∫<sup>6</sup><sub>0</sub> (x<sup>3</sup> + 5x + 7)dx, using Simpson’s Three-Eight rule, use n = 12. Print all values of xi and yi = f(xi), i = 0,1,2,3…12.

*Lab Book – Practical 10, Simpson’s 3/8 rule Q(3) (same question)*

Program:

```python
def f(x):
    return x**3 + 5*x + 7
a = 0
b = 6
n = 12
h = (b - a) / n
result = f(a) + f(b)
for i in range(1, n):
    if i % 3 == 0:
        result += 2 * f(a + i * h)
    else:
        result += 3 * f(a + i * h)
result = result * 3 * h / 8
for i in range(n + 1):
    xi = a + i * h
    yi = f(xi)
    print("x =", f"{xi:.2f}", 'and',"y =", f"{yi:.2f}")
print("Approximate integral =", f"{result:.2f}")
```

Output:

```
x = 0.00 and y = 7.00
x = 0.50 and y = 9.62
x = 1.00 and y = 13.00
x = 1.50 and y = 17.88
x = 2.00 and y = 25.00
x = 2.50 and y = 35.12
x = 3.00 and y = 49.00
x = 3.50 and y = 67.38
x = 4.00 and y = 91.00
x = 4.50 and y = 120.62
x = 5.00 and y = 157.00
x = 5.50 and y = 200.88
x = 6.00 and y = 253.00
Approximate integral = 456.00
```


---

## Notes on the programs

1. Newton's forward / backward interpolation: the lab-book loop `for i in range(1,n)` leaves out the last difference term (for Slip 1 it gives 55.3475 instead of the correct 55.1382). Here the same loop is written `range(1,n+1)` so the answer is correct. Nothing else is changed.
2. Difference tables: `dtype=object` is added in `pd.DataFrame('', ...)`, because newer pandas versions refuse to put numbers into an empty-string column.
3. The lab-book false-position program has no iteration limit; in every slip it converges within the iterations the slip allows (checked), so the program is unchanged.
4. Slips that do not give an interval or give a bad one: Slip 5 (interval [2, 3] as in the lab book), Slip 8 (taken [0, 1]), Slip 4 (f(−1) and f(0) have the same sign, x0 = −1 used), Slip 7 ([0, 1] has the sign change), Slip 15 (the slip says y(3) = 2 but asks for y(0.1), y(0.2); y(0) = 2 is used).
5. Slip 6 Q.2(1): the integrand follows the slip, (x² − 10); Slip 3 Q.1(1): 12 iterations of the lab-book plotting program give the root correct to three decimals.

**ALL THE BEST…..**
