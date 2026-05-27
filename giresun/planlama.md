# Giresun İl Özel İdaresi Kent Bilgi Sistemi - Proje Planlama Dokümanı

Bu doküman, "Web Tabanlı Kent Bilgi Sistemi Kurulumu" (İKN: 2026/829981) projesinin `ozet.md` dosyasında yer alan 11 ana modül ve teknik/idari gereksinimler temel alınarak hazırlanmış **90 günlük (3 Aylık)** adım adım proje iş planıdır.

Projede **alt yüklenici kullanılmayacağı** için tüm planlama firma içi kaynaklara göre yapılmıştır.

---

## AŞAMA 1: Proje Başlangıcı ve Altyapı Hazırlıkları (Gün 1 - 10)

**Hedef:** Sistemin temel omurgasının kurulması ve veri transferlerinin tamamlanması.
* **Sözleşme ve Yer Teslimi:** İdare ile resmi sürecin tamamlanması.
* **Veri Analizi ve Veri Göçü (Data Migration):** İdare'nin mevcut verilerinin (SQLite, CAD vb.) incelenmesi, temizlenmesi ve yeni nesil **PostgreSQL / PostGIS** mimarisine kayıpsız aktarılması.
* **Sunucu ve CBS Altyapısı:** İdare sunucularına temel Linux/Windows Server yapılandırmalarının yapılması. Açık kaynak kodlu **GeoServer** kurulumu (OGC API, Vector Tile destekli).
* **Yazılım Mimarisi Kurulumu:** `.NET Core` (Backend) ve `ReactJS` (Frontend) proje repolarının oluşturulması, temel paketlerin kurulması.

---

## AŞAMA 2: Çekirdek Sistemler ve Ortak Bileşenler (Gün 11 - 25)

**Hedef:** Güvenlik, kullanıcı yönetimi ve projenin kalbi olan harita portalının ayağa kaldırılması.
* **Kimlik Doğrulama ve Güvenlik:** Rol bazlı (Role-Based) JWT token yetkilendirme sisteminin yazılması. Veritabanında **SHA256** şifreleme mantığının oturtulması. Hatalı giriş blokajı ve detaylı loglama mekanizmasının kurulması.
* **Web CBS Portalı (Merkezi Harita):** 
    * OpenStreetMap (OSM) vb. harita altlıklarının entegrasyonu.
    * WMS, WFS, Vector Tile ve OGC API destekli katman okuma/yazma servislerinin yazılması.
    * 2B/3B geçişleri, çizim araçları (özel vektör çizim/paylaşım) ve konumsal yorum (çözüldü/marker) özelliklerinin geliştirilmesi.
* **Dış Entegrasyonların Temeli:** MEGSİS/TAKBİS ve MAKS için kurum servislerine bağlantı testlerinin yapılıp altyapılarının çekilmesi.

---

## AŞAMA 3: Ana Modüllerin Geliştirilmesi - Bölüm 1 (Gün 26 - 50)

**Hedef:** Vatandaşla ve resmi evraklarla en çok temas eden imar, ruhsat ve başvuru kollarının geliştirilmesi.
* **E-Başvuru (Vatandaş ve Müellif Portalı):** ReCaptcha doğrulamalı giriş ekranları, başvuru ekranı (taslak belge yükleme, KML/GeoJSON import) ve SMS/E-Posta bildirim entegrasyonlarının yapılması.
* **E-İmar Modülü:** MPYY uygunluğunda planların işlenmesi, dinamik İmar ve Köy Yerleşik Alan Durum Raporlarının otomatik üretimi.
* **E-Ruhsat Modülü:** İş akışı (workflow) tanımları, dinamik ücret cetveli hesaplaması. Evrak ve onay mekanizmalarının entegrasyonu. Gelir servisi ödeme entegrasyonu.
* **Kırsal Alan Belge Üretim Modülü:** E-Ruhsat ile bütünleşik çalışan, şablonlara uygun yapı inşaat izni belgelerinin otomatik üretimi ve CBS entegrasyonu.
* **E-İmza Entegrasyonu:** Sunucu taraflı CAdES, XAdES, PAdES, ES-T, LTV destekli E-İmza servisinin E-Ruhsat ve başvuru ekranlarına entegre edilmesi.

