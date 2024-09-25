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

# Vektörler ve Matrisler

## Ders Notları: 2

**Matrisler (NumPy Dizi (_numpy.ndarray_) Nesneleri)**

* Tanımlama
* Matris Elemanlarına Erişim ve Değiştirme
  * Bölgesel erişim
  * Matris Elemanlarını Değiştirmek
* Matrise Eleman Ekleme
  * Sihirbazlık: Değişkenleri kopyalamak ('copy')
  * append
  * insert
  * concatenate
* Matristen Eleman Silme
* Matrislerin Özellikleri
  * size
  * shape
  * reshape
  * ndim
  * dtype
* Tipik Matrisler
  * zeros
  * ones
  * fill ile matrisi doldurmak
  * birim matris
  * rastgele matrisler
  * arange ile aralıklar
  * linspace
* Matris işlemleri
  * Dört temel işlem (eleman bazında)
  * Skaler ve Vektörel Çarpımlar
    * Skaler Çarpım
    * Vektörel Çarpım
  * Matrisin transpozesi, tersi ve determinantı
    * Transpozesi
    * Tersi
    * 'Tersimsisi'
    * Determinantı

Vektörler ve Matrisler: Bilgi metotları; tipik matrisler (zeros, ones, doldurulmuş, birim, rastgele); aralıklar (arange ve linspace); matrisler arasındaki işlemler: eleman bazlı işlemler, skaler çarpım, vektörel çarpım; matris işlemleri (transpoze, tersi, ‘tersimsisi’, determinantı). Matris Uygulamaları: n bilinmeyenli n denklem setinin matris çarpımı temsili ve çözümü; dönüş matrisi. Uygulama: Elektrik devresinin Kirchhoff metotu ile lineer denklem seti haline getirilip çözülmesi.


Dr. Emre S. Taşcı, emre.tasci@hacettepe.edu.tr  
Fizik Mühendisliği Bölümü  
Hacettepe Üniversitesi

+++

## NumPy'ın N-boyutlu Dizileri (ndarray)
Bu dersimizde bundan böyle epey bir zaman kullanacağımız etkili ve hızlı NumPy dizilerini göreceğiz. Aslında teknik olarak _dizi_ dense de, bizim temel kullanım amacımız matrisler şeklinde olacak.

### Tanımlama
Bir NumPy dizisini, cinsiyle (yani "np.ndarray"), boş veya ilk değerli olarak tanımlarız. Python dizileri ile benzer olarak, bir liste bir kez oluşturulduktan sonra eleman ekleme/çıkarma yaparken aslında -çok da çaktırmadan- yerine yeni bir liste oluşturulur.

Tanımlama için normal dizilerdeki gibi köşeli parantezler kullanırız:

```{code-cell} ipython3
import numpy as np
mat1 = np.array([0,1,2,3,4])
print(mat1)
```

İki boyutlu bir matrisi iç içe geçmiş köşeli parantezler içinde (satır gruplu olarak) belirtiyoruz:

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5]])
print(mat2)
```

Peki ya üç boyutlu bir matrisi?... (Siz düşünün cevabı sonra 8)

### Matris Elemanlarına Erişim ve Değiştirme
Matrisimizin elemanlarına tıpkı normal dizilerde veya matrix nesnelerinde olduğu gibi köşeli parantezlerle erişebiliriz. Yalnız, onlardan farklı olarak, birden yüksek boyutlu olan matrislerin -tek bir elemana dair(!)- çoklu indislerini belirtirken, hepsini aynı köşeli parantezlerde yazabileceğimiz gibi, ayrı köşeli parantezlerde de belirtebiliriz (fakat ileride bahsedileceği üzere, özellikle çoklu seçimlerde ayrı köşeli parantezlerin bambaşka bir anlamı olduğundan, mümkün mertebe aynı parantezler içindeki notasyonu kullanın).

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5]])
print("Matrisimiz mat2:\n",mat2)
print("---------")
print("Matrisimizin sağ alttaki elemanı: mat2[1,2] = ",mat2[1,2])
print("Aynı elemanı bir de mat2[1][2] ile çağıralım: ",mat2[1][2])
```

#### Bölgesel erişim
Matrisimizin elemanlarına 'bölgesel' (yani, aralık belirterek) de erişebiliriz: bunun için ":" aralık operatörünü kullanabiliriz (aralık operatörünün kullanımı ve özelliklerine dair detaylı bilgiyi 2. kısım olan Listeler'in "Liste elemanlarına ulaşma" bölümünde bulabilirsiniz):

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5],[6,7,8]])
print(mat2)
print(mat2[1:3,1:3])
```

Eğer çağrı aralığımız bir sütun vektörü döndürüyorsa, Python bunu satır vektörü olarak sunacaktır:

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5],[6,7,8]])
print(mat2)

# Butun satirlarin son sutunu
mat2_son_sutun = mat2[:,2]
print(mat2_son_sutun) 

# Butun satirlarin son iki sutunu
mat2_son_2sutun = mat2[:,1:3]
print(mat2_son_2sutun) 
```

Bu (tek sütunlu vektörlerin satır vektörü olarak dönmesi) çok büyük bir sorun değil, çaresini şimdi verelim, detayını ileride göreceğiz: `reshape()` metodu:

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5],[6,7,8]])
print(mat2)

# Butun satirlarin son sutunu
mat2_son_sutun = mat2[:,2]
print(mat2_son_sutun) 

print("\nSihirli 'reshape' çekelim:\n",mat2_son_sutun.reshape(-1,1))
```

Dizilerin aksine, bir blok olmayan (yani aralarında boşluk olan) bölgelerden de elemanlara erişebiliriz. Örneğin, `mat2` matrisimizin ilk ve son sütunlarını alalım:

```{code-cell} ipython3
mat2 = np.array([[0,1,2],[3,4,5],[6,7,8]])
print(mat2)

