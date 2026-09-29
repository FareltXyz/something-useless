**Caesar cipher** adalah salah satu yang paling sederhana dan paling banyak dikenal [enkripsi](https://en.wikipedia.org/wiki/Encryption "Enkripsi") teknik yang digunakan dalam [cryptography](https://en.wikipedia.org/wiki/Cryptography "Kriptografi"). Ia adalah jenis dari [sandi substitusi](https://en.wikipedia.org/wiki/Substitution_cipher "Sandi substitusi") di mana setiap huruf dalam [plaintext](https://en.wikipedia.org/wiki/Plaintext "Plaintext") digantikan oleh huruf dengan jumlah posisi tetap di sepanjang [alfabet](https://en.wikipedia.org/wiki/Alphabet "Alphabet"). Misalnya dengan pergeseran kiri 3, D akan digantikan oleh A, E akan menjadi B, dan sebagainya. Metode ini dinamai [Julius Caesar](https://en.wikipedia.org/wiki/Julius_Caesar "Julius Caesar"), yang menggunakannya dalam korespondensi pribadinya.[](https://en.wikipedia.org/wiki/Caesar_cipher#cite_note-2)[](https://en.wikipedia.org/wiki/Julius_Caesar "Julius Caesar")

Langkah enkripsi yang dilakukan oleh sandi Caesar sering kali dimasukkan sebagai bagian dari skema yang lebih kompleks, seperti [Vigenère cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher "Vigenère cipher"), dan masih memiliki aplikasi modern di [ROT13](https://en.wikipedia.org/wiki/ROT13 "ROT13") system. Seperti semua sandi substitusi alfabet tunggal, sandi Caesar mudah dipecahkan dan dalam praktik modern pada dasarnya tidak menawarkan [keamanan komunikasi](https://en.wikipedia.org/wiki/Communications_security "Keamanan komunikasi").

## Contoh

Transformasi dapat direpresentasikan dengan menyelaraskan dua alfabet; sandi adalah alfabet polos yang digeser ke kiri atau ke kanan dengan sejumlah posisi tertentu. Misalnya, berikut adalah sandi Caesar yang menggunakan pergeseran kiri sebanyak 3 tempat, setara dengan pergeseran kanan sebanyak 23 tempat (parameter pergeseran digunakan sebagai [key](https://en.wikipedia.org/wiki/Key_\(cryptography\) "Kunci (kriptografi)")):

Saat mengenkripsi, seseorang mencari setiap huruf pesan di baris "polos" dan menuliskan huruf terkait di baris "sandi".

Plaintext: RUBAH COKLAT CEPAT MELOMPATI ANJING MALAS
Ciphertext: QEB NRFZH YOLTK CLU GRJMP LSBO QEB IXWV ALD

Penguraian dilakukan secara terbalik, dengan pergeseran ke kanan sebesar 3.

Enkripsi juga dapat direpresentasikan menggunakan [aritmetika modular](https://en.wikipedia.org/wiki/Modular_arithmetic "Aritmetika modular") dengan terlebih dahulu mengubah huruf menjadi angka, sesuai dengan skema, A → 0, B → 1, ..., Z → 25. Enkripsi surat _x_ dengan pergeseran _n_ dapat digambarkan secara matematis sebagai:

```
C = (P + K) mod 26
```

yang dimana:
 C = CipherText
 P = Plaintext, misalnya huruf H = 7 (nomor urutan huruf) 
 K = Jumlah shift
 
Dekripsi dilakukan dengan cara yang sama:

```
P = (C - K) mod 26
```

yang dimana:
 P = PlainText
 C = Ciphertext (dalam nomor urutan huruf)
 K = Jumlah shift 

(Di sini, "mod" mengacu pada [operasi modulo](https://en.wikipedia.org/wiki/Modulo_operation "Operasi modulo"). Nilai tersebut berada pada kisaran 0 sampai 25, **Pelajari lebih lanjut tentang modulo!**

Penggantiannya tetap sama di seluruh pesan, sehingga sandi digolongkan sebagai jenis _[substitusi monoalfabetik](https://en.wikipedia.org/wiki/Monoalphabetic_substitution "Substitusi monoalfabetik")_, sebagai lawan dari _[substitusi polialfabet](https://en.wikipedia.org/wiki/Polyalphabetic_substitution "Substitusi polialfabetik")_.

#### contoh 
```
P = H = 7 
K = 3
 
C = (P + K) mod 26

C = (7 + 3) mod 26 
= 10 
= K (huruf/alphabet K)
```
sumber: https://en.wikipedia.org/wiki/Caesar_cipher