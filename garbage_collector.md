## Garbage Collector (GC) 

Python’da Heap’te oluşan nesneler, işi bitince kendiliğinden “uçmaz”.  
Bir nesnenin bellekte kalıp kalmamasını **Garbage Collector (GC)** ve **referans sayımı (reference counting)** belirler.

> Kısa mantık:  
> Bir nesneye **hiçbir referans kalmazsa**, o nesne “çöp” olur ve bellekten temizlenir.

---

### GC Neden Var?

Python’da çok sayıda nesne oluşur:

- string’ler
- list/dict gibi dinamik yapılar
- class instance’ları

Bu nesneler Heap’te yaşar. Heap sınırsız değildir; kullanılmayan nesneler temizlenmezse bellek şişer.

GC’nin amacı:

- Heap’i gereksiz nesnelerden temizlemek
- Özellikle **döngüsel referansları (cyclic references)** yakalamak

---

## Reference Counting (Referans Sayımı)

CPython’da bellek yönetiminin temelinde **referans sayımı** vardır.

Bir nesneyi kaç farklı değişken/yer işaret ediyor?

```python
a = []
b = a
c = a
```

Bu durumda aynı list nesnesini `a`, `b`, `c` işaret eder → referans sayısı artar.

### Referans Sayısı 0 Olursa Ne Olur?

```python
a = []
a = None
```

- İlk satırda bir list nesnesi oluşur.
- İkinci satırda `a` artık o liste bakmaz.
- Eğer başka hiçbir referans yoksa, referans sayısı 0 olur ve nesne **hemen** silinebilir.

> Not: Bu “hemen” davranışı CPython’da yaygındır.
> Diğer Python implementasyonlarında farklılıklar olabilir.

---

## Döngüsel Referans (Cycle) Problemi

Referans sayımı tek başına her şeyi çözemez.
Çünkü şu durumda referans sayısı hiçbir zaman 0 olmaz:

```python
a = []
a.append(a)
```

Burada `a` listesinin içinde yine `a` var. Yani nesne kendini işaret ediyor:
- `a` → listeyi işaret eder
- listenin içi → tekrar aynı listeyi işaret eder

Bu bir **cycle (döngü)** oluşturur.

Eğer sadece referans sayımı olsaydı, bu nesne hiç silinmeyebilirdi.
İşte burada **Garbage Collector** devreye girer.

---

## GC Nasıl Çalışır? (Basit Model)

GC periyodik olarak Heap’teki nesneleri tarar ve şunu yapar:

- Bir grup nesnenin birbirini işaret edip etmediğini inceler (graph gibi düşün)
- Bu grup nesnelere **dışarıdan ulaşılabiliyor mu?** kontrol eder
- Dışarıdan erişilemiyorsa, bu grup “çöp” kabul edilir
- Cycle olsa bile temizler

> Özet:
> GC, “referans sayısı 0 değil ama programdan erişilemiyor” olan döngüleri temizler.

---

## GC Ne Zaman Çalışır?

- Bazı nesneler referans sayımı ile **hemen** temizlenir
- Döngüsel referanslar için GC zaman zaman çalışır:
    - programın yüküne göre
    - belli eşiklere göre
    - manuel tetiklenebilir

---

## gc Modülü (İleri Seviye: Gözlem ve Kontrol)

Python’da `gc` modülüyle GC’yi inceleyebilirsin:

```python
import gc

gc.isenabled()   # GC açık mı?
gc.collect()     # GC'yi manuel çalıştır
```

### Döngüsel Referans Örneği + Manuel Temizlik

```python
import gc

class Node:
    def __init__(self):
        self.other = None

a = Node()
b = Node()

a.other = b
b.other = a   # a <-> b cycle

del a
del b

gc.collect()  # cycle temizliği için manuel tetikleme
```

---

## del (Destructor) Konusu (Dikkat)

Bazı class’larda `__del__` tanımlarsan, cycle temizliği zorlaşabilir.

```python
class A:
    def __del__(self):
        print("Siliniyor")
```

Cycle içindeki nesnelerde `__del__` varsa GC bazı durumlarda nesneleri “güvenli” şekilde silemeyip bekletebilir.

> Pratik öneri:
> `__del__` kullanacaksan çok dikkatli ol, genelde gerekmez.

---

## GC ile Memory Leak Arasındaki Fark

Python’da “memory leak” her zaman klasik leak değildir.
- Bazı nesneler hala referanslı olduğu için silinmez (sen fark etmeden listede tutulur)
- Global değişkenler, cache’ler, closure’lar bunu tetikleyebilir

Örnek:

```python
cache = []

def add_to_cache(x):
    cache.append(x)
```

Burada `cache` büyür, GC silmez çünkü hala erişilebilir.

> GC sadece “ulaşılamayan” nesneyi siler.
> “Ulaşılabilir ama gereksiz” olanı silmez.

---

## Özet

- Python’da bellek temizliğinin temeli: **Reference Counting**
- Referans sayımı cycle’ları çözemez
- Cycle’lar için: **Garbage Collector**
- GC, dışarıdan erişilemeyen döngüleri bulup temizler
- Ulaşılabilir nesneyi GC silmez (cache gibi)
