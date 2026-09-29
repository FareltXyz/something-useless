## Apa itu Kerentanan dan Paparan Umum (CVE)?

Common Vulnerabilities and Exposures (CVE) umumnya mengacu kepada daftar CVE, katalog kerentanan keamanan informasi yang diungkapkan secara publik yang dibuat dan dikelola oleh MITRE Corporation.

Katalog CVE lebih seperti kamus dibandingkan basis data CVE. Katalog ini memberikan satu nama dan satu deskripsi untuk setiap kerentanan atau eksposur. Dengan demikian, dimungkinkan untuk melakukan komunikasi antara alat dan basis data yang berbeda dan membantu meningkatkan interoperabilitas dan cakupan keamanan. CVE adalah unduhan dan penggunaan gratis atau publik. Daftar CVE memberi umpan National Vulnerability Database (NVD) AS.

CVE, organisasinya, adalah “upaya internasional berbasis komunitas yang mengelola registri data terbuka berbasis 

komunitas tentang kerentanan [keamanan siber](https://www.ibm.com/id-id/think/topics/cybersecurity) yang diketahui secara terbuka, yang dikenal sebagai daftar CVE.”1  

Salah satu tantangan mendasar dalam keamanan siber adalah mengidentifikasi dan mengurangi kerentanan yang dapat dieksploitasi oleh peretas untuk membahayakan [aplikasi](https://www.ibm.com/id-id/think/topics/application-security), sistem, dan data. CVE membantu menjawab tantangan ini dengan menyediakan kerangka kerja standar untuk membuat katalog dan melacak kerentanan keamanan siber yang dapat digunakan organisasi untuk meningkatkan proses manajemen kerentanan.

Sistem CVE menggunakan pengidentifikasi unik, yang dikenal sebagai ID CVE (terkadang disebut nomor CVE), untuk memberi label pada setiap kerentanan yang dilaporkan. Sistem ini memfasilitasi komunikasi yang efektif, kolaborasi dan pengelolaan kelemahan keamanan.

Perusahaan MITRE menciptakan CVE pada tahun 1999 sebagai katalog referensi untuk mengategorikan kerentanan keamanan pada perangkat lunak dan firmware. Sistem CVE membantu organisasi mendiskusikan dan berbagi informasi mengenai kerentanan keamanan siber, menilai tingkat keparahan kerentanan, dan membuat sistem komputer menjadi lebih aman.

Dewan Editorial CVE mengawasi program CVE. Dewan ini terdiri atas anggota dari organisasi yang terkait dengan keamanan siber, anggota dari akademisi, lembaga penelitian, lembaga pemerintah, dan pakar keamanan terkemuka lainnya. Di antara tugas-tugas lainnya, dewan menyetujui sumber data, cakupan produk, sasaran cakupan untuk entri Daftar CVE, dan mengelola penetapan entri baru yang sedang berlangsung.1

US-CERT di biro Keamanan Siber dan Komunikasi di Departemen Keamanan Dalam Negeri AS (DHS) mensponsori program CVE.1

## Kerentanan versus eksposur

Program CVE mendefinisikan kerentanan sebagai “kelemahan dalam logika komputasi yang ditemukan pada komponen perangkat lunak dan perangkat keras yang, jika dieksploitasi, akan mengakibatkan dampak negatif pada kerahasiaan, integritas, atau ketersediaan.” Jadi kerentanan mengacu kepada kelemahan, seperti kesalahan pengodean, yang dapat digunakan oleh penyerang untuk mendapatkan akses tidak sah ke jaringan dan sistem, menginstal [malware](https://www.ibm.com/id-id/think/topics/malware), menjalankan kode, dan mencuri atau menghancurkan data sensitif. Eksposur memungkinkan akses itu.

Bayangkan sebuah rumah: Titik lemahnya adalah jendela dengan kunci yang mudah dibobol pencuri. Eksposur adalah jendela yang lupa dikunci oleh seseorang.

## Apa yang memenuhi syarat sebagai CVE?

Agar memenuhi syarat sebagai CVE, dan diberi pengenal CVE (CVE ID), kelemahan keamanan harus memenuhi kriteria tertentu:

- **Dapat diperbaiki secara terpisah dari kelemahan lainnya:** Kecacatan tersebut harus dapat diperbaiki secara terpisah dari kerentanan lainnya.  
      
    
- **Diakui oleh vendor atau didokumentasikan dalam laporan kerentanan:** Vendor harus mengakui bahwa bug tersebut ada dan berdampak negatif pada keamanan. Atau harus ada laporan kerentanan yang menunjukkan dampak negatif bug terhadap keamanan dan pelanggaran terhadap kebijakan keamanan sistem yang terpengaruh.
- **Memengaruhi satu basis kode:** Bug hanya boleh memengaruhi satu basis kode (satu produk). Kecacat yang memengaruhi lebih dari satu produk diberi CVE terpisah untuk setiap produk.

## Bagaimana ID CVE ditetapkan: CNAs dan root

Otoritas penomoran CVE (CNA) menetapkan ID CVE dan menerbitkan catatan CVE dalam lingkup tertentu. Perusahaan MITRE berfungsi sebagai editor dan CNA utama. CNA lainnya termasuk vendor sistem operasi (OS) dan TI utama (termasuk IBM, Microsoft, dan Oracle), peneliti keamanan, dan entitas resmi lainnya. CNA beroperasi atas dasar sukarela. Saat ini terdapat 389 CNA dari 40 negara berbeda.2

### Roots dan akar tingkat atas

Root adalah organisasi yang berwenang untuk merekrut, melatih, dan mengatur CNA atau akar lain dalam lingkup tertentu.

Akar tingkat atas adalah akar tingkat tertinggi dan bertanggung jawab atas “tata kelola dan administrasi hierarki tertentu, termasuk akar dan CNA di dalam hierarki tersebut.”3 Saat ini ada dua akar tingkat atas dalam program CVE: Perusahaan MITRE dan Badan Keamanan Siber dan Infrastruktur (CISA).

Informasi tambahan tentang struktur organisasi CVE dapat ditemukan [di sini](https://www.cve.org/ProgramOrganization/Structure).

### Siklus hidup catatan CVE

Siapa pun dapat mengirimkan laporan CVE. Kerentanan sering kali ditemukan oleh peneliti keamanan siber, profesional keamanan, vendor perangkat lunak, anggota komunitas sumber terbuka, dan pengguna produk melalui berbagai cara, seperti penelitian independen, penilaian keamanan, [pemindaian kerentanan](https://www.ibm.com/id-id/think/topics/vulnerability-scanning), aktivitas [respons insiden](https://www.ibm.com/id-id/think/topics/incident-response), atau sekadar menggunakan produk. Banyak perusahaan menawarkan program bug bounty—imbalan untuk menemukan dan melaporkan kerentanan yang ditemukan dalam perangkat lunak secara bertanggung jawab.

Setelah kerentanan baru diidentifikasi dan dilaporkan, itu diserahkan ke CNA untuk evaluasi. CVE baru kemudian dicadangkan untuk kerentanan. Ini adalah keadaan awal dari catatan CVE.

Setelah memeriksa kerentanan yang dimaksud, CNA mengirimkan perincian termasuk produk mana yang terpengaruh, versi produk yang diperbarui atau diperbaiki, jenis kerentanan, akar masalah dan dampaknya, dan setidaknya satu referensi publik. Ketika elemen data ini telah ditambahkan ke catatan CVE, CNA akan menerbitkan catatan tersebut ke daftar CVE, sehingga tersedia untuk umum.

Entri CVE kemudian menjadi bagian dari daftar resmi CVE, yang dapat diakses oleh para profesional keamanan siber, peneliti, vendor, dan pengguna di seluruh dunia. Organisasi dapat menggunakan ID CVE untuk melacak dan memprioritaskan kerentanan di dalam lingkungan mereka, menilai paparan mereka terhadap ancaman tertentu, dan menerapkan langkah-langkah mitigasi risiko yang tepat.

## Pengidentifikasi CVE (ID CVE) dan catatan CVE

Entri CVE menyertakan ID CVE, deskripsi singkat tentang kerentanan keamanan dan referensi, termasuk laporan kerentanan dan saran. ID CVE memiliki konstruksi tiga bagian:

1. ID CVE dimulai dengan awalan “CVE”  
      
    
2. Bagian kedua adalah tahun penugasan  
      
    
3. Bagian terakhir dari ID CVE adalah pengenal berurutan

ID lengkapnya terlihat seperti ini: CVE-2024-12345. ID standar ini membantu memastikan konsistensi dan interoperabilitas di berbagai platform dan repositori, sehingga memungkinkan para pemangku kepentingan untuk merujuk dan berbagi informasi tentang kerentanan tertentu dengan menggunakan "bahasa yang sama".

Catatan CVE dikaitkan dengan salah satu dari tiga status:

- **Dicadangkan:** Ini adalah status awal yang ditetapkan pada CVE sebelum diungkapkan ke publik (saat CNA memeriksa kerentanan).  
      
    
- **Diterbitkan:** Ini adalah saat CNA telah mengumpulkan dan menginput data yang terkait dengan ID CVE dan menerbitkan catatan tersebut.  
      
    
- **Ditolak:** Pada tahap ini, ID dan catatan CVE tidak boleh digunakan. Namun, catatan yang ditolak tetap ada pada daftar CVE untuk memberi tahu pengguna bahwa ID dan catatan tersebut tidak valid.  
    

## Apa yang dimaksud dengan Sistem Penilaian Kerentanan Umum (CVSS)?

Salah satu cara organisasi dapat menilai tingkat keparahan kerentanan adalah dengan menggunakan [Sistem Penilaian Kerentanan Umum (CVSS)](https://www.ibm.com/id-id/think/topics/cvss). CVSS, yang dioperasikan oleh Forum Tim Tanggap Insiden dan Keamanan (FIRST), merupakan metode standar yang digunakan oleh Basis Data Kerentanan Nasional (NVD), Tim Tanggap Darurat Keamanan Siber (CERT), dan lainnya, untuk menilai tingkat keparahan dan dampak kerentanan yang dilaporkan. Ini terpisah dari sistem CVE tetapi digunakan bersama CVE: Format catatan CVE memungkinkan CNA untuk menambahkan skor CVSS ke catatan CVE saat menerbitkan catatan ke daftar CVE.6

CVSS memberikan skor numerik untuk kerentanan, mulai dari 0,0 hingga 10, berdasarkan eksploitasi, lingkup dampak, dan metrik lainnya. Semakin tinggi skor, semakin parah masalahnya. Skor ini membantu organisasi mengukur urgensi penanganan kerentanan tertentu dan mengalokasikan sumber daya yang sesuai. Tidak jarang organisasi juga menggunakan sistem penilaian kerentanan mereka sendiri.

Skor CVSS dihitung berdasarkan skor dari tiga kelompok metrik—dasar, temporal, dan lingkungan—yang menggabungkan karakteristik kerentanan yang berbeda.

### Metrik dasar

Perusahaan paling banyak mengandalkan skor metrik dasar, dan peringkat tingkat keparahan publik seperti yang disediakan di Basis Data Kerentanan Institut Standar dan Teknologi Nasional (NIST), menggunakan skor metrik dasar secara eksklusif. Skor metrik dasar ini tidak mempertimbangkan karakteristik kerentanan yang berubah seiring waktu (metrik temporal), faktor dunia nyata seperti lingkungan pengguna atau tindakan yang telah diambil perusahaan untuk mencegah eksploitasi bug.

Metrik dasar dipecah lebih lanjut antara metrik eksploitabilitas dan metrik dampak:

- Metrik eksploitasi mencakup faktor-faktor seperti vektor serangan, kompleksitas serangan, dan hak istimewa yang diperlukan.  
      
    
- Metrik dampak mencakup dampak kerahasiaan, dampak integritas, dan dampak ketersediaan.4  
    

### Metrik temporal

Metrik temporal mengukur kerentanan dalam keadaannya saat ini dan digunakan untuk mencerminkan tingkat keparahan dampak yang berubah dari waktu ke waktu. Remediasi apa pun juga digabungkan,seperti patch yang tersedia. Kematangan kode eksploitasi, tingkat remediasi, dan kepercayaan laporan adalah komponen dari skor metrik temporal.

### Metrik lingkungan

Metrik lingkungan memungkinkan organisasi untuk menyesuaikan skor dasar sesuai dengan lingkungan dan persyaratan keamanannya sendiri. Skor ini membantu menempatkan kerentanan dalam konteks yang lebih jelas karena berkaitan dengan organisasi dan mencakup skor persyaratan kerahasiaan, skor persyaratan integritas, dan skor persyaratan ketersediaan. Metrik ini dihitung bersama dengan metrik dasar yang dimodifikasi yang mengukur lingkungan tertentu (seperti vektor serangan yang dimodifikasi dan kompleksitas serangan yang dimodifikasi) untuk mencapai skor metrik lingkungan.

## Dampak CVE pada manajemen kerentanan

Program CVE merupakan pendekatan kolaboratif dan sistematis untuk mengidentifikasi, membuat katalog, dan mengatasi kerentanan dan paparan keamanan siber. Dengan menawarkan sistem standar untuk mengidentifikasi dan mereferensikan kerentanan, CVE membantu organisasi meningkatkan [manajemen kerentanan](https://www.ibm.com/id-id/think/topics/vulnerability-management) dengan beberapa cara:

Bagikan informasi

CVE membantu organisasi mendiskusikan dan berbagi informasi mengenai kerentanan menggunakan pengenal umum. Sebagai contoh, penasihat keamanan sering kali menerbitkan daftar CVE, bersama dengan skor CVSS, yang digunakan perusahaan untuk menginformasikan strategi manajemen risiko dan siklus perencanaan patch mereka.

Perkuat postur keamanan siber

CVE membantu organisasi mengelola risiko keamanan secara efektif, meningkatkan visibilitas ancaman dan [intelijen ancaman](https://www.ibm.com/id-id/think/topics/threat-intelligence), serta memperkuat postur [keamanan siber](https://www.ibm.com/id-id/think/topics/cybersecurity) mereka secara keseluruhan dalam lingkungan ancaman yang semakin kompleks dan dinamis.

Korelasikan data dengan lebih baik

ID CVE memfasilitasi korelasi data dan memungkinkan tim TI untuk memindai berbagai sumber untuk mendapatkan informasi tentang kerentanan tertentu.

Pilih alat bantu dan strategi

Daftar CVE digunakan untuk membantu menentukan alat keamanan mana yang terbaik untuk kebutuhan organisasi dan untuk membuat strategi manajemen risiko yang mempertimbangkan kerentanan yang diketahui dan dampak potensial dari masalah keamanan ini terhadap sistem dan data perusahaan. Dengan informasi ini, organisasi dapat lebih menentukan bagaimana produk tertentu sesuai dengan postur keamanan mereka dan mengambil langkah-langkah untuk meminimalkan paparan mereka terhadap serangan siber dan [pelanggaran data](https://www.ibm.com/id-id/think/topics/data-breach).

## CVE vs. CWE

CVE adalah katalog kerentanan keamanan siber yang diketahui, di mana satu ID CVE khusus untuk satu kecacatan perangkat lunak. Common Weaknesses Enumeration (CWE) adalah proyek komunitas TI yang berisi daftar berbagai jenis atau categories kelemahan perangkat keras dan perangkat lunak, seperti kesalahan buffer, kesalahan autentikasi, atau masalah CPU. Kelemahan ini dapat menyebabkan kerentanan.

[sumber](https://www.ibm.com/id-id/think/topics/cve)