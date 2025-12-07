# 🏎️ Görev 2: Çift Sensörlü Gaz Pedalı Güvenliği (APPS Logic)


## 🎯 Amaç: "Mühendis Gibi Düşünmek"
Bir yarış aracında gaz pedalına güvenemezsiniz. Kablo kopabilir, sensör bozulabilir veya kısa devre yapabilir. Bu yüzden FSAE kuralları gereği araçlarda **2 farklı sensör** bulunur.

**Problem:** Ya sensörün biri "%100 Gaz" derken, diğeri "%0 Gaz" derse? Araba ne yapmalı? Gaza mı basmalı? Yoksa durmalı mı?

Bu görevde; **FSAE T11.8** kuralını uygulayan, hatalı sensör verilerini yakalayıp aracı **Güvenli Moda (Safe State)** alan bir karar algoritması yazacaksınız.

---

## ⚙️ Senaryo ve Kurallar (The Logic Puzzle)

Elinizde sanal bir gaz pedalı var. Kullanıcıdan iki farklı sensör değeri (0-100 arası) alacaksınız.

### FSAE Kuralı (T11.8 - Implausibility Check)
1.  **Fark Kontrolü:** İki sensör arasındaki fark **%10'dan fazlaysa** bu bir HATADIR (Implausibility).
    * *Örnek:* Sensör A: 50, Sensör B: 65 -> Fark 15 -> **HATA!**
2.  **Karar Mekanizması:**
    * **Eğer HATA YOKSA:** İki sensörün ortalamasını al ve `tork_istegi` olarak motoru sür.
    * **Eğer HATA VARSA:** Motor gücünü (`tork_istegi`) DERHAL **0** yap ve ekrana hata mesajı bas.

---

## 🛠️ Teknik Gereksinimler

Kodunuz aşağıdaki kısıtlamalara harfiyen uymalıdır:

### 1. Struct Zorunluluğu
Tüm veriler dağınık değişkenlerde değil, tek bir `struct` çatısı altında olmalıdır.
```c
// Örnek Yapı
typedef struct {
    int sensor_1;       // 1. Sensör verisi
    int sensor_2;       // 2. Sensör verisi
    int tork_istegi;    // Sonuç motor gücü
    int hata_durumu;    // 0: Normal, 1: Hata
} PedalSistemi;
