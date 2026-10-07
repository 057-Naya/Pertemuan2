# Tugas Pendahuluan – JSONPlaceholder

**Nama:** NURULMAUDY Apriyani  
**NIM:** 2024520057  
**Prodi:** Informatika  
**Universitas:** Universitas Madura  

## 1. Perbandingan Struktur Data `/posts/1` dan `/users/1`

### `/posts/1`

Endpoint:

```text
https://jsonplaceholder.typicode.com/posts/1
```

Contoh data:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit..."
}
```

Field yang terdapat pada `/posts/1` adalah:

| Field | Fungsi |
|---|---|
| `userId` | Menunjukkan ID user yang membuat atau memiliki post |
| `id` | ID unik dari post |
| `title` | Judul dari post |
| `body` | Isi atau konten dari post |

### `/users/1`

Endpoint:

```text
https://jsonplaceholder.typicode.com/users/1
```

Contoh data:

```json
{
  "id": 1,
  "name": "Leanne Graham",
  "username": "Bret",
  "email": "Sincere@april.biz",
  "address": {
    "street": "Kulas Light",
    "suite": "Apt. 556",
    "city": "Gwenborough",
    "zipcode": "92998-3874",
    "geo": {
      "lat": "-37.3159",
      "lng": "81.1496"
    }
  },
  "phone": "1-770-736-8031 x56442",
  "website": "hildegard.org",
  "company": {
    "name": "Romaguera-Crona",
    "catchPhrase": "Multi-layered client-server neural-net",
    "bs": "harness real-time e-markets"
  }
}
```

Field pada `/users/1` digunakan untuk menyimpan informasi mengenai pengguna, seperti identitas, kontak, alamat, website, dan perusahaan.

Perbedaan utamanya adalah `/posts/1` berisi informasi mengenai sebuah postingan, sedangkan `/users/1` berisi informasi mengenai seorang pengguna. Field `userId` pada post dapat digunakan untuk menghubungkan post dengan user yang memiliki ID yang sama.

---

## 2. Analisis Struktur Tabel `/posts` dan `/users`

JSONPlaceholder dapat dianalogikan memiliki dua tabel utama, yaitu tabel `posts` dan tabel `users`.

### Tabel `users`

| Field | Keterangan |
|---|---|
| `id` | Primary key atau ID unik user |
| `name` | Nama lengkap user |
| `username` | Username user |
| `email` | Email user |
| `address` | Informasi alamat user |
| `phone` | Nomor telepon user |
| `website` | Website user |
| `company` | Informasi perusahaan user |

### Tabel `posts`

| Field | Keterangan |
|---|---|
| `userId` | Foreign key yang mengarah ke ID user |
| `id` | Primary key atau ID unik post |
| `title` | Judul postingan |
| `body` | Isi postingan |

### Diagram Relasi

```text
┌─────────────────────┐
│        USERS        │
├─────────────────────┤
│ PK id               │
│ name                │
│ username            │
│ email               │
│ address             │
│ phone               │
│ website             │
│ company             │
└──────────┬──────────┘
           │
           │ 1
           │
           │
           │ N
┌──────────▼──────────┐
│        POSTS        │
├─────────────────────┤
│ PK id               │
│ FK userId           │
│ title               │
│ body                │
└─────────────────────┘
```

Hubungannya adalah **one-to-many (1:N)**. Satu user dapat memiliki banyak post, sedangkan satu post hanya memiliki satu `userId` yang menunjukkan user pemilik post tersebut.

---

## 3. Analisis Hubungan URL, Method, dan Data pada `/posts`

URL menentukan resource yang ingin diakses, sedangkan HTTP method menentukan operasi yang dilakukan terhadap resource tersebut.

Contohnya:

| URL | Method | Fungsi | Data |
|---|---|---|---|
| `/posts` | GET | Mengambil seluruh post | Banyak data post |
| `/posts/1` | GET | Mengambil post dengan ID 1 | Satu data post |
| `/posts` | POST | Menambahkan post | Data post baru dikirim melalui body |
| `/posts/1` | PUT | Mengubah seluruh data post ID 1 | Data baru dikirim melalui body |
| `/posts/1` | PATCH | Mengubah sebagian data post ID 1 | Field yang ingin diubah dikirim melalui body |
| `/posts/1` | DELETE | Menghapus post ID 1 | Tidak membutuhkan body |

Dengan demikian, URL menunjukkan **resource yang dituju**, method menunjukkan **operasi yang dilakukan**, dan response berisi **hasil dari operasi tersebut**.

---

## 4. Perbedaan `/posts/1` dan `?userId=1`

### `/posts/1`

Endpoint:

```text
https://jsonplaceholder.typicode.com/posts/1
```

Endpoint tersebut digunakan untuk mengambil **satu post berdasarkan ID post**.

Contoh hasil:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit..."
}
```

