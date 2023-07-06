# UAS_PENGOLAHANCITRA
# Muhammad Iqbal - 202131131
Praktikum file (https://github.com/ncsiqbal/PA-PC_202131131_Muhammad-Iqbal_C/blob/main/TUGAS%20UAS%20IQBAL/UAS%20MUHAMMAD%20IQBAL%20202131131.ipynb)
file foto buah dari kamera hp (https://github.com/ncsiqbal/PA-PC_202131131_Muhammad-Iqbal_C/blob/main/TUGAS%20UAS%20IQBAL/buah2.jpg)

<h2>Library yang digunakan : <h2>

* OpenCV 
* numpy
* matplotlib 

<h3> Teori : <h3>
* **Segmentasi Warna** merupakan metode segmentasi warna yang digunakan untuk memisahkan piksel-piksel yang berada dalam rentang warna yang ditentukan,sehingga menghasilkan sebuah mask yang menunjukan piksel warna yang masuk dalam rentang warna tersebut.dalam kasus ini segmentasi warna digunakan untuk : menentukan warna, segmentasi warna menggabungkan mask dengan gambar asli
* **Mask layer** adalah lapisan tambahan yang digunakan untuk membatasi efek atau operasi tertentu hanya area tertentu dalam citra. Biasanya, mask layer memiliki dua nilai piksel yang berbeda: 0 dan 255.
* **Kontur** adalah garis lengkung yang menghubungkan piksel-piksel yang memiliki intensitas atau warna yang sama. Dalam konteks pemrosesan citra, kontur digunakan untuk mengindentifikasi dan memisiahkan objek dari latar belakang. pada kasus kali ini kontur di pakai untuk : membersikan Mask dan deteksi kontur

<h3> Source Code : <h3>
* Library yang di butuhkan
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
* Memasukan variabel gambar
```python
img = cv2.imread('buah2.jpg')
```
* memasukan variabel untuk menkonversi ruang warna
```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```
* menentukan range warna untuk mask
```python
lower_orange = np.array([0, 120, 120])
upper_orange = np.array([150,255,255])

lower_red = np.array([100, 40, 40])
upper_red = np.array([179, 300, 300])

lower_green = np.array([25, 35, 35])  
upper_green = np.array([150, 300, 300]) 
```
* membuat mask
```python
mask_orange = cv2.inRange(hsv_img, lower_orange, upper_orange)
mask_red = cv2.inRange(hsv_img, lower_red, upper_red)
mask_green = cv2.inRange(hsv_img, lower_green, upper_green)  
```
* menerapkan mask pada gambar asli
```python
result_orange = cv2.bitwise_and(img, img, mask=mask_orange)
result_red = cv2.bitwise_and(img, img, mask=mask_red)
result_yellow = cv2.bitwise_and(img, img, mask=mask_green)
```  
* operasi morfologi untuk membersikan mask
```python 
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
```
* Membersihkan mask pada gambar 
```python 
cleaned_mask_orange = cv2.morphologyEx(mask_orange, cv2.MORPH_OPEN, kernel)
cleaned_mask_red = cv2.morphologyEx(mask_red, cv2.MORPH_OPEN, kernel)
cleaned_mask_green = cv2.morphologyEx(mask_green, cv2.MORPH_OPEN, kernel)
```
* mencari kontur 
```python 
contours_orange, _ = cv2.findContours(cleaned_mask_orange, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
contours_red, _ = cv2.findContours(cleaned_mask_red, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
contours_green, _ = cv2.findContours(cleaned_mask_green, cv2.RETR_EXTERNAL, cv2.
CHAIN_
```
* menampilkan gambar dan mengatur posisi gambar
```python 
fig, axs = plt.subplots(2, 2, figsize=(10, 10))

axs[0, 0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0, 0].set_title('Gambar Asli')

axs[0, 1].imshow(cv2.cvtColor(result_orange, cv2.COLOR_BGR2RGB))
axs[0, 1].set_title('Jeruk')

axs[1, 0].imshow(cv2.cvtColor(result_red, cv2.COLOR_BGR2RGB))
axs[1, 0].set_title('Apel')

axs[1, 1].imshow(cv2.cvtColor(result_yellow, cv2.COLOR_BGR2RGB))
axs[1, 1].set_title('Alpukat')

plt.tight_layout()

plt.show() 
```