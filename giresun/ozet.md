# GEREKENLER DÖKÜMANTASYONU (GEREKENLER.md)

Bu döküman, **Giresun İl Özel İdaresi** tarafından gerçekleştirilecek olan **"Web Tabanlı Kent Bilgi Sistemi Kurulumu Projesi Hizmet Alımı"** (İhale Kayıt No: **2026/829981**) ihalesine ait idari, hukuki ve teknik şartnamelerin detaylı olarak incelenmesi sonucu ortaya çıkarılan tüm gereksinimleri eksiksiz olarak içermektedir.

---

## 1. İDARİ VE SÖZLEŞMESEL GEREKSİNİMLER

*   **İhale Kayıt Numarası (İKN):** 2026/829981
*   **İşin Süresi:** Sözleşme imzasından itibaren yer teslimini takiben **90 (Doksan) takvim günü**.
*   **İşin Yapılacağı Yer:** Giresun İl Özel İdaresi.
*   **Alt Yüklenici Durumu:** Alt yüklenici çalıştırılması yasaktır.
*   **Avans ve Fiyat Farkı:** Avans ödemesi yapılmayacak, fiyat farkı hesaplanmayacaktır.
*   **Garanti Süresi:** Kesin kabulden itibaren **1 (Bir) yıl**. Garanti bitiminde yıllık bakım bedeli ihale bedelinin %10'unu geçemez.
*   **Ceza Maddesi (Kritik):** İdare'nin yedek alması beklenmeden yapılacak kurulum/güncelleme sırasındaki veri kayıplarında **%15 ceza** kesilir. Gecikme cezası günlük binde 3, maksimum %30'dur.

---

## 2. TEKNOLOJİ YIĞINI (TECH STACK) GEREKSİNİMLERİ