print("\nİlk (0.) ve son (2.) sütunlar:")
mat2_ilk_ve_son_sutunlar = mat2[:,[0,2]]
print(mat2_ilk_ve_son_sutunlar) 
```

İndis belirtirken, başlangıç için nasıl 0 kullanıyorsak, sonuncu için de `end` veya `-1` kullanabiliriz; benzer şekilde `-2` "sondan ikinci", `-3` "sondan üçüncü", vs.. olarak işlenir. Uygulama olarak $(3\times5)$'lik bir matrisin sondan 2. ve 3. sütunlarına erişelim:

```{code-cell} ipython3
mat_3x5 = np.arange(0,15).reshape(3,5)
mat_3x5 = np.array([[ 0,  1,  2,  3,  4],
 [ 5,  6,  7,  8,  9],
 [10, 11, 12, 13, 14]])
print(mat_3x5)
print("---------")
print("Matrisimizin sondan 2. ve 3. sütunları:")
print(mat_3x5[:,[-2,-3]])
```

Aralıkları tersten arttırarak matrisimizin sütunlarının sırasını tersine de çevirebiliriz:

```{code-cell} ipython3
mat_3x5 = np.arange(0,15).reshape(3,5)
mat_3x5 = np.array([[ 0,  1,  2,  3,  4],
 [ 5,  6,  7,  8,  9],
 [10, 11, 12, 13, 14]])
print(mat_3x5)
print("---------")
print("Matrisimizin sütunlarının tersten sıralanmış hali:")
print(mat_3x5[:,4::-1])
```

Yukarıdaki örnekte 0. sütun dahil olduğu için aralığımızı `4:0:-1` şeklinde yazamadık çünkü bu (aralık tanımının {başlangıç}:{bitiş (kadar/dahil değil}:{artış miktarı} olmasından ötürü): 4,3,2,1 değerlerini içerir. `0` yerine `-1` koymak başta makul görünse de, -1'in özel bir anlamı var (yukarıda, satır vektörünü sütun vektörüne çevirirken de kullanmıştık, daha sonra kapsamlı olarak değineceğiz), onu da kullanamıyoruz, indislerin tam sayı (ve $\ge0$ - yani -1 de olmuyor teknik olarak ;) olma zorunluluğundan ötürü `-0.2` gibi bir cinlik de yapamıyoruz. Bu tür durumlarda işi "oluruna" yani _boş_ bırakıyoruz: boş bıraktığımızda "tümü" ya da biraz daha gevşek bir deyişle "_gittiği yere kadar..._" şeklinde bir anlam çıkmakta.

#### Matris Elemanlarını Değiştirmek
Erişebilmeyi öğrendikten sonra, değiştirmek çok kolay. Eriştiğiniz matris elemanları ile aynı boyutta olduktan sonra, istediğiniz gibi değiştirebilirsiniz:

```{code-cell} ipython3
mat_3x5 = np.arange(0,15).reshape(3,5)
mat_3x5 = np.array([[ 0,  1,  2,  3,  4],
 [ 5,  6,  7,  8,  9],
 [10, 11, 12, 13, 14]])
print(mat_3x5)
print("---------")
print("Baştan 2. (indis:1), sondan 2. sütunlar:")
print(mat_3x5[:,[1,-2]])
# Erisebildigimize gore, bunlari degistirelim:
# --(3x2)'lik matris olduguna dikkat ederek--
mat_3x5[:,[1,-2]] = np.array([[11, 13],[21,23], [31,33]])
print("\nBu kısmın değiştirilmiş olduğu hali:")
print(mat_3x5)
```

### Matrise Eleman Ekleme
Bir matrisi (NumPy dizisini) oluşturmayı, mevcut olan elemanlara erişip, onları değiştirmeyi gördük. Peki ya yeni bir eleman eklemek istersek? İlk akla gelen şekilde "olmayanı yoktan tanımlamak" işe yarar mı? (pek olacak gibi görünmüyor, bir deneyelim bakalım...)

```{raw-cell}
# (1x5)'lik saf bir matris (vektor) tanimlayalim
matris = np.array([0,1,2,3,4])
print("Matrisimiz:\n",matris)

print("Matrisimizin sonuncu elemanı: ",matris[4])

# 5. elemani (indisi: 4) degistirelim:
matris[4] = 9
print("Matrisimiz:\n",matris)

print("----------------------")

# 6. elemani (indisi: 5) tanimlayarak eklemeye calisalim:
matris[5] = 5 # Bu noktada elimize gecen hata! husran! gozyasi! :~(
print("Matrisimiz:\n",matris)

---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
Input In [11], in <cell line: 14>()
     11 print("----------------------")
     13 # 6. elemani (indisi: 5) tanimlayarak eklemeye calisalim:
---> 14 matris[5] = 5 # Bu noktada elimize gecen hata! husran! gozyasi! :~(
     15 print("Matrisimiz:\n",matris)

