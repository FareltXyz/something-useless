**Sandi Atbash** (Atbash Cipher) adalah ==jenis **sandi substitusi monoalfabetik** yang sangat sederhana, di mana alfabet **dibalik secara total** dari belakang ke depan==.

Sandi ini awalnya dibuat untuk alfabet Ibrani, namun bisa digunakan untuk alfabet apa saja, termasuk alfabet Latin modern (A-Z) yang kita gunakan saat ini.

Cara Kerja Sandi Atbash

Cara kerjanya mirip seperti cermin. Huruf pertama (A) digantikan oleh huruf terakhir (Z), huruf kedua (B) digantikan oleh huruf kedua dari belakang (Y), dan seterusnya.

Berikut adalah tabel pemetaan untuk alfabet Latin:

| Huruf Asli (Plaintext)                    | Huruf Sandi (Ciphertext)                  |
| ----------------------------------------- | ----------------------------------------- |
| **A, B, C, D, E, F, G, H, I, J, K, L, M** | **Z, Y, X, W, V, U, T, S, R, Q, P, O, N** |
| **N, O, P, Q, R, S, T, U, V, W, X, Y, Z** | **M, L, K, J, I, H, G, F, E, D, C, B, A** |

Contoh Penggunaan

- **Pesan Asli:** `K O P I`

- **Proses:**
    - K menjadi P
    - O menjadi L
    - P menjadi K
    - I menjadi R

- **Pesan Sandi:** `P L K R`

Karakteristik Unik

- **Sandi Simetris:** Atbash adalah sandi yang _self-inverse_. Artinya, **rumus untuk menyandikan (enkripsi) dan membuka sandi (dekripsi) adalah sama**. Anda tidak perlu membalikkan rumus untuk membaca pesan rahasianya; cukup masukkan kembali pesan sandi tersebut ke tabel Atbash yang sama.

- **Asal-Usul Nama:** Nama "Atbash" berasal dari huruf-huruf alfabet Ibrani: **Aleph** (huruf 1), **Taw** (huruf terakhir), **Bet** (huruf 2), dan **Shin** (huruf kedua dari belakang). Jika disingkat menjadi A-T-B-Sh.

Karena polanya yang sangat konsisten dan tanpa kunci rahasia, sandi ini **sangat mudah dipecahkan** dan tidak aman untuk menyembunyikan informasi rahasia di zaman modern. Saat ini, Atbash lebih sering digunakan dalam teka-teki, permainan, atau sebagai materi dasar untuk belajar kriptografi.