Hasilnya berupa **satu objek post** dengan `id` bernilai `1`.

### `?userId=1`

Endpoint:

```text
https://jsonplaceholder.typicode.com/posts?userId=1
```

Endpoint tersebut menggunakan **query parameter** `userId=1` untuk mengambil post yang memiliki `userId` sebesar `1`.

Hasilnya berupa **array yang berisi beberapa post** milik user dengan ID 1.

Perbedaannya adalah `/posts/1` mencari berdasarkan **ID post**, sedangkan `?userId=1` melakukan penyaringan berdasarkan **ID user**.

---

## 5. Perbandingan GET, POST, PUT, PATCH, dan DELETE

| Method | Endpoint | Status Code | Fungsi | Perubahan Data |
|---|---|---:|---|---|
| GET | `/posts/1` | 200 OK | Mengambil data post | Tidak mengubah data |
| POST | `/posts` | 201 Created | Membuat post baru | Disimulasikan sebagai data baru |
| PUT | `/posts/1` | 200 OK | Mengubah seluruh data post | Disimulasikan |
| PATCH | `/posts/1` | 200 OK | Mengubah sebagian data post | Disimulasikan |
| DELETE | `/posts/1` | 200 OK | Menghapus post | Disimulasikan |

### GET

GET digunakan untuk mengambil data dari server. Method ini tidak digunakan untuk membuat atau mengubah data.

Contoh:

```text
GET https://jsonplaceholder.typicode.com/posts/1
```

Response biasanya memiliki status `200 OK` jika data berhasil ditemukan.

### POST

POST digunakan untuk membuat atau menambahkan resource baru.

Contoh:

```text
POST https://jsonplaceholder.typicode.com/posts
```

Data dikirim melalui request body, misalnya:

```json
{
  "title": "Belajar API",
  "body": "Mempelajari JSONPlaceholder",
  "userId": 1
}
```

JSONPlaceholder memberikan status `201 Created` dan mengembalikan data yang disimulasikan sebagai data baru.

### PUT

PUT digunakan untuk mengganti atau memperbarui keseluruhan data sebuah resource.

Contoh:

```text
PUT https://jsonplaceholder.typicode.com/posts/1
```

Data yang dikirim biasanya berisi seluruh field yang ingin digunakan untuk menggantikan data sebelumnya. Response JSONPlaceholder biasanya memiliki status `200 OK`.

### PATCH

PATCH digunakan untuk memperbarui sebagian data dari sebuah resource.

Contoh:

```text
PATCH https://jsonplaceholder.typicode.com/posts/1
```

Misalnya hanya mengubah judul:

```json
{
  "title": "Judul Baru"
}
```

Response biasanya memiliki status `200 OK`.

### DELETE

DELETE digunakan untuk menghapus sebuah resource.

Contoh:

```text
DELETE https://jsonplaceholder.typicode.com/posts/1
```

JSONPlaceholder biasanya memberikan status `200 OK` sebagai response simulasi.

### Catatan

JSONPlaceholder merupakan REST API palsu untuk latihan. Operasi POST, PUT, PATCH, dan DELETE memberikan response seolah-olah terjadi perubahan data, tetapi perubahan tersebut **tidak benar-benar disimpan secara permanen** di server.

---

## Kesimpulan

JSONPlaceholder menyediakan API yang dapat digunakan untuk memahami konsep REST API, HTTP method, struktur data, dan hubungan antar-resource. Resource `users` menyimpan informasi pengguna, sedangkan `posts` menyimpan informasi postingan dan memiliki `userId` yang menghubungkannya dengan user.

Penggunaan URL dan HTTP method menentukan operasi yang dilakukan terhadap resource. GET digunakan untuk mengambil data, POST untuk membuat data, PUT untuk memperbarui keseluruhan data, PATCH untuk memperbarui sebagian data, dan DELETE untuk menghapus data. JSONPlaceholder sangat berguna untuk latihan karena menyediakan response API tanpa membutuhkan database atau backend sendiri.