IndexError: index 5 is out of bounds for axis 0 with size 5
```

Aldığımız hatanın gerisinde yatan temel sebep, _teknik olarak_ bir matrisin (NumPy dizisinin - bir daha bu ek açıklamayı yapmayacağım) sadece ilk tanımlanışı sırasında boyutunun belirlenebilmesi. 

Pratikte tabii ki bu sıkıntıya düşmüyoruz, birazdan göreceğimiz üzere, genişleme de yapacağız, boyutunu da değiştireceğiz, sileceğiz de, ekleyebileceğiz de. Ama bu teknik kısıtlamanın altında ince bir programlama numarası yatmakta. Önceki ders notlarında bundan bahsettiysek de, bunların ders değil de aslında bir referans notu olmasından ötürü burada bir kez daha değineceğim. 8)

**Sihirbazlık: Değişkenleri kopyalamak ('copy')**  
Bu sihirbazlık numarası için yardımınıza ihtiyacım var:  
1. `a` diye bir değişken düşünüp, ona bir değer atayın (örneğin 3)
2. `b` diye bir değişken düşünüp, onu da `a`ya eşitleyin.  
_(şu anda `a` da, `b` de 3'e eşit, buraya kadar hemfikirizdir umarım)_
3. `a`nın değerini başka bir sayı yapın (örneğin 5).
4. `b`nin şu andaki değeri nedir?

Psikoloji bilimi doğru çalışıyorsa, büyük ihtimalle "5" demişsinizdir ("hoca sorduğuna göre o kadar bariz (3) cevap olamaz, vardır bir şaşırtmaca/hinlik) ama gerçekten de o kadar bariz (yani `b` değerimiz hala 3'e eşit), kendi gözlerinizle görün:

```{code-cell} ipython3
a = 3
b = a
print("a: %d\tb: %d"%(a,b))
print("Şimdi a'nın değerini 5 yapıyoruz...\n(b'ye dokunmuyoruz)")
a = 5
print("a: %d\tb: %d"%(a,b))
print("\n¯\_(ツ)_/¯ -- Duh!")
```

E sihirbazlık neresinde kaldı bu işin? Tekrar deneyelim... Bir şans daha. Bu sefer dizilerle yapalım:

```{code-cell} ipython3
dizi_a = np.array([3])
dizi_b = dizi_a
print("a dizisi: ",dizi_a)
print("b dizisi: ",dizi_b)
print("\nŞimdi a dizisinin elemanının değerini 5 yapıyoruz...\n(b dizisine dokunmuyoruz)\n")
dizi_a[0] = 5
print("a dizisi: ",dizi_a)
print("b dizisi: ",dizi_b)
```

![JamesHence_Beaker_Scream.jpg](imgs/JamesHence_Beaker_Scream.jpg)  
(James Hence - "The Meep")

Nasıl oldu? Biz b dizisine dokunmamıştık, nasıl oldu da gitti a'yı değiştirince b de değişiverdi? Cevap: dizilerin (yani birden fazla elemanı olan değişkenlerin) hafızada nasıl tutulduğu. Bize ad diye verilen şey aslında onun hafızada tutulduğu yeri gösteren bir işaretçi (_pointer_). Birebir aynı olmasa da bu ilişkiyi _id_'lere bakarak gözlemleyebiliriz:

```{code-cell} ipython3
dizi_a = np.array([3])
dizi_b = dizi_a
print("a dizisi: ",dizi_a)
print("a dizisinin id'si: ",id(dizi_a))
print("b dizisi: ",dizi_b)
print("b dizisinin id'si: ",id(dizi_b))
print()
print("\nŞimdi a dizisinin elemanının değerini 5 yapıyoruz...\n(b dizisine dokunmuyoruz)\n")
dizi_a[0] = 5
print("a dizisi: ",dizi_a)
print("a dizisinin id'si: ",id(dizi_a))
print("b dizisi: ",dizi_b)
print("b dizisinin id'si: ",id(dizi_b))
```

Görüldüğü üzere, ikisi de değişiklik yapıldıktan sonra bile aynı yeri işaret ediyorlar. Halbuki ilk örneğimizde:

```{code-cell} ipython3
a = 3
b = a
print("a: %d\tb: %d"%(a,b))
print("a'nın id'si: ",id(a))
print("b'nin id'si: ",id(b))
print("Şimdi a'nın değerini 5 yapıyoruz...\n(b'ye dokunmuyoruz)")
a = 5
print()
print("a: %d\tb: %d"%(a,b))
print("a'nın id'si: ",id(a))
print("b'nin id'si: ",id(b))
```

Python'da bir değişken tanımladığımızda, hafızada onun büyüklüğünde bir alan aranır ve o bölgenin başlangıç adresi o değişkenin adı ile ilişkilendirilir. Örneğin (3x4)'lük bir tamsayılar matrisi tanımladığınızda 3x4=12'lik tamsayının kapladığı yer bulunur, o yerin başlangıcı da matrisinizin adına atanır. Yani matrisin adı dediğimiz şey -hemen hemen- onun tutulduğu bölge. `dizi_b = dizi_a` demekle, a dizisinin adresini b dizisine de atamış olduk -- bu bir anahtarı çoğaltmak gibi bir şey! Bu yüzden a dizisinde yaptığımız değişiklik b dizisini de etkiliyor çünkü ikisi de aynı evi gösteriyor! Kardeşinizde de, sizde de birer anahtar var, kardeşiniz halıya vişne suyu döktüğünde, siz eve girince bu lekeyi görüyorsunuz! 8) 

Peki değerleri cinsinden birbirinin aynı ama göbekleri birbirlerine bağlı olmayan iki diziyi nasıl tanımlayacağız o halde? Cevap: `copy` komutu ile:

```{code-cell} ipython3
dizi_a = np.array([3])
dizi_b = np.copy(dizi_a)
print("a dizisi: ",dizi_a)
print("a dizisinin id'si: ",id(dizi_a))
print("b dizisi: ",dizi_b)
print("b dizisinin id'si: ",id(dizi_b))
print()
print("\nŞimdi a dizisinin elemanının değerini 5 yapıyoruz...\n(b dizisine dokunmuyoruz)\n")
dizi_a[0] = 5
print("a dizisi: ",dizi_a)
print("a dizisinin id'si: ",id(dizi_a))
print("b dizisi: ",dizi_b)
print("b dizisinin id'si: ",id(dizi_b))
```

Yine bu hafıza/adres meselesi yüzünden, kafamıza göre olmayan bir elemanı yoktan tanımlayamıyoruz: bilgisayar bize diyelim 12'lik yer bulup ayırmış, hemen dibinden bir başka değişken başlıyor, siz kalkıp da 13. elemanı tanımlayamazsınız, kalkıp yandaki komşunun odasına girecek haliniz yok (bu vesileyle son yıllarda hayli güvenli bilgisayarları yakıp kavuran [Heartbleed bug'ı](https://en.wikipedia.org/wiki/Heartbleed) tam da bu şekilde çalışıp bilgileri sızdırıyordu). O nedenle siz "bana 12 odalı ev yetmiyor, 13. odaya ihtiyacım var" dediğinizde, Python da 13 odalı bir ev oluşturup, sizi -pek de çaktırmadan- oraya taşıyor (adresiniz değişiyor haliyle ama no prob. ;).

* **append()** komutu ile eleman ekleme
`append` ile bir matrisin sonuna elemanlar eklenebilir. Dikkat edilmesi gereken husus, bu komutun yeni bir matris döndürdüğüdür: girdi olarak kullanılan matris doğal olarak -siz çıktı olarak kendisini işaret etmezseniz- değişiklik göstermez.

```{code-cell} ipython3
dizi = np.array([0,1,2,3,4])
print("dizi: \n",dizi)
print("diziye ek yapılmış hali:\n",np.append(dizi,[5,6,7]))
print("dizide bir değişiklik yok: \n",dizi)

