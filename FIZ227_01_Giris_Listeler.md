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

# Python'a Giriş ve Listeler

## Ders Notları: 1

**Python'la 'Merhaba Dünya!'**

* Python'a Giriş
 * Python hakkında çok kısa bilgi
 * Python'ın popülerliği
 * Hangi Python IDE'sini kullanmalıyız?
* Jupyter ortamı
 * Hücreler
* Python kütüphaneleri
* Jupyter sayfanızı aktarma

**Listeler ve Sözlükler (+ demetler, kümeler)**
* Listeler
 * Listeye eleman ekleme
     + append
     + insert
     + extend
     + Liste Birleştirme
 * Liste elemanlarına ulaşma
 * Listeden eleman çıkarma
     + clear
     + pop
     + remove
     + del
 * Listelerle ilgili faydalı komutlar / metotlar
     + len
     + index
     + in
     + count
     + sort
     + reverse
     + copy
* Sözlükler
 * Sözlük tanımlama / özellik ekleme
 * Sözlükten özellik silme
 * Sözlüğün anahtarlarını (özelliklerini) öğrenme
* Listeler ile sözlükler birbirlerini çok severlerse...
* Bilerek bahsedilmeyenler
 * Bir listenin verilen -ardışık olmayan- indislerdeki elemanlarına ulaşmak
 * Bir listeden belli bir değere sahip olan tüm elemanları çıkartmak
 * Demetler (Tuple) nerede, niye bahsedilmedi?
 * Bir de kümeler (set) varmış, onları niye görmüyoruz?
 


Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

+++

# Python'a Giriş

## Python hakkında çok kısa bilgi

