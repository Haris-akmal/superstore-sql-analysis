# Superstore E-Commerce: SQL Sales & Profitability Analysis

## 📌 Latar Belakang Projek
Superstore adalah sebuah syarikat e-commerce dan peruncitan bersaiz sederhana yang menjual produk merangkumi tiga kategori utama: Perabot (Furniture), Barangan Pejabat (Office Supplies), dan Teknologi (Technology). 

Walaupun syarikat mencatatkan angka jualan yang tinggi setiap tahun, pihak pengurusan menyedari bahawa margin keuntungan keseluruhan tidak berkembang secara selari. Projek ini dibangunkan untuk menganalisis pangkalan data jualan Superstore menggunakan **SQL** bagi mengenal pasti punca kebocoran keuntungan, produk terlaris, dan kawasan yang memerlukan penyusunan semula strategi pemasaran.

**Alat yang digunakan:** 
- **Pembersihan Data (ETL):** KNIME Analytics Platform
- **Pangkalan Data Utama:** MySQL
- **Analisis:** SQL (Data Querying & Aggregation)

---

## 📂 Struktur Data
Set data (`SampleSuperstore.csv`) mengandungi 9,994 rekod transaksi dengan 13 lajur (kolum) utama. Untuk tujuan pengoptimuman kelajuan, data ini telah dimuat naik ke dalam MySQL menggunakan kaedah `LOAD DATA INFILE` ke dalam jadual bernama `superstore`.

Antara kolum utama yang dianalisis:
- `Order_Date` / `Ship_Mode`
- `Segment` / `Region`
- `Category` / `Sub_Category`
- `Sales` / `Quantity` / `Profit` / `Discount`

---

## 📊 Analisis Bisnes & SQL Queries

### 1. Kategori Produk: Penjana Untung vs Penyumbang Kerugian
**Soalan:** Antara tiga kategori utama, yang manakah memberi pulangan pelaburan paling tinggi, dan yang manakah merugikan syarikat?

```sql
SELECT 
    Category,
    ROUND(SUM(Sales), 2) AS Jumlah_Jualan_USD,
    ROUND(SUM(Profit), 2) AS Keuntungan_USD,
    ROUND((SUM(Profit) / SUM(Sales)) * 100, 2) AS Margin_Untung_Peratus
FROM superstore
GROUP BY Category
ORDER BY Keuntungan_USD DESC;


Dapatan Utama:

Teknologi (Technology) adalah nadi utama keuntungan syarikat dengan margin paling sihat.

Walaupun Perabot (Furniture) mencatatkan jumlah jualan yang sangat tinggi, ia menyumbang kepada margin keuntungan yang paling rendah (hampir rugi), kemungkinan besar disebabkan oleh kos penghantaran yang mahal dan diskaun yang tinggi.

Cadangan Bisnes: Kurangkan pemberian diskaun melampau untuk barangan Perabot dan fokus belanjawan marketing kepada kategori Teknologi.

2. Produk Terlaris (Top 5 Sub-Category) Berdasarkan Kuantiti
Soalan: Barangan spesifik apakah yang paling kerap dibeli oleh pelanggan supaya pihak gudang boleh memastikan stok sentiasa mencukupi?

SQL


SELECT 
    Sub_Category,
    SUM(Quantity) AS Jumlah_Unit_Terjual,
    ROUND(SUM(Sales), 2) AS Jumlah_Jualan_USD
FROM superstore
GROUP BY Sub_Category
ORDER BY Jumlah_Unit_Terjual DESC
LIMIT 5;
Dapatan Utama:

Kategori seperti Binders, Paper, dan Furnishings mencatatkan jumlah transaksi tertinggi.

Barangan ini adalah "magnet pelanggan" (Fast-Moving Consumer Goods).

Cadangan Bisnes: Kekalkan inventori yang tinggi untuk barangan pejabat asas ini. Gunakan strategi bundle-pricing (Beli Binders dapat diskaun untuk Beli Mesin Pencetak) untuk menaikkan nilai jualan.

3. Kenal Pasti Kawasan (Region) Paling Bermasalah
Soalan: Wilayah manakah yang menyumbang kepada pendapatan paling rendah dan perlukan rombakan strategi jualan?

SQL


SELECT 
    Region,
    ROUND(SUM(Sales), 2) AS Jumlah_Jualan_USD,
    ROUND(SUM(Profit), 2) AS Keuntungan_USD
FROM superstore
GROUP BY Region
ORDER BY Keuntungan_USD ASC;
Dapatan Utama:

Kawasan Central dan South mencatatkan prestasi yang jauh lebih perlahan berbanding East dan West.

Kawasan Central secara puratanya bergelut untuk menghasilkan keuntungan walaupun mempunyai angka jualan yang stabil.

Cadangan Bisnes: Semak semula logistik dan operasi di kawasan Central. Hentikan kempen promosi yang memakan kos tinggi di sana sehingga punca operasi yang merugikan ini diselesaikan.

💡 Kesimpulan
Melalui analisis SQL yang ringkas dan padat ini, kita dapat mengenal pasti bahawa angka "Jualan Tinggi" tidak semestinya bermaksud "Keuntungan Tinggi". Manipulasi data mendedahkan bahawa kategori Perabot dan operasi di wilayah Central menyembunyikan kerugian syarikat. Keputusan berasaskan data (Data-Driven Decisions) adalah kunci kepada kelestarian perniagaan Superstore.
