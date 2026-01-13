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
def greeting(name):
    print(f"{name} hello")

greeting("ipek")
```

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
```

Yeni bir string Heap’te oluşturulur.

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
