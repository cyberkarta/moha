
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
- MANIFEST.MF, berisi berbagai informasi yang digunakan oleh java run-time environment saat membuka JAR(Java Archieve/APK). Contoh: main class, versi package, build number, pembuat package, permission/security policies dari java applets, dan list semua resource file dan SHA-1 milik masing-masing file tersebut.
- CERT.RSA, sertifikat digital yang berasal dari developer aplikasi
- CERT.SF, list  semua file dan hash milik masing-masing.




