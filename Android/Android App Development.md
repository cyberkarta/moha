# Android App Development

## Designing Layout
Element di dalam layout (tombol, gambar, etc) disebut dengan view.
Start from res > layout > activity_main.xml
![](attachments/Pasted%20image%2020211109160119.png)

Three types of layout
1. Constraint  (preferable, flat, less computation)
2. Linear
3. Static (using dp scale)

### Linear
Preferably using code instead drag and dropping the design.
You need to define `android:orientation` to either vertical or horizontal
Vertical
![](attachments/Pasted%20image%2020211109160555.png)

Horizontal
![](attachments/Pasted%20image%2020211109160618.png)

Kamu bisa menentukan margin dalam skala dp.
> istilah penting: layout_width & height, match_parent, wrap_content, fixed_size