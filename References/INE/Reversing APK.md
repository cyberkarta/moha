# Reversing APK
Reversing APK adalah kemampuan yang penting bagi seseorang yang ingin mengaudit aplikasi, ketika source code tidak bisa didapatkan.

Mengembalikan aplikasi yang sudah tercompile menjadi source code (meskipun tidak 100% mirip).

## Apktool
https://ibotpeaches.github.io/Apktool/

Decode the APK
```bash
apktool d example.apk
```

Carilah konten dari Manifest.xml, kamu mungkin akan menemukan lebih dari satu. Ini sebenarnya digabungkan saat membentuk APK final.