print("-----------")

# Degisikligin diziye yapilmasi icin:
dizi = np.append(dizi,[5,6,7])
print("dizi: \n",dizi)
```

(tahmin edeceğiniz üzere, baştaki `dizi` ile, ekleme yapılmış `dizi`nin adresleri de, id'leri de farklı).

* **insert()** komutu ile eleman ekleme  
`insert` komutu işleyiş açısından `append`e benzese de, ondan temel farkı ille de sona değil, listenin herhangi bir yerine aradan ekleme yapma imkanı vermesindedir. İlk parametre olarak ekleme yapılacak dizi; ikinci parametre olarak hangi indisin yerinden ekleme yapılacağı (örneğin "2" dersek, 2 indisli (3.) elemanın soluna eklenir, yani eski 2 indisindeki (3.) eleman sağa kayar:

```{code-cell} ipython3
dizi = np.array([0,1,2,3,4])
print("dizi: \n",dizi)

print("--------")

dizi = np.insert(dizi,2,[99,98,97])
print("dizi: \n",dizi)
```

* **concatenate()** ile dizi birleştirme  
Python'da "normal" (standard) dizileri `+` operatörü ile birleştirebiliyorduk. NumPy matrislerinde bu operatör ile gerçek toplama yapabildiğimizden ötürü, yeni bir komuta gerek olmuş, o komut da işte `concatenate`:

```{code-cell} ipython3
dizi1 = np.array([0,1,2,3,4])
dizi2 = np.array([9,10,15])
dizi3 = np.concatenate((dizi1,dizi2))
print("dizi3: \n",dizi3)
```

 * `concatenate` ile yaptığımız her türlü işlemi `append` ile yapabileceğimiz doğrudur fakat `append` fonksiyonu bizzat concatenate ile tanımlanmıştır. [Kaynak koduna](https://github.com/numpy/numpy/blob/master/numpy/ma/core.py) bakacak olursanız (append en altta yer alıyor; korkmayın, bir bakın bence, açık kaynağın, özgür yazılımın en güzel yanlarından biri de bu! 8):
  
 `def append(a, b, axis=None):` 
 
 şeklinde başlıyor tanımı, bir dolu açıklama metni ve tüm bir fonksiyonun kod olarak aslında tek bir satırda tanımlandığını görüyorsunuz: 
 
 `return concatenate([a, b], axis)`
 
 
  * `concatenate`'i burada, bir boyutlu matrisler üzerinde çalışırken gördük ama ileride hem daha yüksek boyutlu matrislere ekleme yapacağız, hem de `vstack` olsun, `hstack` olsun, daha ince işler, kurulumlar yapacağız.

+++

### Matristen Eleman Silme
Silme işlemini `delete` komutu ile yapıyoruz ama hemen kullanmaya kalkmadan biraz düşünelim:

- `Silmek` ile ne kast ediyoruz?

Tamam, `[0,1,2,3,4,5]` gibi bir dizinin diyelim _2 ve 4 indisli elemanlarını silmekten_ bahsedebiliriz, o zaman `[0,1,3,5]` gibi bir şey olur elimize dönen, hatta:

```{code-cell} ipython3
dizi1 = np.array([0,1,2,3,4,5])
print("dizi1:\n",dizi1)
print("------------")
print(np.delete(dizi1,[2,4]))
```

Nefis!... Bravo... vs..

Peki ya elimizde 2 boyutlu bir dizi varsa?

```{code-cell} ipython3
dizi2 = np.array([[1,2],[3,4],[5,6]])
print("dizi2:\n",dizi2)
```

Bunun _2 ve 4 indisli elemanlarını silmek_ ne demek??? (bkz. _what ne demek?_ 8P).. _1. satırı silelim_, bunu anlarız (Python da anlar), haydi _2. sütunu silelim_ bu da tamam ama _2 ve 4 indisi_ bırakın, _2 indisli elemanı silelim_'in bile 2 boyutlu bir matriste anlamı yok (jenga oynayanlarınız bilir, yapıyı korumak lazım: bir satırında 2 elemanı, bir başka satırında 1 elemanı olan bir matris matematik dünyasında yok (olana da hilkat garibesi muamelesi çekiliyor, girmiyorum o konuya ama çok istiyorsanız bkz. dizi dizileri ya da hücre dizileri)).

Önce bir satırı, sonra bir sütunu uçurup, sonra da tek bir elemanı uçurmaya kalkıp sonuçlara bakalım:

```{code-cell} ipython3
dizi2 = np.array([[1,2,3],[4,5,6],[7,8,9]])
print("dizi2:\n",dizi2)

print("---------")
print("2. satırı uçurduğumuz hali:\n",np.delete(dizi2,1,0))

print("---------")
print("2. sütunu uçurduğumuz hali:\n",np.delete(dizi2,1,1))

print("---------")
print("1. & 3. sütunu uçurduğumuz hali:\n",np.delete(dizi2,[0,2],1))
```

Satırlar ve sütunlar gayet iyi uçuyor (satır uçururken `0`, sütun uçururken `1` değerini alan parametre "eksen" parametresi: 2-boyutlu bir matriste birincil (0) eksen x-ekseni (yani satırlar); ikincil (1) eksen y-ekseni (yani sütunlar)).

Şimdi gelelim bir tek, diyelim 2. elemanı uçurmaya:

```{code-cell} ipython3
dizi2 = np.array([[1,2,3],[4,5,6],[7,8,9]])
print("dizi2:\n",dizi2)

