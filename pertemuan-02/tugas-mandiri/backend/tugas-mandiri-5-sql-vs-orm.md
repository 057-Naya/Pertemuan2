# Tugas Mandiri 5 – Perbandingan Raw SQL dan ORM

**Nama:** NURULMAUDY Apriyani  
**NIM:** 2024520057  
**Prodi:** Informatika  
**Universitas:** Universitas Madura  

## A. Operasi yang Digunakan

Pada tugas ini digunakan operasi **menambahkan data (INSERT)** ke dalam tabel `jadwal`.

Contoh data yang akan ditambahkan:

- `id`: 1
- `mata_kuliah`: Pemrograman Web
- `hari`: Senin
- `jam`: 08:00

Tujuannya adalah membandingkan cara menambahkan data menggunakan **Raw SQL** dengan menggunakan **ORM**.

## B. Raw SQL

Raw SQL adalah cara mengakses database dengan menuliskan perintah SQL secara langsung.

### Query SQL

```sql
INSERT INTO jadwal (id, mata_kuliah, hari, jam)
VALUES (?, ?, ?, ?);
```

Tanda `?` digunakan sebagai parameter agar data tidak langsung digabungkan ke dalam query SQL.

### Contoh Menggunakan Node.js mysql2

```javascript
const [result] = await db.execute(
  `INSERT INTO jadwal (id, mata_kuliah, hari, jam)
   VALUES (?, ?, ?, ?)`,
  [1, 'Pemrograman Web', 'Senin', '08:00']
);
```

Pada contoh tersebut, perintah SQL ditulis secara langsung. Nilai data diberikan melalui parameter secara terpisah.

## C. ORM

ORM (Object Relational Mapping) memungkinkan programmer berinteraksi dengan database menggunakan objek dan method yang tersedia pada ORM, tanpa harus menulis query SQL secara langsung.

### Contoh Menggunakan Prisma

```javascript
const jadwal = await prisma.jadwal.create({
  data: {
    id: 1,
    mata_kuliah: 'Pemrograman Web',
    hari: 'Senin',
    jam: '08:00'
  }
});
```

Pada Prisma, proses penambahan data dilakukan menggunakan method `create()`. Programmer cukup menentukan tabel dan data yang ingin dimasukkan.

## D. Perbandingan Raw SQL dan ORM

| Aspek | Raw SQL | ORM |
|---|---|---|
| Cara penulisan | Menulis query SQL secara langsung | Menggunakan method dan objek |
| Penambahan data | Menggunakan `INSERT INTO` | Menggunakan method seperti `create()` |
| Kemudahan | Membutuhkan pemahaman SQL | Lebih mudah bagi programmer yang terbiasa dengan bahasa pemrograman |
| Kontrol query | Lebih bebas dan detail | Lebih banyak ditangani oleh ORM |
| Keamanan | Harus menggunakan parameter query dengan benar | Umumnya membantu menangani parameterisasi |
| Kode program | Lebih dekat dengan database | Lebih dekat dengan struktur kode aplikasi |

## E. Jawaban Pertanyaan


### 1. Apa perbedaan cara menulis query langsung menggunakan SQL dengan menggunakan ORM?

Pada Raw SQL, programmer harus menulis perintah SQL secara langsung, seperti `INSERT INTO`, `SELECT`, `UPDATE`, dan `DELETE`. Programmer perlu memahami sintaks SQL dan struktur tabel database.

Sedangkan pada ORM, programmer menggunakan method atau fungsi yang sudah disediakan oleh library ORM. Contohnya pada Prisma, penambahan data dilakukan dengan `prisma.jadwal.create()`. Jadi, programmer dapat berinteraksi dengan database menggunakan struktur kode pemrograman tanpa menulis query SQL secara langsung.


### 2. Apa kelebihan Raw SQL dibandingkan ORM?

