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

# 2023-24 1. Ara Sınav Çözümleri

**24/11/2023**

Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
```

# 1

20 x 30’luk, 1 ile 100 arasında (1 ile 100 dahil de olabilir, hariç de, size kalmış) rastgele sayılar içeren (sayılar tam sayı da olabilir, ondalıklı sayı da, bu da size kalmış), A ile B adında iki matris tanımlayın. Bu iki matrisin her bir hücresinin büyük olanını içeren bir C matrisi oluşturan kodu yazın.

Örnek: $\underbrace{\begin{bmatrix}5&6\\3&1\end{bmatrix}}_{A}\oplus\underbrace{\begin{bmatrix}2&8\\2&5\end{bmatrix}}_{B}\Rightarrow\underbrace{\begin{bmatrix}5&8\\3&5\end{bmatrix}}_{C}$

```{code-cell} ipython3
A = np.random.randint(1,100,(20,30))
B = np.random.randint(1,100,(20,30))
```

```{code-cell} ipython3
# Doğrudan, filtre kullanımı ile:

C = B.copy()
C[A>B] = A[A>B]
C[:3,:10]
```

```{code-cell} ipython3
# Döngü kullanıp, kıyaslayarak:

boyutlar = A.shape

C = np.zeros(boyutlar)
for i in range(boyutlar[0]):
    for j in range(boyutlar[1]):
        if (A[i,j] > B[i,j]):
            C[i,j] = A[i,j]
        else:
            C[i,j] = B[i,j]
C[:3,:10]               
```

# 2

$$\begin{gather*}
3x-2y = 5\\
x+6y = -1
\end{gather*}$$

a) denklem setini çözen komut/komutları yazın.   
b) $f(x)=\frac{3x-5}{2}$, $g(x) = -\frac{x+1}{6}$ fonksiyonlarını [-3,3] aralığında en az 300 nokta kullanarak aynı grafik üzerinde çizdirin. 

[Bonus: kesiştikleri noktayı da kırmızı bir kare olarak işaretleyin]

```{code-cell} ipython3
# a 
A = np.array([[3,-2],[1,6]])
b = np.array([[5,-1]]).T

# solve() ile:
print(np.linalg.solve(A,b))

# katsayılar matrisinin tersiyle çarpmak sureti ile:
print(np.dot(np.linalg.inv(A),b))

xy = np.dot(np.linalg.inv(A),b)
```

```{code-cell} ipython3
# b
x = np.linspace(-3,3,300)
f = (3*x-5)/2
g = -(x+1)/6

plt.plot(x,f,"b-")
plt.plot(x,g,"g-")
plt.plot(xy[0,0],xy[1,0],"rs")
plt.show()
```

# 3

a) Bileşenleri [-10,10] aralığında rastgele ondalıklı sayılar olan, iki adet 3 boyutlu vektör oluşturun, bunlara a ile b vektörleri diyelim.  
b) Bu iki vektörün skaler çarpımını hesaplayın.  
c) Bu iki vektör arasındaki açıyı derece cinsinden hesaplayın.

Bu iki vektörün vektör çarpımını hesaplayıp, buna c vektörü deyin (`c = np.cross(a,b)`)

d) c vektörünün a ve b vektörlerine dik olduğunu gösterin.

```{code-cell} ipython3
# a
a = np.random.rand(3)*20-10
b = np.random.rand(3)*20-10
a,b
```

```{code-cell} ipython3
# b
s = np.dot(a,b)
s
```

```{code-cell} ipython3
# c
cos_theta = s / (np.linalg.norm(a)*np.linalg.norm(b))
theta_rad = np.arccos(cos_theta)
theta_deg = np.rad2deg(theta_rad)
theta_deg
```

```{code-cell} ipython3
c = np.cross(a,b)
c
```

```{code-cell} ipython3
# d : doğrudan
# skaler çarpımlarının 0 olduğunu göstererek
np.dot(a,c),np.dot(b,c)
```

```{code-cell} ipython3
# d: aralarındaki açıyı hesaplayarak

cos_ac = np.dot(a,c) / (np.linalg.norm(a)*np.linalg.norm(c))
ac_rad = np.arccos(cos_ac)
ac_deg = np.rad2deg(ac_rad)
print("a : c",ac_deg)

cos_bc = np.dot(a,c) / (np.linalg.norm(b)*np.linalg.norm(c))
bc_rad = np.arccos(cos_bc)
bc_deg = np.rad2deg(bc_rad)
print("b : c",bc_deg)
```

# 4

Her biri 50 elemanlı, [40, 290] aralığında, rastgele tam sayılardan oluşan iki dizi oluşturun (adları A ile B dizileri olsun). Bu iki dizinin ortak elemanlarını C adındaki bir dizide biriktiren kod yazın.

```{code-cell} ipython3
A = np.random.randint(40,291,50)
B = np.random.randint(40,291,50)
A,B
```

```{code-cell} ipython3
# Döngülü, kontrollü çözüm

C = []
for i in range(A.size):
    for j in range(B.size):
        if (A[i] == B[j]):
            if(A[i] not in C):
                # Birden fazla aynı girişi
                # önlemek için, çok lazım
                # değil, bu son kontrolü 
                # koymasanız da sıkıntı
                # olmaz. ;)
                C.append(A[i])
C
```

```{code-cell} ipython3
# Filtreli, kontrollü

C = []
for i in range(A.size):
    filtre = A[i] == B
    if((B[filtre]).size>0):
        C.append(B[filtre][0])
C
```

```{code-cell} ipython3
# Tek komutla (bunu görmedik, referans olsun diye)

np.intersect1d(A,B)
```

# 5

`tutulan_sayi` değişkenine [1,100] aralığında rastgele bir tam sayı atayın. Bilgisayar bulana kadar tahmin etmeye çalışsın, tahmin tutulan sayıdan küçükse "çık"; büyükse "in" desin, bulunca kaç adımda bulduğunu da yazsın.

(Eğer akıllıca bir strateji kullanırsanız (ilk tahmini 50 olarak yaptırıp, sonra "in" derse 25, "çık" derse 75 olacak şekilde, gelen cevaba göre aralığı hep yarıladığınız şekilde) tam puan; "in"/"çık" cevaplarını çok önemsemezseniz yarım puan; hiç önemsemezseniz çeyrek puan üzerinden değerlendirilecektir)

```{code-cell} ipython3
tutulan_sayi = np.random.randint(1,101)
print("Tutulan sayı: ",tutulan_sayi)
print("----------------------\n\n")

flag_bulundu = False
tahmin = 50
kesin_min = 0
kesin_max = 101
i = 1
while(flag_bulundu == False):
    print(i,". Tahmin: ",tahmin)
    if(tahmin == tutulan_sayi):
        print(i," Adımda Bulundu!")
        break
    elif(tahmin < tutulan_sayi):
        print("çık")
        kesin_min = tahmin
    else:
        print("in")
        kesin_max = tahmin
        
    tahmin = int(kesin_min + (kesin_max-kesin_min)/2)

    i = i + 1
```

```{code-cell} ipython3

```
