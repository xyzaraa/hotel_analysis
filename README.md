# 🛎️ Hotel Booking Analysis 🏨
![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Hotel%20Cover%20Github.png?raw=true)
# Project Overview

Project ini bertujuan untuk menganalisis data reservasi hotel yang dapat digunakan untuk eksplorasi faktor penentu keberhasilan manajemen hotel serta tren dan perilaku konsumen. Faktor ini dapat menghasilkan pola-pola tertentu yang dapat membantu manajer hotel atau pihak terkait untuk meningkatkan tingkat pemesanan/reservasi konsumen.

Tujuan utama dari project ini adalah memberikan wawasan untuk pengambilan keputusan yang lebih terinformasi terkait pemesanan kamar dan strategi pemasaran.

## Langkah Analisa
1. Data Cleaning
Missing value akan dibersihkan, memastikan format sudah sesuai (date, categorical, dan numerical), serta memfilter data berdasarkan reservasi yang tidak dibatalkan(is_canceled == 0).

2. Explanatory Data Analysis
Data yang sudah bersih akan dikelompokkan berdasarkan bulan, tahun, tipe hotel dan lain-lain untuk memahami pola pendapatan.

3. Visualisasi
Relasi antar data akan divisualisasikan untuk memberikan pemahaman yang advanced. Hal ini akan menghasilkan pandangan yang lebih luas kepada pihak terkait agar lebih mudah mengambil keputusan.

4. Analisis Tren
Identifikasi saat dimana jumlah reservasi meningkat atau merendah untuk masing-masing tipe hotel, serta evaluasi kemungkinan faktor penyebab (misalnya musim liburan atau perbedaan target konsumen).

5. Model Prediction
Setelah proses data cleaning dan analisis selesai, data akan digunakan untuk membangun dan membandingkan model prediksi menggunakan algoritma XGBoost, CatBoost, dan K-Nearest Neighbors (KNN). Model XGBoost dan CatBoost dipilih karena performanya yang kuat dalam menangani dataset yang kompleks dan besar, sedangkan KNN digunakan sebagai model pembanding yang sederhana namun efektif untuk analisis data kecil atau pola lokal.

## Manfaat dan Implikasi dari Analisis
1. Pengelola Hotel: Dapat menentukan strategi promosi atau penyesuaian harga berdasarkan musim tinggi (high season) dan musim rendah (low season). Misalnya, memberikan diskon di bulan dengan ADR rendah atau meningkatkan penawaran layanan di musim ramai.
2. Wisatawan: Mendapatkan wawasan tentang waktu terbaik untuk memesan hotel dengan harga lebih terjangkau.
3. Peneliti dan Data Analis: Mendapatkan pola tren data hotel yang relevan untuk referensi studi atau laporan.


# Library dan Dependency
- pandas
- matplotlib
- numpy 
- seaborn 
- sklearn
- CatBoost
- XGBoost
- KNeighborsClassifier

## Instalasi library dan dependency
   ```bash
   !pip install -r requirements.txt
   ```
