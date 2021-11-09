# Android App Development

## Mendesain Layout
Element di dalam layout (tombol, gambar, etc) disebut dengan view.
Lokasi ada pada res > layout > activity_main.xml
![](attachments/Pasted%20image%2020211109160119.png)

Three types of layout
1. Constraint  (preferable, flat, less computation)
2. Linear
3. Static (using dp scale)

> istilah penting: padding, edit text, text view, button

### Linear
- Pembuatan lebih mudah menggunakan code daripada drag and drop pada design.
- Kamu harus mendefinisikan `android:orientation` dengan nilai vertical atau horizontal
- Vertical
![](attachments/Pasted%20image%2020211109160555.png)

- Horizontal
![](attachments/Pasted%20image%2020211109160618.png)

- Kamu bisa menentukan margin antar view dalam skala dp.
- Linear layout dapat dibuat bertingkat


> istilah penting: layout_width & height, match_parent, wrap_content, fixed_size, orientation, layout_weight

### Constraint
- Linear layout bertingkat membutuhkan lebih banyak komputasi, sehingga flat desain seperti constraint dapat sangat bermanfaat.
- Peletakan view berdasarkan lokasi relatif terhadap sesuatu, bisa jadi layar paling atas dan paling kanan. Kamu harus mendefinisikan lokasi berdasarkan 2 syarat di bawah.
	- lokasi relatif secara vertikal
	- lokasi relatif secara horizontal
- Untuk membuat view yang berjejeran kamu bisa gunakan `chains -> horizontal chain`
- Apabila tiap view memiliki ukuran berbeda, kamu bisa gunakan fitur `baseline` untuk menyamakan lokasi.
- Penggunaan `layout_width` juga membantu dalam pembuatan