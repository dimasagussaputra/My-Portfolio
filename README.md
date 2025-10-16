# REST API Daftar Barang Cuci Sepatu

## Deskripsi Umum

Proyek ini merupakan tugas responsi untuk modul Pembuatan API dengan JavaScript. API ini dibuat menggunakan Node.js dan Express.js, berfungsi untuk mengelola data sepatu yang sedang dicuci pada sebuah layanan jasa cuci sepatu.

Tujuan utama proyek ini adalah untuk mempermudah proses pencatatan, pemantauan, dan pembaruan status cucian sepatu secara digital melalui REST API sederhana.

## Tujuan

1. Mengimplementasikan konsep CRUD (Create, Read, Update, Delete) dalam REST API.
2. Meningkatkan pemahaman penggunaan Express.js sebagai framework backend.
3. Mengelola data menggunakan format JSON sebagai penyimpanan sederhana.
4. Membangun sistem pencatatan yang relevan dengan kebutuhan bisnis nyata.

## Fitur Utama API

| Metode | Endpoint   | Deskripsi                                                                |
| ------ | ---------- | ------------------------------------------------------------------------ |
| GET    | /items     | Menampilkan seluruh daftar sepatu yang sedang dicuci.                    |
| POST   | /items     | Menambahkan data sepatu baru ke dalam daftar.                            |
| PUT    | /items/:id | Memperbarui status sepatu (misalnya dari Sedang Dicuci menjadi Selesai). |
| DELETE | /items/:id | Menghapus data sepatu yang sudah selesai dicuci.                         |

## Struktur Data

Contoh struktur data sepatu yang disimpan:

```
{
"id": 1,
"nama": "Nike Air Force 1",
"status": "Sedang Dicuci",
"tanggalMasuk": "2025-10-08",
"tanggalSelesai": "-"
}
```

Keterangan:

- id → Nomor unik sepatu
- nama → Nama sepatu atau merek pelanggan
- status → Status proses cuci (Sedang Dicuci / Selesai)
- tanggalMasuk → Tanggal sepatu diterima untuk dicuci
- tanggalSelesai → Tanggal sepatu selesai dicuci

## Bonus Fitur

API ini juga dilengkapi dengan fitur filter berdasarkan status, misalnya:
GET /items?status=Selesai
akan menampilkan hanya sepatu yang sudah selesai dicuci.

## Alur Kerja API

1. Pengguna mengirimkan permintaan HTTP (GET, POST, PUT, DELETE) ke server.
2. Server memproses permintaan menggunakan Express.js.
3. Data sepatu disimpan atau diambil dari file items.json.
4. Server mengembalikan respons dalam format JSON.

## Teknologi yang Digunakan

- Node.js – runtime environment untuk menjalankan JavaScript di sisi server.
- Express.js – framework untuk membangun REST API dengan cepat dan sederhana.
- JSON – format data utama untuk pertukaran informasi antar sistem.
- Supabase - Sebagai DB untuk deploy
- Vercel - Sebagai server

## Hasil Akhir

Dengan adanya API ini, proses pengelolaan data sepatu menjadi lebih mudah, terstruktur, dan dapat dikembangkan ke sistem front-end di masa depan, seperti dashboard berbasis web atau aplikasi mobile.
API ini juga dapat dikembangkan lebih lanjut dengan menambahkan database seperti MongoDB atau Supabase untuk penyimpanan data yang lebih kompleks.

## Contoh Request dan Response

GET /items

Response:

```
[
{
"id": 1,
"nama": "Converse Chuck Taylor",
"status": "Selesai",
"tanggalMasuk": "2025-10-01",
"tanggalSelesai": "2025-10-03"
}
]

```

Body:
POST /items

```
{
"nama": "Nike Air Max",
"status": "Sedang Dicuci",
"tanggalMasuk": "2025-10-08",
"tanggalSelesai": "-"
}
```

Response:

```
{
"message": "Data sepatu berhasil ditambahkan."
}



```

PUT /items/:id
Body:

```
{
"status": "Selesai",
"tanggalSelesai": "2025-10-09"
}
```

```
Response:
{
"message": "Status sepatu berhasil diperbarui."
}
```

DELETE /items/:id
Response:

```
{
"message": "Data sepatu berhasil dihapus."
}
```

## Notes

Praktikan diharapkan mengupload repository dan deploy API ke Vercel. Jangan lupa berikan penjelasan dengan README.md
