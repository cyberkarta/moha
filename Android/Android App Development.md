# Android App Development

## Activity
- Activity bisa diartikan sebagai screen pada Android kamu. Activity juga merepresentasikan kotlin class.
- Activity stack
![](attachments/Pasted%20image%2020211109164056.png)

- Activity life-cycle
![](attachments/Pasted%20image%2020211109164204.png)

- Jika ada aplikasi dengan prioritas lebih tinggi membutuhkan memori, Android bisa mematikan aplikasi lain, kemudian jika user ingin membukanya lagi, proses dimulai dari `onCreate()`
- State `onStop()` tidak dijamin akan dipanggil, jika membutuhkan save data lebih baik dilakukan saat `onPause()`.
- Jika aplikasi berakhir pada `onStop()`, jika user membuka kembali aplikasi, akan dimulai dari `onStart()`
- State `onDestroy()` bisa jadi ketika user menutup aplikasi, menekan tombol back, atau ketika aplikasi ditutup oleh sistem.
	
## Mendesain Layout
- Element di dalam layout (tombol, gambar, etc) disebut dengan view.
 ![](attachments/viewgroup_2x.png)
 
- Lokasi ada pada `res -> layout -> activity_main.xml`
![](attachments/Pasted%20image%2020211109160119.png)

- Pada view, dapat diberikan ID untuk dipanggil pada activity. Untuk hal ini, kamu perlu meng-edit gradle module dan mengimport views. https://stackoverflow.com/questions/47199242/error-unresolved-reference-in-kotlin-android/47199702

Tiga tipe layout:
1. Constraint  (preferable, flat, less computation)
2. Linear
3. Webview

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
- Kamu bisa gunakan `guideline`, sebuah garis yang bisa dijadikan acuan untuk menentukan lokasi constraint.

> istilah penting: chains, layout_width=0dp, baseline, guideline

### Button
 btnApply.setOnClickListener { } to do process after the button is clicked
> istilah penting btnApply.setOnClickListener

## Creating Count App
activity_main.xml
```xml
<TextView  
 android:id="@+id/tvCount"  
 android:layout_width="wrap_content"  
 android:layout_height="wrap_content"  
 android:text="Let's count together: 0"  
 android:textAlignment="center"  
 android:textAllCaps="true"  
 android:textColor="@android:color/holo_green_light"  
 android:textSize="24sp"  
 android:textStyle="bold|italic"  
 app:layout_constraintBottom_toBottomOf="parent"  
 app:layout_constraintEnd_toEndOf="parent"  
 app:layout_constraintStart_toStartOf="parent"  
 app:layout_constraintTop_toTopOf="parent" />  
  
<Button  
 android:id="@+id/btnPlusOne"  
 android:layout_width="wrap_content"  
 android:layout_height="wrap_content"  
 android:text="+1"  
 app:layout_constraintEnd_toEndOf="parent"  
 app:layout_constraintHorizontal_bias="0.526"  
 app:layout_constraintStart_toStartOf="parent"  
 app:layout_constraintTop_toBottomOf="@+id/tvCount" />
```

MainActivity.kt
```kt
var countMe = 0  
btnPlusOne.setOnClickListener {  
 countMe++  
    tvCount.text = "Let's count together: $countMe"  
}
```

![](attachments/Pasted%20image%2020211123160020.png)

Tips and Trick here
activity_main.xml
- use abbreviation to declare faster, i.e. textSize = tesi, textAlignment = teal (Android Studio notices it)
- use ellipsize + define line to limit the text, and show triple dots (...)
```xml
<textSize 
/>
```

## Reference
**Youtube**
Philip Lackner https://www.youtube.com/channel/UCKNTZMRHPLXfqlbdOI7mCkg

**Android Developer Documentation**
https://developer.android.com