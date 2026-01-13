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
