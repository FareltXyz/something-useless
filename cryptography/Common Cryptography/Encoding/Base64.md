# Memahami base64

Oleh Sergei Bachinin

Dalam artikel ini, kita akan membahas **base64** secara menyeluruh. Anda akan mempelajari bagaimana base64 muncul dan mengapa teknologi ini masih banyak digunakan dalam sistem modern.

## Daftar Isi

1. Apa itu base64?
    
2. Mengapa menggunakan base64?
    
3. Kapan menggunakan base64?
    
4. Kasus pada SMTP
    
5. Apakah keterbatasan tersebut masih relevan saat ini?
    
6. Bagaimana base64 mengatasi keterbatasan tersebut?
    
7. Mengapa hanya 64 karakter?
    
8. Apakah saya harus menggunakan base64 dengan HTTP/1.1?
    
9. Mengapa base64 digunakan untuk Data URLs?
    
10. Kesimpulan
    

---

## Apa itu base64?

Base64 adalah cara untuk mengubah data apa pun menjadi sekumpulan karakter yang terlihat seperti gabungan angka dan huruf. Saat ini, base64 digunakan secara luas dan sering dianggap sebagai sesuatu yang biasa. Sebagian besar waktu, Anda menggunakannya karena memang tidak memiliki pilihan lain: dalam banyak situasi, hanya bentuk data yang menyerupai teks seperti inilah yang dianggap **valid**.

Pada saat yang sama, base64 merupakan mekanisme yang cukup mahal. Base64 membuat ukuran data menjadi sekitar **33% lebih besar** dalam penggunaan memory. Oleh karena itu, base64 merupakan salah satu hal kecil yang dapat membuat software menjadi **lebih lambat**. Itulah alasan mengapa base64 sebaiknya hanya digunakan ketika memang benar-benar diperlukan.

Sekali lagi, biasanya Anda memang tidak memiliki pilihan. Namun, terkadang Anda memiliki pilihan tersebut. Karena itu, memahami bagaimana base64 bekerja dan masalah apa yang sebenarnya ingin diselesaikan olehnya akan sangat berguna.

Artikel ini ditujukan bagi mereka yang sudah pernah menemukan base64 dalam praktik programming dan mungkin bertanya-tanya sebenarnya apa fungsi teknologi tersebut. Anda akan lebih mudah memahami panduan ini jika sudah memiliki pengetahuan dasar mengenai data types serta memahami bagaimana computer memory diorganisasikan pada tingkat binary, seperti **bits** dan **bytes**.

Algoritma encoding base64 sebenarnya cukup sederhana. Algoritma ini menerima sebuah binary sequence sebagai input dan menghasilkan binary sequence lainnya sebagai output. Base64 tidak peduli apa arti dari byte asli tersebut—apakah byte tersebut merupakan bagian dari sebuah gambar, PDF, atau jenis data lainnya.

Base64 mengambil data binary asli, membaginya menjadi kelompok-kelompok berukuran **6 bits**, kemudian mengubah setiap kelompok tersebut menjadi sebuah karakter teks yang aman (atau secara lebih tepat, menjadi binary sequence yang merepresentasikan karakter tersebut). Istilah "aman" mengacu pada karakter yang berasal dari kumpulan karakter yang sangat terbatas, yang akan kita bahas lebih lanjut.

  ![[base64-diagram-smaller-1.webp]]

_Gambar tersebut menunjukkan secara sederhana bagaimana teks "Sun" di-encode menjadi base64._

Pada suatu titik, Anda tentu perlu melakukan **decode** terhadap pseudo-text tersebut untuk mengembalikannya menjadi data asli, karena base64 sendiri tidak memiliki makna jika hanya dibiarkan dalam bentuk encoded. Proses decoding melakukan operasi binary yang serupa, tetapi dalam arah sebaliknya. Data yang dikembalikan dijamin sama persis dengan data sebelum proses encoding.

Algoritma encoding dan decoding tidak akan dibahas lebih dalam di sini. Wikipedia menjelaskannya secara sangat lengkap jika Anda ingin mempelajarinya lebih lanjut.

