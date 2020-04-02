# Implementasi Algoritma Rekomendasi Menggunakan KNIME

Oleh : Alifa Izzan

## Daftar Isi

- [Implementasi Algoritma Rekomendasi Menggunakan KNIME](#implementasi-algoritma-rekomendasi-menggunakan-knime)
  - [Daftar Isi](#daftar-isi)
  - [Preproses Workflow](#preproses-workflow)
    - [Mengubah Node Server KNIME](#mengubah-node-server-knime)
  - [CRISP-DM](#crisp-dm)
    - [Bussiness Understanding](#bussiness-understanding)
    - [Data Understanding](#data-understanding)
    - [Data Preparation](#data-preparation)
    - [Modeling](#modeling)
    - [Evaluation](#evaluation)
    - [Deployment](#deployment)
  - [Pengujian Node dan Kesimpulan Pengujian](#pengujian-node-dan-kesimpulan-pengujian)
    - [Pengujian Node](#pengujian-node)
    - [Kesimpulan](#kesimpulan)

## Preproses Workflow

### Mengubah Node Server KNIME

- Pertama unduh file workflow dari web dan lakukan migrasi
- Ikuti petunjuk wizard
- Tampilan workflow awal
![workflow](assets/knimeworkflow.png)
- Lalukan setting untuk mengarahkan ratings.csv dan movies.csv jangan lupa file reader pada node sorting untuk di setting juga.
- Buka komponen ask user...
![edit1](assets/editworkflow1.png)
- di dalam komponen tersebut ubah menjadi seperti ini:
![edit2](assets/editworkflow2.png)
- pada kali ini kita pakai file temporary bernama inputrating.csv dan tambahkan wait node  untuk menunggu 1 menit untuk menunggu input dari user


## CRISP-DM

![crispi](assets/crispdm.jpg)

### Bussiness Understanding

Pada kali ini dibutuhkan rekomendasi film untuk pengguna web agar meningkatkan penggunaan layanan.

### Data Understanding
### Data Preparation
### Modeling
### Evaluation


### Deployment

Interface yang bisa digunakan adalah sebagai berikut:


## Pengujian Node dan Kesimpulan Pengujian

### Pengujian Node

Pada workflow disebutkan bahwa terdapat dua cara untuk membaca data, pertama menggunakan node CSVtoSpark dan node File Reader. Untuk itu diperlukan pengujian waktu dalam penggunaan kedua node tersebut. Kedua node diuji untuk membaca tabel ratings.csv

Untuk menguji node menggunakan workflow dibawah ini:
![benchmark](assets/benchmark1.png)

- Pertama konfigurasi masing masing node untuk melakukan pembacaan
![benchmark2](assets/benchmark2.png)
- Lalu tekan tombol execute pada node timer untuk csvtospark
![benchmark3](assets/benchmark3.png)
- Hasilnya adalah:
![result1](assets/resultbenchmark1.png)
- Pada CSVtoSpark membutuhkan total waktu: **73,36 detik**

- Untuk pengujian File Reader siapkan stopwatch
![benchmark4](assets/benchmark4.png)
-  browse file ratings.csv dan mulai stopwatch
![benchmark5](assets/benchmark5.png)
- stop ketika dataframe muncul pada interface
![resultbenchmark2](assets/resultbenchmark2.png)
- selanjutnya execute node timer
![benchmark6](assets/benchmark6.png)
- hasilnya adalah:
![resultbenchmark3](assets/resultbenchmark3.png)
- File Reader membutuhkan total waktu **378,531 detik** setelah ditambah waktu yang manual dihitung dengan stopwatch

### Kesimpulan

| Node | Waktu |
| :--- | :---- |
| CSVtoSpark | 73,36 |
| File Reader | 378,531 |

Kedua metode telah diuji menggunakan kombinasi fitur Timer Info dan pengukuran manual. kombinasi tersebut diperlukan untuk melakukan pengukuran proses setting yang membutuhan membaca data yang tidak masuk kedalam node Timer Info pada node File Reader karena proses tersebut membutuhkan waktu yang cukup signifikan. Dan akan adil karena saya juga mengukur proses pembuatan Environtment Big Data. tentunya pengukuran manual memiliki deviasi +- 1 detik error.

Kesimpulan yang didapat node CSVtoSpark lebih cepat **502%** dengan error **+- 1%** pada pengujian kali ini.

Workflow pengujian dapat dilihat pada Benchmark.knwf