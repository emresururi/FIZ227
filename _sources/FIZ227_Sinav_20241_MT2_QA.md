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

# 2024-25 2. Ara Sınav

**11/12/2024**

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

Verilen $[a,b]$ aralığındaki bütün tamsayıların toplamını hesaplayan kod yazın.

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
a = 5 
b = 55 # diyelim (a ile b halihazırda verilmiş zira)
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
# Çözüm 1_1
np.arange(a,b+1).sum()
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Çözüm 1_2
dizi = np.arange(a,b+1)
np.sum(dizi)
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
# Çözüm 2
toplam = 0
for i in range(a,b+1):
    toplam = toplam + i
toplam
```

+++ {"panel-layout": {"width": 100, "height": 110.71875, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 2

(100x2)'lik, her bir değeri -1 ile 1 arasında değişen (sınırları dahil de edebilirsiniz, dışarıda da bırakabilirsiniz, size kalmış) rastgele ondalıklı sayılardan oluşan bir 'noktalar' numpy dizisi oluşturun. Bu noktaların (0,0) noktasına olan uzaklıklarını hesaplatıp, sıralı olarak 'mesafeler' dizisinde toplayan kod yazın.

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
noktalar = np.random.rand(100,2)*2 - 1
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
# Çözüm 1
mesafeler = np.linalg.norm(noktalar,axis=1)
mesafeler
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Çözüm 2
mesafeler = []
for nokta_no in range(100):
    mesafe = np.sqrt(noktalar[nokta_no][0]**2 + noktalar[nokta_no][1]**2)
    mesafeler.append(mesafe)
mesafeler
```

+++ {"panel-layout": {"width": 100, "height": 174.140625, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 3

Verilen bir numpy dizisinin elemanlarının karelerinin toplamını döndüren bir fonksiyon yazın.

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
# Çözüm 1_1
def karetopla1_1(dizi):
    return (dizi**2).sum()

# Çözüm 1_2
def karetopla1_2(dizi):
    return np.sum(dizi**2)

# Çözüm 2
def karetopla2(dizi):
    toplam = 0
    for sayi in dizi:
        toplam = toplam + sayi**2
    return toplam
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# Üzerinde işlem yapacağımız bir dizi tanımlayıp,
# fonksiyonları çağıralım
dizimiz = np.array([3,6,1,-3.2])

print(karetopla1_1(dizimiz))
print(karetopla1_2(dizimiz))
print(karetopla2(dizimiz))
```

+++ {"panel-layout": {"width": 100, "height": 122.71875, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 4

Elimizde ne olduğu bizden gizlice tanımlanmış bir f(x) fonksiyonu var: fonksiyonun ne olduğunu bilmiyoruz ama mesela 'f(5)' deyince fonksiyonun $x=5$ noktasındaki değeri geliyor. Dahası bize bu fonksiyonun sürekli, türevlenebilir ve $x\in(-5,5)$ aralığında bir kökü olduğu belirtilmiş. Fonksiyonun kökünü bulan kod yazın. 

(İpucu: Örneğin yarılama yöntemini kullanabilirsiniz)

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 701
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
def f(x):
    # Örnek fonksiyon
    return np.cos(x) + x/5 + 0.6

x = np.linspace(-5,5,300)
plt.plot(x,f(x),"-")
plt.grid(True)
plt.show()
```

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
# Çözüm 1
hassasiyet = 1E-5

a = -5
b = 5
f_a = f(a)
f_b = f(b)

while(np.abs(a-b)>hassasiyet):
    c = (a+b)/2
    f_c = f(c)
    if((f_c * f_a) < 0):
        b = c
        f_b = f_c
    else:
        a = c
        f_a = f_c

print(c,f_c)

# İstenmemiş olsa da, grafikte tekrardan gösterelim:
plt.plot(x,f(x),"-")
plt.plot([-5,5],[0,0],"-k")
plt.plot(c,f_c,"ro")
plt.grid(True)
plt.show()
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
# Çözüm 2
hassasiyet = 1E-5
a = -5
f_a = f(a)
c = a + hassasiyet
f_c = f(c)
while((f_a*f_c)>0):
    a = c
    f_a = f_c
    c = a + hassasiyet
    f_c = f(c)
print(c,f_c)
```

+++ {"panel-layout": {"width": 100, "height": 94.578125, "visible": true}, "editable": true, "slideshow": {"slide_type": ""}}

# 5

Elimizde $x\in [0,10]$ aralığında, düzgün sıralı $10^6$ adet fonksiyon değeri var ('x = np.linspace(0,10,1E6)' yapmışız, sonrasında da ne olduğu bize söylenmeyen bu fonksiyonun o noktalardaki değerini hesaplatmışız gibi) – bu değerler 'degerler' numpy dizisinde tutuluyor olsun. Fonksiyonun türevini hesaplayıp çizdiren kod yazın.

```{code-cell} ipython3
---
editable: true
panel-layout:
  height: 3629.828125
  visible: true
  width: 100
slideshow:
  slide_type: ''
tags: [hide-cell]
---
# Verileri üretmek için yine aynı örnek fonksiyonu kullanıp,
# sonrasında da unutalım.

def f(x):
    # Örnek fonksiyon
    return np.cos(x) + x/5 + 0.6

x = np.linspace(0,10,int(1E6))
degerler = f(x)
```

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [hide-cell, toggle]
---
# Çözüm

x = np.linspace(0,10,int(1E6))
# 'degerler' verilmiş durumda

delta_x = x[1] - x[0]

turev = (degerler[1:] - degerler[0:-1]) / delta_x

plt.plot(x[:-1],turev,"r--")
plt.show()
```

+++ {"editable": true, "slideshow": {"slide_type": ""}}

_Ek olarak (soruda istenmemektedir, bilgi amaçlı olarak yapılmaktadır), türevin köklerinin gerçekten de fonksiyonun minimum/maksimum konumlarına denk geldiğini göstermek için değerlerle birlikte çizdirelim:_

```{code-cell} ipython3
---
editable: true
slideshow:
  slide_type: ''
tags: [toggle, hide-cell]
---
plt.plot(x,degerler,"b-")
plt.plot(x[:-1],turev,"r--")
plt.grid(True)
plt.xticks(np.arange(0,10.01))
plt.plot([0,10],[0,0],"k-")
plt.legend(["f","f'"])
plt.show()
```

```{code-cell} ipython3

```
