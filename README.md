# Superstore E-Commerce Sales Analysis

Projek ini bertujuan menganalisis data jualan kedai runcit (Superstore) menggunakan **SQL** untuk mencari jawapan kepada soalan bisnes yang kritikal seperti keuntungan mengikut kategori dan prestasi kawasan.

## 1. Kategori Produk Mana Paling Menguntungkan?
Bahagian Teknologi membawa keuntungan paling besar, manakala Perabot mendatangkan kerugian.

```sql
SELECT 
    Category,
    ROUND(SUM(Sales), 2) AS Jumlah_Jualan_USD,
    ROUND(SUM(Profit), 2) AS Keuntungan_USD,
    ROUND((SUM(Profit) / SUM(Sales)) * 100, 2) AS Margin_Untung_Peratus
FROM superstore
GROUP BY Category
ORDER BY Keuntungan_USD DESC;

SELECT 
    Sub_Category,
    SUM(Quantity) AS Jumlah_Unit_Terjual,
    ROUND(SUM(Sales), 2) AS Jumlah_Jualan_USD
FROM superstore
GROUP BY Sub_Category
ORDER BY Jumlah_Unit_Terjual DESC
LIMIT 5;