print("---------")
print("2. elemanı uçurduğumuz hali:\n",np.delete(dizi2,1))
```

2\. eleman olan 2 (indis:1) hakikaten de uçtu ama artık matrisin bütünlüğü bozulduğundan, otomatik olarak 1 boyuta indirgendi ki, siz de takdir ederseniz, en mantıklı çözüm bu.

+++

## Matrislerin Özellikleri

Sıklıkla, elimize geçirdiğimiz bir NumPy dizisinin özelliklerini bilmek isteriz: boyu nedir, boyutu nedir, kimlerdendir, içinde sevdiceğimiz var mıdır vs. Bu bölümde temel bilgi komut ve metotlarını işleyeceğiz.

O halde, bir tane 2 boyutlu $(4\times5)$ matris tanımlayıp, işimize bakalım:

```{code-cell} ipython3
mat1 = np.array([[0,1,2,3,4],[10,11,12,13,14],[20,21,22,23,24],[30,31,32,33,34]])
print(mat1)
```

```{code-cell} ipython3
aa = np.array([[1],[2],[3]])
print(aa.ndim,aa.shape)
print([np.array(mat1[:,2])])
```

Fark ettiyseniz, değerler aynı zamanda satır ve sütun indislerini veriyor (ilk satırın (0 satırı) misal 2 indisli elemanını `02` yazamadığımdan, `2` ile yetiniyoruz ama artık o kadar kusur kadı kızında da bulunur).

### size: Matrisin eleman sayısı
`size` metodu bize matrisin toplam eleman sayısını verir. Örneğimizdeki matrisimizin 20 elemanı var, o halde, "size" diye sorunce, "20" demesini bekliyoruz, bakalım:

```{code-cell} ipython3
print("Matrisimizin eleman sayısı: ",mat1.size)
```

## shape: Matrisimizin boyutları _(90-60-90)_

`shape` metodu matrisimizin "şeklini" yani boyutlarını bir demet (_tuple_) olarak döndürür:

```{code-cell} ipython3
print("Matrisimizin boyutları: ",mat1.shape)
print("Matrisimizin ",len(mat1.shape)," adet boyutu var.")
print("Asıl (0 - satırlar) eksendeki 'kat' sayısı: ",mat1.shape[0])
print("İkincil (1 - sütunlar) eksendeki 'daire sayısı: ",mat1.shape[1])
```

Burada dikkatinizi çektiyse, boyutların döndürüldüğü mat1.shape demetinin boyunu bulurken `size` metodunu değil, `len` komutunu kullandık. Bunun sebebi, `size`ın bir ndarray metodu olup, demetlere uygulanabilir olmaması. `len` komutu epey evrensel bir komut olup, hemen her değişkene sorulabilir. O halde niye `len` dururken, matrislerde `size` ile uğraşıyoruz? Hemen bakalım:

```{code-cell} ipython3
print(len(mat1))
```

Gördüğünüz üzere, sadece ilk eksenin (satırların) sayısını veriyor, gayet de mantıklı zira Python bunu -teknik olarak- her birinde 5 elemanlı 1 boyutlu dizi olan, 4 elemanlı bir derleme olarak görüyor (matrisi nasıl tanımladığımızı hatırlayın: [ [1. eleman: 1. dizi], [2. eleman: 2. dizi], ...]). Bu yüzden, n-boyutlu matrislerin eleman sayısını `len` ile değil, `size` ile öğreniyoruz (bu konu sanırım bölüm sonlarında olan "bunları bilmeseniz de olur ama işte..." kısmına daha uygundu!.. 8)

+++

![play-it-sam.jpg](imgs/02_BogartCasablancaSam.jpg)Casablanca, "Play it -again- Sam" (tamam, Bogart hiç _again_ lafını söylemiyor aslında ama olsun)

+++

## reshape: yeniden şekillendir, Sam..
Matrisin şekli çok önemlidir zira o şekli yeniden ("re-") biçimlendirebiliriz ("shape") => `reshape`!

Elimizdeki matris (4x5)'ti, 20 elemanı vardı. Elemanları düzgünce dağıtabileceğimiz (yani bütün boyutlarının çarpımı 20 olduğu sürece) her boyuta çıkabiliriz. Çarpımı 20 olan sayılardan bazılarını sıralayalım:

* 1x20
* 2x10
* 2x2x5
* 20x1

Gördüğünüz üzere, yukarıdakilerden 1. ve 4. örnekler bir boyutlu matrisler (ilki satır, ikincisi sütun vektörü); 2. örnek 2 satırlı, 10 sütunlu iki boyutlu bir matris; 3. ilginç çünkü 3 boyut var. Tek tek deneyelim:

```{code-cell} ipython3
print(mat1.reshape(1,20))
```

```{code-cell} ipython3
print(mat1.reshape(2,10))
```

```{code-cell} ipython3
print(mat1.reshape(2,2,5))
print(mat1.reshape(2,2,5)[1,1,3])
```

(2x2x5) üç boyutlu matrisimizde [1,1,3] indisli elemanı istediğimizde, önce 1. eksende ilerleyip, 1 indisli diziye gittik:

`[[20 21 22 23 24]
  [30 31 32 33 34]]`
 
dizisi. Sonra bu dizinin 1 indisli dizisine gittik:

` [30 31 32 33 34]`

dizisi. Sonra da, bu dizinin 3 indisli elemanına (yani 4. elemanına) gittik: 33

Bu vesileyle, çaktırmadan, 3 boyutlu bir diziyi nasıl oluşturabileceğimize dair bir yolu da keşfetmiş olduk: `reshape` metodu ile.

```{code-cell} ipython3
print(mat1.reshape(20,1))
```

## ndim: kısa yoldan kaç boyutlu bir matrisimiz olduğuna dair...
Elimizdeki matrisimizin kaç boyutlu olduğunu şeklinin kaç elemanı olduğunu sorarak öğrenebilmiştik:

```{code-cell} ipython3
print("Matrisimizin ",len(mat1.shape)," adet boyutu var.")
```

Bunu tek bir metotla da yapmak mümkün, bu iş için `ndim` metotu yardımımıza koşuyor:

```{code-cell} ipython3
print("Matrisimizin ",mat1.ndim," adet boyutu var.")
```

## dtype: elemanlarının cinsi
<a name="karma_diziler"></a>
Aşağıdaki üç diziye bir bakın -- sizce aralarında çok fark var mı?
1. `dizi_1 = np.array([0,1,2])`
2. `dizi_2 = np.array([0,1,2.0])`
3. `dizi_3 = np.array([0,1.0,"iki"])`

...

Herhalde, 3.yü listeye koymasaydık, "fark yok" cevabı normal karşılanacaktı ama 3. işi bozduğundan, bu sefer 1. ile 2. arasında da bir bit yeniği çıkmasını bekliyoruz. Python'a verelim, bakalım o ne diyecek:

```{code-cell} ipython3
dizi_1 = np.array([0,1,2])
dizi_2 = np.array([0,1,2.0])
dizi_3 = np.array([0,1.0,"iki"])

