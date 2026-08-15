# 🛒 E-Commerce Data Analysis with SQL (MySQL / phpMyAdmin)

Bu proje, bir E-Ticaret platformunun müşteri, sipariş, ürün ve kategori verilerini modellemek ve iş kararlarına yön verecek analitik sorguları çalıştırmak amacıyla hazırlanmış bir **Relational Database & Data Analysis** çalışmasıdır.

---

## 📐 Veritabanı Mimarısı (Tablo Yapısı)

Projede 5 ilişkisel tablo oluşturulmuş ve Primary Key / Foreign Key bağlamları kurgulanmıştır:
- **`Musteriler`**: Müşteri bilgileri ve kayıt tarihleri.
- **`Kategoriler`**: Ürün kategorileri.
- **`Urunler`**: Ürün adı, stok ve fiyat bilgileri.
- **`Siparisler`**: Sipariş tarihleri ve kargo durumları.
- **`Siparis_Detay`**: Sipariş edilen ürünler, adet ve birim fiyat detayları.

---

## 📊 Analiz Sorguları ve Bulgular

### 1. Kategori Bazlı Satış ve Ciro Analizi
Hangi ürün kategorisinin toplamda ne kadar satış adedine ve ciroya ulaştığı analiz edilmiştir.

```sql
SELECT 
    k.KategoriAdi,
    SUM(sd.Adet) AS Toplam_Satilan_Adet,
    SUM(sd.Adet * sd.BirimFiyat) AS Toplam_Ciro
FROM Siparis_Detay sd
JOIN Urunler u ON sd.UrunID = u.UrunID
JOIN Kategoriler k ON u.KategoriID = k.KategoriID
GROUP BY k.KategoriAdi
ORDER BY Toplam_Ciro DESC;
SELECT 
    m.Sehir,
    COUNT(DISTINCT s.SiparisID) AS Toplam_Siparis_Sayisi,
    SUM(sd.Adet * sd.BirimFiyat) AS Sehir_Toplam_Ciro
FROM Musteriler m
JOIN Siparisler s ON m.MusteriID = s.MusteriID
JOIN Siparis_Detay sd ON s.SiparisID = sd.SiparisID
GROUP BY m.Sehir
ORDER BY Sehir_Toplam_Ciro DESC;
SELECT 
    u.UrunAdi,
    u.StokMiktari,
    COALESCE(SUM(sd.Adet), 0) AS Toplam_Satilan_Adet
FROM Urunler u
LEFT JOIN Siparis_Detay sd ON u.UrunID = sd.UrunID
GROUP BY u.UrunID, u.UrunAdi, u.StokMiktari
ORDER BY Toplam_Satilan_Adet DESC;
### **3. Adım: Değişiklikleri Kaydet (Commit Changes)**

1. Sağ üstteki yeşil **`Commit changes...`** butonuna tıkla.
2. Açılan pencerede tekrar yeşil **`Commit changes`** butonuna bas.

Kaydettiğinde sayfayı aşağı doğru kaydır. 3 sorgunun da hemen altında ekran görüntüleri açılacak!