Dalam praktiknya, sebagai developer, Anda hampir tidak pernah bekerja langsung dengan binary ketika melakukan encoding terhadap data. Sebaliknya, Anda akan menggunakan wrapper yang tersedia hampir di semua programming language, seperti fungsi `btoa()` dan `atob()` pada JavaScript.

---

## Mengapa Menggunakan base64?

Masalah apa yang sebenarnya ingin diselesaikan oleh base64? Ada tiga teori utama mengenai hal ini:

- Base64 digunakan karena beberapa sistem hanya **dibatasi pada karakter ASCII**, tetapi sebenarnya sistem tersebut digunakan untuk berbagai jenis data. Base64 dapat "menyamarkan" data tersebut sebagai ASCII sehingga data dapat melewati validation.
    
- Beberapa sistem lama menganggap bahwa data terdiri dari kelompok **7-bit**, sedangkan sistem modern menggunakan byte berukuran 8-bit. Hal ini dapat menyebabkan kesalahpahaman antara sistem yang berbeda. Base64 diduga dapat membantu mengatasi masalah ini, meskipun mekanismenya tidak langsung terlihat.
    
- Beberapa karakter memiliki **makna khusus**, dan makna tersebut dapat berbeda antara satu sistem dengan sistem lainnya. Base64 mengatasi masalah ini dengan hanya menggunakan karakter yang paling "murni sebagai teks" dari kumpulan karakter ASCII.
    

Banyak ahli base64 mendukung salah satu teori dan menolak teori lainnya. Seolah-olah kita harus memilih teori yang paling benar dari daftar tersebut. Namun sebenarnya, **semuanya benar**.

Masalah "7-bit" memang jauh lebih tidak relevan saat ini, tetapi dua masalah lainnya masih relevan dan base64 membantu mengatasi keduanya.

---

## Kapan Menggunakan base64?

Kapan Anda perlu menyajikan data dalam bentuk base64? Sebenarnya ada banyak situasi. Namun, mari kita pahami prinsip utamanya terlebih dahulu.

Spesifikasi resmi **RFC4648** menyatakan bahwa base64 digunakan untuk **menyimpan (store)** atau **mentransfer (transfer)** data pada lingkungan yang, mungkin karena alasan legacy, dibatasi hanya untuk data ASCII.

Jadi, Anda membutuhkan base64 ketika:

- Data yang tidak kompatibel perlu **ditransmisikan** melalui network. Salah satu contoh utamanya adalah email. Misalnya, encoding diperlukan ketika Anda ingin melampirkan gambar ke dalam sebuah pesan yang berbentuk teks. Inilah alasan base64 pertama kali diperkenalkan.
    
- Data yang tidak kompatibel perlu **disimpan** dalam file atau tempat lainnya. Sering kali Anda perlu memasukkan data non-textual ke dalam **file** berbasis teks seperti JSON, XML, atau HTML. Anda juga mungkin perlu menyimpan data tertentu di dalam browser **cookie**, sedangkan cookie pada dasarnya harus berupa teks.
    

Spesifikasi resmi tersebut juga menyatakan bahwa base64:

> "memungkinkan object dimanipulasi menggunakan **text editors**."

Kemungkinan yang dimaksud adalah "rich text editors" seperti Microsoft Word, tempat Anda dapat menggabungkan teks dengan gambar dan berbagai jenis konten lainnya. Apakah program seperti itu menggunakan base64 untuk embedded content? Hal tersebut mungkin saja terjadi, tetapi kita tidak akan membahasnya lebih jauh di sini.

---

## Kasus pada SMTP

SMTP adalah email protocol yang sudah sangat lama tetapi masih banyak digunakan hingga sekarang oleh Gmail, Outlook, dan layanan lainnya. SMTP menentukan bagaimana pesan email harus dikirimkan antar-server.

Aturan SMTP pada awalnya sangat ketat, dan menjelang akhir tahun 1980-an aturan tersebut sudah menjadi masalah yang cukup merepotkan.

Pertama-tama, SMTP hanya mengizinkan plain text dalam bahasa Inggris, yang hanya terdiri dari **128 karakter** yang dikenal sebagai ASCII. Oleh karena itu, diperlukan berbagai workaround agar sistem dapat mengirimkan teks non-English maupun attachment non-textual.

  ![[email-sending.webp]]

