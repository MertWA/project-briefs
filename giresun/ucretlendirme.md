# Giresun İl Özel İdaresi Kent Bilgi Sistemi - Bütçe ve Ücretlendirme Analizi (Revize)

Bu döküman, **Giresun İl Özel İdaresi** tarafından gerçekleştirilecek olan **"Web Tabanlı Kent Bilgi Sistemi Kurulumu" (İKN: 2026/829981)** projesi özetine dayanılarak güncellenmiş detaylı bütçe ve fiyatlandırma analizidir. Güncellenen 11 modül ve yapay zeka gereksinimleri dikkate alınarak hazırlanmıştır.

İlgili şartname ve teknoloji yığını göz önüne alındığında, projenin **şirket içi kaynaklarla** geliştirileceği ve **ücretsiz (açık kaynak/ücretsiz servis)** alternatiflerin maksimum düzeyde kullanılacağı varsayılarak kalemler yeniden değerlendirilmiştir.

---

## 1. Yazılım, Efor ve İşçilik Maliyetleri

❌ **Yazılım Geliştirme İşçiliği (Backend, Frontend, CBS)**
* **Analiz:** 11 modülün tamamı (Yapay Zeka kroki oluşturma, E-Ruhsat, vb.) yazılım geliştirme süreçleri (mimari, kodlama, test) doğrudan firma kendi bünyesindeki ekip tarafından gerçekleştirilecektir. Dışarıdan yazılım hizmet alımı yapılmayacağı için bu kaleme dış bütçe ayrılmasına gerek yoktur.
* **Bütçe:** **0 ₺** *(Firma içi efor).*

❌ **Alt Yüklenici Giderleri**
* **Analiz:** Şartnamede *"alt yüklenici çalıştırılması yasaktır"* ibaresi kesin olarak yer almaktadır.
* **Bütçe:** **0 ₺**

❌ **Yazılım Altyapı Lisansları (Veritabanı, Sunucu Yazılımları vb.)**
* **Analiz:** Projede açık kaynak kodlu teknolojiler (PostgreSQL/PostGIS, GeoServer, .NET, React) tercih edilmiştir. Temel lisanslama bütçesine gerek yoktur.
* **Bütçe:** **0 ₺**

---

## 2. API ve Entegrasyon Maliyetleri

❌ / ✅ **Yapay Zeka (AI) Fotoğraftan Kroki Çıkarma Motoru (Kaçak Yapı Modülü)**
* **Ücretsiz Alternatif [❌]:** Açık kaynaklı (OpenCV, YOLO, veya HuggingFace) görüntü işleme/segmentasyon modelleri kullanılarak sınır ve köşe tespiti yapılıp krokiye dönüştürülebilir. Kendi sunucumuzda barındırılır. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** İdare daha detaylı, gelişmiş ve sıfır hatalı bir AI talep ederse (örneğin OpenAI Vision API veya Google Cloud Vision API üzerinden mimari analiz) çağrı başına maliyet çıkacaktır. Bu durumda proje süresince aylık/yıllık tahmini **5.000 ₺ - 20.000 ₺** arası bir API kullanım maliyeti doğabilir. Ancak ihale şartlarında spesifik bir servis istenmediği için açık kaynak modellerle ilerlenmesi tavsiye edilir.

❌ / ✅ **Harita Altlık Servisleri (TileMap API)**
* **Ücretsiz Alternatif [❌]:** Açık kaynaklı **OpenStreetMap (OSM)** verileri standart altlık olarak kullanılabilir veya idarenin sunucusuna ücretsiz kurulabilir. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** Eğer idare çok yüksek çözünürlüklü detaylı uydu görüntüsü isterse Google Maps veya Mapbox altyapısına geçilebilir. Tahmini aylık **1.500 ₺ – 5.000 ₺**.

❌ / ✅ **E-Arşiv OCR (Optik Karakter Tanıma) API'si**
* **Ücretsiz Alternatif [❌]:** Açık kaynaklı **Tesseract OCR (v5)** motoru idarenin sunucusuna entegre edilebilir. Standart bilgisayar çıktıları için fazlasıyla yeterli olacaktır. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** El yazısı veya çok deforme olmuş evraklar için Google Cloud Vision API düşünülebilir (Yıllık tahmini **10.000 ₺ – 40.000 ₺**). Başlangıç için Tesseract en mantıklısıdır.

✅ **E-İmza Entegrasyon Kütüphanesi**
* **Analiz:** CAdES/XAdES/PAdES standartları, LTV ve SİL/CRL cache'leme gibi çok katı ve hukuki bağlayıcılığı olan maddeler bulunmaktadır. Sıfırdan TÜBİTAK Kamu SM testlerinden geçmek aylar süreceğinden, hazır bir E-İmza Entegratör kütüphanesi (API) satın almak şarttır.
* **Bütçe:** Proje bazlı veya yıllık lisans olarak **30.000 ₺ – 75.000 ₺** bütçe ayrılmalıdır.

❌ / ✅ **SMS ve E-Posta (SMTP) Gönderim Servisleri**
* **Ücretsiz Alternatif (E-Posta) [❌]:** İdarenin mevcut kurumsal mail sunucusu (Exchange/SMTP) entegre edilebilir. Bütçe: **0 ₺**.
* **Ücretli Alternatif (SMS) [✅]:** E-başvuru ve taşıt görev onayları için SMS gitmesi şarttır. (Örn: 100.000 SMS için **8.000 ₺ – 15.000 ₺** bütçe).

---

## 3. Altyapı, Operasyon ve Diğer Hizmet Maliyetleri

❌ **Sunucu ve Donanım Maliyeti**
* **Analiz:** Sistem "İdareye ait sunuculara" kurulacağı için donanım/hosting masrafı yoktur.
* **Bütçe:** **0 ₺**

❌ / ✅ **SSL Sertifikası**
* **Ücretsiz Alternatif [❌]:** **Let's Encrypt** kullanılarak ücretsiz SSL sertifikası kurulabilir. Bütçe: **0 ₺**.
* **Ücretli Alternatif (Yetersiz Kalınırsa) [✅]:** Wildcard veya ticari SSL talep edilirse yıllık tahmini **3.000 ₺ – 12.000 ₺** bütçe ayrılmalıdır.

❌ **Veri Göçü (Data Migration) Operasyonu**
* **Analiz:** İdare'nin mevcut verilerinin PostgreSQL'e taşınması işlemi yazılım ekibi (firma içi efor) tarafından yapılacaktır.
* **Bütçe:** **0 ₺** *(Firma içi efor).*

✅ **Kullanıcı ve Yönetici Eğitimleri (Seyahat Giderleri)**
* **Analiz:** Şartnamedeki 5-10 günlük eğitim yüz yüze ve Giresun'da istenirse; eğitimi verecek şirket personelinizin yol, konaklama ve iaşe masrafları olacaktır.
* **Bütçe:** Uçak/otobüs, otel ve yemek masrafları için tahmini: **30.000 ₺ – 70.000 ₺** nakit çıkışı gereklidir. *(Eğer İdare online eğitimi kabul ederse bu masraf da 0 ₺ olur).*
