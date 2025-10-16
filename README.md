# REST API Daftar Barang Cuci Sepatu

## Deskripsi Umum Proyek

Proyek ini adalah tugas responsi untuk modul 1 praktikum PPB Pembuatan API dengan JavaScript. API ini dibuat menggunakan Node.js dan Express.js, berfungsi untuk mengelola data sepatu yang sedang dicuci pada sebuah layanan jasa cuci sepatu.

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

## Request dan Response

Body:
POST /api/items
```
{
"nama": "Adidas Superstar White",
"status": "Sedang Dicuci",
"tanggalMasuk": "2025-10-16",
"tanggalSelesai": "-"
}
```
Response:
```
{
    "message": "Data sepatu berhasil ditambahkan.",
    "sepatu": {
        "id": "382afb38-64da-458a-ad29-eb761b64429c",
        "nama": "Adidas Superstar White",
        "status": "Sedang Dicuci",
        "tanggalMasuk": "2025-10-16",
        "tanggalSelesai": "-"
    }
}
```

Body:
GET /api/items
```
{
"nama": "Adidas Superstar White",
"status": "Sedang Dicuci",
"tanggalMasuk": "2025-10-16",
"tanggalSelesai": "-"
}
```
Response:
```
[
    {
        "id": "382afb38-64da-458a-ad29-eb761b64429c",
        "nama": "Adidas Superstar White",
        "status": "Sedang Dicuci",
        "tanggalMasuk": "2025-10-16",
        "tanggalSelesai": "-"
    }
]
```

Body:
PUT /api/items/:id
```
{
  "status": "Selesai",
  "tanggalSelesai": "2025-10-18"
}
```
Response:
```
{
    "message": "Status sepatu berhasil diperbarui.",
    "updated": {
        "id": "382afb38-64da-458a-ad29-eb761b64429c",
        "nama": "Adidas Superstar White",
        "status": "Selesai",
        "tanggalMasuk": "2025-10-16",
        "tanggalSelesai": "2025-10-18"
    }
}
```

GET /api/items?status=Selesai
Response:
```
[
    {
        "id": "382afb38-64da-458a-ad29-eb761b64429c",
        "nama": "Adidas Superstar White",
        "status": "Selesai",
        "tanggalMasuk": "2025-10-16",
        "tanggalSelesai": "2025-10-18"
    }
]
```

Body:
DELETE /api/items/:id
```
{
  "status": "Selesai",
  "tanggalSelesai": "2025-10-18"
}
```
Response:
```
{
    "message": "Data sepatu berhasil dihapus."
}
```

## Langkah Instalasi dan Cara Menjalankan API

