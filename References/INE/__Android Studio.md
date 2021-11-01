
Kotlin Basic.
https://developer.android.com/training/basics/firstapp/index.html

Using Emulators
https://developer.android.com/studio/run/emulator

Getting started with newer Android Studio and choose which important for security perspective
- AVD manager
- SDK Manager
- Log files
- OEM android

## App Manifest
Example: https://github.com/swisscodemonkeys/appbrain-sdk/blob/master/example/AndroidManifest.xml

`<package>` berisi nama aplikasi, yaitu `com.appbrain.example`.

![](attachments/Pasted%20image%2020211031205729.png)
`<uses-sdk>` mengandung `minSdkVersion` yang memberitahukan versi Android terlama yang kompatibel dengan aplikasi ini.
`targetSdkVersion` adalah versi OS yang ditujukan oleh aplikasi ini dan juga menentukan apakah harus menyalakan fitur compatibility apabila dijalankan pada versi Android terbaru.

Memberikan support ke Android versi lama dapat membuka vulnerability yang terkandung pada versi Android tersebut.

## Directories
`/lib` stores libraries and precompiled code. Di dalam directory ini, terdapat file `.so` yang dibuat developer atau dari third-party. Jika kamu menemukan cara untuk memodifikasi atau mengganti file ini dan membuatnya dieksekusi, maka akan menghasilkan arbitrary code execution. Hal ini cukup rumit untuk dilakukan pada kondisi normal.

`/META-INF` adalah directory yang berkaitan dengan integritas dan keaslian data. Di dalamnya terdapat file:
- MANIFEST.MF, berisi berbagai informasi yang digunakan oleh java run-time environment saat membuka JAR(Java Archieve/APK). Contoh: main class, versi package, build number, pembuat package, permission/security policies dari java applets, dan list nama file di dalam JAR dan SHA-1 milik masing-masing file tersebut. Contoh:
```http
Manifest-Version: 1.0
Created-By: 1.7.0_60 (Oracle Corporation)

Name: res/drawable-xxhdpi-v4/common_plus_signin_btn_text_dark_pressed.9.png
SHA1-Digest: Db3E0/I85K9Aik2yJ4X1dDP3Wq0=

Name: res/drawable-xhdpi-v4/opt_more_item_close_press.9.png
SHA1-Digest: Xxm9cr4gDbEEnnYvxRWfzcIXBEM=

Name: res/anim/accessibility_guide_translate_out.xml
SHA1-Digest: dp8PyrXMy2IBxgTz19x7DATpqz8=
```
- CERT.RSA, sertifikat digital yang berasal dari developer aplikasi
- CERT.SF, list  semua file dan hash milik masing-masing.

`/res` adalah directory dari resource, seperti gambar, musik, dsb. Biasanya isi dari file ini tidak terlalu penting saat testing security. Namun kamu masih bisa menemukan tipe data lain yang berguna:
- Kustomisasi aplikasi dan resource directories
- Third-party libraries
- Template HTML yang digunakan pada Webviews.

## Code Signing
Android tidak akan menjalankan program yang unsigned, walaupun kamu membuat program tersebut untuk testing. Untuk melakukan code signing, digunakan public-key cryptography. Informasi public key tersebut dimasukkan ke dalam sertifikat (X.509 certificate) untuk melakukan verifikasi keaslian file tersebut. Sertifikat ini juga berisi informasi tentang organisasi pembuat aplikasi. 

Code signing pada Android ini tidak memerlukan Certificate Authority (CA) karena self-signed certificate tidak mengurangi keamanannya. Terlebih lagi, nama entitas dan expiration date tidak diverifikasi oleh Android. Android hanya menggunakan sertifikat ini sebagai binary blob.

Proses signing APK sudah built-in pada Android Studio dan hampir tidak terlihat oleh developer.

Abstrak prosesnya:
1. Pembuatan pair key, contohnya dengan menggunakan keytool. `keytool -genkey -v -keystore foo.keystore -alias myalias -keyalg RSA -keysize 2048 -validity 10000`. Alias name adalah nama yang digunakan untuk sign aplikasi kamu.
2. Verifikasi signature, contohnya dengan menggunakan jarsigner. `jarsigner -sigalg SHA1withRSA -digestalg SHA1 -keystore foo.keystore test.apk myalias`

Kamu juga bisa menginspeksi status signature dari APK dengan jarsigner. `jarsigner -verify -verbose -certs com.foo.android.activity.apk`

Didalam MANIFEST.MF kamu bisa melihat list dari file hash yang sudah diencode base64.

```http
Manifest-Version: 1.0
Created-By: 1.0 (Android)

Name: res/drawable-xxhdpi-v4/common_plus_signin_btn_text_dark_pressed.9.png
SHA1-Digest: Db3E0/I85K9Aik2yJ4X1dDP3Wq0=

Name: res/drawable-xhdpi-v4/opt_more_item_close_press.9.png
SHA1-Digest: Xxm9cr4gDbEEnnYvxRWfzcIXBEM=

```

Kamu bisa memverifikasi file hash tersebut dengan openssl `openssl sha1 -binary res/drawable-xxhdpi-v4/common_plus_signin_btn_text_dark_pressed.9.png | openssl base64`
Output: `Db3E0/I85K9Aik2yJ4X1dDP3Wq0=` sama dengan isi di MANIFEST.MF

CERT.RSA dituliskan dalam format biner, kamu bisa mengkonversi formatnya dari DER ke PEM agar bisa 'terbaca'. `openssl pkcs7 -inform DER -pring_certs -out cert.pem -in CERT.RSA`. Kemudian kamu bisa membaca public key dari sertifikat tersebut `openssl x509 -in cert.pem -noout -text`
![](attachments/Pasted%20image%2020211031214102.png)

Pada CERT.SF kamu bisa melihat list resource file, hash dari file MANIFEST.MF juga ditampilkan di sini.
```http
Signature-Version: 1.0  
Created-By: 1.0 (Android)  
SHA1-Digest-Manifest: AeXK7rPJFQU178iionkxrR8X034=  
Name: res/drawable-hdpi/ab_bg.9.png  
SHA1-Digest: h/8GB05R+rJmh4bouTC/4XnutGA=  
Name: res/drawable-xxhdpi/g7.png  
SHA1-Digest: z/rM+901mHn1r5dFVvfc+19n6bQ=
```

page 62