# Affine Cipher
**Affine Cipher** adalah salah satu teknik enkripsi yang paling sederhana. Prinsipnya adalah dengan menggeser posisi setiap [huruf](https://www.kompasiana.com/tag/huruf) pada sebuah pesan sebanyak jumlah tertentu. Misalnya, jika kita menggunakan geseran sebanyak 3 huruf, maka huruf A akan menjadi D, B akan menjadi E, dan seterusnya. Untuk membuka sandi, kita hanya perlu melakukan geseran kembali sebanyak 3 huruf ke belakang.

Affine Cipher memiliki kelemahan yang cukup besar, yaitu mudah ditembus dengan metode analisis frekuensi. Metode ini mengandalkan fakta bahwa dalam bahasa Inggris, huruf E adalah huruf yang paling sering muncul, sehingga jika kita menganalisis frekuensi kemunculan huruf dalam sebuah pesan yang terenkripsi dengan Affine Cipher, maka kita dapat menebak geseran yang digunakan dan membuka sandi dengan mudah.
[sumber](https://www.kompasiana.com/pikriramdani1420/63aabd1ea196e35d9c2c6792/affine-cipher)

### Rumus Enkripsi (Mengubah Teks Asli menjadi Teks Sandi)

> $E(x)=(a\cdot x+b)\mathinner{\;\left(\mod \,m\right)}$

- x: Nilai numerik dari huruf plaintext (teks asli).

- a dan b: Kunci sandi.

- m: Total ukuran alfabet (26).

- $\mathinner{\;\left(\mod \,26 \right)}$: Sisa hasil bagi setelah dibagi 26.

⚠️ **Syarat Penting untuk Kunci a:**  
Nilai a harus **koprima** dengan 26. Artinya, a dan 26 tidak boleh memiliki faktor pembagi yang sama selain angka 1. Jika syarat ini tidak dipenuhi, dua huruf yang berbeda bisa menghasilkan huruf sandi yang sama, sehingga teks tidak akan bisa dideskripsi kembali.  
_Nilai a yang diperbolehkan dari 1–25 adalah: 1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, dan 25._

###  Rumus Dekripsi (Mengubah Teks Sandi kembali menjadi Teks Asli)

> $D(y)=a^{-1}\cdot (y-b)\mathinner{\;\left(\mod \,m\right)}$

- y: Nilai numerik dari huruf ciphertext (teks sandi).

- a⁻¹: _Modular multiplicative inverse_ dari a terhadap m. Ini adalah angka yang jika dikalikan dengan a, lalu dibagi 26, akan menyisakan 1 $(a \cdot a^{-1} \equiv 1 \pmod{26})$.