## Mengakses dataset
```bash
hotels <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2020/2020-02-11/hotels.csv')
```
## Download dataset
Akses [dataset](https://github.com/rfordatascience/tidytuesday/blob/main/data/2020/2020-02-11/hotels.csv) untuk mengunduh dataset. Agar lebih efisien, gunakan google drive untuk menyimpan dataset kemudian lakukan command berikut pada colab :
```
from google.colab import drive
drive.mount('/content/drive')

df = read_csv('/content/drive/MyDrive/<your_dir>/hotels.csv')
``` 
  
# Dataset Overview

Dataset yang digunakan dalam project ini berasal dari [Hotel booking demand datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010) yang dipublish melaluii github [tidytuesday](https://github.com/dslc-io/tidytuesdayR). Dataset ini mendeskripsikan dua dataset dengan data demand hotel. Terdapat dua jenis hotel, yaitu Resort Hotel dan City Hotel. Kedua dataset memiliki struktur yang sama, dengan 31 variable dan merepresentasikan reservasi antara 1 juli 2015 hingga 31 Agustus 2017, termasuk reservasi yang dibatalkan ataupun yang berhasil.

Berikut adalah informasi umum pada dataframe:

| #  | Column                          | Non-Null Count   | Dtype    |
|----|---------------------------------|------------------|----------|
| 0  | hotel                           | 119390 non-null  | object   |
| 1  | is_canceled                     | 119390 non-null  | int64    |
| 2  | lead_time                       | 119390 non-null  | int64    |
| 3  | arrival_date_year               | 119390 non-null  | int64    |
| 4  | arrival_date_month              | 119390 non-null  | object   |
| 5  | arrival_date_week_number        | 119390 non-null  | int64    |
| 6  | arrival_date_day_of_month       | 119390 non-null  | int64    |
| 7  | stays_in_weekend_nights         | 119390 non-null  | int64    |
| 8  | stays_in_week_nights            | 119390 non-null  | int64    |
| 9  | adults                          | 119390 non-null  | int64    |
| 10 | children                        | 119386 non-null  | float64  |
| 11 | babies                          | 119390 non-null  | int64    |
| 12 | meal                            | 119390 non-null  | object   |
| 13 | country                         | 118902 non-null  | object   |
| 14 | market_segment                  | 119390 non-null  | object   |
| 15 | distribution_channel            | 119390 non-null  | object   |
| 16 | is_repeated_guest               | 119390 non-null  | int64    |
| 17 | previous_cancellations          | 119390 non-null  | int64    |
| 18 | previous_bookings_not_canceled  | 119390 non-null  | int64    |
| 19 | reserved_room_type              | 119390 non-null  | object   |
| 20 | assigned_room_type              | 119390 non-null  | object   |
| 21 | booking_changes                 | 119390 non-null  | int64    |
| 22 | deposit_type                    | 119390 non-null  | object   |
| 23 | agent                           | 103050 non-null  | float64  |
| 24 | company                         | 6797 non-null    | float64  |
| 25 | days_in_waiting_list            | 119390 non-null  | int64    |
| 26 | customer_type                   | 119390 non-null  | object   |
| 27 | adr                             | 119390 non-null  | float64  |
| 28 | required_car_parking_spaces     | 119390 non-null  | int64    |
| 29 | total_of_special_requests       | 119390 non-null  | int64    |
| 30 | reservation_status              | 119390 non-null  | object   |
| 31 | reservation_status_date         | 119390 non-null  | object   |

dtypes: float64(4), int64(16), object(12)
memory usage: 29.1+ MB

## Data Preparation
Sebelum dianalisis, data mentah akan melalui data cleaning terlebih dahulu. Proses ini meliputi mengimpor data, menghilangkan duplikasi pada data, memeriksa missing value, dan menangani missing value dengan rata-rata dari kolom tersebut.

- **Before Data Cleaning**
Banyak Kolom Duplikat: 31994

| Column                          | Missing Values |
|---------------------------------|----------------|
| hotel                           | 0              |
| is_canceled                     | 0              |
| lead_time                       | 0              |
| arrival_date_year               | 0              |
| arrival_date_month              | 0              |
| arrival_date_week_number        | 0              |
| arrival_date_day_of_month       | 0              |
| stays_in_weekend_nights         | 0              |
| stays_in_week_nights            | 0              |
| adults                          | 0              |
| children                        | 4              |
| babies                          | 0              |
| meal                            | 0              |
| country                         | 488            |
| market_segment                  | 0              |
| distribution_channel            | 0              |
| is_repeated_guest               | 0              |
| previous_cancellations          | 0              |
| previous_bookings_not_canceled  | 0              |
| reserved_room_type              | 0              |
| assigned_room_type              | 0              |
| booking_changes                 | 0              |
| deposit_type                    | 0              |
| agent                           | 16340          |
| company                         | 112593         |
| days_in_waiting_list            | 0              |
| customer_type                   | 0              |
| adr                             | 0              |
| required_car_parking_spaces     | 0              |
| total_of_special_requests       | 0              |
| reservation_status              | 0              |
| reservation_status_date         | 0              |

dtype: int64

- **After Data Cleaning**
Banyak Kolom Duplikat: 0

| Column                          | Missing Values |
|---------------------------------|----------------|
| hotel                           | 0              |
| is_canceled                     | 0              |
| lead_time                       | 0              |
| arrival_date_year               | 0              |
| arrival_date_month              | 0              |
| arrival_date_week_number        | 0              |
| arrival_date_day_of_month       | 0              |
| stays_in_weekend_nights         | 0              |
| stays_in_week_nights            | 0              |
| adults                          | 0              |
| children                        | 0              |
| babies                          | 0              |
| meal                            | 0              |
| country                         | 0              |
| market_segment                  | 0              |
| distribution_channel            | 0              |
| is_repeated_guest               | 0              |
| previous_cancellations          | 0              |
| previous_bookings_not_canceled  | 0              |
| reserved_room_type              | 0              |
| assigned_room_type              | 0              |
| booking_changes                 | 0              |
| deposit_type                    | 0              |
| agent                           | 0              |
| company                         | 0              |
| days_in_waiting_list            | 0              |
| customer_type                   | 0              |
| adr                             | 0              |
| required_car_parking_spaces     | 0              |
| total_of_special_requests       | 0              |
| reservation_status              | 0              |
| reservation_status_date         | 0              |

dtype: int64

- **Preview data clean**
| **Hotel**        | **Is Canceled** | **Lead Time** | **Arrival Year** | **Arrival Month** | **Week Number** | **Day of Month** | **Weekend Nights** | **Week Nights** | **Adults** | **Agent** | **Company** | **Days in Waiting List** | **Customer Type** | **ADR**  | **Car Parking Spaces** | **Special Requests** | **Reservation Status** | **Reservation Date** | **Month** |
|-------------------|-----------------|---------------|------------------|-------------------|-----------------|------------------|--------------------|-----------------|------------|-----------|-------------|-------------------------|--------------------|---------|------------------------|----------------------|------------------------|----------------------|----------|
| Resort Hotel      | 0               | 342           | 2015             | July              | 27              | 1                | 0                  | 0               | 2          | 94.138     | 183.081     | 0                       | Transient          | 0.0     | 0                      | 0                    | Check-Out             | 2015-07-01          | 7        |
| Resort Hotel      | 0               | 737           | 2015             | July              | 27              | 1                | 0                  | 0               | 2          | 94.138     | 183.081     | 0                       | Transient          | 0.0     | 0                      | 0                    | Check-Out             | 2015-07-01          | 7        |
| Resort Hotel      | 0               | 7             | 2015             | July              | 27              | 1                | 0                  | 1               | 1          | 94.138     | 183.081     | 0                       | Transient          | 75.0    | 0                      | 0                    | Check-Out             | 2015-07-02          | 7        |
| Resort Hotel      | 0               | 13            | 2015             | July              | 27              | 1                | 0                  | 1               | 1          | 304.000    | 183.081     | 0                       | Transient          | 75.0    | 0                      | 0                    | Check-Out             | 2015-07-02          | 7        |
| Resort Hotel      | 0               | 14            | 2015             | July              | 27              | 1                | 0                  | 2               | 2          | 240.000    | 183.081     | 0                       | Transient          | 98.0    | 0                      | 1                    | Check-Out             | 2015-07-03          | 7        |


*Data preview ini adalah subset dari dataset yang telah dibersihkan, dengan 33 kolom dan 5 baris pertama yang ditampilkan.*


# Explanatory Data Analysis

- **Analisis 1: Distribusi Tipe Customer**

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Distribusi_Tipe_Customer.png?raw=true)

Dari hasil visualisasi diatas, kita dapat melihat bahwa 75% dari total customer adalah tipe transient dan yang paling sedikit adalah tipe customer group

- **Analisis 2: Status Reservasi Pada Masing - Masing Hotel**

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Status_Reservasi_Perhotel.png?raw=true)
Dari hasil visualisasi kedua hotel tersebut, jumlah pembatalan tertinggi berada pada city hotel namun untuk reservasi yang terbanyak juga berada di City hotel. Dari informasi ini, kita dapat menganalisa dari tipe hotel manakah yang berkontribusi terhadap pendapatan hotel. Apakah city hotel karena tingginya jumlah reservasi? Atau malah resort hotel yang memiliki total pendapatan lebih banyak? Nanti, kita akan menganalisa pendapatan hotel di akhir.

