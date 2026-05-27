# Teknik Terimler ve Kısaltmalar Sözlüğü

Bu doküman, Giresun İl Özel İdaresi Kent Bilgi Sistemi projesi teknik ve idari şartnamelerinde yer alan yazılım, veritabanı, haritacılık ve altyapı terminolojisini açık ve anlaşılır bir dille izah etmek amacıyla hazırlanmıştır.

Proje dokümanlarının incelenmesi sırasında karşılaşılan sektörel terimlerin ve standartların tanımları aşağıda kategorize edilerek sunulmuştur.

---

## 1. Yazılım ve Kodlama Terimleri

*   **.NET Core (C#):** Sistemlerin arka planında (sunucuda) çalışan mantığın, hesaplamaların ve kuralların yazıldığı, Microsoft tarafından geliştirilmiş çok güçlü bir kodlama dilidir. Arabanın "motoru" gibi düşünebilirsiniz.
*   **Entity Framework Core:** Yazılan kodlar ile veritabanı (bilgilerin tutulduğu yer) arasında tercümanlık yapan köprü sistemdir. Programcının işini kolaylaştırır.
*   **RESTful API:** Farklı yazılımların veya bilgisayarların birbiriyle internet üzerinden standart bir dilde haberleşmesini sağlayan iletişim yapısıdır. (Örneğin e-devletten sabıka kaydı çeken bir sistemin kullandığı köprüdür).
*   **ReactJS:** Web sitesinin ekranını, butonlarını, menülerini kısaca "kullanıcının gördüğü ve tıkladığı her yeri" tasarlamak için kullanılan modern bir ekran teknolojisidir. Arabanın "kaportası ve direksiyonu" gibidir.
*   **TypeScript:** Kullanıcı ekranı yazılırken hata yapılmasını önleyen ve yazılımı daha sağlam hale getiren akıllı bir yazılım dilidir.
*   **HTML5 & CSS3:** Web sitelerinin iskeletini (HTML) ve boyasını/tasarımını (CSS) oluşturan web standartlarıdır. 
*   **Responsive (Duyarlı) Tasarım:** Yapılan sistemin cep telefonu, tablet veya bilgisayar ekranlarında boyutlarının bozulmadan, ekrana tam oturacak şekilde otomatik şekil alabilmesidir.

## 2. Veritabanı (Bilgi Depolama) Terimleri

*   **PostgreSQL:** Dünyanın en güvenilir, ücretsiz ve gelişmiş veri depolama (veritabanı) sistemlerinden biridir. Kişi bilgileri, şifreler, evraklar bu devasa dijital dolapta tutulur.
*   **PostGIS:** PostgreSQL veritabanına özel olarak eklenen bir "harita zekasıdır". Bu sayede veritabanı artık sadece isimleri ve rakamları değil; koordinatları, sınır çizgilerini ve harita poligonlarını da anlayıp depolayabilir hale gelir.
*   **SQLite:** Daha küçük, tek bir dosya içinde çalışan daha basit bir veritabanıdır. İdarenin eski verileri bu yapıda olup, projede modern PostgreSQL'e taşınacaktır.

## 3. Harita ve CBS (Coğrafi Bilgi Sistemi) Terimleri

*   **CBS (Coğrafi Bilgi Sistemi):** Verilerin sadece Excel tablosu gibi listelenmesi yerine, dünya üzerindeki gerçek konumlarıyla (koordinatlarıyla) harita üzerinde gösterildiği ve analiz edildiği akıllı harita sistemleridir.
*   **OGC (Open Geospatial Consortium):** Harita sistemlerinin (Google, Yandex, Apple, Kurumlar) birbiriyle anlaşabilmesi için "dünya çapında haritacılık standartlarını" belirleyen uluslararası bir gruptur. Sistemin OGC uyumlu olması, herkesle konuşabileceği anlamına gelir.
*   **WMS (Web Map Service):** Haritadaki verileri kullanıcının ekranına internet üzerinden **"resim (fotoğraf)"** formatında gönderen standart bir servistir.
*   **WFS (Web Feature Service):** Haritadaki verileri resim olarak değil, üzerine tıklanabilir, tıklanınca bilgileri açılabilir **"çizimler/vektörler"** olarak gönderen servistir.
*   **Vector Tile (Vektör Karo):** Haritayı tek bir dev resim olarak yüklemek yerine, küçük kare parçalara (karolara) bölerek yükleyen, bu sayede çok büyük haritaların bile interneti dondurmadan saniyeler içinde açılmasını sağlayan süper hızlı harita yükleme teknolojisidir.
*   **GeoServer:** Harita verilerini (yollar, binalar, sınırlar) internet üzerinden güvenli bir şekilde dışarıya (vatandaşa veya kurumlara) yayınlamaya yarayan yayıncı programdır.
*   **GeoJSON & KML:** Haritadaki noktaların, çizgilerin ve alanların (örneğin bir parselin) bilgisayarlar arasında transfer edilmesini sağlayan hafif koordinat metin dosyalarıdır. (KML genelde Google Earth için kullanılır).
*   **Shapefile (SHP):** Haritacıların yıllardır kullandığı, coğrafi çizimleri tutan en popüler dosya türüdür.

## 4. Güvenlik ve Kimlik Doğrulama Terimleri

*   **SHA256:** Sistemde kayıtlı şifrelerin (örneğin vatandaşın şifresi) veritabanında apaçık "123456" diye değil, geriye döndürülemez karmaşık bir şifreleme algoritmasıyla anlamsız bir metin dizisine çevrilerek gizlenmesidir.
*   **JWT (JSON Web Token):** Bir kullanıcı sisteme şifresiyle giriş yaptığında eline verilen dijital "giriş bileti"dir. Kişi diğer sayfalarda gezerken şifre sormak yerine bu bileti kontrol edilir.
*   **Rol Bazlı Yetkilendirme:** Sistemdeki kişilere rütbe verilmesidir. (Örn: "Vatandaş" sadece kendi evrakını görür, "Memur" ilçeyi görür, "Müdür" tüm ili görür).
*   **SSL Sertifikası:** Web sitesinin adres çubuğunda görünen kilit sembolüdür. Bilgisayarınız ile kurumun sunucusu arasında gidip gelen bilgilerin (şifrelerin, TC kimliklerin) üçüncü şahıslarca çalınmasını engeller.
*   **Captcha / Google ReCaptcha:** Kullanıcının şifre denemesi yapan kötü niyetli bir "robot/yazılım" olmadığını kanıtlaması için sorulan güvenlik testleridir (örn: trafik lambası seçtirilen ekranlar).

## 5. Elektronik İmza ve Arşiv Terimleri

*   **E-İmza (Elektronik İmza):** Islak imza ile aynı hukuki geçerliliğe sahip, USB bellek veya akıllı kartlarla atılan yasal dijital imza.
*   **CAdES, XAdES, PAdES:** Elektronik imzanın belgeye atılış şekilleridir. PAdES (PDF dosyalarına imza atmak için), XAdES (XML denen veri dosyalarına), CAdES (diğer genel dosyalar için) kullanılır.
*   **LTV (Uzun Dönemli Doğrulama):** Atılan bir e-imzanın, atıldıktan 10 yıl sonra bile (imzayı atan kişinin kartının süresi bitse dahi) hala yasal olarak geçerliliğini ve doğruluğunu kanıtlayabilmesini sağlayan bir imzalama teknolojisidir.
*   **OCSP / SİL (Sertifika İptal Listesi):** İmza atan kişinin e-imzasının o an geçerli olup olmadığını (çalınmış mı, iptal mi edilmiş?) internet üzerinden kontrol eden teyit servisleridir.
*   **OCR (Optik Karakter Tanıma):** Resim çekilerek veya taranarak sisteme yüklenmiş belgelerin (örn: eski bir dilekçenin) içindeki yazıları bilgisayarın "okuyup" onu arama yapılabilir normal bir "metne (yazıya)" dönüştürmesi teknolojisidir. Tesseract, bu işlemi yapan popüler bir OCR motorudur.
*   **AI (Yapay Zeka) Destekli Kroki Çıkarma:** Normal bir bina fotoğrafının yapay zeka tarafından incelenip, kapısının penceresinin köşe sınırlarının tespit edilip mimari bir çizime (krokiye) otomatik dönüştürülmesi işlemidir.

## 6. Dosya ve Belge Formatları

*   **PDF:** Herhangi bir cihazda, telefonda ya da bilgisayarda açıldığında yazı tipi, sayfa düzeni veya boyutu "asla bozulmayan" evrensel belge formatıdır. Resmi yazışmalarda kullanılır.
*   **JPEG / JPG:** Fotoğrafların kalitesinden çok fazla ödün vermeden, boyutlarını (MB) küçülterek internette hızlı açılmalarını sağlayan en yaygın resim/fotoğraf formatıdır.
*   **TIFF:** Özellikle profesyonel arşivcilikte (eski evrakların taranmasında) kullanılan, hiçbir veri veya kalite kaybı yaşatmayan, ancak dosya boyutu çok büyük olan yüksek çözünürlüklü görsel formatıdır.

## 7. Kurumlar Arası Dış Entegrasyonlar (Ulusal Sistemler)

*   **MAKS (Mekânsal Adres Kayıt Sistemi):** İçişleri Bakanlığı tarafından tutulan; Türkiye'deki tüm binaların, sokakların ve dış kapı numaralarının kayıtlı olduğu ulusal veri sistemidir.
*   **TAKBİS:** Tapu ve Kadastro Bilgi Sistemi. Vatandaşların kimin üzerine hangi arsanın, tarlanın tapusu var bilgilerinin tutulduğu devletin ana tapu sistemidir.
*   **MEGSİS:** Mekânsal Gayrimenkul Sistemi. O arsanın tapudaki metrekare sınırlarının (parsellerin) coğrafi olarak çizimlerinin (haritadaki sınırlarının) tutulduğu devlet sistemidir.

---
*Not: Bu dokümandaki açıklamalar, projenin tüm paydaşları tarafından terminolojik birliğin sağlanması ve kavramların net bir biçimde kavranabilmesi amacıyla hazırlanmıştır.*
