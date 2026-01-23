# 🧩 Basic Python Syntax

Bu bölümde Python’un **temel sözdizimini** (syntax) öğreniyoruz.  
Hedefimiz şu: Kod yazarken “bu neydi?” demeden, temel yapı taşlarını **akıcı** kullanmak.

> Bu bölüm; `print`, değişkenler, veri tipleri, operatörler, input, type casting ve f-string’leri kapsar.

---

## 1) `print()` — Ekrana Yazdırma

Python’da ekrana yazdırmak için `print()` kullanırız.

```python
print("Merhaba!")
print(123)
print(3.14)
print(True)
```

### Aynı satıra birden fazla değer yazdırma
`print` içine virgülle birden fazla ifade verebilirsin. Python araya boşluk koyar.

```python
name = "İpek"
age = 25
print("Ad:", name, "Yaş:", age)
```

### `sep` ve `end` kullanımı
- `sep`: değerler arası ayraç
- `end`: satır sonunda ne yazacağı

```python
print("a", "b", "c", sep="-")   # a-b-c
print("Merhaba", end=" ")      # satır bitmez
print("Dünya")                 # aynı satırda devam eder
```

---

## 2) Yorum Satırları (Comments)

Kodun okunabilirliğini artırır, açıklama ekleriz.

```python
# Bu bir yorum satırıdır.
print("Çalışır ama yorum çalışmaz.")
```

### Docstring (çok satırlı açıklama)
Genelde fonksiyon ve sınıf açıklamak için kullanılır.

```python
"""
Bu bir docstring örneğidir.
Birden fazla satır yazabilirsin.
"""
```

---

## 3) Değişkenler (Variables)

Değişken, bir değeri saklayan isimdir.

```python
x = 10
pi = 3.14
name = "İpek"
is_active = True
```

### Python’da tip belirtmek zorunda değilsin
Python dinamik tipli bir dildir: değer değişirse tip de değişebilir.

```python
x = 10
x = "on"   # artık string oldu
```

### Değişken isimlendirme kuralları
✅ Doğru:
- `user_name`
- `total_price`
- `is_admin`

❌ Yanlış:
- `2name` (sayıyla başlayamaz)
- `user-name` (tire olmaz)
- `class` (anahtar kelime)

> Python’da yaygın stil: **snake_case** (`user_name`)

---

## 4) Temel Veri Tipleri

### `int` — Tam sayı
```python
a = 10
type(a)  # <class 'int'>
```

### `float` — Ondalıklı sayı
```python
b = 10.5
type(b)  # <class 'float'>
```

### `str` — Metin
```python
text = "Merhaba"
type(text)  # <class 'str'>
```

### `bool` — True / False
```python
is_ok = True
is_ok = False
type(is_ok)  # <class 'bool'>
```

### `None` — Boş / değer yok
```python
value = None
```

---

## 5) `type()` — Tip Öğrenme

```python
x = 10
print(type(x))  # <class 'int'>
```

---

## 6) Tip Dönüşümü (Type Casting)

Kullanıcıdan gelen değerler genelde `str` olur. Sayısal işlem yapacaksan çevirmelisin.

```python
age_text = "25"
age = int(age_text)
print(age + 5)  # 30
```

### Dikkat: Hatalı dönüştürme hata verir
```python
int("on")  # ValueError
```

### Sık kullanılan dönüşümler
```python
int("10")
float("10.5")
str(100)
bool(1)      # True
bool(0)      # False
```

---

## 7) `input()` — Kullanıcıdan Veri Alma

```python
name = input("Adını gir: ")
print("Merhaba", name)
```

> ⚠️ `input()` her zaman **string** döndürür.

### Sayı almak (int/float)
```python
age = int(input("Yaşını gir: "))
height = float(input("Boyunu gir (örn 1.75): "))
```

---

## 8) Operatörler

### Aritmetik operatörler
```python
a = 10
b = 3

print(a + b)   # 13
print(a - b)   # 7
print(a * b)   # 30
print(a / b)   # 3.333...
print(a // b)  # 3  (tam bölme)
print(a % b)   # 1  (mod)
print(a ** b)  # 1000 (üs)
```

### Karşılaştırma operatörleri (sonuç bool)
```python
x = 10
print(x == 10)  # True
print(x != 10)  # False
print(x > 5)    # True
print(x <= 9)   # False
```

### Mantıksal operatörler
```python
is_member = True
has_card = False

print(is_member and has_card)  # False
print(is_member or has_card)   # True
print(not is_member)           # False
```

---

## 9) String (Metin) Temelleri

### Birleştirme
```python
full_name = "Ada" + " " + "Lovelace"
```

### Uzunluk
```python
len("Python")  # 6
```

### Dilimleme (slicing)
```python
text = "Hello, World!"
print(text[0])     # H
print(text[0:5])   # Hello
print(text[7:12])  # World
```

### `split` ve `replace`
```python
sentence = "Python, çok güzel"
print(sentence.split(", "))
print(sentence.replace("güzel", "harika"))
```

---

## 10) f-string — En Temiz Yazdırma Yöntemi

String içinde değişken kullanmanın en modern yolu:

```python
name = "İpek"
age = 25
print(f"Adım {name}, yaşım {age}.")
```

### Sayı formatlama
```python
pi = 3.1415926
print(f"Pi: {pi:.2f}")  # Pi: 3.14
```

---

## 11) Girinti (Indentation) ve Blok Mantığı

Python’da bloklar `{}` ile değil, **girinti ile** belirlenir.

```python
x = 10

if x > 5:
    print("x 5'ten büyük")
    print("Bu da aynı blokta")
print("Bu satır blok dışı")
```

> ⚠️ 4 boşluk standarttır. Tab/space karıştırma hata çıkarabilir.

---

## 12) Sık Yapılan Hatalar (Çok Normal 😌)

### 1) Tırnak unutmak
```python
print(Merhaba)  # NameError
```

Doğrusu:
```python
print("Merhaba")
```

### 2) `input()` ile sayısal işlem yapmak
```python
a = input("Sayı: ")
print(a + 5)  # hata (str + int)
```

Doğrusu:
```python
a = int(input("Sayı: "))
print(a + 5)
```

### 3) Girinti hatası
```python
if True:
print("hata")  # IndentationError
```

---

## ✅ Mini Alıştırmalar

1) Kullanıcıdan ad ve yaş al, f-string ile yazdır:
- “Merhaba İpek, yaşın 25.”

2) Kullanıcıdan iki sayı al, toplamını yazdır.

3) `a=10`, `b=3` için:
- tam bölme (`//`)
- mod (`%`)
- üs (`**`)
sonuçlarını yazdır.

---

## 🎯 Bu Bölümde Ne Öğrendin?

- `print`, `input`, `type`
- veri tipleri: `int`, `float`, `str`, `bool`, `None`
- operatörler
- f-string
- girinti (indentation) mantığı
- yaygın hatalar

➡️ Sıradaki bölüm: **Data Structures (List, Tuple, Set, Dict)**  
`03-data-structures.md`
