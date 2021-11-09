# Android App Development

## Mendesain Layout
- Element di dalam layout (tombol, gambar, etc) disebut dengan view.
 ![](attachments/viewgroup_2x.png)
 
- Lokasi ada pada `res -> layout -> activity_main.xml`
![](attachments/Pasted%20image%2020211109160119.png)

- Pada view, dapat diberikan ID untuk dipanggil pada activity. Untuk hal ini, kamu perlu meng-edit gradle module dan mengimport views. https://stackoverflow.com/questions/47199242/error-unresolved-reference-in-kotlin-android/47199702

Tiga tipe layout:
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
- Pembuatan lebih mudah dengan drag and drop pada tab design
- Linear layout bertingkat membutuhkan lebih banyak komputasi, sehingga flat desain seperti constraint dapat sangat bermanfaat.
- Peletakan view berdasarkan lokasi relatif terhadap sesuatu, bisa jadi layar paling atas dan paling kanan. Kamu harus mendefinisikan lokasi berdasarkan 2 syarat di bawah.
	- lokasi relatif secara vertikal
	- lokasi relatif secara horizontal
- Untuk membuat view yang berjejeran kamu bisa gunakan `chains -> horizontal chain` dan mengatur `layout_width` menjadi 0dp, artinya menyamakan ukuran dari view sesuai dengan constraint.
- Apabila tiap view memiliki ukuran berbeda, kamu bisa gunakan fitur `baseline` untuk menyamakan lokasi.
- Kamu bisa gunakan guideline, sebuah garis yang bisa dijadikan acuan untuk menentukan lokasi constraint.