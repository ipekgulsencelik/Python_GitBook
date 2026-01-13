# Heap & Stack

# Heap & Stack (Python)

Bu bölümde Python’da belleğin nasıl çalıştığını,
**Stack (Yığın)** ve **Heap (Öbek)** kavramlarını
örneklerle ve sade bir dille öğreneceğiz.

---

## Stack Nedir?

**Stack (Yığın)**, fonksiyon çağrıları sırasında kullanılan,
**geçici ve hızlı** bir bellek alanıdır.

### Stack’in Özellikleri
- LIFO mantığıyla çalışır (Last In – First Out)
- Fonksiyonlar çalışırken oluşur
- Fonksiyon bitince otomatik temizlenir
- Çok hızlıdır

### Stack’te Tutulanlar
- Fonksiyon çağrıları
- Parametreler
- Yerel değişkenler
- Referanslar (adresler)

---

## Heap Nedir?

**Heap (Öbek)**, program çalışırken oluşturulan
**dinamik ve büyük nesnelerin** tutulduğu bellek alanıdır.

### Heap’in Özellikleri
- Dinamiktir
- Daha yavaştır
- Garbage Collector tarafından temizlenir
- Nesneler burada yaşar

### Heap’te Tutulanlar
- list
- dict
- set
- tuple
- string
- class nesneleri

---

## Basit Örnek

```python
x = 3
boxers = ["mike tyson", "muhammed ali"]

### Bellek Açıklaması

- `x` → Stack’te tutulur  
- `3` → Küçük / sabit değer (nesne)  
- `boxers` → Stack’te bir **referans**  
- Liste ve içindeki string’ler → **Heap’te**

---

## Fonksiyon Çağrısı ve Bellek

```python
def greeting(name):
    print(f"{name} hello")

greeting("ipek")

### Ne Olur?

- `greeting` çağrılır → Stack’te yeni bir frame açılır
- `name` parametresi → Stack’te tutulur
- `"ipek"` string’i → Heap’te bulunur
- Fonksiyon biter → Stack otomatik temizlenir
- Heap’teki veri:
  - Başka referans yoksa
  - Garbage Collector (GC) tarafından silinir

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
a = a + "!"

Yeni bir string Heap’te oluşturulur.

---

### Mutable (Değiştirilebilir)

- `list`
- `dict`
- `set`

```python
numbers = [1, 2]
numbers.append(3)

Aynı liste Heap’te değiştirilir.

---

## Stack vs Heap Karşılaştırma

| Özellik | Stack | Heap |
|---|---|---|
| Hız | Çok hızlı | Daha yavaş |
| Boyut | Küçük | Büyük |
| Temizlik | Otomatik | Garbage Collector |
| Kullanım | Geçici | Kalıcı nesneler |

---

## Akılda Kalıcı Örnek

- **Stack** → Masa üstündeki not kağıdı
- **Heap** → Arşiv dolabı

Not kağıdı hızlıdır, geçicidir.  
Arşiv büyüktür, kalıcıdır.

---

## Özet

- Stack geçici ve hızlıdır
- Heap nesnelerin yaşadığı alandır
- Python’da değişkenler genelde **değer değil referans** taşır
- Mutable ve immutable farkı heap davranışını etkiler

---

## Mini Test

1. `a = [1, 2]; b = a; b.append(3)` → `a` ne olur?
2. `s = "hi"; t = s; s += "!"` → `t` ne olur?
3. List neden heap’te tutulur?
