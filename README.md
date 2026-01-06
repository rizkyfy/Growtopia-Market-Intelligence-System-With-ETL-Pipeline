# Growtopia Market Intelligence System

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![ETL Pipeline](https://img.shields.io/badge/Method-ETL_Pipeline-green?style=for-the-badge)
![Data Analysis](https://img.shields.io/badge/Focus-Market_Economy-orange?style=for-the-badge)

> **Sistem Analisis Ekonomi & Sentimen Pasar Otomatis menggunakan Metode ETL (Extract, Transform, Load).**

---

## Tentang Project
Sistem ini tidak bekerja secara manual, melainkan menggunakan pipeline **ETL** untuk mengolah ribuan baris data percakapan (*chat logs*) dari server Discord komunitas jual-beli. Hasil akhirnya adalah laporan **Supply & Demand** yang akurat untuk menentukan apakah sebuah item sedang *High Demand* (banyak dicari) atau *Oversupply* (banjir stok).

### Fitur Utama

* **Automated Parsing:** Mengubah data mentah (JSON) dari ribuan pesan menjadi data terstruktur dalam hitungan detik.
* **Smart Item Recognition:** Menggunakan algoritma *Dictionary Lookup* (via `Items.txt`) untuk mengenali nama item secara presisi dan membuang *spam/noise*.
* **Supply vs Demand Analysis:** Secara otomatis mengklasifikasikan pesan ke dalam kategori **Buy** (Permintaan) atau **Sell** (Penawaran) menggunakan *Keyword Intent Classification*.
* **Market Sentiment Indicator:** Memberikan status otomatis pada item (contoh: `>> HIGH DEMAND <<` atau `>> STABIL <<`) berdasarkan rasio pembeli dan penjual.
* **Time-Series Filtering:** Mampu memfilter data berdasarkan rentang waktu tertentu (misal: 24 jam terakhir) untuk analisis *real-time*.

---

## Tech Stack & Tools

Project ini dibangun menggunakan teknologi berikut:

* **Programming Language:** [Python](https://www.python.org/) (Data Processing & Logic)
* **Data Extraction:** [DiscordChatExporter](https://github.com/Tyrrrz/DiscordChatExporter) (Untuk mengambil raw data chat)
* **Data Format:** JSON (Input) & TXT (Report Output)
* **Libraries:** `json`, `datetime` (Standard Library, tanpa instalasi berat).

---

## Prasyarat (Prerequisites)

Sebelum menjalankan sistem ini, pastikan Anda memiliki:

1.  **Python 3.x** terinstall di komputer Anda.
2.  **DiscordChatExporter** (CLI atau GUI) untuk mengambil data chat.
    * *Credit:* Tool ini dibuat oleh [Tyrrrz](https://github.com/Tyrrrz/DiscordChatExporter). Silakan unduh di repository resminya.
3.  **File Database Item (`Items.txt`)**: Daftar nama item Growtopia (Format: `ID|Name`).

---

## Cara Penggunaan (How to Run)

Ikuti langkah-langkah berikut:

### Langkah 1: Extract Data (Ambil Data Chat)
Gunakan **DiscordChatExporter** untuk mengambil history chat dari channel jual-beli Discord.
* **Penting:** Export file dalam format **JSON**.
* Simpan file tersebut dengan nama `data_chat.json` di dalam folder project ini.

### Langkah 2: Konfigurasi Script
Buka file `filter_items_pro.py` dan sesuaikan konfigurasi jika perlu (misalnya tanggal filter):

```python
FILE_CHAT   = 'data_chat.json' #Bisa Di edit sesuaikan data yang udah di scrap dari discord
FILE_ITEMS  = 'Items.txt' #growtopia source
FILE_OUTPUT = 'laporan_supply_demand.txt' # Ini hasil output yang akan keluar