Kelebihan utama Raw SQL adalah programmer memiliki kontrol yang lebih besar terhadap query yang dijalankan. Programmer dapat membuat query yang spesifik dan kompleks sesuai kebutuhan database.

Raw SQL juga cocok digunakan ketika membutuhkan query dengan optimasi tertentu atau fitur database yang belum didukung dengan baik oleh ORM. Selain itu, karena query ditulis secara langsung, programmer dapat melihat dengan jelas perintah yang akan dijalankan pada database.


### 3. Apa kelebihan ORM dibandingkan Raw SQL?

ORM membuat proses pengembangan aplikasi menjadi lebih sederhana karena programmer tidak harus menulis query SQL untuk setiap operasi database. Programmer dapat menggunakan method seperti `create()`, `findMany()`, `update()`, dan `delete()`.

ORM juga membuat kode program lebih mudah dibaca dan lebih terstruktur karena operasi database dapat ditulis dengan gaya yang sesuai dengan bahasa pemrograman yang digunakan. Selain itu, ORM biasanya membantu dalam pengelolaan parameter query dan mengurangi risiko kesalahan dalam penulisan SQL.


### 4. Apa yang dimaksud dengan SQL Injection dan apa dampaknya?

SQL Injection adalah serangan yang terjadi ketika input dari pengguna dimasukkan ke dalam query SQL tanpa pengamanan yang benar. Penyerang dapat memasukkan perintah SQL tertentu sehingga query yang dijalankan oleh aplikasi berubah dari tujuan awal.

Dampaknya dapat berupa akses terhadap data yang tidak seharusnya dilihat, perubahan data, penghapusan data, bahkan kerusakan atau pengambilalihan database apabila sistem memiliki kerentanan yang serius.

### 5. Mengapa penggunaan parameter query dapat mengurangi risiko SQL Injection?

Parameter query memisahkan antara **perintah SQL** dengan **data yang diberikan oleh pengguna**. Data yang dimasukkan tidak dianggap sebagai bagian dari perintah SQL.

Contohnya:

```javascript
const [result] = await db.execute(
  `INSERT INTO jadwal (id, mata_kuliah, hari, jam)
   VALUES (?, ?, ?, ?)`,
  [1, 'Pemrograman Web', 'Senin', '08:00']
);
```

Nilai data diberikan melalui parameter `?`, sehingga apabila data berisi karakter atau perintah SQL tertentu, database akan memperlakukannya sebagai data dan bukan sebagai perintah SQL tambahan.


### 6. Bagaimana ORM membantu programmer dalam mengakses database? Kaitkan dengan contoh kode.

ORM membantu programmer dengan menyediakan method yang dapat digunakan untuk melakukan operasi database melalui kode program. Programmer tidak perlu menulis query SQL secara langsung untuk setiap operasi.

Contohnya pada Prisma:

```javascript
const jadwal = await prisma.jadwal.create({
  data: {
    id: 1,
    mata_kuliah: 'Pemrograman Web',
    hari: 'Senin',
    jam: '08:00'
  }
});
```

Kode tersebut digunakan untuk menambahkan data ke tabel `jadwal`. Prisma akan menangani proses komunikasi dengan database berdasarkan struktur model yang telah dibuat. Dengan demikian, programmer dapat lebih fokus pada logika aplikasi tanpa harus menuliskan seluruh query SQL secara manual.

## G. Kesimpulan

Raw SQL dan ORM sama-sama dapat digunakan untuk mengakses dan mengelola database, tetapi memiliki cara penggunaan yang berbeda. Raw SQL memberikan kontrol yang lebih besar karena programmer menulis query secara langsung, sedangkan ORM membuat proses pengelolaan database menjadi lebih sederhana dengan menggunakan method dan objek.

Pada operasi penambahan data ke tabel `jadwal`, Raw SQL menggunakan perintah `INSERT INTO`, sedangkan Prisma menggunakan method `create()`. Penggunaan parameter query juga penting untuk meningkatkan keamanan aplikasi dan mengurangi risiko SQL Injection.