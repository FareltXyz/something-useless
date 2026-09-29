# Single-byte XOR Cipher

Algoritme sandi XOR byte tunggal bekerja dengan kunci enkripsi berukuran 1 byte - yang berarti kunci enkripsi dapat menjadi salah satu dari kemungkinan 256 nilai byte. Sekarang kita melihat secara detail bagaimana proses enkripsi dan dekripsi untuk cipher ini.

## Enkripsi

Sebagai bagian dari proses enkripsi, pesan asli diiterasi secara bytewise dan setiap byte `b` di-XOR dengan kunci enkripsi `key` dan aliran byte yang dihasilkan diterjemahkan kembali sebagai karakter dan dikirim ke pihak lain. Byte terenkripsi ini tidak harus berada di antara karakter biasa yang dapat dicetak dan idealnya harus ditafsirkan sebagai aliran byte. Berikut adalah implementasi proses enkripsi berbasis python.

```python
def single_byte_xor(text: bytes, key: int) -> bytes: """Given a plain text `text` as bytes and an encryption key `key` as a byte in range [0, 256) the function encrypts the text by performing XOR of all the bytes and the `key` and returns the resultant. """ return bytes([b ^ key for b in text])

```

Sebagai contoh, kita dapat mencoba mengenkripsi teks biasa - `abcd` - dengan kunci enkripsi `69` dan sesuai algoritme, kami melakukan XOR bytewise pada teks biasa yang diberikan. Untuk karakter `a`, byte yaitu. Nilai ASCII adalah `97` yang ketika XOR dengan `69` menghasilkan `36` yang padanan karakternya adalah `$`, demikian pula untuk `b` byte terenkripsi adalah `'`, untuk `c` it is `&` dan untuk `d` it is `!`. Oleh karena itu ketika `abcd` dienkripsi menggunakan sandi XOR byte tunggal dan kunci enkripsi `69`, ciphertext resultan yaitu pesan terenkripsi adalah `$'&!`.

## Dekripsi

Dekripsi adalah proses mengekstraksi pesan asli dari ciphertext terenkripsi yang diberi kunci enkripsi. XOR memiliki a [properti](https://brainly.in/question/3038497) - jika `a = b ^ c` then `b = a ^ c`, maka proses dekripsi persis sama dengan enkripsi yaitu kita iterasi melalui pesan terenkripsi bytewise dan XOR setiap byte dengan kunci enkripsi - resultan akan menjadi pesan asli.

Karena enkripsi dan dekripsi keduanya memiliki implementasi yang sama persis - kami meneruskan ciphertext ke fungsi tersebut `single_byte_xor`, didefinisikan di atas, untuk mendapatkan pesan asli kembali.

``` python
single_byte_xor(b"$'&!", 69) 
b'abcd'
```

# Menguraikan tanpa kunci enkripsi

Segalanya menjadi sangat menarik ketika kita harus memulihkan pesan asli yang diberikan ciphertext dan tidak memiliki pengetahuan tentang kunci enkripsi; meskipun kita mengetahui algoritma enkripsi.

Sebagai contoh teks biasa, kami mengambil beberapa pesan terakhir, yang dikirim melalui jaringan radio militer Jerman selama Perang Dunia II. Pesan-pesan ini disadap dan didekripsi oleh pasukan Inggris. Selama masa perang, pesan-pesan tersebut dienkripsi menggunakan [Mesin Enigma](https://en.wikipedia.org/wiki/Enigma_machine) and [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing) terkenal [memecahkan Kode Enigma](https://www.iwm.org.uk/history/how-alan-turing-cracked-the-enigma-code) (mirip dengan kunci enkripsi) yang digunakan untuk menyandikan pesan Jerman.

Di sini, kami berasumsi bahwa pesan asli, yang akan dienkripsi, adalah kalimat asli dalam bahasa Inggris. Ciphertext yang akan kita coba pecahkan dapat diperoleh sebagai

```python 
key = 82
plain_text = b'british troops entered cuxhaven at 1400 on 6 may - from now on all radio traffic will cease - wishing you all the best. lt kunkel.'
single_byte_xor(plain_text, key) 
b'0 ;&;!:r& =="!r7<&7 76r1\'*:3$7<r3&rcfbbr=<rdr?3+r\x7fr4 =?r<=%r=<r3>>r 36;=r& 344;1r%;>>r173!7r\x7fr%;!:;<5r+=\'r3>>r&:7r07!&|r>&r9\'<97>|'
```

## bruteforce

Ada jumlah kunci enkripsi yang sangat terbatas - tepatnya 256 - kita dapat, dengan sangat mudah, menggunakan pendekatan Bruteforce dan mencoba mendekripsi teks tersandi dengan semuanya. Jadi kami mulai mengulang semua kunci dalam rentang tersebut `[0, 256)` dan dekripsi ciphertext dan lihat mana yang paling mirip dengan pesan asli.

sumber: https://www.codementor.io/@arpitbhayani/deciphering-single-byte-xor-ciphertext-17mtwlzh30