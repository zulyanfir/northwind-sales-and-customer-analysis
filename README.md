<div align='center'>
<h1 style="font-family: 'Trebuchet MS', sans-serif; monospace;">Northwind Sales and Customer Analysis 🔎</h1>
</div>

Hai! 🙋‍♂️

<div align='justify'>
   
Portofolio ini berisi analisis data menggunakan Northwind Database sebagai studi kasus.
Tujuan dari proyek ini adalah untuk mengeksplorasi data Northwind (dummy) menggunakan SQL, Python, dan Tableau serta menghasilkan insight yang relevan untuk mendukung pengambilan keputusan bisnis.

Northwind Database adalah database contoh fiktif tentang perusahaan ekspor-impor (Northwind Traders) yang dibuat oleh Microsoft untuk tujuan edukasi. Database ini berisi data penjualan, pelanggan, pemasok, produk, karyawan, dan detail pesanan, menunjukkan bagaimana data disimpan dalam database relasional. 

</div>

<br>

<h2 style="font-family: 'Trebuchet MS', sans-serif; monospace;">Tahapan :</h2>

![My Skills](https://skills.syvixor.com/api/icons?perline=15&i=postgresql) ➡️ ![My Skills](https://skills.syvixor.com/api/icons?perline=15&i=jupyter) ➡️ ![My Skills](https://skills.syvixor.com/api/icons?perline=15&i=tableau)

1. Membuat query data mart sebelum dikoneksikan ke Python.
2. Menarik data dari PostgreSQL menggunakan Psycopg, data wrangling, analisis deskriptif dan inferensia menggunakan Python.
3. Convert cleaned data menjadi format `csv` dan membuat dashboard Interaktif menggunakan Tableau.

<br>
<h2 style="font-family: 'Trebuchet MS', sans-serif; monospace;">Business Question (dummy):</h2>

Deskriptif:
1. Berapa jumlah pelanggan dari setiap negara?
2. Siapa saja pelanggan yang paling menguntungkan?
3. Siapa saja pelanggan yang harus dipertahankan menurut segmentasi?
4. Berapa rata-rata diskon berdasarkan pelanggan dan perbandingan yang non diskon?
5. Bagaimana tren penjualan berdasarkan tahun?
6. Bagaimana tren pendapatan berdasarkan tahun?
7. Produk apakah yang paling laris?
8. Kategori produk apakah yang paling menguntungkan?
9. Berapa rata-rata lama pengiriman berdasarkan jasa pengirim?

Inferensia:
1. Apakah diskon memiliki perbedaan signifikan terhadap jumlah transaksi?
2. Apakah diskon memiliki perbedaan signifikan terhadap jumlah transaksi masing-masing kategori produk?
3. Apakah perbedaan performa murni kualitas jasa pengirim atau hanya kebetulan?
   
<br>

<h2 style="font-family: 'Trebuchet MS', sans-serif; monospace;">Hasil :</h2>

Observe my dashboard on Tableau by click link below 👇
https://public.tableau.com/app/profile/zulyan.firdaus/viz/NorthwindSalesandCustomerDashboard/DashboardGrowth

<br>

<h2 style="font-family: 'Trebuchet MS', sans-serif; monospace;">Lampiran :</h2>

- Query Data Mart

```sql
select 
	o."OrderID" as id_pesan,
	o."CustomerID" as id_pelanggan,
	c."CompanyName" as nama_pelanggan,
	c."City" as kota,
	c."Country" as negara,
	od."ProductID" as id_produk,
	p."ProductName" as nama_produk,
	c2."CategoryName" as kategori_produk,
	od."UnitPrice" as harga,
	od."Quantity" as jumlah_transaksi,
	od."Discount" as diskon,
	o."OrderDate" as tanggal_pesan,
	o."RequiredDate" as estimasi_tiba,
	o."ShippedDate" as tanggal_tiba,
	o."ShipVia" as id_shipper,
	s."CompanyName" as nama_jasa_pengiriman
from orders o 
left join order_details od on od."OrderID" = o."OrderID" 
left join customers c on c."CustomerID" = o."CustomerID"
left join products p on p."ProductID" = od."ProductID" 
left join shippers s on s."ShipperID" = o."ShipVia"
left join categories c2 on c2."CategoryID"  = p."CategoryID";
```

- Output Tabel
<img width="1665" height="436" alt="image" src="https://github.com/user-attachments/assets/63456dbe-24dc-4544-902c-986561e618d0" />

- Dashboard Growth
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c7d3c0ad-4f2e-4011-9bf5-8b9642da5b45" />
  
- Dashboard Customer Segmentation
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1d0feab9-3c51-40dc-8548-0179d7c5eaa4" />

