---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.16.4
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

+++ {"panel-layout": {"width": 100, "height": 157, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 2024-25 1. Ara Sınav

**06/11/2024**

Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
---
import numpy as np
import matplotlib.pyplot as plt
```

+++ {"panel-layout": {"width": 100, "height": 157, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 1

a) Verilen n elemanlı, 1 boyutlu A dizisinin elemanlarının sırasını tersine çevirip, B dizisine atayan kod yazın. (A dizisinin tanımlı olarak verildiğini ve tam sayılardan oluştuğunu varsayın. Normal bir Python listesi veya numpy dizisi olabilir.)

b) Tanımlanmış bir x değerinin A dizisinin kaçıncı elemanı olduğunu bulan bir kod yazın. (Eğer dizide birden fazla x değerine sahip eleman varsa, ilk bulduğunun sırasını (indisini) yazsın; eğer dizide x değeri yoksa -1 yazsın)

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Rastgele sayıda eleman içeren bir dizi oluşturalım 
# (bunun, soruda verilmiş olduğu varsayılıyor, yani
# çözüme dahil değil ;)
n = np.random.randint(5,21)
# n = len(A)
A = np.random.randint(-7,16,n)
A
```

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# a
B = A[::-1]
B
```

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# A'nın içerisinden rastgele bir eleman çekip,
# x_var'ı bu şekilde tanımlayalım; A'da olmayan bir elemanı da 
# x_yok olarak tanımlayalım
# (bunun, soruda verilmiş olduğu varsayılıyor, yani
# çözüme dahil değil ;)
x_var = A[np.random.randint(0,n)]
x_yok = 999
x_var,x_yok
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# b
x = x_var # x'in olduğu durum
#x = x_yok # x'in olmadığı durum
for i in range(n):
    flag_bulundu = False
    if(A[i] == x):
        print(i,". eleman = ",x)
        flag_bulundu = True
        break
if(flag_bulundu == False):
    print(-1)
```

+++ {"panel-layout": {"width": 100, "height": 50.796875, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

## Alternatif Çözümler

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# a (alternatif)
B = []
for i in range(n-1,-1,-1):
    B.append(A[i])
B
```

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# a (alternatif)
B = []
for i in range(n):
    B.append(A[n-i-1])
B
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# b (alternatif, Python listesi kullanıldığı varsayılırsa)
x = x_var # x'in olduğu durum
#x = x_yok # x'in olmadığı durum
A_list = list(A)
if(x in A_list):
    print(A_list.index(x))
else:
    print(-1)
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# b (alternatif, numpy dizisi kullanıldığı varsayılırsa)
x = x_var # x'in olduğu durum
#x = x_yok # x'in olmadığı durum
A_np = np.array(A)
filtre = A_np == x
if(filtre.sum()>0):
    print(np.arange(n)[filtre][0])
else:
    print(-1)
```

+++ {"panel-layout": {"width": 100, "height": 110.71875, "visible": true}}

# 2

(6x7)’lik, değerleri [-1,10] aralığında, rastgele tam sayılardan oluşan bir A matrisi üretip, ortalamasını hesaplayan kod yazın. (Örneğin, bütün elemanları toplayıp, eleman sayısına bölün)

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 112.84375
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
A = np.random.randint(-1,11,(6,7))
m,n = A.shape
A,m,n
```

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 0
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
toplam = 0
for i in range(m):
    for j in range(n):
        toplam = toplam + A[i,j]
ortalama = toplam / (m*n)
print(ortalama)
```

+++ {"panel-layout": {"width": 100, "height": 50.796875, "visible": true}}

## Alternatifler

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# sum() fonksiyonu ile de kolayca çözülebilir
toplam = A.sum()
ortalama = toplam/A.size
ortalama
```

+++ {"panel-layout": {"width": 100, "height": 52.140625, "visible": true}}

Derste `mean()` fonksiyonunu görmemiş olsak da, bazı arkadaşlar o şekilde çözmüş olabileceklerinden, o doğrudan çözümü de paylaşayım:

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Derste görmediğimiz mean() fonksiyonu ile daha da pratik
A.mean()
```

+++ {"panel-layout": {"width": 100, "height": 174.140625, "visible": true}}

# 3

$$\begin{gather*}
y = 4-3x\\
y = \frac{1-2x}{3}
\end{gather*}$$

doğrularının kesiştiği noktayı bulup, bileşenlerini x0 ve y0 değişkenlerine atayan kod yazınız.

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Denklemleri düzenlersek:
# 3x +  y = 4
# 2x + 3y = 1

# Katsayılar matrisi
A = np.array([[3,1],[2,3]])
# Değerler vektörü
b = np.array([4,1])

x0,y0 = np.linalg.solve(A,b)
x0,y0
```

+++ {"panel-layout": {"width": 100, "height": 50.796875, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

## Alternatif

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 27.140625
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Eşitliğin iki tarafını da soldan A'nın tersiyle 
# çarpmak suretiyle
x0,y0 = np.dot(np.linalg.inv(A),b)
x0,y0
```

+++ {"panel-layout": {"width": 100, "height": 122.71875, "visible": true}}

# 4

3\. soruda denklemleri verilen doğruları $x\in[0,5]$ aralığında çizdiren kod yazınız (doğrular düz çizgi şeklinde ve farklı renklerde olsunlar).

Bonus: 3. soruda bulduğunuz kesişim noktasını grafikte yıldız şeklinde işaretleyin.

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 701
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
x = np.linspace(0,5,300)
y1 = 4-3*x
y2 = (1-2*x)/3

plt.plot(x,y1,"b-")
plt.plot(x,y2,"g-")
# Bonus
plt.plot(x0,y0,"r*")

plt.show()
```

+++ {"panel-layout": {"width": 100, "height": 94.578125, "visible": true}}

# 5

1000’e kadar olan asal sayıları bulup `asal_sayilar` dizisinde biriktiren kod yazın.

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 3629.828125
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
asal_sayilar = [2]
for i in range(3,1001):
    #print(i,"**")
    flag_asal_degil = 0
    for kucuk in range(2,i):
        #print(kucuk,sep=",")
        if(i % kucuk == 0):  
            #print("Bölündü! Asal sayı olamaz! 🙀")
            flag_asal_degil = 1
            break
    if(flag_asal_degil == 0):
        asal_sayilar.append(i)
    #print()
asal_sayilar
```
