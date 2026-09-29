## Apa itu XOR
Exclusive OR atau [XOR](https://www.geeksforgeeks.org/digital-logic/xor-gate/) adalah jenis operator biner dalam operasi logis. Gerbang ini mengambil masukan dari dua variabel dan memberikan keluaran tunggal. Ini memberikan output setinggi ketika satu input tinggi dan yang lainnya rendah. Outputnya akan rendah bila kedua inputnya sama (tinggi atau rendah). Gerbang ini seperti fungsi pertidaksamaan karena keluarannya Tinggi atau Benar hanya jika kedua masukannya berbeda.

| x   | y   | x XOR y |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 1       |
| 1   | 0   | 1       |
| 1   | 1   | 0       |
## Contoh
### contoh
> 5 = 00000101
> 3 = 00000011
> =========
>     00000110
> = 6

### contoh pada python

``` python
a = 5
b = 3
print ( a ^ b ) // output: 6
```