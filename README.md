# Analisis Tingkat Kepuasan Pengguna Layanan Keuangan Digital (E-Wallet dan Mobile Banking) dalam Mendukung Kebutuhan Sehari-hari Mahasiswa FMIPA Universitas Mataram
## Latar Belakang
Perkembangan teknologi digital telah membawa perubahan besar dalam sistem transaksi keuangan melalui hadirnya layanan seperti E-Wallet dan Mobile Banking. Layanan ini memberikan kemudahan dalam melakukan transaksi secara cepat, praktis, dan efisien sehingga penggunaannya terus meningkat di berbagai kalangan masyarakat, terutama mahasiswa yang cenderung adaptif terhadap perkembangan teknologi. Kemudahan akses melalui smartphone menjadikan layanan keuangan digital semakin diminati dalam aktivitas sehari-hari.

Mahasiswa memanfaatkan layanan keuangan digital untuk berbagai kebutuhan, seperti pembayaran makanan, transportasi, pembelian pulsa dan paket data, pembayaran tagihan, hingga transaksi akademik. Selain praktis, layanan E-Wallet dan Mobile Banking juga menawarkan berbagai fitur pendukung seperti kemudahan top up saldo, integrasi dengan berbagai layanan, serta proses transaksi yang cepat. Hal tersebut membuat layanan keuangan digital menjadi alternatif utama dibandingkan penggunaan uang tunai.

Di lingkungan FMIPA Universitas Mataram, penggunaan layanan keuangan digital juga berkembang cukup pesat untuk menunjang aktivitas sehari-hari mahasiswa. Namun, tingkat kepuasan pengguna terhadap layanan tersebut dapat berbeda-beda, dipengaruhi oleh aspek kemudahan penggunaan, keamanan, kecepatan transaksi, dan kenyamanan aplikasi. Tingkat kepuasan pengguna menjadi indikator penting dalam menilai kualitas layanan keuangan digital karena dapat memengaruhi keberlanjutan penggunaan layanan tersebut dalam kehidupan sehari-hari mahasiswa.

Penelitian ini bertujuan untuk mengetahui tingkat kepuasan mahasiswa FMIPA Universitas Mataram terhadap penggunaan layanan keuangan digital, khususnya E-Wallet dan Mobile Banking. Selain itu, penelitian ini juga memberikan gambaran mengenai peran layanan tersebut dalam mendukung kebutuhan harian mahasiswa. Data diperoleh melalui survei daring dengan teknik non probability sampling dengan metode purposive sampling, sehingga hasil penelitian diharapkan mampu memberikan informasi deskriptif terkait perilaku serta tingkat kepuasan pengguna layanan keuangan digital di lingkungan mahasiswa FMIPA Universitas Mataram.

## Tujuan
1. Mengetahui tingkat kepuasan mahasiswa FMIPA Universitas Mataram terhadap penggunaan layanan keuangan digital.
2. Mengetahui peran E-Wallet dan Mobile Banking dalam mendukung kebutuhan sehari-hari mahasiswa.
3. Menganalisis hasil survei online menggunakan metode non-probability sampling.

## Metode
Penelitian ini merupakan penelitian kuantitatif dengan pendekatan survei yang bertujuan untuk menggambarkan tingkat kepuasan mahasiswa FMIPA Universitas Mataram terhadap penggunaan layanan keuangan digital seperti e-wallet dan mobile banking. Data diperoleh dari 30 responden yang dipilih menggunakan teknik nonprobability sampling dengan metode purposive sampling, yaitu berdasarkan kriteria mahasiswa yang aktif menggunakan layanan tersebut. Pengumpulan data dilakukan melalui kuesioner online berbasis Google Form dengan skala Likert 1–5 untuk mengukur persepsi responden terhadap indikator kepuasan yang meliputi kemudahan penggunaan, kecepatan transaksi, keamanan layanan, dan manfaat penggunaan. Data yang diperoleh kemudian dianalisis secara deskriptif kuantitatif kemudian dilakukan perbandingan dua pendekatan analisis, yaitu naive estimation yang menggunakan rata-rata sederhana seluruh indikator, dan weighted estimation yang memberikan bobot pada setiap indikator sesuai tingkat kepentingannya untuk menghasilkan nilai kepuasan yang lebih representatif.