print("dizi_1:\n",dizi_1,"\n")
print("dizi_2:\n",dizi_2,"\n")
print("dizi_3:\n",dizi_3,"\n")
```

Hemen fark edenler kendilerine bir 10 puan yazsınlar bakalım! Detaylıca incelediğimizde, ilkinde sayılarımızın ondalık noktalarının olmadığını, ikincisinde diziyi girerken sadece 2'yi ondalıklı girdiğimiz halde (o da hani "2.3" gibi değil, bildiğiniz "2.0" masumane şekliyleydi!) 0 ve 1'in kuyruklarına da ondalık noktasının takılmış olduğunu, üçüncü dizide ise hepsinin (0'ın ve 1.0'ın bile!) bir kelimeymişçesine kesme (') işaretleri arasına alınmış olduğunu görüyoruz. Bunun sebebi şu:

NumPy dizileri sadece tek bir eleman cinsini tutarlar. İlk dizimizde bütün elemanlarımız tam sayı, o yüzden tam sayı olarak tutulabiliyorlar; ikinci dizimizde iki tam sayı, bir tane ondalıklı sayı girdiğimizde, ondalıklı sayının varlığı (değerinden bağımsız olarak), dizinin elemanları tuttuğu cins olarak tam sayıyı değil, hepsini içerebilecek ondalıklı sayı cinsini seçmesini gerektiriyor (genel olarak: tam sayıları bilgi kaybı olmadan ondalıklı olarak tutabilsek de, tersi mümkün değil); üçüncüsünde ise, tam sayı olsun, ondalıklı sayı olsun, bunları string olarak tutabiliyoruz ama string değişkenlerini -genel olarak- sayı olarak ifade edemediğimizden, elemanların cinsi "en küçük ortak cins" olan string olarak tanımlanıyor.

Bir dizinin tuttuğu eleman cinsini de `dtype` metodu ile öğreniyoruz:

```{code-cell} ipython3
print("dizi_1'in elemanlarının cinsi :",dizi_1.dtype,"\n")
print("dizi_2'nin elemanlarının cinsi:",dizi_2.dtype,"\n")
print("dizi_3'ün elemanlarının cinsi :",dizi_3.dtype,"\n")
```

Tipte yazılı kısım cinsi (integer: tam sayı; float: ondalıklı sayı; U: Unicode string) verirken, peşinden gelen sayı her bir eleman için hafızada ayrılan yer miktarını (bit cinsinden) verir.

Bir dizinin elemanlarının cinsini **zorla** bir başka cinse dönüştürmek mümkündür: bunu `astype` metotu ile yaparız:

```{code-cell} ipython3
dizi_2[2] = 2.6
```

```{code-cell} ipython3
print(dizi_2.astype(int))
```

```{code-cell} ipython3
dizi_2
```

Ama bunun mümkün olmadığı yerde de zorlamanın pek bir alemi yok:

```{raw-cell}
print(dizi_3.astype(float))

---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Input In [40], in <cell line: 1>()
----> 1 print(dizi_3.astype(float))

