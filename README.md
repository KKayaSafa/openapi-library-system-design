# Üniversite Kütüphane Sistemi OpenAPI Spesifikasyonu

Bu proje, Açık Kaynak Kodlu Yazılımlar dersi kapsamında hazırlanmış bir OpenAPI 3.0 spesifikasyonudur. Bir üniversite kütüphanesinin çevrim içi sistemini yönetmek için RESTful API tasarımı içermektedir.

## 🎯 Proje Amacı

Bu API spesifikasyonu ile:
- Kitap koleksiyonu yönetimi
- Öğrenci kayıt sistemi
- Kitap ödünç alma ve iade işlemleri
gerçekleştirilebilir.

## 📋 Özellikler

### 🔧 Teknik Özellikler
- **OpenAPI Sürümü**: 3.0.4
- **Format**: YAML
- **Kimlik Doğrulama**: API Key ve Bearer Token desteği
- **Sayfalama**: Kitap listesinde sayfalama desteği
- **Validation**: Kapsamlı veri doğrulama kuralları

### 📚 API Endpoints

#### Books (Kitaplar)
- `GET /books` - Tüm kitapları listele (sayfalama ile)
- `GET /books/{id}` - Tek kitap detayı
- `POST /books` - Yeni kitap ekle
- `PUT /books/{id}` - Kitap güncelle
- `DELETE /books/{id}` - Kitap sil

#### Students (Öğrenciler)
- `GET /students` - Tüm öğrencileri listele
- `GET /students/{id}` - Tek öğrenci detayı
- `POST /students` - Yeni öğrenci ekle
- `PUT /students/{id}` - Öğrenci güncelle
- `DELETE /students/{id}` - Öğrenci sil

#### Loans (Ödünç İşlemleri)
- `GET /loans` - Tüm ödünç işlemlerini listele
- `GET /loans/{id}` - Tek ödünç işlemi detayı
- `POST /loans` - Kitap ödünç al
- `PATCH /loans/{id}/return` - Kitap iade et

## 🗂️ Veri Modelleri

### Book (Kitap)
- `id`: UUID format
- `title`: Kitap başlığı
- `author`: Yazar
- `isbn`: ISBN-13 format
- `publisher`: Yayınevi
- `pageCount`: Sayfa sayısı
- `stock`: Stok adedi

### Student (Öğrenci)
- `id`: UUID format
- `name`: Ad soyad
- `studentNumber`: Öğrenci numarası
- `email`: E-posta adresi
- `isActive`: Aktif durum

### Loan (Ödünç)
- `id`: UUID format
- `studentId`: Öğrenci ID'si
- `bookId`: Kitap ID'si
- `loanDate`: Ödünç alma tarihi
- `returnDate`: İade tarihi (nullable)
- `status`: Durum (ongoing/returned/late)

## 🚀 Kullanım

1. `openapi.yaml` dosyasını [Swagger Editor](https://editor.swagger.io) ile açın
2. API spesifikasyonunu görüntüleyin ve test edin
3. Kod üretimi için çeşitli diller seçebilirsiniz

## 📝 Validation Kuralları

- **ISBN**: 978-XXXXXXXXXX formatında olmalı
- **Email**: Geçerli e-posta formatında olmalı
- **UUID**: Tüm ID'ler UUID v4 formatında olmalı
- **Student Number**: 8-12 haneli sayı olmalı
- **Page Count**: Pozitif sayı olmalı
- **Stock**: Negatif olamaz

## 🔒 Güvenlik

API iki tür kimlik doğrulama destekler:
- **API Key**: Header'da `X-API-Key` ile
- **Bearer Token**: JWT formatında

## 📊 HTTP Status Kodları

- `200 OK`: Başarılı işlem
- `201 Created`: Kaynak oluşturuldu
- `400 Bad Request`: Geçersiz istek
- `404 Not Found`: Kaynak bulunamadı
- `500 Internal Server Error`: Sunucu hatası

## 🧪 Test Etme

Swagger Editor'da test etmek için:
1. Dosyayı editor'a yükleyin
2. "Try it out" butonunu kullanın
3. Örnek verileri gönderin
4. Response'ları inceleyin

## 👨‍💻 Geliştirici Notları

Bu spesifikasyon eğitim amaçlıdır ve gerçek bir backend implementasyonu içermez. Production kullanımı için:
- Rate limiting ekleyin
- CORS ayarları yapın
- Logging ve monitoring entegre edin
- Database connection'ları ayarlayın

---

**Not**: Bu proje OpenAPI Tasarımı ödevi kapsamında hazırlanmıştır.