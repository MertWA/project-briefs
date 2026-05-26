# GEREKENLER DÖKÜMANTASYONU (GEREKENLER.md)

Bu döküman, **Giresun İl Özel İdaresi** tarafından gerçekleştirilecek olan **"Web Tabanlı Kent Bilgi Sistemi Kurulumu Projesi Hizmet Alımı"** (İhale Kayıt No: **2026/829981**) ihalesine ait idari, hukuki ve teknik şartnamelerin detaylı olarak incelenmesi sonucu ortaya çıkarılan gereksinimleri içermektedir.

---

## 1. İDARİ VE SÖZLEŞMESEL GEREKSİNİMLER

*   **İhale Kayıt Numarası (İKN):** 2026/829981
*   **İhale Tarihi ve Saati:** 04.06.2026 - 10:00
*   **İşin Süresi:** İşe başlama tarihinden (sözleşme imzasından itibaren 10 gün içinde yer teslimi yapılır) itibaren **90 (Doksan) takvim günü**.
*   **İşin Yapılacağı Yer:** Giresun İl Özel İdaresi.
*   **Alt Yüklenici Durumu:** Bu ihalede **alt yüklenici çalıştırılması yasaktır**. Tüm iş yüklenici tarafından bizzat yapılacaktır.
*   **Avans Durumu:** Yükleniciye herhangi bir **avans ödemesi yapılmayacaktır**.
*   **Fiyat Farkı:** Sözleşme süresince **fiyat farkı hesaplanmayacaktır**.
*   **Garanti Süresi:** Kesin kabul onayından itibaren **1 (Bir) yıl** garanti ve bakım süresi vardır. Garanti bitiminde yıllık bakım bedeli ihale bedelinin %10'unu geçemez.
*   **Ceza Maddesi (Kritik):** Güncelleme/kurulum öncesi İdare'nin yedek alması beklenecektir. Yedekleme yapılmadan gerçekleştirilecek kurulum/güncelleme sırasında oluşacak veri kayıpları durumunda yükleniciye **sözleşme bedelinin %15'i tutarında ceza** kesilir. Gecikme cezası günlük binde 3'tür. Toplam ceza limiti sözleşme bedelinin %30'udur.

---

## 2. TEKNOLOJİ YIĞINI (TECH STACK) GEREKSİNİMLERİ

İdari ve Teknik Şartnamede tanımlanan ve mevcut uygulama yapısıyla uyumlu teknoloji gereksinimleri:

