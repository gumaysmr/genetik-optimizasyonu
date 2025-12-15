# 📚 Öğrenci Etüt Programı Optimizasyonu: Genetik Algoritma (GA)

Bu proje, bir öğrencinin **matematik (x₁)** ve **fen (x₂)** derslerine ayırdığı haftalık etüt sürelerini,
**maksimum akademik başarı** sağlayacak şekilde **Genetik Algoritma (GA)** kullanarak optimize etmektedir.

Problem, hem amaç fonksiyonu hem de çeşitli kısıtlar içerdiği için **kısıtlı bir optimizasyon problemi**
olarak ele alınmıştır.

---

## 1. 📝 Problem Tanımı ve Matematiksel Model

Amaç, öğrencinin matematik ve fen derslerine ayırdığı çalışma sürelerini kullanarak
başarı skorunu temsil eden fonksiyonu **maksimize etmektir**.

### Amaç Fonksiyonu (Maksimizasyon)

Öğrencinin başarı skorunu hesaplamak için kullanılan fonksiyon:

$$
y = 4x_1 + 5x_2 - 0.5x_1^2 - 0.2x_2^2
$$

- **x₁:** Matematik etüt süresi (saat)
- **x₂:** Fen etüt süresi (saat)

Fonksiyonda doğrusal terimler çalışmanın başarı üzerindeki olumlu etkisini,
kareli terimler ise aşırı çalışmanın verim düşürücü etkisini modellemektedir.

---

### Kısıtlamalar

Karar değişkenleri hem fiziksel aralıklar hem de problem özgü kısıtlar ile sınırlandırılmıştır:

| Kısıt Türü | Değişken | Aralık / Kural |
|-----------|---------|----------------|
| Fiziksel Aralık | x₁ (Matematik) | 0 ≤ x₁ ≤ 10 |
| Fiziksel Aralık | x₂ (Fen) | 0 ≤ x₂ ≤ 10 |
| Problem Kısıtı | x₁ + x₂ | ≤ 12 |
| Problem Kısıtı | x₂ | ≥ 2 |

Kısıtlar, genetik algoritma sürecinde **ceza (penalty) yöntemi** ile ele alınmıştır.

---

## 2. ⚙️ Genetik Algoritma (GA) Yapısı

Bu optimizasyon problemini çözmek için kullanılan Genetik Algoritma'nın temel parametreleri
ve mekanizmaları aşağıda özetlenmiştir.

### GA Parametreleri

| Parametre | Açıklama |
|---------|----------|
| Popülasyon Boyutu | Her nesildeki birey sayısı |
| Nesil Sayısı | Algoritmanın çalıştırıldığı iterasyon sayısı |
| Mutasyon Oranı | Mutasyonun uygulanma olasılığı |
| Elitizm | En iyi bireyin yeni nesle doğrudan aktarılması |

---

### GA Operatörleri ve Stratejileri

- **Başlangıç Popülasyonu:** Bireyler, tanımlı aralıklar içinde rastgele oluşturulmuştur.
- **Seçilim (Selection):** Ebeveyn seçimi için *Rulet Tekerleği Seçimi* yöntemi kullanılmıştır.
- **Çaprazlama (Crossover):** *Tek Noktalı Çaprazlama* yöntemi uygulanmıştır.
- **Mutasyon (Mutation):** Belirli bir olasılıkla gen değerlerine küçük rastgele değişiklikler eklenmiştir.
- **Kısıt Yönetimi:** Kısıtları ihlal eden bireylerin fitness değeri ceza yöntemiyle düşürülmüştür.
- **Elitizm:** Her nesildeki en iyi birey korunarak yeni nesle aktarılmıştır.

---

## 3. 🚀 Çalıştırma ve Kurulum

Bu proje tek bir Jupyter Notebook dosyası içermektedir ve Python ortamında çalıştırılmalıdır.

### Gerekli Kütüphaneler

Projeyi çalıştırmak için aşağıdaki kütüphanelerin yüklü olması gerekmektedir:

```bash
pip install numpy matplotlib
