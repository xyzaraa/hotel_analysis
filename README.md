
# 🛎️ Hotel Booking Analysis 🏨

# Project Overview

Project ini bertujuan untuk menganalisis data reservasi hotel yang dapat digunakan untuk eksplorasi faktor penentu keberhasilan manajemen hotel serta tren dan perilaku konsumen. Faktor ini dapat menghasilkan pola-pola tertentu yang dapat membantu manajer hotel atau pihak terkait untuk meningkatkan tingkat pemesanan/reservasi konsumen.

Tujuan utama dari project ini adalah memberikan wawasan untuk pengambilan keputusan yang lebih terinformasi terkait pemesanan kamar dan strategi pemasaran

## Analysis Plan
1. Data Cleaning
Missing value akan dibersihkan, memastikan format sudah sesuai (date, categorical, dan numerical), serta memfilter data berdasarkan reservasi yang tidak dibatalkan(is_canceled == 0).
2. Explanatory Data Analysis
Data yang sudah bersih akan dikelompokkan berdasarkan bulan, tahun, tipe hotel dan lain-lain untuk memahami pola pendapatan.
3. Visualisasi
Relasi antar data akan divisualisasikan untuk memberikan pemahaman yang advanced. Hal ini akan menghasilkan pandangan yang lebih luas kepada pihak terkait agar lebih mudah mengambil keputusan.
4. Analisis Tren
Identifikasi saat dimana jumlah reservasi meningkat atau meerndah untuk masing-masing tipe hotel, serta evaluasi kemungkinan faktor penyebab (misalnya musim liburan atau perbedaan target konsumen).

## Analytical Approaches and Techniques
1. Statistik Deskriptif: Menghitung nilai rata-rata Average Daily Rate (ADR) tiap tipe hotel perbulan.
2. Visualisasi Data: Menggunakan teknik visual seperti bar plot untuk menyajikan pola bulanan dengan mudah dipahami.
3. Segmentasi Berdasarkan Tipe Hotel: Membandingkan pola pendapatan antara Resort Hotel dan City Hotel, sehingga dapat memberikan wawasan tentang preferensi konsumen untuk kedua tipe ini.

## Benefits and Implications of Analysis
1. Pengelola Hotel: Dapat menentukan strategi promosi atau penyesuaian harga berdasarkan musim tinggi (high season) dan musim rendah (low season). Misalnya, memberikan diskon di bulan dengan ADR rendah atau meningkatkan penawaran layanan di musim ramai.
2. Wisatawan: Mendapatkan wawasan tentang waktu terbaik untuk memesan hotel dengan harga lebih terjangkau.
3. Peneliti dan Data Analis: Mendapatkan pola tren data hotel yang relevan untuk referensi studi atau laporan.


# Installation
**Instal dependencies:**
   Instal library yang dibutuhkan dengan menjalankan perintah berikut:
   ```bash
   pip install matplotlib numpy pandas seaborn plotly
   ```
   Tambahan library:
   - Mount Google Drive (khusus untuk Google Colab):
     ```python
     from google.colab import drive
     drive.mount('/content/drive')
     ```



# Dataset Overview

Dataset yang digunakan dalam project ini berasal dari [Hotel booking demand datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191#f0010). Dataset ini mendeskripsikan dua dataset dengan data demand hotel. Terdapat dua jenis hotel, yaitu Resort Hotel dan City Hotel. Kedua dataset memiliki struktur yang sama, dengan 31 variable dan merepresentasikan reservasi antara 1 juli 2015 hingga 31 Agustus 2017, termasuk reservasi yang dibatalkan ataupun yang berhasil.

Berikut adalah informasi umum pada dataframe:

RangeIndex: 119390 entries, 0 to 119389

Data columns (total 32 columns):
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
  
| hotel         | is_canceled | lead_time | arrival_date_year | arrival_date_month | arrival_date_week_number | arrival_date_day_of_month | stays_in_weekend_nights | stays_in_week_nights | adults | ... | agent   | company  | days_in_waiting_list | customer_type | adr        | required_car_parking_spaces | total_of_special_requests | reservation_status | reservation_status_date | month |
|---------------|-------------|-----------|-------------------|---------------------|--------------------------|---------------------------|------------------------|----------------------|--------|-----|---------|----------|----------------------|---------------|------------|----------------------------|---------------------------|-------------------|--------------------------|-------|
| Resort Hotel  | 0           | 342       | 2015              | July                | 27                       | 1                         | 0                      | 0                    | 2      | ... | 94.138  | 183.081  | 0                    | Transient     | 0.0        | 0                          | 0                         | Check-Out         | 2015-07-01               | 7     |
| Resort Hotel  | 0           | 737       | 2015              | July                | 27                       | 1                         | 0                      | 0                    | 2      | ... | 94.138  | 183.081  | 0                    | Transient     | 0.0        | 0                          | 0                         | Check-Out         | 2015-07-01               | 7     |
| Resort Hotel  | 0           | 7         | 2015              | July                | 27                       | 1                         | 0                      | 1                    | 1      | ... | 94.138  | 183.081  | 0                    | Transient     | 75.0       | 0                          | 0                         | Check-Out         | 2015-07-02               | 7     |
| Resort Hotel  | 0           | 13        | 2015              | July                | 27                       | 1                         | 0                      | 1                    | 1      | ... | 304.000 | 183.081  | 0                    | Transient     | 75.0       | 0                          | 0                         | Check-Out         | 2015-07-02               | 7     |
| Resort Hotel  | 0           | 14        | 2015              | July                | 27                       | 1                         | 0                      | 2                    | 2      | ... | 240.000 | 183.081  | 0                    | Transient     | 98.0       | 0                          | 1                         | Check-Out         | 2015-07-03               | 7     |

*Data preview ini adalah subset dari dataset yang telah dibersihkan, dengan 33 kolom dan 5 baris pertama yang ditampilkan.*


# Explanatory Data Analysis

- **Analisis 1: **

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/ADR_Month.png?raw=true)



- **Analisis 2:**

![image](https://github.com/xyzaraa/hotel_analysis/blob/main/Assets/Reservation_Status_Month.png?raw=true)

Dari grafik tersebut diketahui bahwa bulan Agustus menjadi high season hotel. Di bulan ini, jumlah reservasi paling tinggi dan jumlah pembatalan rendah. Sebaliknya, pada bulan Januari jumlah reservasi paling rendah, tetapi jumlah pembatalan paling tinggi.

## Author 👨‍💻 
- [Alviya Laela Lestari (202110370311400)](https://github.com/alviyalaela)
- [Kiara Azzahra (202110370311426)](https://github.com/xyzaraa)
