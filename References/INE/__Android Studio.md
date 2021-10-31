
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

`<uses-sdk>` mengandung `minSdkVersion` yang memberitahukan versi Android terlama yang kompatibel dengan aplikasi ini.
`targetSdkVersion` adalah versi OS yang ditujukan oleh aplikasi ini dan juga menentukan apakah harus menyalakan fitur compatibility apabila dijalankan pada versi Android terbaru.

Memberikan support ke Android versi lama dapat membuka vulnerability yang terkandung pada versi Android tersebut.