1. Langkah pertama yaitu pembuatan API, dengan cara kunjungi situs web Supabase (https://supabase.com/) dan daftar atau masuk ke akun.
2. Buat proyek baru, lalu klik "New Project" atau "New Organization", kemudian isi nama proyek DaftarBarangCuciSepatu, password database, kemudian pilih region yang sesuai misalnya Singapore, lalu klik Create Project.
3. Setelah berhasil membuat proyek baru di Supabase, buka SQL Editor melalui ikon di sidebar, lalu klik "+ New query" untuk mulai membuat tabel menggunakan SQL.
5. Salin skema SQL berikut ke dalam editor, lalu klik RUN. Ini akan membuat satu tabel utama bernama sepatu untuk menyimpan data sepatu laundry.
   ```
   create table sepatu (
      id uuid primary key default gen_random_uuid(),
      nama text not null,
      status text check (status in ('Sedang Dicuci', 'Selesai')) default 'Sedang Dicuci',
      "tanggalMasuk" date not null,
      "tanggalSelesai" text default '-'
   );
   ```
6. Verifikasi tabel di Table Editor setelah query berhasil dijalankan, buka Table Editor dari sidebar kiri. Pastikan tabel sepatu sudah terbentuk serta periksa struktur kolom dan pastikan kolom id, nama, status, tanggalMasuk dan tanggalSelesai sudah terlihat.
7. Dapatkan kredensial API dengan masuk ke Project Settings, lalu pilih Data API untuk menyalin Project URL, dan buka API Keys untuk menyalin anon public key sebagai nilai SUPABASE_URL dan SUPABASE_KEY yang akan digunakan pada konfigurasi selanjutnya
8. Buat folder proyek baru di direktori lokal, lalu beri nama proyek Daftar-Barang-Cuci-Sepatu.
9. Buka terminal atau command prompt di dalam folder tersebut.
10. Jalankan perintah berikut untuk menginisialisasi proyek Node.js dan membuat file package.json.
    ```
    npm init -y
    ```
11. Sekarang, pasang semua pustaka yang dibutuhkan untuk proyek. Pustaka ini diperlukan untuk menjalankan server, terhubung ke Supabase, dan mengelola variabel lingkungan.
    ```
    npm install @supabase/supabase-js dotenv express
    npm install --save-dev nodemon
    ```
12. Masuk ke Visual Studio Code dengan mengetikan code . di terminal atau command prompt.
13. Buat struktur folder dan file src-nya.
14. Tambahkan kode ini ke src/config/supabaseClient.js. File ini akan menginisialisasi klien Supabase menggunakan kredensial dari file .env.
    ```
    import dotenv from "dotenv";
    import { createClient } from "@supabase/supabase-js";
    
    dotenv.config();
    
    const supabaseUrl = process.env.SUPABASE_URL;
    const supabaseKey = process.env.SUPABASE_KEY;
    
    export const supabase = createClient(supabaseUrl, supabaseKey);
    ```
15. Tambahkan kode ini ke dalam folder src/models, yaitu src/models/sepatuModel.js.
    ```
    import { supabase } from "../config/supabaseClient.js";
    
    export const SepatuModel = {
        async getAll(status) {
            let query = supabase.from("sepatu").select("*").order("tanggalMasuk", { ascending: false });
            if (status) query = query.eq("status", status);
            const { data, error } = await query;
            if (error) throw error;
            return data;
        },
    
        async getById(id) {
            const { data, error } = await supabase.from("sepatu").select("*").eq("id", id).single();
            if (error) throw error;
            return data;
        },
    
        async create(payload) {
            const { data, error } = await supabase.from("sepatu").insert([payload]).select().single();
            if (error) throw error;
            return data;
        },
    
        async update(id, payload) {
            const { data, error } = await supabase.from("sepatu").update(payload).eq("id", id).select().single();
            if (error) throw error;
            return data;
        },
    
        async remove(id) {
            const { error } = await supabase.from("sepatu").delete().eq("id", id);
            if (error) throw error;
            return { message: "Data sepatu berhasil dihapus." };
        },
    };
    ```
16. Tambahkan kode ini ke dalam folder src/controllers, yaitu src/controllers/sepatuController.js.
    ```
    import { SepatuModel } from "../models/sepatuModel.js";
    
    export const SepatuController = {
        async getAll(req, res) {
            try {
                const { status } = req.query;
                const sepatu = await SepatuModel.getAll(status);
                res.json(sepatu);
            } catch (err) {
                res.status(500).json({ error: err.message });
            }
        },
    
        async getById(req, res) {
            try {
                const sepatu = await SepatuModel.getById(req.params.id);
                res.json(sepatu);
            } catch (err) {
                res.status(404).json({ error: err.message });
            }
        },
    
        async create(req, res) {
            try {
                const sepatu = await SepatuModel.create(req.body);
                res.status(201).json({ message: "Data sepatu berhasil ditambahkan.", sepatu });
            } catch (err) {
                res.status(400).json({ error: err.message });
            }
        },
    
        async update(req, res) {
            try {
                const updated = await SepatuModel.update(req.params.id, req.body);
                res.json({ message: "Status sepatu berhasil diperbarui.", updated });
            } catch (err) {
                res.status(400).json({ error: err.message });
            }
        },
    
        async remove(req, res) {
            try {
                const result = await SepatuModel.remove(req.params.id);
                res.json(result);
            } catch (err) {
                res.status(400).json({ error: err.message });
            }
        },
    };
    ```
17. Tambahkan kode ini ke dalam folder src/routes, yaitu src/routes/sepatuRoutes.js.
    ```
    import express from "express";
    import { SepatuController } from "../controllers/sepatuController.js";
    
    const router = express.Router();
    
    router.get("/", SepatuController.getAll);
    router.get("/:id", SepatuController.getById);
    router.post("/", SepatuController.create);
    router.put("/:id", SepatuController.update);
    router.delete("/:id", SepatuController.remove);
    
    export default router;
    ```
18. Tambahkan kode ini ke dalam folder src/routes, yaitu src/routes/sepatuItems.js.
    ```
    import express from "express";
    import { SepatuModel } from "../models/sepatuModel.js";
    
    const router = express.Router();
    
    router.get("/", async (req, res) => {
        try {
            const { status } = req.query;
            const sepatu = await SepatuModel.getAll(status);
            res.json(sepatu);
        } catch (error) {
            res.status(500).json({ error: error.message });
        }
    });
    
    export default router;
    ```
19. Tambahakan kode berikut ke src/index.js. Ini adalah file utama yang akan menjalankan server.
    ```
    import express from "express";
    import dotenv from "dotenv";
    import sepatuRoutes from "./routes/sepatuRoutes.js";
    
    dotenv.config();
    
    const app = express();
    app.use(express.json());
    
    app.use("/api/items", sepatuRoutes);
    
    const port = process.env.PORT || 3000;
    app.listen(port, () => {
        console.log(`Server running on port ${port}`);
    });
    ```
20. Buat file .env di direktori root proyek yaitu file template untuk kredensial. Masukkan Project URL dan anon public key yang telah diperoleh sebelumnya ke dalam file .env dengan menuliskan nilainya masing-masing pada variabel SUPABASE_URL dan SUPABASE_KEY.
    ```
    SUPABASE_URL=https://tcepzrpobtyynosfsmrl.supabase.co
    SUPABASE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InRjZXB6cnBvYnR5eW5vc2ZzbXJsIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjA1MjU1NDgsImV4cCI6MjA3NjEwMTU0OH0.srAGuabfK8l8d8R8_hXvuZw4_cNT2yOBI6cutzThVY8
    PORT=3002
    ```
21. Buat file .gitignore di direktori root proyek yaitu file yang akan memastikan file sensitif tidak diunggah ke repositori.
    ```
    .env
    /node_modules
    ```
22. Pastikan file package.json memiliki konfigurasi seperti berikut untuk menjalankan proyek.
    ```
    {
      "name": "sepatu-laundry-api",
      "version": "1.0.0",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "start": "node src/index.js",
        "dev": "nodemon src/index.js"
      },
      "dependencies": {
        "@supabase/supabase-js": "^2.75.0",
        "dotenv": "^17.2.3",
        "express": "^5.1.0"
      },
      "devDependencies": {
        "nodemon": "^3.1.10"
      },
      "description": "",
      "keywords": [],
      "author": "",
      "license": "ISC"
    }
    ```
23. Tambahkan source code berikut kedalam vercel.json.
    ```
    {
        "version": 2,
        "builds": [
            {
                "src": "src/index.js",
                "use": "@vercel/node"
            }
        ],
        "routes": [
            {
                "src": "/(.*)",
                "dest": "src/index.js"
            }
        ]
    }
    ```
24. Buka terminal di folder proyek dan jalankan perintah npm run dev. Jika berhasil, maka akan melihat pesan seperti "Server running on port 3002".
25. Saatnya pengujian POST api/items. Disini kita perlu memasukkan source code-nya lalu masukkan dalam body raw JSON.
    ```
    {
    "nama": "Nike Air Force 1",
    "status": "Sedang Dicuci",
    "tanggalMasuk": "2025-10-16",
    "tanggalSelesai": "-"
    }
    ```
    Maka akan ada body respond dibawahnya jika berhasil.
    ```
    {
        "message": "Data sepatu berhasil ditambahkan.",
        "sepatu": {
            "id": "2bd2e0f3-fe89-4a95-9a52-ccef0fc38fe4",
            "nama": "Nike Air Force 1",
            "status": "Sedang Dicuci",
            "tanggalMasuk": "2025-10-16",
            "tanggalSelesai": "-"
        }
    }
    ```
26. Selanjutnya pengujian GET api/items. Disini kita perlu memasukkan source code-nya lalu masukkan dalam body raw JSON.
    ```
    {
    "nama": "Nike Air Force 1",
    "status": "Sedang Dicuci",
    "tanggalMasuk": "2025-10-16",
    "tanggalSelesai": "-"
    }
    ```
    Maka akan ada body respond dibawahnya jika berhasil.
    ```
    [
        {
            "id": "2bd2e0f3-fe89-4a95-9a52-ccef0fc38fe4",
            "nama": "Nike Air Force 1",
            "status": "Sedang Dicuci",
            "tanggalMasuk": "2025-10-16",
            "tanggalSelesai": "-"
        }
    ]
    ```
27. Selanjutnya pengujian PUT api/items/:id, dengan id yang didapat dari id hasil respond GET api/items. Disini kita perlu memasukkan source code-nya lalu masukkan dalam body raw JSON.
    ```
    {
      "status": "Selesai",
      "tanggalSelesai": "2025-10-18"
    }
    ```
    Maka akan ada body respond dibawahnya jika berhasil.
    ```
    {
        "message": "Status sepatu berhasil diperbarui.",
        "updated": {
            "id": "2bd2e0f3-fe89-4a95-9a52-ccef0fc38fe4",
            "nama": "Nike Air Force 1",
            "status": "Selesai",
            "tanggalMasuk": "2025-10-16",
            "tanggalSelesai": "2025-10-18"
        }
    }
    ```
28. Selanjutnya pengujian GET /items?status=Selesai, yaitu fitur filter berdasarkan status yang akan menampilkan hanya sepatu yang sudah selesai dicuci. Maka akan ada body respond dibawahnya jika berhasil.
    ```
    [
        {
            "id": "2bd2e0f3-fe89-4a95-9a52-ccef0fc38fe4",
            "nama": "Nike Air Force 1",
            "status": "Selesai",
            "tanggalMasuk": "2025-10-16",
            "tanggalSelesai": "2025-10-18"
        }
    ]
    ```
29. Selanjutnya pengujian DELETE api/items/:id, dengan id yang didapat dari id hasil respond PUT api/items. Disini kita perlu memasukkan source code-nya lalu masukkan dalam body raw JSON.
    ```
    {
      "status": "Selesai",
      "tanggalSelesai": "2025-10-18"
    }
    ```
    Maka akan ada body respond dibawahnya jika berhasil.
    ```
    {
        "message": "Data sepatu berhasil dihapus."
    }
    ```
30. Kemudian melakukan deployment API, dengan cara unggah Proyek ke Repositori Git, lalu login ke Vercel dan buka https://vercel.com/.
31. Buka dashboard lalu klik "Add New...", pilih "Project", cari repositori tempat kode API disimpan, dan klik "Import".
32. Setelah repositori berhasil di import, Vercel akan mendeteksi proyek sebagai Node.js dan otomatis mengatur Framework Preset ke "Other", serta pastikan Root Directory sesuai dengan lokasi kode Anda.
33. Selanjutnya, pada bagian Environment Variables, tambahkan kredensial Supabase dengan membuat variabel SUPABASE_URL berisi Project URL dan variabel SUPABASE_KEY berisi anon key, lalu klik Add untuk menyimpan.
34. klik "Deploy" setelah menambahkan variabel lingkungan, lalu tunggu proses build berjalan hingga selesai dengan log yang dapat dipantau secara real-time.
35. Kemudian, setelah deployment berhasil, Vercel akan menampilkan URL publik yang bisa diakses melalui tombol "Visit".
36. Terakhir, lakukan verifikasi API dengan menguji endpoint melalui browser atau Postman menggunakan URL publik yang diberikan, misalnya https://daftar-barang-cuci-sepatu-2lar-284lqek3b.vercel.app/api/items untuk memastikan API berjalan dengan benar dan menampilkan data JSON dari Supabase.

## Link deploy (Vercel)

https://daftar-barang-cuci-sepatu-2lar-284lqek3b.vercel.app/api/items

## Hasil Akhir

Dengan adanya API ini, proses pengelolaan data sepatu menjadi lebih mudah, terstruktur, dan dapat dikembangkan ke sistem front-end di masa depan, seperti dashboard berbasis web atau aplikasi mobile.
API ini juga dapat dikembangkan lebih lanjut dengan menambahkan database seperti MongoDB atau Supabase untuk penyimpanan data yang lebih kompleks.
