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

# 2023-24 2. Ara Sınav

**22/12/2023**

Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt
```

# 1

a,b ve c değişkenlerine [-5.5,5.5] aralığında rastgele (ondalık) değerler atayın ve bu değerleri ekrana yazdırın. Sonrasında,

$$x_{1,2} = \frac{-b\pm \sqrt{b^2-4ac}}{2a}$$

formülünden $ax^2+bx+c=0$ denkleminin köklerini hesaplatıp ekrana yazdırın. Formülü kullanmadan önce $b^2-4ac\ge0$ eşitsizliğinin sağlandığını kontrol edip, eğer sağlanmıyorsa kök bulma işlemine geçmeyip ekrana “Gerçek kök yoktur” yazdırıp, programı sonlandırın (yani kökleri hesaplattırmadan bitirin).

+++

# 2

Değerleri [-10,10] aralığında değişen rastgele ondalıklı sayılardan (100 x 2)'lik bir 'noktalar' matrisi oluşturun. Bu matrisin her satırı bir noktanın x ve y koordinatlarına karşılık gelmektedir. Matristeki noktalardan orijine (0,0) 5 birimden daha yakın olanlarının indis numaralarını 'yakinlar' adındaki bir dizide biriktirin.

+++

# 3

$\vec a = -2\hat\imath + 3\hat\jmath - \hat k$ ile $\vec b = 3\hat\imath + 2\hat\jmath + 5\hat k$ vektörleri arasındaki açıyı hesaplayın.

+++

# 4

Taş-Kağıt-Makas oyunu, iki oyuncunun aynı anda bu üç seçenekten birini seçip söylemesiyle oynanır: taş, makası; makas, kağıdı; kağıt ise taşı yener.

Bilgisayara kendisiyle 50 kere taş-kağıt-makas oynattırın. Oyuncular her turda rastgele olarak bu üç seçenekten birini seçip söylesinler, kazandıkları durumda 1 puan, beraberlik veya kaybettikleri durumda 0 puan alsınlar. 

 a) Her bir oyunda ne söylediklerini ekrana yazdırın; sonrasında duruma göre “1. oyuncu kazandı”, “2. oyuncu kazandı” veya “Berabere kaldılar” yazılsın.  
 b) 50 turun sonunda iki oyuncunun da toplam skorunu yazdırın.

+++

# 5

M = 0.5 kg  kütleli bir cisim, L = 1 m uzunluğunda bir ipe asılarak bir sarkaç oluşturulmuştur. Küçük açı yaklaşımıyla, $\omega=\sqrt{g/L}$ açısal frekansı olmak üzere, hareket denklemi $\theta(t) = \theta_{max} \cos(\omega t+\phi)$ olarak verilmektedir. Burada $\theta_{max}$ salınımın genliği, $\phi$ ise faz açısı olup, başlangıç koşullarından bulunmaktadır.

Başlangıç açısı $\theta_0=-\tfrac{\pi}{6}$ rad ve ilk hızı $\dot\theta_0 = 0.1$ rad/s olarak belirtilmiş sarkacın, $\theta_{max}$ ve $\phi$ parametrelerini bulup, açı-zaman ve hız zaman grafiklerini bir periyot boyunca 300 nokta kullanarak çizdiren kod yazın. ( g = 9.81 m/s<sup>2</sup> alın ve 
aman dikkat edin: $\theta_{max}$ başlangıç açısına eşit değil!)

```{code-cell} ipython3

```