Python dili 1990 yılında, Guido van Rossum tarafından geliştirilmiştir. Yüksek seviye bir dil olup, işlemci tarafında pek çok zahmetli işlem (örn. _hafıza ayarlamaları, çöp toplama_) sistem tarafından otomatik olarak halledilmektedir. Ayrıca nesne tabanlı bir yapıya sahiptir (daha da ileri gidersek: Python'da hemen hemen **her şey** bir nesnedir).

Dil, ismini İngiliz anarşist komedi topluluğu [Monty Python](https://en.wikipedia.org/wiki/Monty_Python)'dan almaktadır (hatta, bizzat van Rossum'un örneklerde kullanılacak değişken ve durumların da grubun skeçlerinden seçilmesi konusunda ricası vardır).

## Python'ın popülerliği

Yaygın kütüphane desteği ve internetin doğrudan işletim sistemlerinde kaynak olarak kullanımının önünün açılması sonucu 2000'li yıllardan itibaren "en çok kullanılan diller" listelerinde hep üst sıraya yerleşmiştir. Bu listelerde kriter sayılan [TIOBE endeksinde](https://www.tiobe.com/tiobe-index/) Python, Java (%17.8) ve C'den (%16.3) sonra %10.1'lik kullanımla 3. sırada yer almaktadır ve [yükselişini kararlı bir biçimde sürdürmektedir](https://www.tiobe.com/tiobe-index/python/). GitHub ve Stack Overflow istatistiklerinden yola çıkılarak hazırlanan bir diğer endeks olan [RedMonk sıralamasında](https://redmonk.com/sogrady/2020/02/28/language-rankings-1-20/) ise Ocak 2020 itibarı ile JavaScript ile birinciliğe başabaş oynamaktadır. İnternette en çok başlangıç ve tanıtımları ziyaret edilen diller üzerinden sıralama yapan PYPL endeksinde ise açık ara ile (Python: %30.1; Java: %18.8) birinci sıradadır. _(Bütün istatistikler 2020 Mart ayı açıklamalarına dairdir)_

2022 Şubat itibarı ile:  
[TIOBE](https://www.tiobe.com/tiobe-index/)
* Python %15.33
* C %14.08
* Java %12.13

[PYPL](https://pypl.github.io/PYPL.html)
* Python %28.52
* Java %18.12

## Hangi Python IDE'sini kullanmalıyız?

Temel olarak Python yorumlanarak çalışan ("interpreted") bir dil olduğundan, bir yorumcuya ("interpreter") ihtiyaç duyar. Python'ın kendisi ile gelen _IDLE_ IDE'si temelde iş görse de, yaşamı kolaylaştırıcı pek çok özellikten mahrumdur. Bu nedenle, zorunlu durumlar dışında pek kullanılmaz.

Python'da program geliştirmek için yoğun olarak [PyCharm](https://www.jetbrains.com/pycharm/), [IPython](https://ipython.org/) ve Microsoft'un [Visual Studio Code](https://code.visualstudio.com/) IDE'leri kullanılmaktadırlar. [Anaconda](https://www.anaconda.com/) ise, IPython IDE'sini (Jupyter üzerinden) ve pek çok popüler sayısal analiz kütüphanesini içinde barındıran bir yazılım paketi olup, kullanım kolaylığı açısından benim de tavsiye ettiğim IDE'dir. Bunlara ek olarak, Google'ın [Colaboratory](https://colab.research.google.com/)'si ve [kaggle](https://www.kaggle.com/) gibi çevrimiçi servisleri kullanarak doğrudan onların sunucularında sanal bilgisayarlar üzerinde de kodunuzu geliştirebilirsiniz (Anaconda da çevrimiçi hizmet vermeye yakın zamanda başlamış) -- özellikle yavaş bilgisayarlarınız varsa gayet pratik bir çözüm olmakta.

Jupyter yoluyla bir web tarayıcısında yazılan Jupyter defterleri (_ipynb - IPython Notebooks_) gerek görsel, gerekse kullanım açısından gerçekten de akıcı bir geliştirmeye olanak tanır (bu uygulama notları da bizzat Jupyter ile hazırlanmaktadır 8). Jupyter'ın (_cupiter_ diye okunur, -benim gibi- _cupaytır_ diye değil bu vesileyle 8P) geliştiricileri Fernando Pérez ile Brian Granger olup, ikisi de akademisyen fizikçidir.

# Jupyter ortamı
## Hücreler
Jupyter'ı bir kelime işlemci (örn: MS Word) belgesi olarak düşünebilirsiniz: bu dökümanın bazı yerlerine açıklamalar yazıp, aralara da resimler eklediğiniz gibi, bir Jupyter defterinin istediğiniz kısımlarına yazı yazıp, istediğiniz kısımlarında da programınızı yazıp çalıştırabilirsiniz -- tıpkı şu anda yapmakta olduğum gibi. Python'da basit bir işlem yapalım:

```{code-cell} ipython3
5 + 7
```

Yukarıdaki işlemin olduğu kısım, şu anda bu satırların olduğu kısım gibi, çalışmamızın bir parçası olup, "hücre" (_cell_) adıyla anılırlar. Bir hücre şu üç çeşitten biri olabilir:
1. **Kod Hücresi:** Bu hücre -doğal olarak- en temel hücre tipimiz olacaktır. Buraya yazılan kodlar çalıştırılıp, çıktıları da aynı hücrenin altında monte şekilde gösterilecektir. (Kısayol tuşu: **Y**)
2. **Metin Hücresi:** Metin hücreleri de şu anda okumakta olduğunuz hücreler gibi, bilgi paylaşımı amacıyla oluşturulan hücrelerdir. Bu kısımları programlarda açıklamaları yazdığımız yorum satırlarının gelişmiş versiyonları olarak düşünebiliriz. **Kalın**, _italik_ vs. şeklindeki basit biçimlendirmelere de izin verirler (bu biçimlendirmeler için kullanılan notasyona **MarkDown** notasyonu adı verilmekte olup, detaylı açıklamalar ve örnekler için [Adam Pritchard'ın kapsamlı sayfasına bakabilirsiniz](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). Metin hücreleri, MathJax motoru sayesinde, karmaşık formülleri $\LaTeX$ yoluyla yazmanıza da izin vermektedir, örneğin: $\oint E \cdot \text{d}A = \frac{\rho}{\epsilon_0}$. (Kısayol tuşu: **M**)
3. **Çiğ Hücre:** Çiğ hücreler bir kodu (veya _şiiri_ ;) şeklini bozmadan, normalde çeşitli anlamlara gelen sembolleri olduğu gibi girmenize yarar. Şimdilik pek kullanacağımız bir hücre tipi değil. (Kısayol tuşu: **R**)

Hücrelerle ilgili çok kullanacağınız birkaç diğer kısayol tuşu ise şunlardır:
* &lt;Enter> : Seçili hücreyi değiştirme moduna alır.
* &lt;CTRL>+&lt;Enter> : Seçili olan hücreyi _çalıştırır_ (kod hücresi ise yazılı kodu çalıştırıp, çıktısını döndürür; metin hücresi ise markdown ve LateX sembollerini işler)
* b (below/aşağı) ve a (above/yukarı) : Seçili olan hücrenin aşağısına (veya yukarısına) yeni bir hücre ekler.
* &lt;CTRL>+&lt;Shift>+&lt;-> (split) : Seçili olan hücreyi o anda imleçin olduğu satırdan iki ayrı hücreye böler.
* h (help) : Kısayol tuşlarının karşılıklarını gösterir.

Bütün defteri çalıştırmak için ise **Kernel** menüsünden "Restart & Run All" diyebilirsiniz - bu durumda, defteri yeni açmışsınız gibi çekirdek (_kernel_) baştan yüklenir ve her şey sıfırdan çalıştırılır; **Cell** menüsünden "Run All" seçeneği ise, hücreleri en tepeden aşağıya doğru sırayla çalıştırır fakat daha önce çalıştırdığınızda edinilen (değişken değerleri gibi) bilgileri de kullanır. Kod hücrelerinin sol başlarındaki sayılar hücrelerin hangi sırayla çalıştırıldıklarını işaret eder (beklemediğiniz bir çıktı almanız halinde gidişatı kolayca takip edip, durumu anlayabilmeniz için).

# Python kütüphaneleri
Python, çeşitli işlere özgü (örn: matris hesabı, grafik çizimi, veritabanı, konumsal işlemler, görüntüleme, ses işleme, yapay zeka vs.) metotları barındıran pek çok kütüphane ile desteklenir; zaten bu kadar geniş kullanıcı sayısına ulaşmasında da bu çeşitliliğin büyük katkısı vardır. Python'da kütüphaneler _modül_ (_module_) olarak adlandırılır.

Sayısal hesap işlemlerinde yoğun olarak kullanacağımız üç adet kütüphane:
1. NumPy : Temel matematiksel fonksiyonları ve gelişmiş dizi & matris tiplerini, işlemlerini içerir.
2. SciPy : NumPy'ın bir üst kütüphanesi olarak düşünebiliriz. İleri fonksiyonlar ve metotlar bu kütüphanede bulunur, hayli kapsamlıdır.
3. MatPlotLib : Grafik çizmek için GNU Octave / MATLAB benzeri komutlarla işimizi kolaylaştırır.

Python'da istediğimiz kütüphaneyi:  
`import <kütüphane-adı> as <kütüphane-adı-kısaltması>`  
veya  
`from <kütüphane-adı> import <istenilen-metotlar>`  
biçimiyle çağırabiliriz. İki kullanım biçimi birbirinden farklıdır: İlkinde kütüphane elemanlarını çağırırken kütüphanenin kısa adıyla işaret ederiz (bu tür aidiyete "isimuzayı" (_namespace_) denir); ikinci türde ise kütüphane elemanları doğrudan ana isimuzayına eklenir, ilgili kütüphaneyi işaret etmemiz gerekmez. İkinci yaklaşım daha pratik gelse de birden fazla kütüphanenin aktarıldığı durumlarda karışıklığa yol açabilir, bu nedenle mümkün mertebe ilk yaklaşımı kullanmak gerekir. 

**Not:** ikinci yaklaşımla sadece bir tek metot eklense bile, Python yine de bütün kütüphaneyi yükleyecektir. `import numpy as np` ile `from numpy import pi` arasında performans bakımından hiçbir fark yoktur: iki durumda da bütün NumPy modülü yüklenir - ikinci durumda sadece _pi_'nin kullanımı mümkün olsa bile!

```{raw-cell}
# Örnek:
print(pi) # tanımlı olmadığından hata gelecektir

---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Input In [2], in <cell line: 2>()
      1 # Örnek:
----> 2 print(pi)

NameError: name 'pi' is not defined
```

_(Sayfada hata çıkması jupyter-book'un sayfayı işlemesini yarıda kestiğinden, hata veren kısımlar kod bloğu olarak yazılmamaktadır.)_

```{code-cell} ipython3
# Kütüphaneyi 'np' kısaltmasıyla aktaralım:
import numpy as np
print(np.pi) # pi de tanımlı,
print(np.e) # e de...
```

```{raw-cell}
# Kütüphaneden sadece pi'yi aktarıp, öyle çağıralım:
from numpy import pi
print(pi) # pi tanımlı,
print(e) # fakat e değil...

---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Input In [4], in <cell line: 4>()
      2 from numpy import pi
      3 print(pi) # pi tanımlı,
----> 4 print(e)

NameError: name 'e' is not defined
```

# Jupyter sayfanızı aktarma
Jupyter'da hazırladığınız sayfalar otomatik olarak sıklıkla kaydedilir (bunun yanısıra, siz de sol üstteki ikondan veya &lt;CTRL>+s kestirmesinden dilediğiniz zaman kaydedebilirsiniz).

Dosyanızı bir başkasına doğrudan veya farklı bir biçimde göndermek içinse **File** menüsünden "Download as..." seçeneğini kullanabilirsiniz. Bu menüde çıkan seçeneklerden başlıcaları:

* Notebook (.ipynb) : Oluşturmuş olduğunuz defterin tam olarak bir kopyasını verir.
* Python (.py) : İlgili kod kısımlarını tutar, yazı kısımlarını ise yorum olarak işleyip verir.
* HTML (.html) : Grafikler de dahil olmak üzere, bütün içeriği web tarayıcınızda gördüğünüz şekilde _statik olarak_ kaydeder fakat kod doğrudan çalıştırılamaz ya da siz defterdekine benzer şekilde işlemler yapamazsınız.
* PDF (.pdf)

+++

# Listeler, Demetler ve Sözlükler
Python'da verileri bir arada tutmak için temelde üç çeşit dizi tipi vardır: **liste** (_list_) ve **demet** (_tuple_) verileri sıralı şekilde tutar; **sözlük** (_dictionary_) tipinin gücü ise, anahtar (_key_) indislemeden gelmektedir.

## Listeler
Python listeleri sıralıdır, ilk elemanın indisi 0 olup, göreceğimiz üzere bütün sıralamalar 0'dan başlar. Listeleri tanımlamak için köşeli parantez içine yazarız.

```{code-cell} ipython3
liste = [1,"iki","3"]
print(liste)
print(liste[1])
```

Liste elemanlarını istediğimiz gibi değiştirebiliriz:

```{code-cell} ipython3
liste[1] = "bir"
print(liste[1])
```

...ama tanımlı olmayan bir elemanı indisle ekleyemeyiz:

```{raw-cell}
liste[3] = "üç"

---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
Input In [8], in <cell line: 1>()
----> 1 liste[3] = "üç"

IndexError: list assignment index out of range
```

### Listeye eleman ekleme
Bir listeye farklı yollardan eleman ekleyebiliriz:
* **append:** `append()` komutu listenin sonuna belirttiğimiz elemanı ekler:

```{code-cell} ipython3
liste.append("üç")
print(liste)
```

* **insert:**
  `insert()` komutu ile listenin istediğimiz bir yerine (aradan) bir eleman ekleriz:

```{code-cell} ipython3
liste.insert(1,"beş")
print(liste)
```

Görüldüğü üzere, 1 numaralı indise "beş" değeri eklenip, sağındaki değerler bir yana kaydırılmıştır.

* **extend:** Bazen listeye birden fazla değişken eklemek gerekir. Bu gibi durumlarda `extend()` komutu ile işimizi görürüz:

```{code-cell} ipython3
liste.extend(['yedi',8])
print(liste)
```

* **Liste Birleştirme:** Son olarak, bazen elimizdeki iki listeyi birleştirip, yeni bir liste oluşturmak işimize en uygun çözüm olabilir. Bu gibi durumlarda da liste birleştirme işlemcisi olan `+` sembolünü kullanırız:

```{code-cell} ipython3
liste_1 = ["sıfır",1,2,3]
liste_2 = ["dört",5,2]
liste_son = liste_1 + liste_2

print(liste_1)
print(liste_2)
print(liste_son)
```

### Liste elemanlarına ulaşma
Listenin bir kısım elemanına ulaşmak için, yukarıdaki örneklerde yaptığımız gibi ilgili elemanın indisini belirtebilir, ya da birden fazla elemana ulaşmak istiyorsak birden fazla indisi aralık veya tek tek girebiliriz:

```{code-cell} ipython3
print("Bütün listemiz: ",liste_son)
print("4 indisli eleman: ",liste_son[4])
print("3, 4 ve 5 indisli elemanlar: ", liste_son[3:6])
print("3 indisli eleman ve sonrası: ",liste_son[3:])
print("Baştan 3 indisli elemana kadar olan elemanlar: ",liste_son[:3])
```

Aralığı belirlerken `[3:5]` şeklinde değil de, `[3:6]` şeklinde yazdığımıza dikkat edin! Bunun sebebi, Python'da aralık belirtirken son değerin _kadar ve dahil_ şeklinde değil de, **_kadar_** olarak yorumlanmasıdır. Aralıklarda son değer içerilmez. Bu bir tercih meselesidir ve pek çok dilde (örn: C, C++, Go, Haskell, Java, JavaScript, Perl, PHP, Visual Basic) bu şekilde alınmaktadır -- bkz. ["sıralı tam liste" 8)](https://en.wikipedia.org/wiki/Comparison_of_programming_languages_%28array%29#Array_system_cross-reference_list). Bu şekildeki tercihin birçok açıklaması vardır, sözü _pirimiz_ [Edgar W. Dijkstra'ya bırakırsak](http://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html) başlıca sebepler olarak:
1. Başlangıç ve bitiş parametrelerinin farkının doğrudan aralıktaki eleman sayısını vermesini,
2. Döngü kontrollerinde pratiklik ve tek işlem (sadece _küçük mü?_ değerlendirmesi) sağlamasını,
3. (Ayrıca) Dizinin göstergecinin (_pointer_) doğrudan hafızadaki adresi olmasını ve bu adresin aynı zamanda ilk elemanın tutulduğu yerin başlangıcı olmasını,

sayabiliriz.

Ayrıca son iki örnekte görüldüğü üzere, başlangıç veya bitişin belirtilmediği durumlarda (sırası ile) 0 ve _eleman sayısı + 1_ alınır.

Python'da -özellikle de listenin eleman sayısını bilmediğimizde- negatif indisleri kullanarak **sondan** da ilerleyebiliriz. '-1' indisi her zaman için dizinin sonuncu elemanına; '-2' indisi sondan bir önceki elemanına, vs.. işaret eder. Aralıkları da benzer şekilde kullanabiliriz:

```{code-cell} ipython3
print("Bütün listemiz: ",liste_son)
print("\nSonuncu eleman: ",liste_son[6])
print("Sonuncu eleman: ",liste_son[-1])
print("Sondan bir önceki eleman: ",liste_son[-2])
print("Sondan iki ve üç önceki elemanlar: ",liste_son[-3:-1])
```

şeklinde ulaşabiliriz.

Listenin eleman sayısını bulmak içinse `len()` fonksiyonunu kullanırız:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
print("Bütün listemiz: ",liste_son)
print("Listemizdeki eleman sayısı: ",len(liste_son))
```

Son bir not olarak, aralıklarda başlangıç ve sondan başka, adım sayısını da belirtebiliriz (3. parametre olarak). Başlama ya da bitiş belirtilmezse, otomatik olarak -sırasıyla- ilk ve son elemanlar alınır. Örneğin:

```{code-cell} ipython3
sayilar = [0,1,2,3,4,5,6,7,8,9,10]
print(sayilar[3:8:2]) # 3 indisten, 8'e kadar, 2 artarak gider
print(sayilar[:8:2]) # İlk elemandan 8'e kadar, 2 artarak gider
print(sayilar[1::2]) # 1 indisten, sona kadar, 2 artarak gider
print("")

# Aşağıdaki iki aralık kullanımının farkına dikkat edin!
print(sayilar[:10:2]) # Baştan 10'a *kadar* 2 artarak gider
print(sayilar[::2]) # Baştan *sona* kadar (son dahil!) 2 artarak gider
```

### Listeden eleman çıkarma
Tıpkı eklemede olduğu üzere, listeden eleman çıkarmak için de birden fazla yöntem vardır:

* **clear:** `clear()` komutu ile listeyi boşaltırız:

```{code-cell} ipython3
liste_gidici = ["A",1,2,"üç"]
print("Mevcut liste: ",liste_gidici)
liste_gidici.clear()
print("clear() çekilmiş liste: ",liste_gidici)
```

* **pop:** istediğimiz bir indise sahip elemanı `pop()` komutu ile uçurabiliriz:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
liste_son.pop(1)
print(liste_son)
```

indisler sözkonusu olduğundan, dilersek negatif indis de kullanabiliriz; örneğin sondan ikinci elemanı çıkarmak istersek:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
liste_son.pop(-2)
print(liste_son)
```

İndis belirtilmediği durumda ise doğrudan son eleman çıkartılır.

`pop()`la ilgili faydalı bir özellik de, çıkardığı elemanın değerini döndürmesidir, örneğin:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
cikan = liste_son.pop(1)
print(liste_son)
print("Listeden cikarttigimiz eleman: ",cikan)
```

* **remove:** Listemizden belli bir değere sahip olan elemanı çıkartmak için `remove()` komutunu kullanırız. Örneğin, değeri "5" olan elemanı çıkartalım:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
liste_son.remove(5)
print(liste_son)
```

`remove()` komutunu kullanırken dikkat edilmesi gereken şey, eğer belirttiğimiz değerden birden fazla varsa, sadece başa en yakın olanı çıkartacaktır. Örneğin, listemizden "2" değerini çıkarmasını istersek:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213]
liste_son.remove(2)
print(liste_son)
```

* **del:** `del`i `pop()` gibi düşünebiliriz ama ona ek olarak, aralık boyunca da silme yapmamıza izin verir:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213]

# Tek bir eleman silelim
del liste_son[3]
print(liste_son)
del liste_son[-2]
print(liste_son)

# Aralik silelim
del liste_son[1:4]
print(liste_son)
```

Aralık verirken de yine pozitif indislerle negatif indisleri beraber kullanabiliriz:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213]
print(liste_son)
# 2 indisli elemandan sondan 3. elemana *kadar* silelim
del liste_son[2:-3]
print(liste_son)
```

### Listelerle ilgili faydalı komutlar / metotlar
`len, index, in, count, sort, reverse, copy`

Listelerin elemanlarına nasıl ulaşıp, ekleme-çıkartma yapabileceğimizi gördükten sonra, sıklıkla kullanılan komut ve metotları inceleyip, derleyelim:

* **len:** listenin eleman sayısını döndürür:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213]
print("Listemiz: ",liste_son)
print("Listemizdeki eleman sayısı: ",len(liste_son))
```

* **index:** İlgili listenin verilen elemanının indisini döndürür:

```{code-cell} ipython3
print("Listemizde 'dört' değerinin indisi: ",liste_son.index("dört"))
print("Listemizde '213' değerinin indisi: ",liste_son.index(213))
```

Eğer aranılan değer listede yoksa hata ('ValueError') uyarısı verecektir:

```{raw-cell}
print("Listemizde '777' değerinin indisi: ",liste_son.index(777))

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [27], in <cell line: 1>()
----> 1 print("Listemizde '777' değerinin indisi: ",liste_son.index(777))

ValueError: 777 is not in list
```

Normal şartlarda hata alıp programın çalışmasının durması pek hoş değildir, bu nedenle ya bu hatayı yakalamaya çalışırız, ya da bir başka prosedür olan `in` yapısını kullanırız:

**Hatayı yakalamak suretiyle icabına bakmak**  
(Bu yol biraz daha ileri bir teknik, şimdilik atlayabilirsiniz)

```{code-cell} ipython3
indis = "yok"
deger = 777
try:
    indis = liste_son.index(deger)
except ValueError:
    print(deger," değeri listede bulunamadı.")
print(deger," değerinin bulunduğu indis: ",indis)

print("---------------------")

deger = 213
try:
    indis = liste_son.index(213)
except ValueError:
    print(deger," değeri listede bulunamadı.")
print(deger," değerinin bulunduğu indis: ",indis)
```

**`in` prosedürünün kullanımı ile işimizi görmek:**

```{code-cell} ipython3
print("dört" in liste_son)
print(777 in liste_son)
```

* **count:** Bir değerin listede kaç kere bulunduğunu verir:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213, 2]
print("Listemiz: ",liste_son)
print("Listemizde 2 değerinden ",liste_son.count(2)," adet vardır.")
print("Listemizde 'dört' değerinden ",liste_son.count("dört")," adet vardır.")
print("Listemizde 219 değerinden ",liste_son.count(219)," adet vardır.")
```

(yukarıdaki örneğimizde de göreceğiniz üzere, listede aranan değerin bulunmaması durumunda hata değil, 0 değerini alırız)

* **sort:** Listeyi sıralamakta kullanılır. Standard dışı bir sıralama için ek parametreleri kabul eder. Dikkat edilecek nokta, bunun bir işlem olmasıdır. Listeyi sıralayıp, o hale getirir, bir sonuç döndürmez, yani `print("Sıralı listemiz: ",liste_sayilar.sort())` komutunu çalıştırdığımızda ekrana listeye dair bir şey yazılmaz ama liste çevrilmiş olur; bu sebepten önce sıralama işlemini yapıp, sonra listeyi yazdırabiliriz (bkz. aşağıdaki örnek).

```{code-cell} ipython3
liste_sayilar = [67, 1, 6, 2, 3, 5, 2, 213, 2]
print("Sayı listemiz: ",liste_sayilar)
liste_sayilar.sort() # listemizi siraladik
print("Sıralı sayı listemiz: ",liste_sayilar)

print("---------------")

liste_isimler = ["Berk","Ahmet","Cengiz","Ebru"]
print("İsim listemiz: ",liste_isimler)
liste_isimler.sort() # listemizi siraladik
print("Sıralı isim listemiz: ",liste_isimler)
```

**Dikkat!** Sort metodu karma veri tipleriyle (örneğin sayılar ve stringler) doğrudan çalışamamaktadır (bu iş için yukarıda bahsettiğimiz `key` ek kıstas parametresi/bilgisini kullanmak gerekir).

* **reverse:** Listemizin sırasını tersine çevirir -- bu metot da, tıpkı `sort()` gibi, doğrudan liste üzerine etki eder.

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213, 2]
print("Listemiz: ",liste_son)
liste_son.reverse()
print("Tersine çevrilmiş listemiz: ",liste_son)
```

* **Liste kopyalama:** Liste kopyalama işlemi, bir ihtimal `liste_2 = liste_1` şeklinde sanılabileceği kadar kolay değildir. Aşağıdaki örneğe bir göz atalım:

```{code-cell} ipython3
liste_1 =liste_1 = [1,2,3]
liste_2 = liste_1
liste_1.append(4)
print(liste_2)
```

Nasıl yani??? Biz, `liste_1`'e, `liste_2`'yi onun önceki halini eşitledikten sonra eleman eklemiştik -- nasıl oldu da sonradan eklediğimiz eleman `liste_2`'ye de eklendi???

Bunun sebebi, dilin yapısından kaynaklanmaktadır. Değişken isimleri aslında göstergeç (_pointer_) denilen, değerin tutulduğu adresi saklamakla yükümlüdürler. Tek değerli değişkenlerde birebir ilişki olsa da, birden fazla değişkeni tutan derleme yapılarda, isim doğrudan adresi gösterir. Bu yüzden `liste_2 = liste_1` dediğimizde, `liste_1`'de tutulan adres bilgisi `liste_2`'ye atanır (ikisi de aynı yeri gösterir). Bunu da daha açık bir şekilde -bir nevi- adresleri gösteren `id()` komutu ile kontrol edebiliriz:

```{code-cell} ipython3
print("liste_1'in  adresi: ",id(liste_1))
print("liste_2'nin adresi: ",id(liste_2))
```

Bundan ötürü `liste_1`'de değişiklik yapsak, `liste_2`'de de yapsak, ikisinin de etkilenmek üzere gösterdiği adres aynı olduğundan ikisi de değişir (yazılımda bu durumlar yumuşak kopya (_soft copy_) olarak da adlandırılır).

Eğer yapmak istediğimiz _gerçekten_ birbirlerine o anda eşit, ama sonrasında bağımsız iki liste oluşturmaksa, bunu da `copy()` metodu ile elde ederiz:

```{code-cell} ipython3
liste_1 = [1,2,3]
liste_2 = liste_1.copy()
liste_1.append(4)
print(liste_2)

print("liste_1'in  adresi: ",id(liste_1))
print("liste_2'nin adresi: ",id(liste_2))
```

Bir listenin bazı elemanlarını bir başka liste olarak atamak istediğimizi düşünelim:

```{code-cell} ipython3
liste_1 = ['sıfır', 1, 2, 3, 'dört', 5, 2, 213, 2]
print("liste_1: ",liste_1)

# Bu listenin 2 indisli elemanından 
# sondan 3. elemanına kadar olan elemanları
# liste_2 olarak atayalım:
liste_2 = liste_1[2:-3]
print("liste_2: ",liste_2)
```

İkinci liste, birinci listenin bazı elemanlarını çağırıp eşitlediğimizden, birinci listeden bağımsız. Bunu, birinci listenin 4 indisli elemanını değiştirerek kontrol edebiliriz:

```{code-cell} ipython3
print(liste_1[4])
liste_1[4] = "four"
print("liste_1: ",liste_1)
print("liste_2: ",liste_2)
print("----------")
print("liste_1'in  adresi: ",id(liste_1))
print("liste_2'nin adresi: ",id(liste_2))
```

Görüldüğü üzere, biz ikinci listenin ilgili elemanını birinci listeden almış olsak da, sonrasında birinci listede ilgili eleman değişse bile, listeler bağımsız olduğundan, ikinci liste bu değişiklikten etkilenmemekte.

Bu özelliği uça götürüp, ikinci listeyi, birinci listenin _tüm elemanlarına_ (`liste_1[:]`) da eşitleyerek tanımlayabiliriz -- sonuç yine iki bağımsız liste olacaktır:

```{code-cell} ipython3
liste_1 = [1,2,3]
liste_2 = liste_1[:]
liste_1.append(4)
print(liste_2)

print("liste_1'in  adresi: ",id(liste_1))
print("liste_2'nin adresi: ",id(liste_2))
```

## Sözlükler
Sözlüklerin (_dictionary_), listelerden farkı, indislerinin de tanımlanabilir olmasıdır. Bir sözlüğün indisini _özellik_ veya _anahtar_ (_key_) terimleri ile belirtiriz.


### Sözlük tanımlama / özellik ekleme
Hemen örneğe geçip, bir `ogrenci` sözlüğü üzerinden, özellikleri tanımlayalım:

```{code-cell} ipython3
# Bos bir sozluk tanimlayarak baslayalim:
ogrenci_1 = {}

# ad ve numara ozelliklerini ekleyelim:
ogrenci_1["ad"]="Ayşe Celik"
ogrenci_1["numara"] = 12345678

# ozellikleri ille tek tek girmek zorunda da degiliz
#ogrenci["matematik 123":"B1", "fizik 125":"A2", "giris yili":20191]

print("'ogrenci_1' sözlüğümüz: ",ogrenci_1)
print("Öğrencinin Adı: ",ogrenci_1["ad"])
print("Öğrencinin Numarası: ",ogrenci_1["numara"])
```

Özellikleri, başta sözlüğümüzü tanımlarken de girebiliriz:

```{code-cell} ipython3
ogrenci_2 = {"ad":"Barış Ateş", "numara":21912123}
print("'ogrenci_2' sözlüğümüz: ",ogrenci_2)
print("Öğrencinin Adı: ",ogrenci_2["ad"])
print("Öğrencinin Numarası: ",ogrenci_2["numara"])
```

Dahası, `update()` metodunu kullanarak halihazırda mevcut bir sözlüğe, topluca özellik eklemesi de yapabiliriz:

```{code-cell} ipython3
ogrenci_2 = {"ad":"Barış Ateş", "numara":21912123}
print("'ogrenci_2' sözlüğümüz: ",ogrenci_2)

print("----------")

ogrenci_2.update({"matematik 123":"B1", "fizik 125":"A2", "giris yili":20191})
print("'ogrenci_2' sözlüğümüz: ",ogrenci_2)
print()
print("Öğrencinin Adı: ",ogrenci_2["ad"])
print("Öğrencinin Numarası: ",ogrenci_2["numara"])
print("Öğrencinin giriş yılı: ",ogrenci_2["giris yili"])
print("Öğrencinin Matematik 123 notu: ",ogrenci_2["matematik 123"])
print("Öğrencinin Fizik 125 notu: ",ogrenci_2["fizik 125"])
```

Bir özellik tanımlanırken, önceden tanımlanmışsa, yeni değerle güncellenir; halihazırda tanımlı değilse o özellik eklenir:

```{code-cell} ipython3
ogrenci_2 = {'ad': 'Barış Ateş', 'numara': 21912123, 'matematik 123': 'B1', 'fizik 125': 'A2', 'giris yili': 20191}

# Daha onceden tanimli olan "ad" ozelligini guncelliyoruz:
ogrenci_2["ad"] = "Barış Cengiz Ateş"

# Daha onceden tanimlanmamis olan "kimya 155" ozelligini ekliyoruz:
ogrenci_2["kimya 155"] = "C1"

print("Öğrencinin Adı: ",ogrenci_2["ad"])
print("Öğrencinin Numarası: ",ogrenci_2["numara"])
print("Öğrencinin giriş yılı: ",ogrenci_2["giris yili"])
print("Öğrencinin Matematik 123 notu: ",ogrenci_2["matematik 123"])
print("Öğrencinin Fizik 125 notu: ",ogrenci_2["fizik 125"])
print("Öğrencinin Kimya 155 notu: ",ogrenci_2["kimya 155"])

print("---------------")

# update() metodu ile toplu guncelleme/ekleme yapabiliriz:
ogrenci_2.update({"kimya 155":"B2","fizik lab 101":"C3"})
print("Öğrencinin Adı: ",ogrenci_2["ad"])
print("Öğrencinin Numarası: ",ogrenci_2["numara"])
print("Öğrencinin giriş yılı: ",ogrenci_2["giris yili"])
print("Öğrencinin Matematik 123 notu: ",ogrenci_2["matematik 123"])
print("Öğrencinin Fizik 125 notu: ",ogrenci_2["fizik 125"])
print("Öğrencinin Fizik Lab 101 notu: ",ogrenci_2["fizik lab 101"])
print("Öğrencinin Kimya 155 notu: ",ogrenci_2["kimya 155"])
```

### Sözlükten özellik silme
Silmek istediğiniz özelliğin değerini `del` (`del sozluk["ozellik"]`) komutuyla silebilirsiniz:

```{code-cell} ipython3
ogrenci_2 = {'ad': 'Barış Ateş', 'numara': 21912123, 'matematik 123': 'B1', 'fizik 125': 'A2', 'giris yili': 20191}
print("'ogrenci_2' sözlüğümüz: ",ogrenci_2)

# Matematik 123 not bilgisini silelim:
del ogrenci_2["matematik 123"]
print("'ogrenci_2' sözlüğümüz: ",ogrenci_2)
```

### Sözlüğün anahtarlarını (özelliklerini) öğrenme
Sözlük değişkeninin sahip olduğu özelliklerin listesini `list()` komutu ile elde ederiz:

```{code-cell} ipython3
ogrenci_2 = {'ad': 'Barış Ateş', 'numara': 21912123, 'matematik 123': 'B1', 'fizik 125': 'A2', 'giris yili': 20191}
print("ogrenci_2 sözlüğünün anahtarları (özellikleri): ", list(ogrenci_2))
```

Adından da anlaşılacağı üzere, `list()` komutu bize anahtarları bir liste halinde verir (giriliş sırası ile). Döndürdüğü sonuç liste cinsinden olduğundan, bütün liste metotlarını ve indisle ulaşmasını kullanabiliriz:

Aynı anda hem anahtarı, hem de değeri almak içinse `items()` metodundan faydalanırız:

```{code-cell} ipython3
ogrenci_2 = {'ad': 'Barış Ateş', 'numara': 21912123, 'matematik 123': 'B1', 'fizik 125': 'A2', 'giris yili': 20191}
ogrenci_2_anahtarlar = list(ogrenci_2)
print("ogrenci_2 sözlüğünün 2 ve 3 indisli anahtarları: ", ogrenci_2_anahtarlar[2:4])

print(ogrenci_2.items())
```

## Listeler ile sözlükler birbirlerini çok severlerse...
Listeler ile sözlükleri birbirleri içinde geçişli olarak kullanmak mümkündür (_sözlük listeleri_, _liste listeleri_, _sözlük sözlükleri_, vs..). Bu bize veri derlerken müthiş bir esneklik sağlar. Örneğin, sözlük olarak tanımladığımız `ogrenci` sözlüklerimizi bir liste altında derleyelim:

```{code-cell} ipython3
ogrenci_1 = {'ad': 'Ayşe Celik', 'numara': 12345678}
ogrenci_2 = {'ad': 'Barış Ateş', 'numara': 21912123, 'matematik 123': 'B1', 'fizik 125': 'A2', 'giris yili': 20191}

ogrenciler_listesi = [ogrenci_1, ogrenci_2]
print(ogrenciler_listesi)

print ("--------")
print ("0 indisli öğrencinin adı: ",ogrenciler_listesi[0]["ad"])
print ("1 indisli öğrencinin adı: ",ogrenciler_listesi[1]["ad"])
```

(normal uygulamalarda böyle 0., 1. diye tek tek çağırmayacağız tabii: bir döngü üzerinden güzelce işleyeceğiz derlenmiş bilgileri ama o kısım `for` döngüsünü öğrenince gelecek. ;)

# Bilerek bahsedilmeyenler
**Bir listenin verilen -ardışık olmayan- indislerdeki elemanlarına ulaşmak**  
Pek çok dildeki karşılığının aksine (örn: `liste_son[2,4]`), maalesef bunu yapmanın doğrudan bir yolu yoktur. 

Ama boş geçmemek adına:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
# 2 ve 4 indisli elemanlara ulaşalım:

# 1. yöntem: map() + __getitem__ fonksiyon ve metotları ile:
liste_24_1 = list(map(liste_son.__getitem__,[2,4]))
print("1. yöntem (map() + __getitem__): ",liste_24_1)

# 2. yöntem: operator modülünden itemgetter() fonksiyonunu kullanarak:
from operator import itemgetter
liste_24_2 = list(itemgetter(*[2,4])(liste_son))
print("2. yöntem (operator.itemgetter): ",liste_24_2)
```

Neyse ki -pek çok diğer derdin yanında- bu dertten de bizi NumPy dizileri kurtarıyor:

```{code-cell} ipython3
import numpy as np
liste_son_np = np.array(['sıfır', 1, 2, 3, 'dört', 5, 2])
print(liste_son_np[[2,4]])
```

**Bir listeden belli bir değere sahip olan tüm elemanları çıkartmak**
`remove()` komutunun sadece ilk bulduğu elemanı çıkardığını, gerisine karışmadığını gördük, ama bazen bütün ilgili değerleri çıkarmak isteyebiliriz. Bu durumda `filter()` fonksiyonu yardımımıza koşmakta:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
liste_son_filtre = list(filter(lambda x: x != 2, liste_son))
print(liste_son_filtre)
```

(oradaki `lambda` yönergesi tek satırda, tek kullanımlık fonksiyon yazmamızı sağlayan bir yönerge; daha genel olarak "[anonim fonksiyon](https://en.wikipedia.org/wiki/Anonymous_function)" adıyla anılıp, programlamada epey önemli bir yer teşkil ederler)

Ya da `filter`'ı bir kenara bırakıp doğrudan `for`+`if` kombosu çekebiliriz:

```{code-cell} ipython3
liste_son = ['sıfır', 1, 2, 3, 'dört', 5, 2]
liste_son_filtre = list(s for s in liste_son if s != 2)
print(liste_son_filtre)
```

<a name="demetler"></a>**Demetler (_Tuple_) nerede, niye bahsedilmedi?** Demetler pek çok açıdan listelere benzese de, listelerin aksine _değiştirilemezler_ (_immutable_). Yani bir demete _(doğrudan)_ yeni eleman ekleyemez, içinden eleman çıkaramaz, mevcut elemanı da değiştiremezsiniz. E o zaman ne anladık? diyebilirsiniz ama demetlerin kullanımının avantajlı olduğu yerler de vardır (referans tabloları ve kayıtlar gibi, sabit kalmasını istediğimiz verileri demetlerde toplarız). Demetleri tanımlarken normal parantezler kullanırız, ama elemanlarına ulaşırken tıpkı listelerdeki gibi köşeli parantezlerle ulaşırız örneğin:

```{code-cell} ipython3
d = (0,1,"iki",3)
print("Demetimiz: ",d)
print("Demetimizin 1 indisli elemanı: ",d[1])
print("Demetimizin sondan 2. elemanı: ",d[-2])
print("Demetimizin 2 ve 3 indisli elemanları: ",d[2:4])
```

Kendi işlerimizde demetlere pek ihtiyacımız olmadığı için, bir de değiştirilemez oluşlarından ötürü bu aşamada çareden çok dert olacaklarından, demetlere girmeden teğet geçiyoruz.

**Bir de kümeler (_set_) varmış, onları niye görmüyoruz?**
Kıvrık parantezlerle  '{}' tanımlanan kümeler de listelere benzemekle beraber, en temel özelliği bir elemanın sadece bir kere yer almasıdır. Bu özellikleri listelerde basit bir döngüyle de sağlanabildiğinden dolayı -benim bildiğim kadarıyla- çok yaygın bir kullanımı yoktur. Kümelerin bir diğer ayırt edici yönü ise, elemanlarına tek tek ulaşımın mümkün olmamasıdır (yani indis kullanarak tek bir elemana ulaşamayız, ancak bütün üzerinden döngü kurabiliriz -- bir nevi _ya hep, ya hiç_ 8).

```{code-cell} ipython3
k = {0,1,"iki",1,"iki",2,4}
print("Kümemiz: ",k)
```