_Diagram yang menunjukkan bagaimana email dikirim antara dua orang melalui server menggunakan teks bahasa Inggris._

Base64 menyelesaikan masalah tersebut dengan mengubah semua data menjadi **"safe English text"**.

Conversion ini hanya diperlukan untuk sementara. Setelah data melewati sistem yang memiliki batasan tersebut, data dapat dikonversi kembali ke bentuk normal.

Pada dasarnya, ini merupakan praktik yang cukup buruk yang kurang lebih mirip dengan contraband. Data di-obfuscate (meskipun sebenarnya istilah yang lebih tepat bukan demikian) agar dapat melewati sistem yang tidak mengizinkan jenis data tersebut.

Dan sebenarnya, batasan SMTP pada awalnya dibuat untuk alasan **safety**. Namun hal tersebut terjadi sangat lama sekali. Saat ini, orang membutuhkan channel yang tidak mengganggu untuk mentransportasikan berbagai jenis data.

Dengan demikian, aturan lama tersebut sekarang terasa seperti birokrasi yang mengganggu. Namun, begitulah legacy systems bekerja dan kita harus tetap berurusan dengannya.

---

## Apakah Keterbatasan Tersebut Masih Relevan Saat Ini?

Ya, meskipun sudah ada berbagai extension dan workaround.

Banyak keterbatasan SMTP telah dikurangi berkat berbagai extension. Misalnya, extension **"8BIT MIME"** memungkinkan Anda mengirim email menggunakan 8-bit bytes dan karakter selain ASCII.

Secara teori, saat ini Anda dapat mengirim email beserta attachment tanpa melakukan encoding.

Namun dalam praktiknya, masih tidak mungkin untuk sepenuhnya mengabaikan batasan lama tersebut. Alasannya adalah masih terdapat email server lama yang belum mengadopsi extension baru.

Anda tetap harus dapat berkomunikasi dengan server-server tersebut meskipun email server Anda sendiri sudah mendukung berbagai fitur modern.

Sebelum mengirim pesan ke sebuah email server tertentu, Anda terlebih dahulu menanyakan jenis aturan SMTP apa saja yang didukungnya.

Apakah server tersebut mengimplementasikan extension 8BIT MIME? Jika tidak, Anda perlu mengubah pesan ke format yang lebih lama.

---

## Bagaimana base64 Mengatasi Keterbatasan Tersebut?

Sudah cukup jelas bahwa base64 merupakan solusi untuk masalah **"ASCII only"**, karena base64 mengubah semua data menjadi karakter ASCII.

Namun, menjadi kurang jelas ketika kita menghubungkannya dengan masalah **"7 bits"**.

Apa pun karakter yang digunakan, karakter tersebut harus dapat ditransmisikan melalui channel 7-bit maupun 8-bit, tergantung situasinya.

Para ahli biasanya mengatakan sesuatu seperti:

> "Base64 mengubah binary sequence `01001101 01100001 01101110` (apa pun artinya) menjadi teks `TWFu`."

Pernyataan seperti ini dapat membuat kita berpikir bahwa sesuatu yang awalnya binary berubah menjadi non-binary.

Sebenarnya, semua karakter ASCII yang dihasilkan oleh base64 pada akhirnya tetap berupa bits dan bytes, sama seperti data aslinya.

Perbedaannya adalah **jumlah dan urutan bits tersebut berubah**.

Berikut adalah bash command untuk mendapatkan binary representation dari sebuah string:

```
echo -n "TWFu" | xxd -b
```

Command tersebut akan menunjukkan bahwa `TWFu` sebenarnya adalah:

```
01010100 01010111 01000110 01110101
```

Namun, jika setiap karakter memiliki panjang 8 bits, sebuah 7-bit channel mungkin tidak mengenali `TWFu` sebagai text.

Artinya, perlu dilakukan manipulasi binary tambahan agar data dapat bekerja pada kedua jenis channel tersebut.

Untungnya, dengan ASCII, manipulasi binary tersebut cukup mudah.

Untuk menyimpan sebuah karakter ASCII di memory, sebenarnya hanya dibutuhkan **7 bits**. Bit tersebut dapat diperluas menjadi 8 bits apabila diperlukan sebuah conventional "octet".

Caranya cukup dengan menambahkan satu bit `0` di bagian depan tujuh bit asli.