Selanjutnya, kita akan menganalisa customer yang melakukan reservasi ulang

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Jumlah_Customer_Reservasi_Ulang.png?raw=true)

Ternyata hanya 3.19% dari total customer 119.390 yang melakukan reservasi ulang :0  Mari kita lihat lebih detail banyaknya customer yang membatalkan reservasi setiap bulannya pada masing-masing tahun
![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Status_Reservasi_Pertahun_Tiap_Hotel.png?raw=true)

- Tahun 2014: Jumlah reservasi secara keseluruhan masih relatif rendah dibandingkan tahun-tahun berikutnya. Terdapat fluktuasi yang cukup signifikan dari bulan ke bulan, namun tidak ada tren yang sangat jelas.
- Tahun 2015: Terjadi peningkatan yang signifikan pada jumlah reservasi dibandingkan tahun sebelumnya. Puncak reservasi terjadi pada bulan Juli, sementara tingkat pembatalan cenderung lebih stabil dibandingkan tahun 2014.
- Tahun 2016: Jumlah reservasi terus meningkat dan mencapai puncaknya pada tahun ini. Fluktuasi musiman juga lebih terlihat jelas, dengan puncak reservasi terjadi pada bulan-bulan tertentu. Tingkat pembatalan juga cenderung lebih tinggi dibandingkan tahun sebelumnya.
- Tahun 2017: Meskipun masih terdapat peningkatan jumlah reservasi, namun pertumbuhannya tidak secepat tahun sebelumnya. Tingkat pembatalan juga cenderung lebih tinggi, terutama pada beberapa bulan tertentu.

