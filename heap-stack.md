# Heap & Stack

Bu bölümde Python’da bellek yönetimini iki ana kavram üzerinden öğreneceğiz:

- **Stack (Yığın):** Fonksiyon çağrıları ve geçici/yerel bilgiler
- **Heap (Öbek):** Program çalışırken oluşan nesneler (list, dict, str, class vb.)

> 📌 Önemli fikir:  
> Python’da çoğu zaman değişkenler “değeri” değil, **bir nesneye işaret eden referansı** taşır.

---

## Stack Nedir?

**Stack (Yığın)**, fonksiyon çalışırken kullanılan, **geçici, düzenli ve hızlı** bir bellek alanıdır.

### Stack’in Özellikleri
Stack, **LIFO** mantığıyla çalışır:

- **Last In** (son giren)
- **First Out** (ilk çıkar)
  
Fonksiyonlar çalışırken oluşur
Fonksiyon çağrısı olduğunda stack’e bir “çerçeve” (**stack frame**) eklenir.  
Fonksiyon bittiğinde o frame **otomatik kaldırılır**
Çok hızlıdır

### Stack’te Tutulanlar
- Fonksiyon çağrıları (call frames)
- Parametreler
- Yerel değişkenler (local variables)
- Çoğunlukla **referanslar/adresler** (nesnenin kendisi değil)

> Stack’in en güçlü yanı:  
> **Hızlıdır** ve **kendiliğinden temizlenir**.

---

## Heap Nedir?

**Heap (Öbek)**, program çalışırken oluşturulan **dinamik ve büyük nesnelerin** tutulduğu bellek alanıdır.

### Heap’in Özellikleri
- Boyut dinamik olabilir (liste büyür-küçülür)
- Daha yavaştır
- Temizliği “otomatik” ama stack gibi anında değil:
  - **Garbage Collector** (GC) ile yapılır
- Nesneler burada yaşar (list/dict/str/class)r

### Heap’te Tutulanlar
- list
- dict
- set
- tuple
- `str`
- class instance’ları (nesneler)
- çoğu “Python object”

---

## Python’da “Değişken = Referans” Mantığı

Aşağıdaki satıra bakalım:

```python
x = 3
```

Bu satırın anlamı:

- Heap’te bir **`3` nesnesi** vardır  
  (Python’da `int` dahil her şey bir nesnedir)

- `x` ise bu nesneye işaret eden bir **isim / referanstır**

> **Pratik kural:**  
> `x` bir kutu değildir.  
> `x`, Heap’teki bir nesneyi işaret eden **etiket** gibidir.

---

## Örnek: List Neden Heap’te Tutulur?

```python
boxers = ["mike tyson", "muhammed ali"]
```

Burada olan şey:

- `boxers` → stack’te duran bir **referans**
- `["mike tyson", "muhammed ali"]` → heap’te duran **list nesnesi**
- `"mike tyson"` ve `"muhammed ali"` → heap’te duran **string nesneleri**

List büyük ve dinamik olduğu için heap’te yaşar.

---

## Basit Örnek

```python
x = 3
boxers = ["mike tyson", "muhammed ali"]
```
### Bellek Açıklaması

- `x` → Stack’te tutulur  
- `3` → Küçük / sabit değer (nesne)  
- `boxers` → Stack’te bir **referans**  
- Liste ve içindeki string’ler → **Heap’te**

---

## Fonksiyon Çağrısı ve Bellek

```python
def greeting(first_name: str):
    print(f"{first_name} hello")

greeting("ipek")
```

### Ne Olur?

- `greeting` çağrılır → Stack’te yeni bir frame eklenir
- `first_name` parametresi frame içinde oluşur → Stack’te tutulur
- `"ipek"` string nesnesi heap’te bulunur (veya heap’te oluşturulur)
- `first_name` heap’teki `"ipek"` nesnesine referans tutar