Sebagai contoh, karakter `"T"` dapat disimpan sebagai:

```
1010100
```

atau:

```
01010100
```

Jadi, conversion antara karakter ASCII 7-bit dan 8-bit pada dasarnya hanya membutuhkan penambahan atau penghapusan bit `0` paling kiri.

Tampaknya email server harus melakukan proses semacam ini ketika berkomunikasi satu sama lain.

  ![[T-1.webp]]

_Gambar menunjukkan bagaimana karakter "T" yang dihasilkan oleh base64 dapat digunakan oleh channel 7-bit maupun 8-bit._

Dengan demikian, perlu diingat bahwa base64 sendiri **tidak menyelesaikan masalah "7 bit"**.

Base64 hanya menghasilkan karakter ASCII, sehingga memungkinkan conversion yang mudah antara 7-bit dan 8-bit.

Conversion tersebut sebenarnya merupakan tanggung jawab sistem yang lebih luas, seperti **MIME**, yang merupakan extension dari SMTP.

---

## Biaya Memory Bergantung pada Panjang Byte

Jika Anda hanya menggunakan 7 bits untuk setiap karakter, base64 seharusnya menjadi lebih hemat dalam penggunaan memory.

Teori yang umum menyatakan bahwa base64 menyebabkan memory overhead sebesar **33%** (atau 37%, atau angka lainnya). Namun, tampaknya angka tersebut hanya benar untuk skenario 8-bit.

Seperti yang telah dijelaskan sebelumnya, base64 mengubah setiap kelompok 6-bit dari data asli menjadi satu karakter ASCII.

Jika karakter tersebut memiliki panjang 8 bits, berarti terdapat 2 bits yang terbuang untuk setiap kelompok data asli.

Hal ini menghasilkan overhead sekitar 33%, sesuai dengan yang biasanya dijelaskan oleh para ahli.

Namun, jika karakter tersebut menggunakan 7 bits, kehilangan tersebut seharusnya kira-kira setengah dari ukuran tersebut.

---

## Mengapa Hanya 64 Karakter?

Base64 sebenarnya akan terlalu berlebihan jika hanya dibuat untuk melewati batasan ASCII.

ASCII memiliki **128 karakter**. Jika semua karakter tersebut dapat digunakan, algoritma encoding akan lebih efisien dalam penggunaan memory.

Secara singkat, dengan alphabet berukuran 128 karakter, satu karakter dapat merepresentasikan **7 bits** data asli, bukan hanya 6 bits.

Namun, pembuat base64 memutuskan untuk hanya menggunakan **setengah dari karakter ASCII**, dan tentu saja mereka memiliki alasan yang sangat baik.

Sebuah karakter dapat menjadi salah atau tidak aman (**unsafe**) setidaknya karena dua alasan:

1. Karakter tersebut dapat **invalid**, yaitu dilarang oleh suatu sistem. Contohnya SMTP melarang karakter di luar ASCII.
    
2. Karakter tersebut dapat valid tetapi secara tidak sengaja dikenali sebagai **special character**.
    

Di dalam ASCII terdapat lebih dari 30 **control characters**.

Karakter-karakter ini tidak dapat dicetak (**non-printable**) dan digunakan untuk menghasilkan efek tertentu.

Contohnya adalah:

- line feed
    
- backspace
    
- delete
    
- escape
    

Banyak command tersebut merupakan peninggalan dari perangkat-perangkat lama seperti teleprinter.

  ![[ascii-control-chars.webp]]

_Tabel yang menunjukkan 34 karakter non-printable dari kumpulan ASCII._

Karena itu, semua non-printable characters harus dikeluarkan dari alphabet encoding.

Setelah itu, tersisa lebih dari 90 printable characters.

Namun, printable tidak berarti aman dan reliable.

Karakter-karakter tersebut juga dapat memiliki **special meaning** dalam sistem tertentu.

Banyak karakter memiliki makna khusus dalam SMTP, misalnya `"@"`, `"<"`, dan `">"`.

Karakter-karakter tersebut dapat menghasilkan efek yang tidak diinginkan.

Pada akhirnya, digunakanlah **64 karakter**.

Salah satu alasannya adalah karena angka 64 lebih mudah digunakan secara algorithmically.

