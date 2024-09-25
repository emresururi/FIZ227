---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# 2023-24 Genel Sınav

**16/01/2024**

Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
```

# 1

```{code-cell} ipython3
FIZ227_Apartmani = np.random.randint(1,6,(10,4))
FIZ227_Apartmani
```

```{code-cell} ipython3
filtre = FIZ227_Apartmani>=3
print(FIZ227_Apartmani[filtre].size)
print(filtre.sum())
```

# 2

+++

$$\begin{align}
z=&2x+3y-3&\Rightarrow&& 2x+3y-z &= 3\\
z=&-3x+y+5&\Rightarrow&& -3x+y-z &= -5\\
z=&\frac{-3x+3y+4}{2}&\Rightarrow&& -3x+3y-2z &= -4
\end{align}$$

```{code-cell} ipython3
A = np.array([[2,3,-1],[-3,1,-1],[-3,3,-2]])
b = np.array([3,-5,-4])
np.linalg.solve(A,b)
```

```{code-cell} ipython3
(x,y,z) = [4,-6,-13]
print(2*x+3*y-z-3)
print(-3*x+y-z+5)
print((-3*x+3*y+4)/2-z)
```

# 3

```{code-cell} ipython3
dizi = np.random.randint(30,71,100)
filtre = (dizi%6==0)
altiya_bolunenler = dizi[filtre]
altiya_bolunenler
```

# 4


```{code-cell} ipython3
dx = 1E-8
def f(x):
    return x**2*np.sin(3*x-5)

def f_ussu(x,dx):
    return (f(x+dx)-f(x-dx))/(2*dx)

f_ussu(np.pi/8,dx)
```

```{code-cell} ipython3
def f_ussu_analitik(x):
    return x*(2*np.sin(3*x-5)+3*x*np.cos(3*x-5))
f_ussu_analitik(np.pi/8)
```

```{code-cell} ipython3
dx = 1
while(np.abs(f_ussu(np.pi/8,dx)-f_ussu_analitik(np.pi/8))>1E-5):
    dx = dx/10
    #print(dx,f_ussu(np.pi/8,dx),np.abs(f_ussu(np.pi/8,dx)-f_ussu_analitik(np.pi/8)))
print(dx,f_ussu(np.pi/8,dx),np.abs(f_ussu(np.pi/8,dx)-f_ussu_analitik(np.pi/8)))
```

```{code-cell} ipython3
x = np.linspace(-2*np.pi,2*np.pi,300)
y = f_ussu(x,dx)
plt.plot(x,f_ussu_analitik(x),"b-")
plt.plot(x,y,"r--")
plt.legend(["Analitik","Sayısal"])
plt.show()
```

# 5


```{code-cell} ipython3
g = 9.81 # m/s^2
theta_0 = 60 # derece
theta_0_rad = np.deg2rad(theta_0)
v0 = 10 # m/s

t_ucus = 2*v0*np.sin(theta_0_rad)/g
t = np.linspace(0,t_ucus,300)

def x(t,theta_0_rad,v0):
    return v0*np.cos(theta_0_rad)*t

def y(t,theta_0_rad,v0):
    return v0*np.sin(theta_0_rad)*t - 0.5*g*t**2

plt.plot(x(t,theta_0_rad,v0),y(t,theta_0_rad,v0),"b-")
plt.show()
```