### Fonksiyon bitince
- `first_name` stack’ten silinir
- `"ipek"` nesnesine başka referans yoksa GC daha sonra temizleyebilir

### Özet
- Fonksiyon biter → Stack otomatik temizlenir
- Heap’teki veri:
  - Başka referans yoksa Garbage Collector (GC) tarafından silinir

---

## Mutable vs Immutable

### Immutable (Değiştirilemez)

- `int`
- `float`
- `bool`
- `str`
- `tuple`

```python
a = "hi"
s += "!"
```

Yeni bir string Heap’te oluşturulur.

Bu “değiştirme” gibi görünür ama aslında:
- `"hi!"` diye **yeni bir string nesnesi** oluşur
- `s` artık yeni nesneyi işaret eder

> Immutable nesnelerde “değişiklik” çoğunlukla **yeni nesne** üretir.

---

### Mutable (Değiştirilebilir)

- `list`
- `dict`
- `set`

```python
numbers = [1, 2]
numbers.append(3)
```

Aynı liste Heap’te değiştirilir.

Burada:
- Aynı list nesnesi heap’te durur
- İçeriği değiştirilir
- `lst` aynı nesneyi işaret etmeye devam eder

> Mutable nesnelerde aynı heap nesnesinin içi değişir.

---

## “Aynı Nesneyi Paylaşma” Problemi (Çok önemli)

```python
a = [1, 2]
b = a
b.append(3)
print(a)
```

Çıktı:
```python
[1, 2, 3]
```

Neden?
- `a` ve `b` aynı heap listesine işaret ediyor
- `b.append(3)` aynı nesneyi değiştirdiği için `a` da değişmiş gibi görünür
 
> Bu, Python’da en sık bug üreten konulardan biridir.

---

## Shallow Copy vs Deep Copy (Heap kopyalama)
### Shallow Copy (Yüzeysel)

Sadece üst kabı kopyalar, içerideki nesneler paylaşılabilir:

```python
import copy

a = [[1, 2], [3, 4]]
b = copy.copy(a)
b[0].append(99)
print(a)
```

`a` da değişebilir çünkü iç listeler hâlâ ortak.

### Deep Copy (Derin)

İç içe nesneleri de kopyalar:

```python
import copy

a = [[1, 2], [3, 4]]
b = copy.deepcopy(a)
b[0].append(99)
print(a)
```

`a` değişmez.

---

## Garbage Collector (GC) Kısaca

Python’da bellek temizliği iki mekanizma ile olur:
- **Reference Counting:** Bir nesneyi işaret eden referans sayısı 0 olursa serbest kalır
- **GC (cycle collector):** Döngüsel referansları (A -> B, B -> A) temizler

> Pratikte: Sen “delete” yapmasan bile Python çoğu işi otomatik halleder.
> Ama döngüsel referanslar için GC devreye girer.

---

## Stack vs Heap Karşılaştırma

| Özellik | Stack | Heap |
|---|---|---|
| Hız | Çok hızlı | Daha yavaş |
| Boyut | Sınırlı | Daha geniş, dinamik |
| Temizlik | Otomatik (frame kapanır) | Garbage Collector / refcount |
| Kullanım | Fonksiyon çağrıları, geçici bilgiler | Kalıcı Nesneler (list/dict/str/class) |
| Yaşam Süresi | Fonksiyon süresi | Referans kaldığı sürece |

---

## Akılda Kalıcı Örnek

- **Stack** → Masa üstündeki not kağıdı (hızlı, geçici)
- **Heap** → Arşiv dolabı (büyük, kalıcı)

Not kağıdı hızlıdır, geçicidir.  
Arşiv büyüktür, kalıcıdır.

---

## Özet

- Stack geçici ve hızlıdır
- Heap nesnelerin yaşadığı alandır
- Python’da değişkenler genelde **değer değil referans** taşır
- Mutable ve immutable farkı heap davranışını etkiler