Selain itu, kumpulan karakter tersebut terlihat cukup aman untuk digunakan pada berbagai jenis sistem, bukan hanya SMTP.

Sayangnya, alphabet tersebut tidak sepenuhnya aman.

Hanya terdapat **62 karakter** yang dijamin tidak memiliki special meaning pada semua sistem.

Karakter tersebut adalah:

- angka
    
- huruf kecil bahasa Inggris
    
- huruf kapital bahasa Inggris
    

Base64 membutuhkan **2 karakter tambahan**.

Pemilihan dua karakter tersebut dapat berbeda tergantung sistem.

Karakter yang paling umum digunakan adalah:

```
+
/
```

Namun, pada beberapa situasi karakter tersebut dapat menyebabkan masalah.

Sebagai contoh, keduanya memiliki special meaning dalam URL.

Karena itu terdapat varian **base64url**, yang menggunakan:

```
_
-
```

sebagai pengganti dua karakter tersebut.

---

## Base64 Tidak Memperbaiki Masalah "Ambiguous" Special Characters

Di sini terdapat sebuah misconception yang cukup sering muncul dalam pembahasan mengenai base64.

Beberapa special characters diperlakukan secara berbeda oleh sistem yang berbeda.

Contoh yang paling terkenal adalah **line feed** dan **carriage return**.

Keduanya berhubungan dengan line breaks.

Namun, sistem yang berbeda memiliki cara berbeda dalam menggabungkan kedua karakter tersebut untuk menghasilkan line break yang sebenarnya.

Ada anggapan bahwa base64 dapat membantu menyelaraskan perbedaan tersebut.

Namun, base64 tidak memiliki hubungan dengan bagaimana data **diinterpretasikan**.

Sebagai contoh, base64 tidak menentukan bagaimana sebuah teks ditampilkan pada layar.

Untuk menampilkan data tersebut, Anda terlebih dahulu harus melakukan **decode** dari base64 kembali ke bentuk asli.

Data hasil decoding akan sama persis dengan data sebelum encoding.

Urutan bits-nya tetap sama dan karakter-karakter ambigu tersebut juga tetap sama.

Jadi, sekali lagi, base64 hanya dapat **menyembunyikan** special characters untuk sementara.

Base64 tidak secara ajaib melakukan sanitization terhadap data dari dangerous characters.

---

## Apakah Saya Harus Menggunakan base64 dengan HTTP/1.1?

HTTP/1.1 merupakan protocol yang berbasis teks.

Karena itu, Anda mungkin bertanya apakah data non-textual harus di-encode agar dapat dikirimkan melalui Internet.

Dalam pembahasan ini, kita akan menyebutnya cukup sebagai HTTP.

Perlu diingat bahwa **HTTP/2 dan HTTP/3 merupakan binary protocols**, sehingga keduanya tidak menjadi fokus pembahasan ini.

HTTP sebenarnya memungkinkan **semua jenis data** berada di dalam **body** sebuah message.

Body tidak dibatasi hanya untuk karakter tekstual.

Sebagai contoh, sebuah image dapat dikirim dalam bentuk aslinya tanpa perlu mengacak atau mengubah bits dan bytes-nya.

Bagian yang benar-benar "text-based" dari HTTP adalah **headers**.

Pada dasarnya, headers dibatasi pada ASCII.

Hal ini sebenarnya tidak sepenuhnya benar, tetapi menggunakan ASCII saja merupakan praktik yang baik.

Saat ini HTTP headers digunakan dalam berbagai cara dan terkadang harus membawa data non-ASCII.

Sebagai contoh, sebuah basic HTTP authentication scheme menyarankan agar username dan password dikirim sebagai bagian dari **"Authentication" header**.

Username dan password dapat mengandung berbagai karakter yang tidak kompatibel.

Oleh karena itu, data tersebut harus di-encode menjadi karakter tekstual yang aman.

Base64 direkomendasikan untuk digunakan dalam kasus seperti ini.

Karena alasan tersebut, beberapa developer menganggap bahwa base64 merupakan semacam encryption atau perlindungan data.

**Hal tersebut tidak benar.**

Base64 adalah **encoding**, bukan encryption.

---