## Tahap Analisis Data
### Import Data
Tahap ini dilakukan untuk mengimpor data penelitian ke dalam aplikasi R agar dapat diolah lebih lanjut. Data dibaca dari file yang telah disiapkan agar dapat diolah dan dianalisis lebih lanjut. 
```r
library(readxl)
data <- read_excel("C:/Users/ACER/OneDrive/Documents/RESPONDEN.xlsx")
```
### Analisis Deskriptif
Tahap ini dilakukan untuk analisis deskriptif menggunakan R dengan menghitung frekuensi dan persentase pada variabel data responden guna mengetahui sebaran data responden.
```r
table(data$`Jenis Kelamin`)
prop.table(table(data$`Jenis Kelamin`)) * 100
table(data$`Usia`)
prop.table(table(data$`Usia`))*100
```
### Tabel Distribusi Frekuensi dan Persentase
Tahap ini dilakukan untuk menyajikan hasil analisis dalam bentuk tabel distribusi frekuensi dan persentase agar memudahkan dalam melihat sebaran data pada setiap kategori variabel.
```r
frekuensi <- table(data$`Jenis Kelamin`)
frekuensi
persentase <- prop.table(frekuensi) * 100
persentase
tabel_jenis_kelamin <- data.frame(
  Jenis_Kelamin = names(frekuensi),
  Frekuensi = as.vector(frekuensi),
  Persentase = round(as.vector(persentase), 2)
)
tabel_jenis_kelamin

frekuensi_usia <- table(data$`Usia`)
persentase_usia <- prop.table(frekuensi_usia)*100
tabel_usia <- data.frame(
  Usia = names(frekuensi_usia),
  Frekuensi = as.vector(frekuensi_usia),
  Persentase = round(as.vector(persentase_usia),2)
)
tabel_usia
```
### Grafik Distribusi Responden
Tahap ini dilakukan untuk menyajikan data dalam bentuk grafik distribusi responden agar sebaran setiap kategori variabel dapat terlihat lebih jelas dan mudah dipahami.
```r
barplot(
  table(data$`Jenis Kelamin`),
  main = "Distribusi Responden Berdasarkan Jenis Kelamin"
)
frekuensi_usia <- table(data$`Usia`)
barplot(
  frekuensi_usia,
  main = "Distribusi Responden Berdasarkan Usia",
  xlab = "Usia",
  ylab = "Frekuensi",
  col = "grey"
)
```
### Naive Estimation
Tahap ini dilakukan untuk menghitung naive estimation sebagai nilai pembanding dasar dalam pemodelan, yaitu dengan mengasumsikan kelas mayoritas sebagai hasil prediksi utama tanpa mempertimbangkan variabel lain.
```r
kepuasan_total <- rowMeans(data[, c("P1","P2","P3","P4","P5","P6","P7","P8","P9","P10")], na.rm = TRUE)
puas <- sum(kepuasan_total >= 4, na.rm = TRUE)
puas
n <- sum(!is.na(kepuasan_total))
estimasi_puas <- puas / n
estimasi_puas
estimasi_puas * 100
```
### Weighting Sederhana Berdasarkan Jenis Kelamin
Tahap ini dilakukan untuk memberikan pembobotan sederhana berdasarkan variabel jenis kelamin guna menyeimbangkan pengaruh masing-masing kategori dalam analisis data.
```r
proporsi_laki <- 0.5
proporsi_perempuan <- 0.5
sampel_laki <- 0.2666667
sampel_perempuan <- 0.7333333
w_laki <- proporsi_laki / sampel_laki
w_perempuan <- proporsi_perempuan / sampel_perempuan
w_laki
w_perempuan

# Jumlah responden puas berdasarkan jenis kelamin
table(data$`Jenis Kelamin`, kepuasan_total >= 4)
puas_laki <- 7
puas_perempuan <- 15

# Perhitungan weighted estimation
weighted_laki <- puas_laki * w_laki
weighted_perempuan <- puas_perempuan * w_perempuan

total_weighted <- weighted_laki + weighted_perempuan

weighted_estimation <- total_weighted / n

weighted_estimation
weighted_estimation * 100
```
### Perbandingan Naive dan Weighted Estimation
Tahap ini dilakukan untuk membandingkan hasil naive estimation dengan weighted estimation guna melihat perbedaan hasil sebelum dan sesudah pemberian pembobotan pada data.
```r
naive <- puas / n
estimasi <- c(
  Naive = naive * 100,
  Weighted = weighted_estimation * 100
)
barplot(
  estimasi,
  main = "Perbandingan Hasil Estimasi",
  ylab = "Persentase",
  col = c("skyblue", "blue")
)
```
## Hasil dan Pembahasan
### Analisis Deskriptif
| Jenis Kelamin | Frekuensi | Persentase |
|---|---|---|
| Laki-laki | 8 | 26.67% |
| Perempuan | 22 | 73.33% |
| Total | 30 | 100% |