*   **Arka Uç (Back-End):**
    *   `.NET Core` (C#) nesne yönelimli (OOP) mimari.
    *   `Entity Framework Core` ORM aracı.
    *   `RESTful API` mimarisi.
    *   *Mevcut Durum Analizi:* Proje .NET 10.0 ile geliştirilmektedir ve bu standartları tam olarak karşılamaktadır.
*   **Ön Yüz (Front-End):**
    *   `ReactJS` tabanlı kullanıcı arayüzü.
    *   `HTML5` ve `CSS3` standartları.
    *   Mobil, tablet ve PC platformlarına uygun, çözünürlüğe duyarlı (`Responsive`) tasarım.
    *   Chrome, Firefox, Safari ve Internet Explorer 10+ tarayıcılarında sorunsuz çalışma.
    *   *Mevcut Durum Analizi:* Proje React 19 ve TypeScript kullanılarak geliştirilmektedir, şartnameye tam uyumludur.
*   **Veri Tabanı (Veri Depolama):**
    *   `PostgreSQL / PostGIS` ilişkisel ve konumsal veritabanı (Şartname Madde 5.5.14).
    *   Güvenlik parametreleri için şifre, gizli soru/cevap gibi verilerin **SHA256** algoritması ile şifrelenerek saklanması.
    *   *Mevcut Durum Analizi:* Mevcut projede kullanılan SQLite (`mekanik_leaflet.db`) veritabanının PostgreSQL/PostGIS yapısına dönüştürülmesi gerekmektedir.
*   **Coğrafi Bilgi Sistemi (CBS) Sunucusu & Standartları:**
    *   `OGC (Open Geospatial Consortium)` standartları desteği.
    *   `WMS` (Web Map Service), `WFS` (Web Feature Service), `OGC API Features`, `OGC API Tiles`, `OGC API Styles` servis desteği.
    *   `Vector Tile` (MVT - Mapbox Vector Tile) desteği.
    *   TileMap tabanlı Google Maps, Bing Maps, Mapbox altlık servislerinin entegrasyonu.
    *   Açık kaynak kodlu CBS sunucu yazılımı kurulumu (GeoServer vb.).

---

## 3. MODÜLER VE TEKNİK GEREKSİNİMLER

Sistem, tek bir çatı portal altında birleşecek 10 ana modül/bileşenden oluşacaktır:

### 3.1. Web CBS Portalı (Merkezi Harita ve Katman Yönetimi)
*   Sınırsız sayıda OGC servisi (WMS, WFS, OGC API), Shapefile, KML, GeoJSON katmanı ekleyebilme.
*   Konumsal verileri GeoJSON, KML ve Vector Tile olarak dışa aktarabilme (REST API üzerinden).
*   Yetkilendirmeye tabi API Anahtarı (API Key) üretimi ve süre sınırı koyabilme.
*   Katmanların zoom seviyesi görünürlüğü, şeffaflık, lejant ve dinamik semboloji (kategorik ve ısı haritası) yönetimi.
*   Temel ve Gelişmiş Harita Görüntüleyici olmak üzere iki tip harita arayüzü.
*   Haritada nokta, çizgi, poligon çizimi, ölçüm araçları (alan/mesafe), 2B ve 3B modlar arası sayfa yenilemeden geçiş yapabilme.
*   Harita üzerinde konumsal yorum ekleme (kullanıcı baş harflerinden oluşan marker, cevap yazma, çözüldü olarak işaretleme).
*   Gündüz/Gece modu, PDF/PNG formatında harita çıktısı alma, XLSX/PDF/GeoJSON/KML veri dışa aktarımı.

### 3.2. E-İmar (İmar Uygulamaları Veri Yönetimi)
*   İmar planlarının coğrafi veritabanında **MPYY** (Mekânsal Planlar Yapım Yönetmeliği) veri kataloğuna uygun olarak tutulması.
*   Plan sınırları, meclis kararları, plan notları ve raster paftaların ilişkilendirilerek gösterilmesi.
*   Seçilen parsele ilişkin plan fonksiyonu ve yapılaşma koşullarının (TAKS, KAKS, Yükseklik, Bahçe Mesafeleri vb.) dinamik sorgulanması.
*   Resmi geçerliliği olmayan bilgi amaçlı **"İmar Durum Raporu"** üretilmesi.
*   **Köy Yerleşik Alan Sorgusu** ve parselin konumuna göre (içinde, kısmen içinde, dışında) **"Köy Yerleşik Alan Durum Raporu"** üretilmesi.
*   **Sit Alanı** ve **Afete Maruz Alan** sorgulamalarının coğrafi veri katmanları üzerinden otomatik yapılması.
*   E-Başvuru modülü ile gelen imar başvurularının takibi, evrak onay/ret/iade süreçleri, taslak plan sınırlarının (KML/GeoJSON) veritabanına işlenmesi.

### 3.3. E-Ruhsat (Ruhsat Süreçleri Yönetimi)
*   Yapı Ruhsatı, Yapı Kullanım İzni (İskan), İzinsiz İnşaat, İşyeri Ruhsatı, Uygun Görüş ve İnşaat İzni süreçlerinin uçtan uca takibi.
*   Dinamik iş akışı (workflow) tanımlama ve durum güncellemelerinin anlık olarak CBS veritabanına işlenmesi.
*   Ruhsat verilerinin ilgili parsel geometrisi ile harita üzerinde ilişkilendirilmesi.
*   Süreç tiplerine göre dinamik evrak listesi tanımlama (hangi evrakın müellif, hangisinin kurum personeli tarafından e-imzalanacağı tanımı).
*   Ücretlerin hizmet türüne göre dinamik ücret cetvelleri üzerinden otomatik hesaplanması.
*   Gelir Servisi ödeme onayı entegrasyonu (ödeme onaylanmadan ruhsat personelinin inceleme yetkisi kısıtlanır).
*   İlişkili E-Arşiv modülü ile tüm ruhsat evraklarının arşivlenmesi.

### 3.4. E-Başvuru (Vatandaş ve Müellif Portalı)
*   Vatandaş, proje müellifi ve yapı denetim firmaları için üyelik ve giriş arayüzü.
*   Gerçek kişi (T.C. Kimlik No) ve Tüzel kişi (Vergi No) kayıt tipleri, **Google ReCaptcha** doğrulaması ve İdare onayı sonrasında hesap aktivasyonu.
*   Kullanıcı dashboard ekranı (aktif, onaylanan, reddedilen başvuru istatistikleri ve son 5 başvuru listesi).
*   Harita üzerinden parsel seçerek ruhsat veya imar başvurusu oluşturma.
*   Başvuru taslak aşamasındayken evrak yükleme/silme; İdare'ye gönderildikten sonra silme butonunun pasifleştirilmesi.
*   İmar plan başvurularında plan sınırının **KML/GeoJSON** formatında yüklenmesi.
*   Başvuru süreçlerinin durum değişikliklerinde SMS, E-posta ve uygulama içi bildirim ile bilgilendirme.
*   Ödeme dekontunun sisteme yüklenmesi ve e-imza entegrasyonu.

### 3.5. E-Arşiv (Dijital Arşiv ve Belge Yönetimi)
*   Bakanlık **Standart Dosya Planı**na uygun evrak kaydı.
*   Fiziksel arşiv lokasyonları (oda, raf, klasör) ile dijital arşiv nesneleri arasında ilişki kurulması.
*   Evrakların ilgili coğrafi geometrilerle (parsel, sit sınırı, bina, kültür varlığı) harita üzerinden ilişkilendirilmesi.
*   **Otomatik OCR Desteği:** Yüklenen PDF, JPEG, TIFF formatındaki belgelerin otomatik OCR işleminden geçirilmesi ve belge içi metin araması (Full-Text Search) yapılması.
*   Evrak revizyon (versiyon) geçmişinin tutulması ve eski sürümlere erişim.
*   **Birim yetkilendirmesi:** Sadece yetkili birim personellerinin kendi evraklarını görmesi.
*   E-imza ile evrak imzalama ve doğrulama süreçleri.

### 3.6. E-Taşınmaz (Taşınmaz Envanter ve Süreç Yönetimi)
*   İdareye ait arsa ve binaların sözel ve konumsal envanter yönetimi.
*   Satış, kiralama, trampa (takas), ipotek, kamulaştırma, tahsis, bağış ve devir süreçlerinin takibi.
*   Kıymet takdir komisyonu değer girişleri ve takibi.
*   Kiralık, satılık, ipotekli mülkler ve fuzuli işgaliye alanlarının harita üzerinde farklı renklerle gösterilmesi ve takibi.
*   "Kamu İdarelerine Ait Taşınmazların Kaydına İlişkin Yönetmelik" çerçevesinde **Taşınmaz Rapor ve İcmal Cetvellerinin** otomatik üretimi.
*   Entegre E-Arşiv modülü ile taşınmaza ait tapu, sözleşme vb. belgelerin saklanması.

### 3.7. E-Proje (Proje Takip ve Yönetim Sistemi)
*   İdare tarafından yürütülen ihaleli veya kurum içi yatırım projelerinin konumsal takibi.
*   Proje künye bilgileri: Mahalle/ilçe, sorumlu birim, iş kalemleri, çalışan personel, ihale ve yüklenici bilgileri, imalat aşamaları.
*   Proje imalat görselleri ve belgelerinin (E-Arşiv entegreli) sisteme yüklenmesi.
*   Dinamik iş adımları ve raporlama modülü.
*   Projelerin 3B harita ekranında konumsal olarak gösterilmesi.

### 3.8. E-Kudeb (Kültür Varlıkları Yönetim Sistemi)
*   Sit alanları ve tescilli kültür varlığı envanterinin (ada/parsel, koruma alan sınırı) CBS ortamında depolanması.
*   Basit bakım onarım izinleri, restorasyon, restitüsyon ve röleve projelerinin onay süreçleri ve takibi.
*   Dinamik KUDEB iş akış tanımları ve onay mekanizmaları.
*   Evrakların E-Arşiv modülü ile ilişkilendirilerek arşivlenmesi ve harita üzerinden erişilmesi.

### 3.9. Taşıt Görev Emri Yönetim Modülü
*   Kağıt ortamındaki taşıt görev emri formlarının dijitalleştirilmesi.
*   Yöneticiler için vekalet (proxy) tanımlı dinamik onay iş akışları (sıralı amir onay zinciri).
*   Talep oluşturulduğunda ve amir onayına düştüğünde ilgili kişilere anlık SMS ve E-posta bildirimi.
*   Destek Hizmetleri Müdürlüğü araç yönetim arayüzü; araç doluluk kapasitesi ile personel sayısı kontrolü (kapasite yetersizse atamayı engelleme).
*   En üst amir onayından sonra taşıt görev emrinin e-imza ile imzalanması.
*   Araç ve şoför envanter yönetimi, görev dönüşünde çıkış/dönüş KM ve saat girişleri.
*   Aylık **Personel İcmal Cetvelleri** ve **İl Dışı Görev Dönüş Raporlarının** otomatik üretilmesi.
*   İdarenin araç takip sistemi ile coğrafi entegrasyon kurularak, gidilen rotanın CBS verisi olarak kaydedilmesi ve haritada gösterilmesi.

### 3.10. Kaçak Yapı Modülü
*   E-Ruhsat uygulamasıyla tam entegre yapı.
*   Kaçak yapı ihbarlarının kaydı ve ada/parsel bilgileri ile coğrafi olarak haritada işaretlenmesi.
*   Dinamik kaçak yapı iş süreçlerinin takibi, tespit tutanağı ve resmi yazışma formlarının otomatik üretilmesi.
*   İşlemlerin ilgili diğer kurum birimleriyle CBS üzerinden paylaşılması.

---

## 4. ORTAK BİLEŞENLER VE ENTEGRASYONLAR

### 4.1. E-İmza Entegrasyonu (Kritik Teknik Standartlar)
*   **İmza Formatları:** CAdES (ETSI TS 101 733), XAdES (ETSI TS 101 903) ve PAdES (ETSI TS 102 778).
*   **Paket Standardı:** EYP 2.0 (Open Packaging Conventions - e-yazışma paketi).
*   **Sertifika Standartları:** X.509 v3 sertifikaları, RSA, DSA ve Eliptik Eğri algoritmaları, SHA256 ve SHA512 desteği.
*   **Doğrulama:** Çevrimiçi Sertifika Durum Protokolü (OCSP) ve çevrimdışı yedek olarak Sertifika İptal Listesi (SİL/CRL) cache'leme desteği.
*   **Güvenlik:** Doğrulama ve imzalama işlemlerinin istemci taraflı değil, sunucu taraflı yapılması (Server-Side Validation).
*   **Donanım Desteği:** PKCS#11 uyumlu akıllı kartlar, USB tokenlar ve Mobil İmza desteği. İstemci tarafında akıllı kart sürücüsü yükleme zorunluluğunun olmaması.
*   **LTV Desteği:** Uzun dönem doğrulanabilir (Long Time Validation) imza desteği.

### 4.2. Dış Entegrasyonlar
*   **MEGSİS / TAKBİS (TKGM):** Kadastro parsel geometrileri ve mülkiyet bilgilerinin günlük entegrasyonu.
*   **MAKS (Mekânsal Adres Kayıt Sistemi):** Adres, bina, numarataj ve bağımsız bölüm verilerinin senkronizasyonu.
*   *Numarataj Uygulaması:* Kapı numarasındaki karekodun (QR Code) saha personeli tarafından okunarak konumsal bilgilere erişilmesi ve saha fotoğraflarının sisteme yüklenmesi.
*   **SMS & E-Posta Entegrasyonları:** Durum bildirimleri ve şifre işlemleri için.

### 4.3. Güvenlik, Rol ve Log Yönetimi
*   Rol bazlı ve JWT token tabanlı kimlik doğrulama.
*   Sistem girişinde Captcha koruması, hatalı giriş limiti aşımında kullanıcı kilitleme (admin tarafından tekrar aktif etme).
*   Veritabanında şifre ve kritik bilgilerin **SHA256** ile şifrelenmesi.
*   **Detaylı Loglama:** Yapılan tüm işlemlerin (IP adresi, kullanıcı adı, işlem zamanı, işlem türü ve çalıştırılan veritabanı sorguları) loglanması ve yetkisiz erişim teşebbüslerinin kayıt altına alınması.

---

## 5. DİĞER HİZMETLER

*   **Veri Çalışmaları (Veri Göçü):** İdarenin mevcut verilerinin incelenmesi, temizlenmesi ve yeni oluşturulacak PostgreSQL/PostGIS veritabanı yapısına taşınması.
*   **Eğitim:** İdarenin belirleyeceği yerde veya online ortamda 5 (beş) iş günü (gerektiğinde 10 güne kadar uzatılabilir) detaylı kullanıcı ve yönetici eğitimlerinin verilmesi.
*   **Kurulum:** Sistemlerin İdareye ait sunuculara kurulması, SSL sertifikalarının yüklenmesi ve çalışır durumda teslim edilmesi.
