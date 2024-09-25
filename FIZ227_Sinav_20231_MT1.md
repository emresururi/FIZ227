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

# 2023-24 1. Ara Sınav

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

+++

# 2

$$\begin{gather*}
3x-2y = 5\\
x+6y = -1
\end{gather*}$$

a) denklem setini çözen komut/komutları yazın.   
b) $f(x)=\frac{3x-5}{2}$, $g(x) = -\frac{x+1}{6}$ fonksiyonlarını [-3,3] aralığında en az 300 nokta kullanarak aynı grafik üzerinde çizdirin. 

[Bonus: kesiştikleri noktayı da kırmızı bir kare olarak işaretleyin]

+++

# 3

a) Bileşenleri [-10,10] aralığında rastgele ondalıklı sayılar olan, iki adet 3 boyutlu vektör oluşturun, bunlara a ile b vektörleri diyelim.  
b) Bu iki vektörün skaler çarpımını hesaplayın.  
c) Bu iki vektör arasındaki açıyı derece cinsinden hesaplayın.

Bu iki vektörün vektör çarpımını hesaplayıp, buna c vektörü deyin (`c = np.cross(a,b)`)

d) c vektörünün a ve b vektörlerine dik olduğunu gösterin.

+++

# 4

Her biri 50 elemanlı, [40, 290] aralığında, rastgele tam sayılardan oluşan iki dizi oluşturun (adları A ile B dizileri olsun). Bu iki dizinin ortak elemanlarını C adındaki bir dizide biriktiren kod yazın.

+++

# 5

`tutulan_sayi` değişkenine [1,100] aralığında rastgele bir tam sayı atayın. Bilgisayar bulana kadar tahmin etmeye çalışsın, tahmin tutulan sayıdan küçükse "çık"; büyükse "in" desin, bulunca kaç adımda bulduğunu da yazsın.

(Eğer akıllıca bir strateji kullanırsanız (ilk tahmini 50 olarak yaptırıp, sonra "in" derse 25, "çık" derse 75 olacak şekilde, gelen cevaba göre aralığı hep yarıladığınız şekilde) tam puan; "in"/"çık" cevaplarını çok önemsemezseniz yarım puan; hiç önemsemezseniz çeyrek puan üzerinden değerlendirilecektir)

```{code-cell} ipython3

```
