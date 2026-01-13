# Python: Class Attribute vs Object (Instance) Attribute

Bu dokümanda Python’da **class attribute** ve **object (instance) attribute** kavramlarının
mantığı, farkları ve en sık yapılan hatalar örneklerle açıklanmaktadır.

---

## Object (Instance) Attribute Nedir?

**Object attribute**, her nesneye (instance) özel olan değişkendir.  
Genellikle `__init__` metodu içinde `self` anahtar kelimesiyle tanımlanır.

### Özellikleri
- Her nesnenin **kendi kopyası** vardır
- Bir nesnede değişirse **diğer nesneleri etkilemez**
- Nesnenin **durumunu (state)** temsil eder

### Örnek
```python
class User:
    def __init__(self, name, age):
        self.name = name   # object attribute
        self.age = age     # object attribute


u1 = User("İpek", 28)
u2 = User("Burak", 35)

u1.age = 29

print(u1.age)  # 29
print(u2.age)  # 35
```

- `age` her kullanıcıya özeldir
- `u1` değişti, `u2` etkilenmedi

---

## Class Attribute Nedir?

**Class attribute**, sınıfa ait olan ve tüm nesneler (instance’lar) tarafından **paylaşılan** değişkendir.  
Sınıfın gövdesinde (Sınıf seviyesinde), metodların dışında tanımlanır.

### Özellikleri

- **Tek bir kopyası** vardır
- Tüm nesneler **aynı veriyi paylaşır**
- Ortak bilgi, sabit değer veya genel kural tanımlamak için kullanılır

### Örnek

```python
class User:
    role = "member"   # class attribute

    def __init__(self, name):
        self.name = name


u1 = User("İpek")
u2 = User("Burak")

print(u1.role)  # member
print(u2.role)  # member
```

`role` değişkeni sınıfa aittir ve tüm nesneler tarafından ortak olarak kullanılır.

- `role` sınıfa aittir
- Her instance aynı değeri görür

---

## En Sık Yapılan Hata (Mutable Class Attribute)

Python’da **list, dict, set** gibi *mutable* (değiştirilebilir) yapılar **class attribute olarak tanımlanmamalıdır**.

Bunun nedeni, class attribute’ların **tüm nesneler tarafından ortak olarak paylaşılmasıdır**.

---

### Hatalı Kullanım

```python
class Developer:
    languages = []  # ❌ class attribute (mutable)

    def add_language(self, lang):
        self.languages.append(lang)


d1 = Developer()
d2 = Developer()

d1.add_language("Python")

print(d1.languages)  # ['Python']
print(d2.languages)  # ['Python']
```

**Neden Bu Bir Hata?**
- `languages` listesi **sınıfa aittir**
- Tüm nesneler **aynı listeyi paylaşır**
- Bir nesnede yapılan değişiklik **diğerlerini de etkiler**
- Bu durum genellikle **istenmeyen yan etkilere** yol açar
  
🚨 Yani:
- `languages` **tek bir liste**
- Tüm nesneler aynı listeyi paylaşıyor

---

### Doğru Kullanım (Object Attribute)

Mutable yapılar, her nesneye özel olacak şekilde **object (instance) attribute** olarak tanımlanmalıdır.

```python
class Developer:
    def __init__(self):
        self.languages = []  # ✅ object attribute

    def add_language(self, lang):
        self.languages.append(lang)


d1 = Developer()
d2 = Developer()

d1.add_language("Python")

print(d1.languages)  # ['Python']
print(d2.languages)  # []
```

✔️ Her nesnenin **kendi listesi** var
✔️ Yan etki yok

**Özet**
- **Mutable veri + class attribute = HATA**
- Liste, sözlük, set gibi yapılar:
  - `__init__` içinde
  - `self` ile
  - object attribute olarak tanımlanmalıdır

---

## Class Attribute Ne Zaman Kullanılır?

### ✅ Doğru Kullanım Senaryoları

```python
class Car:
    wheel_count = 4          # sabit bilgi
    company = "Tesla"        # ortak bilgi
```

- Sabit değerler
- Ortak kurallar (Tüm nesneler için geçerli kurallar)
- Konfigürasyon
- Sayaç (counter)

### 🔢 Örnek: Sayaç

```python
class User:
    total_users = 0

    def __init__(self, name):
        self.name = name
        User.total_users += 1
```

---

## Attribute Arama Sırası (ÇOK ÖNEMLİ)

Python bir attribute ararken şu sırayı izler:

1️⃣ **Object(instance) attribute**
2️⃣ **Class attribute**
3️⃣ **Parent class attribute**

#### 🔍 Örnek

```python
class A:
    x = 10

a = A()
print(a.x)  # 10

a.x = 99
print(a.x)  # 99 (object attribute oluştu!)
```

🧠 `a.x = 99` ifadesi class attribute’u değiştirmez → class attribute’ü **ezmez**,
sadece **nesneye özel yeni bir attribute** yaratır.

---

## Özet Tablo

| Özellik | Object Attribute | Class Attribute |
|------|-----------------|----------------|
| Tanım Yeri | `__init__` (`self.`) | Sınıf seviyesi / gövdesi |
| Kime Ait | Nesne | Sınıf |
| Kopya Sayısı | Her nesnede ayrı | Tek |
| Mutable Risk | ❌ Yok | ⚠️ Var |
| Kullanım Amacı | Kişisel veri | Ortak veri |

---

## 🎯 Altın Kural

> **Değişmesi beklenen her şey → object attribute**  
> **Ortak ve sabit olan → class attribute**
