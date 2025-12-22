Hello! 


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
	CASE
        WHEN od."Discount" > 0 THEN 'Discount'
     	ELSE 'No Discount'
    END AS status_diskon,
	o."OrderDate" as tanggal_pesan,
	o."RequiredDate" as estimasi_tiba,
	o."ShippedDate" as waktu_tiba,
	(o."ShippedDate" - o."OrderDate") as lama_pengiriman,
	EXTRACT(YEAR FROM "OrderDate") AS tahun,
  	EXTRACT(MONTH FROM "OrderDate") AS bulan,
  	TO_CHAR("OrderDate", 'Month') AS nama_bulan,
  	EXTRACT(DAY FROM "OrderDate") AS tanggal,
  	TO_CHAR("OrderDate", 'Day') AS hari,
	o."ShipVia" as id_shipper,
	s."CompanyName" as nama_jasa_pengiriman,
	o."Freight" as biaya_pengiriman
from orders o 
left join order_details od on od."OrderID" = o."OrderID" 
left join customers c on c."CustomerID" = o."CustomerID"
left join products p on p."ProductID" = od."ProductID" 
left join shippers s on s."ShipperID" = o."ShipVia"
left join categories c2 on c2."CategoryID"  = p."CategoryID";
```


```sql
WITH rfm AS (
  SELECT
    customer_id,
    DATE '1998-12-31' - MAX(order_date) AS recency,
    COUNT(DISTINCT order_id) AS frequency,
    SUM(sales_amount) AS monetary
  FROM fact_sales
  GROUP BY customer_id
)
SELECT *,
  NTILE(5) OVER (ORDER BY recency DESC) AS r_score,
  NTILE(5) OVER (ORDER BY frequency) AS f_score,
  NTILE(5) OVER (ORDER BY monetary) AS m_score
FROM rfm
order by 
	r_score desc,
	f_score desc,
	m_score desc;
```







Observe my dashboard on Tableau by click link below 👇
https://public.tableau.com/app/profile/zulyan.firdaus/viz/NorthwindDashboard_17663584932570/Dashboard