## Mengapa base64 Digunakan untuk Data URLs? Apakah Ada Encoding yang Lebih Efisien?

Data URLs mungkin merupakan salah satu penggunaan base64 yang paling terkenal saat ini.

Data URLs merupakan cara untuk memasukkan berbagai asset seperti image secara langsung ke dalam file HTML atau CSS, bukan dengan menggunakan link menuju asset tersebut, tetapi dengan memasukkan kode data sebenarnya.

Perlu diperhatikan bahwa Data URLs tidak memiliki hubungan dengan transmission data.

Base64 digunakan di sini bukan karena HTTP protocol melarang binary sequences.

Ketika HTML atau CSS dikirim melalui network, HTTP tidak peduli dengan isi file tersebut.

Namun, HTML dan CSS harus berbentuk teks agar dapat diinterpretasikan dan ditampilkan dengan benar oleh text editors dan browsers.

Hal tersebut memang masuk akal, tetapi tetap memiliki kekurangan karena base64 cukup mahal.

Memory overhead yang terkenal sebesar **33% atau 37%** sangat mengganggu terutama ketika digunakan dalam Data URLs.

Dalam banyak kasus, overhead tersebut justru menghilangkan tujuan penggunaan Data URLs.

Tujuan utamanya tentu saja adalah meningkatkan **performance**.

Anda mendapatkan image tanpa melakukan HTTP request tambahan sehingga dapat menghemat beberapa milliseconds.

Namun, peningkatan performance tersebut relatif kecil dan dapat dengan mudah dihilangkan oleh tambahan bytes yang dihasilkan oleh base64.

Lalu, mengapa base64 tetap digunakan untuk Data URLs?

Apakah kita dapat menggunakan encoding yang lebih hemat, misalnya encoding yang menggunakan alphabet lebih besar sehingga menghasilkan string yang lebih pendek?

Saat ini, hal tersebut sangat tidak mungkin.

Alasannya adalah browsers hanya mengizinkan **URL-safe characters** dalam Data URLs.

Jumlah URL-safe characters tidak terlalu banyak, hanya sedikit lebih banyak dari 64 karakter.

Mengapa kita dibatasi pada URL-safe characters?

Karena encoded data tersebut dimasukkan ke dalam tempat yang oleh browser dianggap sebagai sebuah URL.

Secara teori, browser dapat dibuat lebih pintar dan melonggarkan batasan tersebut ketika diperlukan.

Karena itu, muncul pertanyaan yang lebih luas.

---

## Apakah Ada Encoding yang Lebih Baik untuk Data Non-Textual di HTML?

Secara teknis, Data URLs **bukan satu-satunya cara** untuk memasukkan data non-textual ke dalam file HTML.

Anda dapat membuat solusi sendiri, misalnya dengan memasukkan data non-textual ke bagian lain dari HTML markup seperti attributes, `innerText`, atau tempat lainnya.

Dalam kasus seperti itu, Anda tidak dibatasi oleh URL-safe alphabet.

Secara teori, Anda dapat menggunakan karakter apa pun yang diperbolehkan oleh HTML.

Sebagian besar file HTML menggunakan character set **UTF-8**.

UTF-8 mencakup seluruh karakter Unicode, yang jumlahnya lebih dari 1 juta.

Dengan demikian, secara teori kita dapat membuat sebuah encoding **baseNNN** yang menggunakan setidaknya 256 karakter Unicode.

Encoding seperti itu hampir tidak akan memiliki memory overhead.

Namun, dalam praktiknya semuanya jauh lebih rumit.

  ![[chars-3.webp]]

_Diagram yang menunjukkan betapa sedikitnya karakter UTF-8 yang benar-benar aman dan dapat digunakan untuk hypothetical baseNNN encoding._

Mengapa kita tidak menggunakan karakter bahasa Chinese, misalnya?

Karena karakter-karakter tersebut terlalu berat.

Karakter tersebut membutuhkan 3 atau bahkan 4 bytes memory.

Begitulah cara UTF-8 bekerja: UTF-8 menggunakan jumlah bytes yang berbeda untuk karakter yang berbeda.

Dalam pembahasan ini, kita hanya tertarik pada karakter yang menggunakan **1 byte**.

