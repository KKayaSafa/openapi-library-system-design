# OpenAPI Tasarımı Ödevi Teslim Raporu

## 👤 Öğrenci Bilgileri
- **Ad Soyad**: Safa Kılıçkaya
- **Öğrenci Numarası**: 170422044

---

## 📂 OpenAPI YAML Dosyası

- **openapi.yaml** dosyasını projenizin GitHub reposuna yükleyiniz.
- Swagger Editor ile test ettiğinizden emin olunuz.

### 🔗 GitHub Repo Linki
https://github.com/KKayaSafa/openapi-library-system-design.git

---

## 📝 API Açıklaması

Bu projede bir üniversite kütüphanesi için kapsamlı bir REST API tasarladım. API, OpenAPI 3.0.4 standardında yazılmış olup, kitap yönetimi, öğrenci kaydı ve ödünç işlemlerini desteklemektedir.

### 📚 Varlıklar (Entities)

1. **books**: Kütüphane kitap koleksiyonu
   - id (UUID), title, author, isbn (ISBN-13), publisher, pageCount, stock

2. **students**: Üniversite öğrencileri  
   - id (UUID), name, studentNumber, email, isActive

3. **loans**: Kitap ödünç alma kayıtları
   - id (UUID), studentId, bookId, loanDate, returnDate, status (enum)

### 🔗 CRUD İşlemleri

**Books Endpoints:**
- `GET /books` → Tüm kitapları getir (sayfalama ile)
- `GET /books/{id}` → Tek kitap detayı  
- `POST /books` → Yeni kitap ekle
- `PUT /books/{id}` → Kitap güncelle
- `DELETE /books/{id}` → Kitap sil

**Students Endpoints:**
- `GET /students` → Tüm öğrencileri getir
- `GET /students/{id}` → Tek öğrenci detayı
- `POST /students` → Yeni öğrenci ekle  
- `PUT /students/{id}` → Öğrenci güncelle
- `DELETE /students/{id}` → Öğrenci sil

**Loans Endpoints:**
- `GET /loans` → Tüm ödünç kayıtlarını getir
- `GET /loans/{id}` → Tek ödünç kaydı detayı
- `POST /loans` → Kitap ödünç al
- `PATCH /loans/{id}/return` → Kitap iade et

### 🧩 Components Kullanımı

**Schemas:** Her varlık için ayrı schema tanımları (Book, Student, Loan) ile Create/Update varyantları. Ayrıca Pagination ve Error şemaları.

**Parameters:** Path parametreleri (UUID id'ler), Query parametreleri (sayfalama, filtreleme), Header parametreleri (X-Return-Date, X-API-Key).

**Responses:** Tekrar kullanılabilir response şablonları (BadRequest, NotFound, InternalServerError) ile tutarlı hata döndürme.

### 📄 Sayfalama ve Hata Yönetimi

**Sayfalama:** GET /books endpoint'inde `page` ve `size` parametreleri ile implement edildi. Response'da pagination metadata (currentPage, totalPages, totalItems) döndürülüyor.

**Hata Durumları:** Kapsamlı HTTP status kodları (200, 201, 400, 404, 500) ile açıklayıcı error mesajları. Her hata türü için özel schema ve örnekler mevcut.

---


## 🧪 Test Notları (Opsiyonel)

### GET /books Çağrısı
```json
{
  "data": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "title": "Java ile Programlamaya Giriş", 
      "author": "Mehmet Yılmaz",
      "isbn": "978-0123456789",
      "publisher": "Teknik Yayınları",
      "pageCount": 450,
      "stock": 5
    }
  ],
  "pagination": {
    "currentPage": 1,
    "totalPages": 15,
    "totalItems": 150,
    "itemsPerPage": 10
  }
}
```

### POST /students RequestBody Örneği
```json
{
  "name": "Ayşe Yılmaz",
  "studentNumber": "20220002", 
  "email": "ayse.yilmaz@ogrenci.universite.edu.tr",
  "isActive": true
}
```

### 400 Hata Örneği
```json
{
  "error": "BAD_REQUEST",
  "message": "İstek verileri geçersiz",
  "details": ["title alanı gerekli", "pageCount pozitif bir sayı olmalı"]
}
```

---

## 📌 Ek Açıklamalar

- **Güvenlik:** API Key ve Bearer Token ile çift kimlik doğrulama desteği
- **Validation:** ISBN-13, email, UUID formatları için regex pattern'ları
- **Filtering:** Kitap arama, öğrenci durumu ve ödünç status filtreleri
- **Swagger Editor'da test edildi** ve tüm endpoint'ler düzgün çalışıyor
- **Production ready** kalitesinde, gerçek projede kullanılabilir