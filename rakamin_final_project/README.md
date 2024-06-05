### Final Project Rakamin - E-Commerce Dataset 
<b>By Data Center Group</b><br>
[**Exploratory Data Analysis**](https://github.com/Adhete/final_project_rakamin/blob/main/ecommerce_finpro.ipynb "Data Preprocessing")
# 💡Summary Insight
**1. Descriptive Statistics**
- Tipe data kolom `operating system` dapat menggunakan tipe data int,
tipe data kolom `month` juga dapat menggunakan int. kolom lainnnya sudah sesuai.
- Terdapat 12.946 baris data, dengan jumlah fitur 18. Dari 18 fitur tersebut, ada 5 fitur yang memiliki nilai null diantaranya:
	1. Administrative `111` null data.
	2. Administrative_Duration `633` null data.
	3. ProductRelated_Duration `639` null data.
	4. BounceRates `74` null data.
	5. OperatingSystems `524` null data.
Selain nilai null, juga terdapat 711 data Duplicated.
- Untuk fitur numerik (nums) terdapat outlier pada masing-masing fiturnya, dan sebaran nilai masing-masing fitur merupakan sebaran positively skewed, karena nilai mean yang lebih besar dari nilai median nya.
- Sedangkan untuk fitur kategorikal (cats), fitur revenue dipilih sebagai target. tetapi atribut ini memiliki imbalances, dimana nilai False/Not Buyer terdapat sebanyak 10.938 data, sehingga perlu untuk disesuaikan ketika proses training.

------------
**2. Univariate Analysis**<br>
Untuk kolom **numerikal** berikut ini memiliki distribusi positively skewed
dan juga memiliki outlier:
- `administrative`
- `administrative_duration`
- `informational`
- `informational_duration`
- `productrelated`
- `productrelated_duration`
- `bouncerates`
- `exitrates`
- `pagevalues`

Untuk tahap preprocessing dapat dilakukan, handling outlier dan feature
transformation.

Untuk kolom **kategorikal** :
- `month` : jumlah data didominasi bulan: May, Nov, Mar, Dec
- `weekend` : didominasi oleh nilai 'False'
- `specialday` : kunjungan situs mayoritas dilakukan saat, jauh dari specialday (hari khusus)
- `region` : observasi menunjukan user region 1 mendominasi• 'operatingsystem' : yang digunakan banyak user 2, 1, 3, 4
- `browser` : jenis 2 mendominasi data dari 13 jenis browser
- `traffictype` : jenis traffic yang paling banyak membawa user
merupakan traffic 2, 1, 3
- `visitortype` : kunjungan mayoritas dilakukan oleh
returning_visitor
- `revenue` : sebanyak 84.48% dari kunjungan tidak melakakukan
pembelian / tidak menghasilkan pendapatan

Untuk kolom revenue sebagai target perlu dilakukan imbalances handling kolom visitortype dan month, dapat dilakukan feature encoding agar dapat dilakukan algoritma korelasi.

------------

**3. Multivariate Analysis**<br>
Fitur `administrative`, `informational`, `productrelated` memiliki korelasi dengan target `pagevalues` menjadi fitur yang memiliki korelasi sangat relevan dengan target (0.63).

berdasarkan hasil korelasi heatmap yang ditampilkan, terdapat korelasi
yang tinggi antara fitur :
- `productrelated` dengan productrelated_duration (0.88)
- `administrative` dengan administrative_duration (0.94)• informational dengan informational_duration (0.95)
- `bounce_rates` dengan exitrates (0.60)

Maka antara salah satu fitur yang berkorelasi tinggi, akan di drop berdasarkan korelasi yang rendah terhadap target `revenue`. fitur `pagevalues` memiliki korelasi yang tinggi/relevan terhadap target. sebesar (0.63) ada kemungkinan fitur `month` dan `visitortype` berkorelasi tinggi terhadap target, maka perlu encoding untuk tahap preprocessing dan melihat korelasinya.

------------

**4. Business Insight**
- Region 1 memiliki pengunjung paling banyak diantara region lainnya. akan tetapi revenue rate region 2 16.64% menjadi paling tinggi diantara region lainnya.
- Kunjungan user pada platform, yang menghasilkan revenue didominasi pada bulan November 25,48% Revenue Rate, Sementara bulan Februari memiliki kunjungan yang menghasilkan revenue yang paling sedikit 1.57% Revenue Rate (3 buyer).
- Bulan May memiliki kunjungan yang paling banyak diantara yang lain terdapat total kunjungan 3533 akan tetapi, hanya 379 dari total kunjungan yang menghasilkan revenue.
- Kunjungan user pada weekday lebih tinggi dari weekend tetapi revenue rate weekend > weekday 17.5% /14.9%
- Sesi dilakukan mayoritas oleh Returning Visitors. namun, persentase Buyer pada Returning Visitors secara signifikan lebih sedikit dari Non-Buyers. pada New visitor, proporsi Buyers mendekati proporsi Non-Buyers. hal ini menunjukan bahwa Returning Visitor lebih banyak sesi kunjungannya, tetapi New Visitors mempunyai purchase rate yang lebih tinggi 24.65%.
- Pengunjung yang memutuskan untuk melakukan pembelian Buyer, memiliki nilai rata-rata yang lebih tinggi dari Non-Buyer. dalam melihat halaman productrelated 47.89 / 28.67.
- ketika session melibatkan pagevalues > 0 purchase rate tinggi 56.44%. Sebaliknya, sesi dengan pagevalues nol menunjukkan purchase rate yang lebih rendah 3.88%.


------------
**5. Business Recommendation**<br>
untuk region yang masih rendah nilai revenue_rate nya, tim marketing dapat menampilkan halaman web yang memiliki pagavalues > 0, dan juga menampilkan rekomendasi yang relevan dengan halaman web yang yang dikunjungi user (product related). strategi marketing tersebut dapat dilakukan pada weekend, dikarenakan disaat weekend revenue_rate lebih tinggi dibandingkan weekday. maka hal ini dapat membantu meningkatkan revenue platform e-commerce.


------------


**6. Metrics**<br>
Revenue rate

------------

## Data Pre-Procesing

**1. Missing values**
Setelah dilakukan penegcekan, adapun missing value pada dataset. yaitu productrelated_duration sebanyak 639, administrative_duration sebanyak 633, operatingsystems sebanyak 524, administrative sebanyak 111, bouncesrate sebanyak 74. Dengan hal ini, untuk handle missing value dilakukan karena dataset tersebut masih dibawa 10% maka dataset dihapus atau diisi dengan median menggunakan fungsi fillna dan hasilnya seperti pada gambar 2. Dengan demikian, sudah tidak ada lagi data yang kosong.

**2. Duplicated data**
Data yang duplikat ada 717. Data sebelum dilakukan handle duplicate ada 12946. Setelah di-handle, diperoleh 12229 data.

**3. Outliers**
Sebelum dilakukan penghapusan outlier dilakukan split dataset terlebih dahulu. Handle Outlier menggunakan metode Z-Score.

**4. Feature transformation**
Adapun feature transformation dilakukan untuk transform numerical feature dengan menggunakan Standardization pada dataset train dan test.

**5. Feature encoding**
Pada fitur kategorikal `month`, `operatingsystems`, `browser` `region`, `traffictype`, `visitortype` dilakukan one hot encoding.

**6. Cass imbalance**
Metode yang digunakan untuk mengatasi class imbalance adalah SMOTE (Synthetic Minority Over-sampling Technique) dengan data yang digunakan adalah data train.

**7. Feature selection**
Untuk mencari feature selection menggunkan fungsi `SelectKBest` dan `mutual_info_classif` pada library `sklearn.feature_selection`

**8. Feature extraction**
Berdasarkan Live Mentoring bersama dengan tutor, tidak dilakukan feature extraction dikarenakan tidak memiliki fitur atau kolom yang bisa di-extraction yang berisi informasi tanggal, waktu, atau tahun dalam dataset.

**9. 4 Fitur tambahan (selain yang sudah tersedia di dataset)**
		1.  Average Session Duration
		2.  Bounce Rate by Device Type
		3.  Date
		4.  User Demographics