Berdasarkan hasil survei dengan jumlah responden sebanyak 30 orang, dipeproleh hasil bahwa 8 responden laki-laki (26,67%) dan 22 responden perempuan (73,33%). Data tersebut menunjukkan bahwa responden dalam penelitian ini didominasi oleh perempuan.

| Usia | Frekuensi | Persentase |
|---|---|---|
| <20 tahun | 3 | 10.00% |
| >22 tahun | 1 | 3.33% |
| 20–22 tahun | 26 | 86.67% |
| Total | 30 | 100% |

Berdasarkan hasil survei dengan jumlah responden sebanyak 30 orang, diperoleh hasil bahwa 3 responden berusia <20 tahun (10,0%), 26 responden berusia 20–22 tahun (86,67%), dan 1 responden berusia >22 tahun (3,33%). Data tersebut menunjukkan bahwa responden dalam penelitian ini didominasi oleh usia 20–22 tahun.

### Naive Estimation
Naive estimation digunakan untuk memperoleh estimasi awal tingkat kepuasan mahasiswa berdasarkan data responden secara langsung tanpa memberikan pembobotan pada data. Berdasarkan hasil analisis menggunakan R diperoleh:

Jumlah responden puas = 22 orang

Total responden = 30 orang

Hasil ini menunjukkan bahwa sebesar 73.33% mahasiswa merasa puas terhadap layanan keuangan digital. 

### Weighting Sederhana
Weighting sederhana digunakan untuk menyesuaikan distribusi sampel agar lebih mendekati distribusi populasi yang sebenarnya. Berdasarkan hasil analisis menggunakan R diperoleh hasil weighted estimation sebesar 77.84%. Hasil tersebut menunjukkan bahwa setelah dilakukan pembobotan berdasarkan jenis kelamin, tingkat kepuasan mahasiswa terhadap layanan keuangan digital tetap berada pada kategori cukup tinggi.

### Perbandingan Estimasi
| Metode Estimasi | Hasil | 
|---|---|
| Naive Estimation | 73.33% | 
| Weighted Estimation | 77.84% | 

## Kesimpulan
Berdasarkan hasil analisis non-probability sampling pada survei online terkait tingkat kepuasan mahasiswa FMIPA terhadap layanan keuangan digital, diketahui bahwa sebagian besar responden memberikan penilaian positif terhadap pelayanan yang diterima. Hasil distribusi responden memperlihatkan bahwa jumlah responden perempuan lebih banyak dibandingkan laki-laki. Perhitungan naive estimation menghasilkan tingkat kepuasan sebesar 73.33%, sedangkan hasil weighted estimation berdasarkan jenis kelamin menunjukkan nilai sebesar 77.84%. Selisih hasil yang tidak terlalu besar menandakan bahwa sampel penelitian telah cukup menggambarkan kondisi populasi.

## Link Kuesioner
https://forms.gle/m1NcoGDUoyeBa8uK8