Anda sebenarnya dapat mempertimbangkan penggunaan multi-byte characters untuk baseNNN encoding, tetapi kita tidak akan membahasnya di sini.

Anggap saja bahwa kita hanya membutuhkan karakter 1-byte.

Berapa banyak karakter 1-byte yang tersedia dalam UTF-8?

Hanya **128 karakter**, yaitu rentang ASCII yang sudah kita kenal.

Apakah kita dapat menggunakan semuanya?

Tidak.

Sekali lagi, kita hanya membutuhkan printable characters.

Karakter tersebut harus dapat dilihat dengan baik di text editors, developer tools, dan berbagai tempat lainnya.

Kemudian, seperti pada kasus SMTP, kita harus menghilangkan sejumlah visible characters karena karakter-karakter tersebut memiliki special meaning dalam HTML.

Sebagai contoh, double quote (`"`) tidak dapat digunakan karena dapat menghentikan string Data URL secara prematur.

Contoh berikut tidak akan bekerja:

```html
<img src="data:image/png;base64,iVBOR"w0KAA" />
```

Dengan demikian, alphabet yang tersedia kembali menyusut menjadi sekitar **80–90 karakter**.

Secara teori, hal tersebut memungkinkan kita membuat encoding lain yang menggunakan memory sedikit lebih kecil daripada base64.

Encoding seperti itu sebenarnya memang ada.

Salah satunya adalah **base85**, yang dibuat oleh Adobe.

Base85 lebih efisien dalam penggunaan memory karena meng-encode **4 bytes** data asli menjadi **5 karakter**.

Namun, base85 juga jauh lebih lambat untuk dihitung sehingga manfaat keseluruhannya sangat kecil, jika memang ada.

Selain itu, base85 tidak ditujukan untuk web development dan mengandung karakter yang dapat merusak atau mengganggu HTML dan CSS.

Walaupun demikian, secara teori mungkin untuk membuat algoritma yang serupa tetapi web-friendly dengan mengganti karakter-karakter tersebut.

Lalu, apakah kita dapat menemukan baseNNN yang lebih baik untuk jenis text files lainnya seperti JSON, XML, dan sebagainya?

Tampaknya hal tersebut tidak mungkin.

Alasannya karena format-format tersebut sebagian besar menggunakan encoding UTF-8.

Artinya, kita akan menghadapi keterbatasan yang kurang lebih sama seperti pada HTML.

Jumlah special printable characters mungkin berbeda—misalnya jumlahnya sangat kecil dalam JSON—tetapi perbedaannya tidak terlalu signifikan.

---

# Kesimpulan

Base64 pertama kali diperkenalkan sebagai cara untuk melewati sejumlah keterbatasan kuno yang diberlakukan terhadap email oleh **SMTP protocol**.

Base64 memungkinkan data apa pun untuk "disamarkan" sebagai teks sehingga dapat melewati validation ketika ditransmisikan antara email servers.

Base64 juga memastikan bahwa pseudo-text tersebut hanya menggunakan karakter yang aman, yaitu:

1. Hanya karakter yang dapat dicetak (**printable characters**).
    
2. Hanya karakter yang tidak memiliki special meaning dalam SMTP dan, mudah-mudahan, dalam sebagian besar sistem lainnya.
    

Alphabet yang dihasilkan ternyata sangat terbatas.

Namun, alphabet tersebut memungkinkan base64 digunakan hampir di mana saja, meskipun dalam beberapa varian yang sedikit berbeda.

Base64 sangat membantu dalam berbagai situasi ketika kita harus menggabungkan data tekstual dan non-textual.

Sistem modern juga masih menggunakan base64 meskipun memiliki memory cost yang cukup besar.

Pada pandangan pertama, hal ini terlihat aneh karena sistem modern tidak lagi memiliki keterbatasan kuno seperti yang dahulu dimiliki SMTP.

Namun, ternyata dalam banyak kasus kita masih hanya memiliki sedikit karakter yang murah digunakan dan tidak memiliki special meaning.

Sementara itu, alternatif terhadap base64 hanya memberikan keuntungan yang sangat kecil.

---

materi tersebut diterjemahkan dari sumber berikut
- [FreeCodeCamp - What is base64 Encoding and Why is it Necessary?](https://www.freecodecamp.org/news/what-is-base64-encoding/)