---

## AŞAMA 4: Ana Modüllerin Geliştirilmesi - Bölüm 2 (Gün 51 - 70)

**Hedef:** Kurum içi idari yönetimi sağlayan araçların, envanterlerin, yapay zeka entegrasyonlarının ve KUDEB süreçlerinin tamamlanması.
* **E-Arşiv Modülü:** Standart dosya planına uygun kayıt ekranları, evrak revizyon takibi. Bilgisayar çıktıları için **Otomatik OCR** entegrasyonu ile metin içi arama özelliğinin aktif edilmesi.
* **E-Taşınmaz Modülü:** Mülkiyet haritasının (Kiralık, satılık vb. renkli lejant) oluşturulması. Taşınmaz Rapor ve İcmal cetvellerinin otomatik üretimi.
* **E-Proje ve E-Kudeb Modülleri:** Yatırım projelerinin ve tescilli kültür varlıklarının CBS üzerinden takibi, onarım izni ve iş akış ekranlarının oluşturulması.
* **Taşıt Görev Emri Yönetimi:** Proxy onaylı (vekalet) araç talepleri, araç kapasite kontrolü ve Araç Takip Sistemi CBS entegrasyonunun (rota takibi) yapılması.
* **Kaçak Yapı Modülü ve Yapay Zeka:** Kaçak yapı ihbar tespit tutanaklarının üretimi. **Yapay zeka (AI) destekli, fotoğraftan otomatik yapı krokisi çıkarma motorunun** geliştirilmesi. Tablet uyumlu saha kroki/ölçü giriş arayüzü kodlanması.
* **MAKS Entegrasyonu Genişletmesi:** Saha ekipleri için tablet/telefon destekli numarataj plakası karekod okutma ve fotoğraf yükleme özelliklerinin tamamlanması.

---

## AŞAMA 5: Test, Güvenlik ve Optimizasyon (Gün 71 - 80)

**Hedef:** Geliştirilen tüm 11 modülün hatasız çalıştığından emin olmak ve performans iyileştirmeleri yapmak.
* **Uçtan Uca (End-to-End) Testler:** Modüllerin birbirleriyle olan ilişkisinin (Örn: Kaçak yapıdaki tutanağın E-Arşive düşmesi) test edilmesi.
* **Sızma (Penetrasyon) Testleri:** İdare sunucularında güvenlik açığı taraması, loglama denetimi.
* **Performans Optimizasyonu:** React frontend tarafında 3B harita geçişlerinin, GeoJSON ve Vector Tile verilerinin hızlı yüklenmesi için rendering iyileştirmeleri.
* **Hata Giderimleri:** Test sürecinde ortaya çıkan bug'ların giderilmesi.

---

## AŞAMA 6: Kurulum, Eğitim ve Canlıya Alma (Gün 81 - 90)

**Hedef:** Sistemin kuruma teslimi, personel eğitimi ve garanti sürecinin başlaması.
* **Son Kurulum ve SSL:** SSL sertifikalarının yapılandırılması, Production (Canlı) ortam ayarlamaları.
* **Kullanıcı ve Yönetici Eğitimleri:** İdarenin belirlediği yerde **5 (Beş) İş Günü** sürecek detaylı sistem kullanım eğitimlerinin verilmesi. (Yüz yüze veya online).
* **Kesin Kabul:** Yedekleme mekanizmalarının aktif edilmesi (Sözleşme gereği %15 ceza yememek için otomatik backup senaryoları) ve İdare onayına sunulması.
* **Proje Kapanışı ve Garanti Başlangıcı:** Projenin canlı kullanıma açılması ve 1 yıllık garanti/bakım dönemine geçilmesi.
