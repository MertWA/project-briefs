# Giresun İl Özel İdaresi Kent Bilgi Sistemi - Bütçe ve Ücretlendirme Analizi (Revize)

Bu döküman, **Giresun İl Özel İdaresi** tarafından gerçekleştirilecek olan **"Web Tabanlı Kent Bilgi Sistemi Kurulumu" (İKN: 2026/829981)** projesi özetine dayanılarak güncellenmiş detaylı bütçe ve fiyatlandırma analizidir.

İlgili şartname ve teknoloji yığını göz önüne alındığında, projenin **şirket içi kaynaklarla** geliştirileceği ve **ücretsiz (açık kaynak/ücretsiz servis)** alternatiflerin maksimum düzeyde kullanılacağı varsayılarak kalemler yeniden değerlendirilmiştir.

---

## 1. Yazılım, Efor ve İşçilik Maliyetleri

❌ **Yazılım Geliştirme İşçiliği (Backend, Frontend, CBS)**
* **Analiz:** Yazılım geliştirme süreçleri (mimari, kodlama, test) doğrudan firma kendi bünyesindeki ekip tarafından gerçekleştirilecektir. Dışarıdan yazılım hizmet alımı yapılmayacağı için bu kaleme dış bütçe ayrılmasına gerek yoktur.
* **Bütçe:** **0 ₺** *(Firma içi efor).*

❌ **Alt Yüklenici Giderleri**
* **Analiz:** Şartnamede *"alt yüklenici çalıştırılması yasaktır"* ibaresi kesin olarak yer almaktadır.
* **Bütçe:** **0 ₺**

❌ **Yazılım Altyapı Lisansları (Veritabanı, Sunucu Yazılımları vb.)**
* **Analiz:** Projede açık kaynak kodlu teknolojiler (PostgreSQL/PostGIS, GeoServer, .NET, React) tercih edilmiştir. Temel lisanslama bütçesine gerek yoktur.
* **Bütçe:** **0 ₺**

---

## 2. API ve Entegrasyon Maliyetleri

❌ / ✅ **Harita Altlık Servisleri (TileMap API)**
* **Ücretsiz Alternatif [❌]:** Açık kaynaklı **OpenStreetMap (OSM)** verileri standart altlık olarak kullanılabilir veya idarenin sunucusuna (TileServer GL vb. ile) ücretsiz kurulabilir. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** Eğer idare ileride çok yüksek çözünürlüklü detaylı uydu görüntüsü isterse veya sunucu trafiği OSM ücretsiz sınırlarını zorlarsa, Google Maps veya Mapbox altyapısına geçilebilir. Bu durumda aylık tahmini **1.500 ₺ – 5.000 ₺** kullanım bütçesi doğar.

❌ / ✅ **E-Arşiv OCR (Optik Karakter Tanıma) API'si**
* **Ücretsiz Alternatif [❌]:** Açık kaynaklı **Tesseract OCR (v5)** motoru idarenin sunucusuna entegre edilebilir. Kurumların bilgisayar çıktısı (daktilo, lazer yazıcı vb.) resmi evraklarının metne çevrilmesinde Tesseract'ın Türkçe dil modeli **fazlasıyla yeterli olacaktır**. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** Geçmişten kalan, el yazısı yoğunluklu, çok silik, kahve dökülmüş veya yırtık deforme olmuş evraklarda Tesseract'ın hata payı artabilir. Eğer bu tarz "kalitesiz" arşiv çok büyükse, alternatif olarak Google Cloud Vision API düşünülebilir (Yıllık tahmini **10.000 ₺ – 40.000 ₺**). Ancak başlangıç için Tesseract ile ilerlemek en mantıklısıdır.

✅ **E-İmza Entegrasyon Kütüphanesi**
* **Analiz:** Şartnamede "Sunucu taraflı imzalama, CAdES/XAdES/PAdES standartları, LTV ve OCSP/SİL doğrulama" gibi çok katı ve hukuki bağlayıcılığı olan maddeler bulunmaktadır. Açık kaynak kütüphaneler (Örn. BouncyCastle) ile bunları sıfırdan yazmak aylar sürer ve TÜBİTAK Kamu SM testlerinden geçmesi çok zordur. Zaman ve efor kaybı yaşamamak adına hazır bir E-İmza Entegratör kütüphanesi (API) satın almak şarttır.
* **Bütçe:** Proje bazlı veya yıllık lisans olarak **30.000 ₺ – 75.000 ₺** bütçe ayrılmalıdır.

❌ / ✅ **SMS ve E-Posta (SMTP) Gönderim Servisleri**
* **Ücretsiz Alternatif (E-Posta) [❌]:** İdarenin halihazırda var olan kurumsal mail sunucusu (Exchange/SMTP) entegre edilebilir. Bütçe: **0 ₺**.
* **Ücretli Alternatif (SMS) [✅]:** E-başvuru ve taşıt görev onayları için SMS gitmesi şarttır. İdarenin mevcut bir SMS havuzu yoksa, NetGSM, MutluCell gibi operatörlerden toplu SMS paketi alınmalıdır. (Örn: 100.000 SMS için **8.000 ₺ – 15.000 ₺** bütçe).

---

## 3. Altyapı, Operasyon ve Diğer Hizmet Maliyetleri

❌ **Sunucu ve Donanım Maliyeti**
* **Analiz:** Sistem "İdareye ait sunuculara" kurulacağı için donanım/hosting masrafı yoktur.
* **Bütçe:** **0 ₺**

❌ / ✅ **SSL Sertifikası**
* **Ücretsiz Alternatif [❌]:** **Let's Encrypt** kullanılarak ücretsiz ve güvenli (3 ayda bir otomatik yenilenen) SSL sertifikası kurulabilir. Kamu kurumlarında yaygınca kullanılır. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** İdare özellikle "Kurumsal Doğrulamalı (OV)" veya Wildcard ticari SSL talep ederse yıllık tahmini **3.000 ₺ – 12.000 ₺** bütçe ayrılmalıdır.

❌ **Veri Göçü (Data Migration) Operasyonu**
* **Analiz:** Mevcut `mekanik_leaflet.db` (SQLite) veritabanının PostgreSQL'e taşınması işlemi yazılım ekibi (kendi içinizdeki DBA veya Developer) tarafından yapılacaktır.
* **Bütçe:** **0 ₺** *(Firma içi efor).*

✅ **Kullanıcı ve Yönetici Eğitimleri (Seyahat Giderleri)**
* **Analiz:** Şartnamedeki 5-10 günlük eğitim yüz yüze ve Giresun'da istenirse; eğitimi verecek şirket personelinizin yol, konaklama ve günlük iaşe (harcırah) masrafları olacaktır.
* **Bütçe:** Uçak/otobüs, otel ve yemek masrafları için tahmini: **30.000 ₺ – 70.000 ₺** nakit çıkışı gereklidir. *(Eğer İdare online eğitimi kabul ederse bu masraf da 0 ₺ olur).*