Berdasarkan grafik di atas, kita dapat melihat fluktuasi yang cukup signifikan pada jumlah reservasi yang berhasil dan dibatalkan setiap bulannya. Terlihat bahwa bulan Juli mengalami puncak tertinggi pada jumlah reservasi yang berhasil, sementara bulan Januari mencatatkan jumlah reservasi yang berhasil paling rendah. Tren pembatalan reservasi juga menunjukkan pola yang menarik, dengan puncak pembatalan terjadi pada bulan-bulan tertentu. Fluktuasi ini kemungkinan besar dipengaruhi oleh berbagai faktor, seperti musim liburan, event khusus, atau bahkan perubahan kebijakan perusahaan. Secara keseluruhan, grafik ini memberikan gambaran yang jelas tentang kinerja reservasi sepanjang tahun dan dapat menjadi dasar untuk melakukan analisis lebih lanjut yaitu dengan membandingkan data ini dengan data tahun sebelumnya.

- **Analisis 3: Pendapatan Pertahun dari Kedua Tipe Hotel**
![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Jumlah_Customer_Pertahun.png?raw=true)
Pendapatan resort hotel selama tiga tahun berturut - turut lebih tinggi daripada city hotel dengan puncak tertingginya pada tahun 2016. Untuk mengetahui lebih lanjut, kita akan menganalisa tipe customer manakah yang paling banyak memberikan kontribusi terhadap pendapatan hotel. Supaya lebih rinci, kita akan melakukan analisa pada resort hotel terlebih dahulu.

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Resort%20Hotel%20ADR%20Relation.png?raw=true)

Berdasarkan analisis keempat grafik untuk Resort Hotels, dapat diidentifikasi beberapa pola yang berbeda dengan City Hotels. Pada grafik pertama, segmen Transient tetap mendominasi dengan ADR tertinggi, namun terdapat perbedaan yang lebih signifikan dengan segmen lainnya, dimana Contract menempati posisi kedua, diikuti Transient-Party dan Group. Analisis lead time pada grafik kedua menunjukkan tren peningkatan ADR seiring bertambahnya waktu pemesanan, dengan median ADR yang lebih tinggi pada pemesanan 15-30 hari dan 30+ hari sebelum kedatangan. Grafik ketiga memperlihatkan korelasi positif yang lebih kuat antara jumlah special request dengan ADR, dengan outlier yang mencapai ADR 500, mengindikasikan variasi harga yang lebih lebar di resort hotels. Sementara itu, pola seasonal pada grafik keempat menunjukkan perbedaan yang sangat signifikan, dimana puncak ADR terjadi pada periode Juli-Agustus dengan nilai hampir mencapai 200, jauh lebih tinggi dibanding bulan-bulan lainnya, hal ini mencerminkan karakteristik resort yang sangat dipengaruhi oleh musim liburan.

Selain melakukan analisa pada resort hotel, kita akan melakukan analisa pada city hotel

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/City%20Hotel%20ADR%20Relation.png?raw=true)

Berdasarkan analisis dari keempat grafik pada city hotel, dapat diidentifikasi beberapa pola signifikan dalam pengelolaan hotel. Grafik pertama menunjukkan bahwa segmen Transient memiliki ADR tertinggi dibandingkan segmen lainnya, mengindikasikan kontribusi pendapatan yang lebih substansial dari tamu individual. Analisis hubungan antara lead time dengan ADR pada grafik kedua menunjukkan distribusi yang relatif stabil, meskipun terdapat beberapa outlier yang mencapai ADR 250, menandakan adanya kasus-kasus khusus dalam penetapan harga. Selanjutnya, grafik ketiga memperlihatkan korelasi positif antara jumlah special request dengan ADR, dimana peningkatan jumlah permintaan khusus berbanding lurus dengan tingkat ADR - hal ini mengindikasikan hubungan antara ekspektasi layanan dengan kesediaan membayar dari tamu. Pada grafik terakhir, terlihat pola seasonal yang jelas dimana ADR mencapai puncaknya pada periode Mei hingga September, dengan segmen Transient secara konsisten mempertahankan posisi ADR tertinggi di hampir setiap bulan, memberikan implikasi penting untuk strategi penetapan harga dan manajemen pendapatan hotel.

# Kesimpulan
lorem ipsum

## Author 👨‍💻 
- [Alviya Laela Lestari (202110370311400)](https://github.com/alviyalaela)
- [Kiara Azzahra (202110370311426)](https://github.com/xyzaraa)