ValueError: could not convert string to float: 'iki'
```

150 tane tam sayı elemanı olan bir diziye, 151. eleman olarak ondalıklı sayı eklediğimizde bütün elemanlarının tipi nasıl da tümden ondalıklı sayılara dönüşüyorsa, iki sayıyı topladığımızda da bu kural otomatikman uygulanır:

```{code-cell} ipython3
# Tam sayı + tam sayı = tam sayı:
5 + 7
```

```{code-cell} ipython3
# Tam sayı + ondalıklı sayı = ondalıklı sayı:
5 + 7.5
```

```{code-cell} ipython3
# Çok mu barizdi? Öyleyse bir de şuna bakalım:
5 + 7.0
```

## Tipik Matrisler
Şimdi eğri oturup, doğru konuşalım: NumPy'da matris elemanlarını tanımlamak çoğu kez epey sıkıcı. Bu yüzden hayatı kolaylaştırıcı birkaç tipik hazır matris türü var.

### zeros : sıfır sıfır sıfır...
Adı üzerinde, istediğimiz boyutta, tüm elemanları sıfır olan bir matris döndürür - yapmamız gereken, istediğimiz matris boyutunu belirlemekten ibaret:

```{code-cell} ipython3
mat_0 = np.zeros([2,3,4])
print (mat_0)
```

### ones : bir bir bir... (nereye kadar gideceğiz böyle, haydi bakalım...)

Bu da, bütün elemanları 1 olan bir matris döndürür:

```{code-cell} ipython3
mat_1 = np.ones([2,5,2])
print(mat_1)
```

### fill ile matrisi doldurmak
Bütün elemanları sıfır veya bir olan bir matrisi nasıl tanımlayacağımızı artık biliyoruz, peki bütün elemanlarının 2.7 olmasını istiyorsak? Bu durumda, iki-üç(-çok?) yolumuz var: 

1. 0-matrisi oluşturup, bütün elemanlarına 2.7 ekleriz:

```{code-cell} ipython3
mat_0 + 2.7
```

2. 1-matrisi oluşturup, bütün elemanlarını 2.7 ile çarparız:

```{code-cell} ipython3
mat_1 * 2.7
```

3. Herhangi bir matris oluşturup (ya da hazır alıp), bütün elemanlarını 2.7 ile _doldururuz_:

```{code-cell} ipython3
mat_n = np.array([[1,2,3.],[4,5,6]])
print(mat_n)
print("----------")
mat_n.fill(2.3)
print(mat_n)
```

`fill` metodunu kullanırken dikkat etmeniz gereken iki şey var: 
* Metodu kullandığınızda doğrudan ilgili matrise etki eder, yeni bir matris döndürmez.
* Elinizdeki matrisin cinsi ne ise, doldururken kullandığınız değerin cinsini matrisin cinsine döndürür.

İkinci noktanın nasıl çalıştığını görmek için üstteki örneği bir kez daha, bu kez "hilesiz, el çabukluğu kerametsiz", ağır çekimde izleyelim:

```{code-cell} ipython3
mat_n = np.array([[1,2,3],[4,5,6]])
print(mat_n)
print("----------")
mat_n.fill(2.3)
print(mat_n)
```

Hoppala! Yukarıdakinin _aynısını_ yazdık ama bu sefer 2.3 yerine, 2 ile doldurdu... nereyi farklı girdik ki?.. (haydi bulun bakalım, size 1 dakika süre...)

...

Buldunuz mu? İki girişte de ilk satırdaki "3"e bakın. Evet, tam orası işte! İlk kodda "3." diyerek, çaktırmadan bütün diziyi ondalıklı tipine dönüştürmüşüz, ikincisinde hepsi tam sayı. Bu yüzden ikincisinde "2.3" ondalıklı sayısı ile doldur deyince matrisimize, "hiç kusura bakma, ben tam sayı matrisiyim, çok istiyorsa tam sayı kılığına girsin, 2 olarak eklerim" diyor, olayımız bundan ibaret. 8P 8)

### birim matris

Birim matris, tanım itibarı ile -ve tabii ki boyutları ile uyumlu olmak şartıyla- bir matrisle çarpıldığı zaman, o matrisi değiştirmeyen matristir. Bunu da sağlamanın tek yolu, köşegeni boyunca "1" değerini almasıdır. "Identity" (birim, etkisiz) olarak isimlendirilip "I" harfi ile temsil edildiğinden, okunuşundan yola çıkıp, ufak bir kelime oyunu ile `eye` olarak tanımlanır:

```{code-cell} ipython3
mat_birim_5x5 = np.eye(5,5)
print(mat_birim_5x5)
```

```{code-cell} ipython3
# Kare matris olması zorunluluğu yoktur:
mat_birim_3x5 = np.eye(3,5)
print(mat_birim_3x5)
```

### rastgele matrisler
Bazen uğraşmak istemeyiz, "sen kafana göre doldur, ben sonra bakarım" deriz. Bu durumlarda numpy.random kütüphanesinin rand ve randint'i epey yardımcı olur:

```{code-cell} ipython3
mat_rastgele_tamsayilar = np.random.randint(5,10,[2,3,4])
print(mat_rastgele_tamsayilar)
```

```{code-cell} ipython3
mat_rastgele_ondaliklar = np.random.rand(2,3,4)
print(mat_rastgele_ondaliklar)
```

Parametreler anlaşılıyor mu çağrıştan? randint'e ilk parametre olarak alt limiti (dahil), ikinci parametre olarak üst limiti (hariç), üçüncü parametre olarak da matrisimizin arzu ettiğimiz boyutunu belirtiyoruz (Bu arada, Python'da harikulade bir parametre sıralama opsiyonu var, birkaç haftaya göreceğiz inşallah 8)

rand'da ise parametre olarak sadece boyutu verebiliyoruz, o da bize, alışık olduğumuz üzere 0 ile 1 arasında (0 dahil, 1 hariç) sayılar üretiyor (teknik not: düzgün dağılımdan).

+++

<a name="arange_araliklar"></a>
### arange ile aralıklar 
`arange` komutu bize bir boyutlu diziler verir ama elemanlarını istediğimiz adımla türetebildiğimiz için, peşine bir de `reshape` çekersek tadından yenmez olur. İlk parametre başlayacağı sayı (dahil), ikinci parametre biteceği sayı (hariç), üçüncü parametre de adım boyu olur:

```{code-cell} ipython3
mat_aralik = np.arange(4,10.1,2.3)
print(mat_aralik)
```

Gördüğünüz üzere, ne başlangıcın, ne bitişin, ne de adım boyunun tam sayı olmak gibi bir zorunluluğu yok. İleriye doğru gidebildiğimiz gibi, geriye doğru da gidebiliriz (Nasıl?.. Adım boyumuzu negatif alarak tabii ki!):

```{code-cell} ipython3
mat_aralik_gerigeri = np.arange(10,2,-2)
print(mat_aralik_gerigeri)
```

```{code-cell} ipython3
# Bir de arange + reshape kombosu yapalım, tam olsun:
mat_kombo_3x3 = np.arange(1,10).reshape(3,3)
print(mat_kombo_3x3)
```

Yukarıdaki örnekte nokta ardından nokta birleşik yazımı (metodun dönüşüne metot) kafanızı karıştırıyorsa, parantez içinde de güzel güzel belirtebilirsiniz:

```{code-cell} ipython3
mat_kombo_3x3 = (np.arange(1,10)).reshape(3,3)
print(mat_kombo_3x3)
```

![SelcukErdem_AkilliEfendiKopek.png](imgs/SelcukErdem_AkilliEfendiKopek.png)
(Selçuk Erdem, Karikatürler 1, s.72)

### linspace: düzenli, disiplinli
Sayısal örneklerle haşır neşir olacağımız için bir fonksiyonun belli -ve hemen her zaman düzenl aralıklı- noktalarda değerini hesaplatmak istediğimizde arange yardıma koşar. Ama mesela doğrudan "23 ile 30 arasındaki değerleri hesaplayalım, 100 tane değer alalım" dersek, o zaman biraz zorlanıyoruz (ben zorlanıyorum en azından... `adım_boyu = (30 - 23) / 100`?.. 

Bu gibi durumlarda, bu işi yapan hazır linspace komutumuz var:

```{code-cell} ipython3
mat_duzenli_guzel_aralik = np.linspace(23,30,100)
print(mat_duzenli_guzel_aralik)
print("---------------------")
print("Bu güzel, düzenli dizinin eleman sayısı: ",mat_duzenli_guzel_aralik.size)
```

Yani, linspace ile tek yapmamız gereken başlangıcı (dahil), bitişi (**o da dahil**, aman dikkat!) ve toplamda kaç tane nokta istediğimiz belirtip, arkamıza yaslanmak!

## Matris işlemleri (dört işlem + bir ters, bir düz)
### Dört temel işlem (eleman bazında)
Matrislerimizi -birbirleriyle boyutları uyumlu olduğu sürece- dört temel işlemi kullanarak <u>eleman bazında</u> toplayabilir, çıkarabilir, çarpabilir ve hatta bölebiliriz.

```{code-cell} ipython3
np.random.seed(227)
mat_a_3x2 = np.random.randint(1,10,[3,2])
print("mat_a_3x2:\n",mat_a_3x2)
print("-"*50)

