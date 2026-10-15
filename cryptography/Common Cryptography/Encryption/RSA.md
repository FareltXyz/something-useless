Algoritma RSA (**R**ivest-**S**hamir-**A**dleman) adalah algoritma **kriptografi asimetris** atau **kriptografi kunci publik**, yang berarti algoritma ini bekerja menggunakan dua kunci yang berbeda: **Kunci Publik** dan **Kunci Privat**. Kunci Publik digunakan untuk **enkripsi** dan diketahui oleh semua orang, sedangkan Kunci Privat digunakan untuk **dekripsi** dan harus dijaga kerahasiaannya oleh penerima. Nama Algoritma RSA diambil dari inisial para penciptanya, yaitu Ron **R**ivest, Adi **S**hamir, dan Leonard **A**dleman, yang mempublikasikan algoritma ini pada tahun 1977.  

**Contoh Kriptografi Asimetris:**
Jika Orang **A** ingin mengirim pesan secara aman kepada Orang **B**:
- Orang A **mengenkripsi** pesan menggunakan **Kunci Publik** milik Orang B.
- Orang B **mendekripsi** pesan menggunakan **Kunci Privat** miliknya sendiri.

### Algoritma RSA

> Algoritma RSA didasarkan pada **faktorisasi** bilangan besar dan **aritmatika modular** untuk mengenkripsi dan mendekripsi data. Algoritma ini terdiri dari tiga tahap utama:
> 1. **Pembuatan Kunci (Key Generation):** Membuat Kunci Publik dan Kunci Privat.
> 2. **Enkripsi:** Pengirim mengenkripsi data menggunakan Kunci Publik untuk menghasilkan **teks tersandi (cipher text)**.
> 3. **Dekripsi:** Mendekripsi **teks tersandi** menggunakan Kunci Privat untuk mendapatkan kembali data asli.

#### **1. Pembuatan Kunci (Key Generation)**

  

