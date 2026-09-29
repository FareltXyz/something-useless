## Vigenere Cipher

**Vigenere Cipher** merupakan jenis algoritma cryptography dengan melakukan perubahan informasi melalui subtitusi (pergeseran) dengan menggunakan **key** berupa deretan kata.

Algoritma ini pertama kali dikenalkan oleh [Giovan Battista Bellaso](https://en.wikipedia.org/wiki/Giovan_Battista_Bellaso) pada abad ke 16 dengan sebutan **Autokey Cipher**. Algoritma ini sangatlah tangguh terhadap pembobolan sampai abad ke 19. Sampai dengan [Friedrich Kasiski](https://en.wikipedia.org/wiki/Friedrich_Kasiski) memperkenalkan metode miliknya untuk melakukan **dechipering Vigenere Cipher** yang disebut **Kasiski Algorithm.** Pada abad ke 19 juga seorang ilmuan bernama [Blaise de Vigenère](https://en.wikipedia.org/wiki/Blaise_de_Vigen%C3%A8re) memperbaharui algoritma **Autokey Cipher**, dan telah terjadi kesalah pahaman tentang “first inventor” dari algoritma ini, sehingga namanya-lah yang digunakan sebagai nama dari algoritma **Vigenere Cipher** hingga sampai saat ini.

Pada dasarnya algoritma ini hampir sama dengan algoritma **Caesar Cipher** hanya saja **key** yang digunakan tidak menggunakan satu nilai, melainkan deretan kata yang telah dimetakan kedalam angka numerik. Formula yang digunakan untuk melakukan **encryption** dan **decryption**nya pun serupa yaitu:

| Encryption              | Decryption             |
| ----------------------- | ---------------------- |
| E(x) = ( x + k ) mod 26 | D(x) = ( x- k ) mod 26 |
- E(x) adalah hasil **encryption**, dimana x adalah dari huruf original atau **plaintext**.
- D(x) adalah hasil **decryption**, dimana x adalah dari huruf yang telah terdecrypt atau **ciphertext**.
- k adalah nilai atau **key** yang digunakan untuk menggeser huruf. Pada **Vigenere Cipher** i menunjukan huruf ke- yang dilakukan **encryption**
- Mod 26 masih digunakan dikarenakan untuk membuat kata kita masih menggunakan huruf alfabet, sehingga ketika nilai operasinya lebih atau kurang dari 26 maka kita akan tetap dapat melakukan pemetaannya.
- Kita ingin memastikan bahwa hasil dari encryption masih berada dalam rentang dari (0, ukuran_alfabet-1), sehingga kita gunakanlah mod26.

sumber: https://kresna-devara.medium.com/cryptography-vigenere-cipher-5575752f4d10