*   **Arka Uç (Back-End):** `.NET Core` (C#), Entity Framework Core, RESTful API.
*   **Ön Yüz (Front-End):** `ReactJS`, TypeScript, HTML5, CSS3, Responsive Tasarım (Chrome, Firefox, Safari, IE10+).
*   **Veri Tabanı:** `PostgreSQL / PostGIS` (İlişkisel ve Konumsal). Veriler SHA256 ile şifrelenecek.
*   **CBS Sunucusu:** OGC API (Features, Tiles, Styles, Commons), WMS, WFS, Vector Tile (MVT) destekli açık kaynaklı CBS sunucu kurulumu.
*   **Altlık Haritalar:** Google Maps, Bing Maps, Mapbox tile map desteği.

---

## 3. MODÜLER VE TEKNİK GEREKSİNİMLER

Sistem, tek bir çatı portal (Web CBS Portalı) altında birleşecek 11 ana modül/bileşenden oluşacaktır:

### 3.1. Web CBS Portalı (Merkezi Harita ve Katman Yönetimi)
*   Sınırsız OGC servisi, Shapefile, KML, GeoJSON, Vector Tile ekleyebilme. REST API üzerinden GeoJSON, KML, Vector Tile veri yayını.
*   API Key üretimi ve süre kısıtlaması, harita temaları belirleme özelliği.
*   Katmanların şeffaflık, görünürlük, lejant, dinamik semboloji (kategorik/ısı haritası) ayarları.
*   Temel ve Gelişmiş Harita Görüntüleyici olmak üzere iki farklı arayüz. 2B ve 3B harita gösterimi arası sayfa yenilemeden geçiş, döndürme ve yatıklık ayarı.
*   Haritada alan/mesafe ölçümü, nokta/çizgi/poligon çizimi. Kullanıcının kendine özel vektör çizim yapması, kaydetmesi ve paylaşması.
*   Konumsal yorum ekleme (marker ile), cevap yazma, "çözüldü" işaretleme. Gündüz/Gece modu. PDF/PNG çıktı ve XLSX/PDF/GeoJSON/KML liste dışa aktarımı.

### 3.2. E-İmar (İmar Uygulamaları Veri Yönetimi)
*   İmar planlarının MPYY (Mekânsal Planlar Yapım Yönetmeliği) katalog standartlarına uygun CBS depolanması.
*   Plan sınırları, meclis kararları, plan notları, raster paftaların ilişkilendirilmesi.
*   Seçilen parsele ilişkin "İmar Durum Raporu" ile "Köy Yerleşik Alan Durum Raporu" (içinde/kısmen/dışında) üretimi.
*   Sit Alanı ve Afete Maruz Alan coğrafi otomatik sorgulamaları.
*   E-Başvuru ile tam entegre imar talep takibi, taslak plan (KML/GeoJSON) girişi.

### 3.3. E-Ruhsat (Ruhsat Süreçleri Yönetimi)
*   Yapı Ruhsatı, Yapı Kullanım İzni, İzinsiz İnşaat, İşyeri Ruhsatı, Uygun Görüş ve İnşaat İzni süreçlerinin uçtan uca, dinamik iş akışlarıyla takibi.
*   Parsel geometrisi ile ruhsat kayıtlarının ve evraklarının coğrafi ilişkilendirilmesi.
*   Hizmet türüne ve yapı tipine göre dinamik evrak listesi ve ücret hesabı tanımlaması.
*   Gelir Servisi ödeme onayı entegrasyonu (onay olmadan dosya incelenemez). E-İmza ile evrak onayı.

### 3.4. E-Başvuru (Vatandaş ve Müellif Portalı)
*   Vatandaş, müellif ve yapı denetim firmaları için üyelik (Gerçek/Tüzel), Google ReCaptcha ve kurum onayı ile aktivasyon.
*   Kullanıcı dashboard ekranı (istatistikler, son 5 başvuru, bildirimler).
*   Haritadan parsel seçerek başvuruların oluşturulması. Taslak kaydetme, evrak ekleme/silme (kuruma gidince silme iptal).
*   Başvuru süreçlerinde SMS, E-Posta ve uygulama içi bilgilendirmeler. Ödeme dekontu yükleme.

### 3.5. E-Arşiv (Dijital Arşiv ve Belge Yönetimi)
*   Bakanlık Standart Dosya Planına uygun, fiziksel/dijital arşiv (oda/raf/klasör) ilişkilendirilmesi.
*   Sisteme eklenen PDF, JPEG, TIFF belgeleri için **Otomatik OCR** işlemi ve evrak içi metin (Full-Text) araması.
*   Evrakların coğrafi nesnelerle (parsel, bina, sit alanı vb.) ilişkilendirilmesi, harita üzerinden evrağa ulaşılması.
*   Evrak revizyon geçmişinin tutulması, eski sürümlerin incelenebilmesi. Birimlerin sadece kendi evraklarını görebilmesi.

### 3.6. E-Taşınmaz (Taşınmaz Envanter ve Süreç Yönetimi)
*   Arsa ve bina envanterleri, satış, kiralama, trampa, ipotek, kamulaştırma, tahsis, bağış ve devir süreç takibi.
*   Kıymet takdir komisyonu değer girişleri. Kiralık, satılık vb. mülklerin haritada farklı renklerle takibi.
*   Mevzuata uygun "Taşınmaz Rapor ve İcmal Cetvellerinin" otomatik üretimi.
*   Sözleşme vb. belgelerin e-arşiv entegrasyonu ile coğrafi ilişkilendirilmesi.

### 3.7. E-Proje (Proje Takip ve Yönetim Sistemi)
*   İhaleli veya kurum içi yatırım projelerinin harita tabanlı takibi.
*   Proje künyesi (sorumlu birim, iş kalemleri, yüklenici, personel), imalat bilgisi ve görsellerinin eklenmesi.
*   Dinamik iş süreçleri ve raporlama, 3B harita gösterimi.

### 3.8. E-Kudeb (Kültür Varlıkları Yönetim Sistemi)
*   Sit alanları ve tescilli kültür varlıklarının CBS ortamında konumsal envanteri.
*   Basit bakım, onarım, röleve, restitüsyon ve restorasyon projelerinin iş akışı onayı ve E-Arşiv depolanması.

### 3.9. Taşıt Görev Emri Yönetim Modülü
*   Dijital taşıt görev emri onayı (Sıralı dinamik amir onay zinciri, proxy/vekalet desteği).
*   Araç kapasite kontrolü (personel sayısı yetersiz araca atamayı engelleme). En üst amirin e-imza onayı.
*   Şoför, araç envanterleri, çıkış-dönüş km/saat takibi. Personel İcmal Cetvelleri ve İl Dışı Görev Dönüş Raporu üretimi.
*   SMS ve e-posta bildirimleri. Araç takip sistemi coğrafi entegrasyonu (rotanın haritada gösterimi).

### 3.10. Kaçak Yapı Modülü
*   Kaçak yapı ihbarlarının ve ada/parsel bilgilerinin haritada takibi, tespit tutanağı/resmi yazıların otomatik üretimi.
*   **Yapay Zeka Destekli Kroki:** Yapı tatil zabıt tutanağı için idare personelinin çektiği yapı fotoğrafından **yapay zeka** entegrasyonuyla otomatik **yapı krokisi** çıkarılması.
*   Tablet ortamında kroki çizim araçları, ölçü yazma ve açıklama girilmesi özellikleri.
*   Yıkım ve cezai işlemlerin tarihleriyle takibi. E-Ruhsat ile tam entegrasyon.

### 3.11. Kırsal Alan Yapı Kullanım İzin ve Yapı İnşaat İzin Belgeleri Üretim Modülü
*   E-Ruhsat uygulaması içerisinde bütünleşik bir yapı.
*   İdare şablonlarına uygun yapı inşaat izni ve fen sağlık kurallarına uygunluk belgelerinin otomatik üretimi.
*   Üretilen belgelerin e-imza ile imzalanıp E-Başvuru üzerinden vatandaşa elektronik ortamda teslimi.
*   Ada/parsel konumsal ilişkilendirmesi ve otomatik E-Arşiv entegrasyonu.

---

## 4. ORTAK BİLEŞENLER VE ENTEGRASYONLAR

### 4.1. E-İmza Entegrasyonu (Kritik Standardlar)
*   CAdES, XAdES, PAdES imza formatları ve EYP 2.0 paket standardı.
*   ES-T (Zaman damgalı), LTV (Uzun dönemli doğrulama), ES-BES, ES-A imza profilleri.
*   Sertifika iptal listeleri (SİL/CRL) cache desteği ve OCSP doğrulama.
*   Sunucu taraflı doğrulama (Server-Side Validation), PKCS#11 akıllı kart/token desteği, Mobil imza entegrasyonu.

### 4.2. Dış Entegrasyonlar
*   **MAKS (Mekânsal Adres Kayıt Sistemi):** Adres, numarataj verilerinin günlük güncellenmesi. Numarataj plakası tasarımı ve saha ekiplerinin karekod okutarak sisteme erişmesi ve fotoğraf yüklemesi.
*   **MEGSİS/TAKBİS:** Kadastro parsel ve mülkiyet bilgilerinin günlük senkronizasyonu.
*   **SMS & E-Posta:** Şifre yenileme, başvuru durum değişiklik bildirimleri.

### 4.3. Güvenlik, Rol ve Log Yönetimi
*   Rol bazlı ve JWT token tabanlı (REST) yetkilendirme altyapısı.
*   Şifrelerin ve gizli soruların **SHA256** ile şifrelenmesi. Hatalı giriş sınırında hesabın kilitlenmesi.
*   Yapılan tüm veri değişikliklerinin ve giriş teşebbüslerinin loglanması (IP, zaman, kullanıcı, işlem türü).

---

## 5. DİĞER HİZMETLER

*   **Veri Çalışmaları (Veri Göçü):** Mevcut verilerin incelenmesi, temizlenmesi ve yeni PostgreSQL/PostGIS yapısına aktarımı.
*   **Eğitim:** İdarenin uygun göreceği şekilde 5 (gerekirse 10) iş günü detaylı son kullanıcı ve yönetici eğitimleri.
*   **Kurulum:** Sistemlerin İdareye ait sunuculara kurulması, SSL sertifikalarının yüklenmesi ve tüm testlerden geçerek çalışır durumda teslimi.