- Pilih dua bilangan prima besar, sebut saja **p** dan **q**. Bilangan prima ini harus dijaga kerahasiaannya.
- Hitung hasil kali dari bilangan prima tersebut, yaitu **n = p * q**. Hasil kali ini menjadi bagian dari kunci publik maupun kunci privat.
- Hitung [Fungsi Totien Euler](https://www.geeksforgeeks.org/dsa/eulers-totient-function/) **Φ(n)** sebagai **Φ(n) = Φ(p * q) = Φ(p) * Φ(q) = (p - 1) * (q - 1).**
- Pilih eksponen enkripsi **e** sedemikian rupa sehingga:
    - 1 < e < Φ(n), dan
    - gcd(e, Φ(n)) = 1, artinya e harus merupakan koprima dengan Φ(n).
- Hitung eksponen dekripsi **d**, sedemikian rupa sehingga:
    - **(d * e) ≡ 1 mod Φ(n)**, artinya d adalah [invers perkalian modular](https://www.geeksforgeeks.org/dsa/multiplicative-inverse-under-modulo-m/) dari **e** mod Φ(n). Beberapa metode umum untuk menghitung invers perkalian meliputi: [Algoritma Euklides Diperluas](https://www.geeksforgeeks.org/dsa/euclidean-algorithms-basic-and-extended/), [Teorema Kecil Fermat](https://www.geeksforgeeks.org/dsa/fermats-little-theorem/), dll.
    - Kita dapat memiliki beberapa nilai d yang memenuhi **(d * e) ≡ 1 mod Φ(n)**, tetapi nilai mana pun yang kita pilih tidak menjadi masalah karena semuanya merupakan kunci yang valid dan akan menghasilkan pesan yang sama saat didekripsi.
Akhirnya, **Kunci Publik = (n, e)** dan **Kunci Privat = (n, d)**.

  

#### **2. Enkripsi**

  

Untuk mengenkripsi sebuah pesan **M**, pesan tersebut terlebih dahulu diubah ke dalam representasi numerik menggunakan ASCII atau skema pengkodean lainnya. Selanjutnya, gunakan kunci publik (n, e) untuk mengenkripsi pesan dan mendapatkan teks tersandi menggunakan rumus:

> $c = n^{e}\pmod N$, di mana C adalah teks tersandi, serta e dan n adalah bagian dari kunci publik.
> 
>   

#### **3. Dekripsi**

Untuk mendekripsi teks tersandi **C**, gunakan kunci privat (n, d) dan dapatkan data asli menggunakan rumus:

> $M = C^d \pmod n$, di mana M adalah pesan, serta d dan n adalah bagian dari kunci privat.
> 
>   

### Contoh Algoritma RSA

Sebelumnya Putar Selanjutnya 1 / 6

  

### Konsep di Balik Algoritma RSA

Gagasan utama RSA didasarkan pada fakta bahwa sangat sulit untuk memfaktorkan bilangan bulat yang berukuran sangat besar. Kunci Publik adalah (n, e), di mana n dan e diketahui oleh publik, sedangkan Kunci Privat adalah (n, d). Karena hanya penerima yang mengetahui nilai d, maka hanya penerima tersebut yang dapat mendekripsi pesan. **Namun, apakah mungkin untuk mencari nilai d menggunakan n dan e?**

  

Kita tahu bahwa **(d * e) ≡ 1 mod Φ(n)**, jadi jika kita dapat menghitung nilai **Φ(n)**, kita dapat menemukan nilai **d**. Akan tetapi, **Φ(n) = (p - 1) * (q - 1).** Oleh karena itu, kita memerlukan nilai p dan q. Seseorang mungkin berpikir bahwa mencari nilai p dan q cukup mudah karena **n = p * q** dan n sudah diketahui publik; namun, Algoritma RSA menggunakan nilai p dan q yang sangat besar, yang pada gilirannya membuat nilai n menjadi sangat besar sehingga memfaktorkan nilai sebesar itu secara komputasi tidak mungkin dilakukan (mustahil).

  

Oleh karena itu, kekuatan enkripsi terletak pada nilai **p** dan **q**. Kunci RSA umumnya dapat memiliki panjang 1024 atau 2048 bit, meskipun para ahli percaya bahwa kunci 1024-bit dapat dipecahkan dalam waktu dekat. Namun, hingga saat ini hal tersebut masih dianggap sebagai tugas yang tidak layak dilakukan.

  

**Catatan:** Jika seseorang berhasil mengetahui nilai **p** dan **q**, maka ia dapat menghitung nilai **d** dan mendekripsi pesan tersebut.

  

### Implementasi Algoritma RSA

``` python
# Python Program for implementation of RSA Algorithm

def power(base, expo, m):
    res = 1
    base = base % m
    while expo > 0:
        if expo & 1:
            res = (res * base) % m
        base = (base * base) % m
        expo = expo // 2
    return res

# Function to find modular inverse of e modulo phi(n)
# Here we are calculating phi(n) using Hit and Trial Method
# but we can optimize it using Extended Euclidean Algorithm
def modInverse(e, phi):
    for d in range(2, phi):
        if (e * d) % phi == 1:
            return d
    return -1

# RSA Key Generation
def generateKeys():
    p = 7919
    q = 1009
    
    n = p * q
    phi = (p - 1) * (q - 1)

    # Choose e, where 1 < e < phi(n) and gcd(e, phi(n)) == 1
    e = 0
    for e in range(2, phi):
        if gcd(e, phi) == 1:
            break

    # Compute d such that e * d ≡ 1 (mod phi(n))
    d = modInverse(e, phi)

    return e, d, n

# Function to calculate gcd
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

# Encrypt message using public key (e, n)
def encrypt(m, e, n):
    return power(m, e, n)

# Decrypt message using private key (d, n)
def decrypt(c, d, n):
    return power(c, d, n)

# Main execution
if __name__ == "__main__":
    
    # Key Generation
    e, d, n = generateKeys()
  
    print(f"Public Key (e, n): ({e}, {n})")
    print(f"Private Key (d, n): ({d}, {n})")

    # Message
    M = 123
    print(f"Original Message: {M}")

    # Encrypt the message
    C = encrypt(M, e, n)
    print(f"Encrypted Message: {C}")

    # Decrypt the message
    decrypted = decrypt(C, d, n)
    print(f"Decrypted Message: {decrypted}")
```

### Kelebihan

- **Keamanan:** Algoritma RSA dianggap sangat aman dan banyak digunakan untuk transmisi data yang aman.
- **Kriptografi kunci publik:** Algoritma RSA adalah algoritma kriptografi kunci publik, yang berarti algoritma ini menggunakan dua kunci berbeda untuk enkripsi dan dekripsi. Kunci publik digunakan untuk mengenkripsi data, sedangkan kunci privat digunakan untuk mendekripsi data.
- **Pertukaran kunci:** Algoritma RSA dapat digunakan untuk pertukaran kunci yang aman, yang berarti dua pihak dapat bertukar kunci rahasia tanpa benar-benar mengirimkan kunci tersebut melalui jaringan.
- **Tanda tangan digital (Digital signatures):** Algoritma RSA dapat digunakan untuk tanda tangan digital, yang berarti pengirim dapat menandatangani pesan menggunakan kunci privat mereka, dan penerima dapat memverifikasi tanda tangan tersebut menggunakan kunci publik pengirim.
- **Banyak digunakan:** Perbankan online, e-commerce, dan komunikasi aman hanyalah beberapa bidang dan aplikasi di mana algoritma RSA banyak dikembangkan. 

### Kekurangan

- **Kecepatan pemrosesan lambat:** Algoritma RSA lebih lambat dibandingkan algoritma enkripsi lainnya, terutama ketika menangani data dalam jumlah besar.
- **Ukuran kunci yang besar:** Algoritma RSA memerlukan ukuran kunci yang besar agar tetap aman, yang berarti algoritma ini membutuhkan lebih banyak sumber daya komputasi dan ruang penyimpanan.
- **Rentan terhadap serangan saluran samping (side-channel attacks):** Algoritma RSA rentan terhadap serangan saluran samping, yang berarti penyerang dapat menggunakan informasi yang bocor melalui saluran samping seperti konsumsi daya, radiasi elektromagnetik, dan analisis waktu untuk mengekstrak kunci privat.
- **Penggunaan yang terbatas pada beberapa aplikasi:** Algoritma RSA tidak cocok untuk beberapa aplikasi—seperti aplikasi yang memerlukan enkripsi dan dekripsi konstan untuk data berukuran besar—karena kecepatan pemrosesannya yang lambat.
- **Kompleksitas:** Algoritma RSA adalah teknik matematika canggih yang mungkin dianggap sulit untuk dipahami dan digunakan oleh sebagian orang.
- **Manajemen Kunci:** Pengelolaan kunci privat yang aman sangat diperlukan untuk algoritma RSA, meskipun dalam beberapa kasus hal ini bisa menjadi hal yang sulit.
- **Rentan terhadap Komputasi Kuantum:** Komputer kuantum memiliki kemampuan untuk menyerang algoritma RSA, yang berpotensi mendekripsi data di masa mendatang.

---
materi tersebut diperoleh dari beberapa sumber berikut
-  [](https://www.geeksforgeeks.org/computer-networks/rsa-algorithm-cryptography/)

