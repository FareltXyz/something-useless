# Apa itu AES encryption?

Dalam kriptografi, AES mengacu pada Advanced Encryption Standard, sebuah algoritma enkripsi yang cepat, efisien, dan aman yang disertifikasi oleh US National Institute of Standards and Technology (NIST). Ini adalah _symmetric-key cipher_ yang menggunakan kunci yang sama untuk melakukan enkripsi maupun dekripsi data. Proses ini relatif cepat, sehingga menjadikannya ideal untuk mengenkripsi data dalam jumlah besar pada kondisi _data at rest_.

Karena kekuatan dan keandalannya, AES merupakan salah satu jenis enkripsi yang paling populer dan umum digunakan dalam _wireless network security_, data dan [disk encryption](https://proton.me/learn/encryption/types-of-encryption/full-disk-encryption), sistem _online payment_, [cloud storage](https://proton.me/drive), [password management](https://proton.me/pass), bahkan aplikasi militer dan pemerintahan. Pemerintah AS menggunakan AES encryption untuk mengamankan _classified information_, yang turut berkontribusi terhadap popularitasnya.

## Apakah algoritma AES aman?

Ya. Pada tahun 2000, setelah proses seleksi yang sangat [menyeluruh](https://www.schneier.com/crypto-gram/archives/2000/1015.html#8) dan terbuka, NIST mengumumkan bahwa AES (yang hingga saat itu dikenal sebagai _Rijndael algorithm_, diciptakan oleh Vincent Rijmen dan Joan Daemen) akan menggantikan DES sebagai algoritma yang [direkomendasikan](https://csrc.nist.gov/news/1997/announcing-development-of-fips-for-advanced-encryp): _"unclassified, publicly disclosed encryption algorithm capable of protecting sensitive government information well into the next century."_

Menurut [NIST](https://proton.me/business/blog/nist-password-guidelines), semua _key lengths_ pada algoritma AES dianggap "cukup" (_sufficient_) untuk melindungi _classified information_ hingga level "Secret". Untuk informasi berlevel "Top Secret", diperlukan AES-192 atau AES-256.

### Serangan brute force (Brute force attacks)

Bentuk serangan paling mendasar yang mungkin dilakukan terhadap _cipher_ enkripsi apa pun adalah [serangan brute-force](https://proton.me/blog/what-is-brute-force-attack), yaitu mencoba setiap kemungkinan kombinasi kunci hingga kunci yang tepat ditemukan. 

[Frontier](https://en.wikipedia.org/wiki/Frontier_\(supercomputer\)) adalah superkomputer publik paling kuat di dunia saat ini. Jika seluruh kemampuannya didedikasikan penuh hanya untuk melakukan _brute force_ terhadap AES-128, superkomputer ini masih memerlukan waktu sekitar 10–12 triliun tahun untuk mencoba semua kombinasi yang mungkin. Waktu ini jauh lebih lama dari perkiraan usia alam semesta. Oleh karena itu, bahkan pada ukuran kunci terendahnya sekalipun, AES sangat tahan terhadap serangan _brute force_ dari komputer konvensional. 

AES-256 adalah 340 miliar-miliar-miliar-miliar ($2^{128}$) kali lebih sulit untuk di-_brute force_ dibandingkan dengan AES-128.

Meskipun [algoritma Grover](https://en.wikipedia.org/wiki/Grover's_algorithm) secara teoretis memangkas tingkat keamanan kunci simetris hingga separuhnya terhadap [ancaman komputasi kuantum](https://proton.me/learn/encryption/glossary/post-quantum-cryptography), kunci simetris masih relatif tahan terhadap ancaman kuantum (_quantum-resistant_), terutama jika menggunakan kunci berukuran 256-bit.

### Serangan terhadap kunci (Key attacks)

Selama bertahun-tahun, sejumlah serangan teoretis terhadap kunci AES telah dipublikasikan oleh para kriptografer, namun semuanya tidak praktis untuk dijalankan di dunia nyata, atau hanya efektif pada implementasi AES yang sengaja mengurangi jumlah putaran (_rounds_) (lihat penjelasan di bawah). 

Upaya paling berhasil adalah [biclique attack](https://en.wikipedia.org/wiki/Biclique_attack) teoretis yang dipublikasikan pada tahun 2011, yang dapat memangkas waktu komputasi _brute force_ AES dengan faktor empat (empat kali lebih cepat). Namun, proses tersebut tetap membutuhkan waktu miliaran tahun untuk memecahkan AES pada perangkat keras komputer saat ini maupun di masa depan yang dapat diprediksi. 

Hingga saat ini, belum ada metode serangan kunci praktis yang terbukti berhasil menembus AES-128 atau versi di atasnya yang diimplementasikan dengan benar. 

### Serangan saluran samping (Side-channel attacks)

Serangan saluran samping (_side-channel attack_) berupaya memperkecil jumlah kombinasi yang diperlukan dalam serangan _brute force_ dengan cara mencari petunjuk fisik dari komputer yang tengah melakukan komputasi enkripsi. Petunjuk tersebut dapat dikumpulkan melalui pengamatan terhadap:

- Waktu (_timing_) — berapa lama waktu yang dibutuhkan komputer untuk memproses suatu operasi
- Kebocoran radiasi elektromagnetik
- Indikasi suara (_audio cues_)
- Indikasi visual (misalnya ditangkap menggunakan kamera beresolusi tinggi).

Secara khusus, serangan _cache-timing_ terbukti cukup efektif dalam membobol AES. Dalam studi kasus yang paling terkenal pada tahun 2016, para peneliti berhasil [memulihkan](https://ieeexplore.ieee.org/document/7467359) kunci AES-128 hanya dengan menggunakan "sekitar 6–7 blok _plaintext_ atau [ciphertext](https://proton.me/learn/encryption/glossary/what-is-ciphertext) (secara teoretis bahkan satu blok saja sudah mencukupi)".

Kendati demikian, ada sejumlah langkah mitigasi yang dapat diterapkan untuk meredam ancaman serangan _side-channel_:

- Implementasi AES yang tepat dan aman dapat mencegah kebocoran data.
- Perangkat keras yang mengintegrasikan set instruksi AES secara khusus mampu memperkecil bidang celah serangan (_attack surface_) _side-channel_.
- Teknik pengacakan (_randomization_) dapat digunakan untuk memutus pola hubungan antara data yang dilindungi AES dengan kebocoran informasi yang mungkin terkumpul lewat saluran samping. 

Pada banyak skenario, serangan _side-channel_ mengharuskan penyerang berada sangat dekat atau memiliki akses fisik langsung ke perangkat saat proses dekripsi data berlangsung, meskipun serangan jarak jauh tetap dimungkinkan apabila perangkat telah disusupi perangkat lunak berbahaya (_malware_), terutama pada kasus serangan berbasis waktu.

## Cara kerja AES

AES adalah sebuah _block cipher_ yang mengenkripsi dan mendekripsi data dalam blok-blok berukuran 128 bit menggunakan kunci berukuran 128-bit, 192-bit, atau 256-bit. Sebagaimana dijelaskan sebelumnya, kunci yang sama digunakan untuk enkripsi maupun dekripsi. AES yang menggunakan kunci 128-bit biasa disebut AES-128, begitu pula dengan AES-192 dan AES-256.

![](https://pmecdn.protonweb.com/image-transformation/?s=a&image=how_aes_works_mobile_2dc344bc72.png&width=776&height=776)

Data dienkripsi melalui serangkaian putaran (_rounds_), di mana setiap putaran terdiri dari sekumpulan operasi matematika. 

Proses diawali dengan algoritma penjadwalan kunci Rijndael (_key schedule algorithm_) untuk menghasilkan serangkaian kunci putaran (_round keys_) baru dari kunci rahasia utama. Tahap ini dikenal sebagai ekspansi kunci (_key expansion_).

Setiap putaran selanjutnya terdiri atas satu atau kombinasi dari operasi-operasi berikut:

1. **Add Round Key**: Operasi [XOR](https://en.wikipedia.org/wiki/Exclusive_or) dilakukan untuk mengombinasikan data yang akan dienkripsi (_ciphertext_) dengan setiap kunci putaran (_round key_).

![](https://pmecdn.protonweb.com/image-transformation/?s=a&image=aes_round_key_mobile_7290792a7f.png&width=776&height=776)

2. **Sub Bytes**: Tabel substitusi (S-box) digunakan untuk mengacak data lebih jauh. Prinsipnya mirip dengan sandi substitusi sederhana saat masa kecil, di mana setiap huruf digantikan dengan huruf lain pada urutan tertentu dalam alfabet.

![](https://pmecdn.protonweb.com/image-transformation/?s=a&image=aes_sub_bytes_mobile_45ad9549a6.png&width=776&height=776)

3. **Shift Rows**: Setiap blok data 128-bit disusun ke dalam matriks 4x4 (masing-masing 16 bita). Operasi ini menggeser setiap bita dalam baris matriks ke arah kiri dengan jumlah pergeseran tertentu.

![](https://pmecdn.protonweb.com/image-transformation/?s=a&image=aes_shift_rows_mobile_7533546070.png&width=776&height=776)

4. **Mix Columns**: Transformasi linier yang dapat dibalik (_invertible linear transformation_) diterapkan pada masing-masing kolom matriks.

![](https://pmecdn.protonweb.com/image-transformation/?s=a&image=aes_mix_columns_mobile_238d797507.png&width=776&height=776)

Rangkaian transformasi ini menyusun satu putaran (_round_), yang kemudian diulang pada data sejumlah putaran tertentu tergantung pada panjang kunci yang digunakan:

- AES-128 — 10 putaran
- AES-192 — 12 putaran
- AES-256 — 14 putaran

Untuk mendekripsi data, seluruh tahapan enkripsi di atas cukup dilakukan secara terbalik. Proses ini membutuhkan kunci rahasia awal untuk membalik alur transformasi menggunakan masing-masing _inverse round key_.

## Mengapa AES-256 lebih dipilih daripada AES-192 atau AES-128?

Dibutuhkan waktu yang lebih panjang daripada usia alam semesta untuk melakukan _brute force_ pada AES-128 dengan teknologi komputasi saat ini maupun masa depan yang dapat diantisipasi. Kriptografer kenamaan Bruce Schneier bahkan pernah [berpendapat](https://www.schneier.com/blog/archives/2009/07/another_new_aes.html) bahwa AES-128 berpotensi lebih tangguh dibanding AES-256 karena memiliki penjadwalan kunci (_key schedule_) yang lebih solid — yaitu algoritma yang menghitung seluruh kunci putaran dari kunci rahasia utama.

Meski begitu, AES-256 telah menjadi standar emas _de facto_ untuk enkripsi berbasis kunci simetris. Algoritma ini kerap (walau diwarnai perdebatan teknis) dianggap sebagai pilihan yang lebih mantap karena panjang kuncinya yang lebih besar memberikan margin keamanan cadangan, memastikan data terenkripsi tetap terlindungi andai suatu saat ditemukan metode yang mampu melemahkan algoritma AES secara signifikan. Pertimbangan ini kian relevan seiring dengan meningkatnya kebutuhan proteksi terhadap komputer kuantum (_post-quantum resistance_). 

## AES-CBC vs AES-GCM

Hingga beberapa tahun belakangan, AES umumnya dijalankan dalam mode Cipher Block Chaining (CBC), di mana setiap blok _plaintext_ di-XOR terlebih dahulu dengan blok _ciphertext_ sebelumnya sebelum dienkripsi. Dalam mode CBC, algoritma hashing [HMAC](https://en.wikipedia.org/wiki/HMAC) seperti HMAC-SHA256 diperlukan untuk memverifikasi keabsahan dan integritas data.

Namun, kini AES semakin lumrah digunakan dalam mode Galois/Counter Mode (GCM), yang mengusung varian [mode counter (CTR)](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Counter_\(CTR\)). Keunggulan utamanya adalah pemanfaatan [Galois field](https://en.wikipedia.org/wiki/Finite_field) untuk memverifikasi integritas data secara langsung tanpa membutuhkan algoritma eksternal tambahan. Hal ini menjadikannya jauh lebih efisien dibandingkan skema autentikasi terpisah yang sering kali memakan beban komputasi tinggi.

Meskipun AES-CBC dengan autentikasi HMAC tergolong aman, mode CBC rentan terhadap [padding attacks](https://en.wikipedia.org/wiki/Padding_\(cryptography\)), seperti serangan celah keamanan [POODLE](https://en.wikipedia.org/wiki/POODLE). Sebaliknya, mode GCM kebal terhadap risiko serangan tersebut.

## Akselerasi perangkat keras AES (Hardware-accelerated AES)

Sebagian besar prosesor (CPU) modern telah menyertakan Advanced Encryption Standard New Instructions ([AES-NI](https://en.wikipedia.org/wiki/AES_instruction_set)), yaitu kumpulan instruksi bawaan perangkat keras yang mengeksekusi operasi AES langsung di tingkat prosesor. Ini tidak hanya mempercepat proses enkripsi/dekripsi secara signifikan, tetapi juga membantu menangkal serangan _side-channel_ berbasis waktu (_timing attacks_), karena seluruh operasi berlangsung di dalam unit eksekusi terisolasi prosesor sehingga variasi selang waktu yang dapat dianalisis dan dieksploitasi oleh penyerang menjadi sangat minim.


---

materi tersebut diterjemahkan berdasarkan sumber dari
- [Proton - What is AES Encryption?](https://proton.me/learn/encryption/types-of-encryption/aes-encryption)