mat_b_3x2 = np.random.randint(1,10,[3,2])
print("mat_b_3x2:\n",mat_b_3x2)
print("-"*50)

mat_c_2x4 = np.random.randint(1,10,[2,4])
print("mat_c_2x4:\n",mat_c_2x4)
print("-"*50)
```

```{code-cell} ipython3
print("mat_a_3x2 + mat_b_3x2")
print(mat_a_3x2 + mat_b_3x2)
```

```{code-cell} ipython3
print("mat_a_3x2 * mat_b_3x2")
print(mat_a_3x2 * mat_b_3x2)
```

```{code-cell} ipython3
print("mat_a_3x2 / mat_b_3x2")
print(mat_a_3x2 / mat_b_3x2)
```

### Skaler ve Vektörel Çarpımlar
**Skaler Çarpım**  
Matrislerin skaler çarpımını ise `dot` fonksiyonu ile sağlarız:

```{code-cell} ipython3
skaler_carpim_3x4 = np.dot(mat_a_3x2,mat_c_2x4)
print("skaler_carpim_3x4 = np.dot(mat_a_3x2,mat_c_2x4):")
print(skaler_carpim_3x4)
```

**Vektörel Çarpım**  
Vektörel çarpım ise `cross` fonksiyonu ile yapılmakta:
$$\hat{i}\times \hat{j} = \hat{k}$$

```{code-cell} ipython3
i_hat = np.array([1,0,0])
j_hat = np.array([0,1,0])
k_hat = np.array([0,0,1])

print("i_hat x j_hat = ",np.cross(i_hat,j_hat))
print("-"*50)
print("mat_a_3x2 x mat_b_3x2 =",np.cross(mat_a_3x2,mat_b_3x2))
```

### Matrisin transpozesi, tersi ve determinantı
**Transpozesi**
Matrislerimizin transpozesini `T` metodu ile alırız (Uzun uzadıya yazmak isterseniz transpose() komutunu kullanabilirsiniz)

```{code-cell} ipython3
print(mat_a_3x2)
print("-"*50)
print(mat_a_3x2.T)
print()
print(np.transpose(mat_a_3x2))
mat_d_2x3x4 = np.random.randint(1,10,[2,3,4])
print("="*50)

print(mat_d_2x3x4)
print("-"*50)
print(mat_d_2x3x4.T)
```

**Tersi**  
Kare bir matrisin tersini `linalg` (_linear algebra_) kütüphanesinin `inv` (_inverse_) komutu ile alabiliriz:

```{code-cell} ipython3
np.random.seed(227)
mat_e_3x3 = np.random.randint(1,10,[3,3])
mat_e_3x3_tersi = np.linalg.inv(mat_e_3x3)
print(mat_e_3x3)
print(mat_e_3x3_tersi)
```

Bildiğiniz üzere, bir matrisin tersi, o matrisle çarpıldığında, birim matrisini veren matristir, yani:
$$A\cdot A^{-1} = \mathbb{1}$$

Yukarıdaki hesabımızı kontrol edelim:

```{code-cell} ipython3
print(np.dot(mat_e_3x3,mat_e_3x3_tersi))
```

$10^{-16}$ küçüklüğünü pratik olarak 0 alabileceğimiz için, çarpımın gayet güzel bir birim matris vermiş olduğunu görüyoruz! 8)

**'Tersimsisi'**  
Bir matrisin tersi hesaplanırken, analitik olarak determinantından da faydalanır. Determinant ise sadece kare matrislerin bir özelliği olduğundan, bu nedenle kare olmayan matrislerin analitik olarak tersleri yoktur. Fakat, nümerik olarak kare olmayan (nxm)'lik bir matris ile çarpılıp, (nxn)'lik bir birim matrisi verebilecek (mxn)'lik bir matris bulunabilir. Kare olmayan bu ters matrisler de sanki-ters, 'tersimsi' (_pseudo-inverse_) olarak adlandırılıp, buradan kısaltmayla, yine `linalg` kütüphanesinin `pinv` komutu ile bulunur (yalnız tabii her matrisin tersi olacak diye bir garanti yoktur).

```{code-cell} ipython3
np.random.seed(227)
mat_a_3x5 = np.random.randint(1,10,[3,5])
print("mat_a_3x5:")
print(mat_a_3x5)
print("-"*50)

print("mat_a_3x5_tersimsi:")
mat_a_3x5_tersimsi = np.linalg.pinv(mat_a_3x5)
print(mat_a_3x5_tersimsi)
print("-"*50)

print("mat_a_3x5 x mat_a_3x5_tersimsi =")
print(np.dot(mat_a_3x5,mat_a_3x5_tersimsi))
```

**Determinantı**  
Kare bir matrisin determinantını da şaşırtıcı olmayan bir biçimde, `linalg` kütüphanesinin `det` komutu ile elde ederiz:

```{code-cell} ipython3
print("mat_e_3x3")
print(mat_e_3x3)
print("-"*50)
print("det(mat_e_3x3):")
print(np.linalg.det(mat_e_3x3))
```

```{code-cell} ipython3

```
