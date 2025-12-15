# Genetik Algoritma ile Öğrenci Etüt Programı Optimizasyonu

Bu proje, BLG-307 Yapay Zeka Sistemleri dersi kapsamında,
bir öğrencinin matematik (x₁) ve fen (x₂) derslerine ayırdığı etüt sürelerini,
akademik başarıyı en üst düzeye çıkaracak biçimde belirlemek amacıyla geliştirilmiştir.

Problem, hem doğrusal olmayan bir amaç fonksiyonu
hem de birden fazla gerçekçi kısıt içerdiği için
klasik optimizasyon yöntemleriyle çözümü zor olan
kısıtlı bir optimizasyon problemi olarak ele alınmıştır.
Bu nedenle çözüm sürecinde,
rastgelelik ve evrimsel arama mantığına dayanan
Genetik Algoritma yöntemi tercih edilmiştir.

---

## 1. Problem Tanımı ve Matematiksel Model

Bir öğrencinin çalışma kapasitesi sınırlıdır ve bu kapasite,
matematik ve fen dersleri arasında dengeli bir şekilde dağıtılmalıdır.
Her iki ders için ayrılan çalışma süreleri,
öğrencinin akademik başarısını doğrudan etkilemektedir.

Ancak çalışma süresi ile başarı arasındaki ilişki doğrusal değildir:
- Yetersiz çalışma başarının düşmesine neden olurken,
- Aşırı çalışma belirli bir noktadan sonra verim kaybına yol açabilmektedir.
- Ayrıca fen dersi için minimum çalışma süresi gibi
gerçek hayata uygun zorunluluklar bulunmaktadır.

Bu nedenlerle problem,
yalnızca başarıyı maksimize etmeyi değil,
aynı zamanda uygulanabilir, dengeli ve gerçekçi
bir etüt programı oluşturmayı hedeflemektedir.

---

### Amaç Fonksiyonu 

Öğrencinin başarısını temsil eden amaç fonksiyonu aşağıdaki şekilde tanımlanmıştır:

\[
y = 4x_1 + 5x_2 - 0.5x_1^2 - 0.2x_2^2
\]

Burada:
- x₁: Matematik dersi için ayrılan etüt süresi (saat)
- x₂: Fen dersi için ayrılan etüt süresi (saat)

Fonksiyondaki doğrusal terimler,
çalışma süresinin başarı üzerindeki olumlu etkisini temsil ederken;
ikinci dereceden terimler,
aşırı çalışmanın verim düşürücü etkisini
matematiksel olarak modele dahil etmektedir.
Bu yapı sayesinde daha gerçekçi bir başarı modeli elde edilmiştir.

---

### Kısıtlar

Optimizasyon problemi aşağıdaki kısıtlara sahiptir:

| Kısıt | Açıklama |
|------|----------|
| x₁ + x₂ ≤ 12 | Toplam çalışma süresi sınırı |
| x₂ ≥ 2 | Fen dersi için minimum çalışma süresi |
| 0 ≤ x₁ ≤ 10 | Matematik çalışma süresi aralığı |
| 0 ≤ x₂ ≤ 10 | Fen çalışma süresi aralığı |

Genetik Algoritma sürecinde bu kısıtlar,
çözümleri doğrudan elemek yerine
ceza yöntemi ile fitness fonksiyonuna entegre edilmiştir.
Bu yaklaşım, algoritmanın arama sürecini
geçerli çözüm bölgesine yönlendirmesini sağlar.

---

## 2. Genetik Algoritma Yapısı

Genetik Algoritma,
rastgelelik, seçilim ve varyasyon temelli
bir optimizasyon yöntemidir.
Bu çalışmada Genetik Algoritma,
nesiller boyunca daha iyi çözümler üretecek şekilde yapılandırılmıştır.

---

### Genetik Algoritma Parametreleri

Algoritmanın davranışını belirleyen temel parametreler şunlardır:

| Parametre | Açıklama |
|---------|----------|
| Popülasyon Boyutu | Her nesilde değerlendirilen aday çözüm sayısı |
| Nesil Sayısı | Algoritmanın evrimleştiği iterasyon sayısı |
| Çaprazlama Oranı | Yeni birey üretme olasılığı |
| Mutasyon Oranı | Genlerde rastgele değişim olasılığı |
| Elitizm | En iyi bireyin korunma mekanizması |

Bu parametreler,
keşif ve yakınsama dengesi açısından
kritik öneme sahiptir.

---

### Genetik Algoritma Operatörleri ve Akış

- *Başlangıç Popülasyonu:*  
  Bireyler, x₁ ve x₂ değişkenleri için
  tanımlı aralıklar içerisinde rastgele oluşturulmuştur.
  Bu durum, çözüm uzayının geniş bir bölümünün araştırılmasını sağlar.

- *Fitness Değerlendirmesi:*  
  Her birey için önce amaç fonksiyonu değeri hesaplanır,
  ardından kısıt ihlalleri kontrol edilerek ceza uygulanır.
  Elde edilen değer, bireyin fitness değeri olarak kullanılır.

- *Seçilim:*  
  Ebeveyn seçimi için Rulet Tekerleği Seçimi yöntemi tercih edilmiştir.
  Bu yöntem, iyi çözümlerin daha sık seçilmesini sağlarken,
  popülasyon çeşitliliğini korur.

- *Çaprazlama:*  
  Tek noktalı çaprazlama yöntemi ile
  ebeveyn bireylerin genetik bilgileri birleştirilerek
  yeni aday çözümler oluşturulmuştur.

- *Mutasyon:*  
  Belirli bir olasılıkla gen değerlerine küçük rastgele değişiklikler eklenmiştir.
  Bu işlem, algoritmanın yerel optimumlara sıkışmasını önler
  ve çözüm uzayının farklı bölgelerinin keşfedilmesine yardımcı olur.

- *Elitizm:*  
  Her nesilde en yüksek fitness değerine sahip birey,
  bilgi kaybını önlemek amacıyla
  doğrudan bir sonraki nesle aktarılmıştır.

---

## 3. Sonuçların Analizi

Algoritmanın çalışması sonucunda,
nesiller ilerledikçe fitness değerlerinin genel olarak arttığı,
ve çözümlerin kısıtları sağlayan kararlı bir noktaya yakınsadığı gözlemlenmiştir.

Elde edilen sonuçlar:
- En iyi fitness değerinin nesillere göre değişimi
- Matematik ve fen etüt sürelerinin zaman içindeki yakınsama davranışı

grafikler aracılığıyla analiz edilmiştir.
Bu analizler, Genetik Algoritma yaklaşımının
problem için etkili ve uygun bir çözüm sunduğunu göstermektedir.

---

## 4. Çalıştırma ve Kurulum

Proje tek bir Google Colab (.ipynb) dosyasından oluşmaktadır.

### Gerekli Kütüphaneler
- numpy
- random
- matplotlib

Notebook dosyası,
Google Colab ortamında
hücreler sırasıyla çalıştırılarak kullanılabilir.

---

## 5. Proje Bilgileri

- Ders: BLG-307 Yapay Zeka Sistemleri  
- Konu: Genetik Algoritma ile Öğrenci Etüt Programı Optimizasyonu  
- Geliştirici: Gökçe Umay Samur
