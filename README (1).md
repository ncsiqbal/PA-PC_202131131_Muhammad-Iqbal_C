#Penjelasan tentang Project Akhir Pengolahan Citra 
Kodingan yang akan di jelaskan meruoakan kodingan untuk melakukan pemrosesan gambar dengan menggunakan library OpenCV dan Matplotlib untuk menampilkan gambar.

#Import Library
Kodingan yang pertama di ketik adalah dengan megimport library yaitu cv2 sebagai OpenCV, Numpy untuk operasi array dan matplotlib.pylot uttuk menampilkan gambar

#Membaca gambar:
Kodingan selanjutnya adalah img = vc2.imread(‘buah2.jpg’)untuk membaca nama file dan menyimpannya kedalam variabel img

#Mengkonversi HSV
Kodingan “hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)” adalahh kode untuk mengkonversi gambar dari bode BGR(Blue, Green,Red) ke mode HSV ( Hue,Saturation, Value)

#Menentukan range warna untuk mask
Kode seperti lower_orange,upper_red,green merupakan kodingan untuk menentukan rentang warna yang akan di ambil dalam format HSV.

#Membuat mask
kodingan “mask_orange, mask_red, dan mask_green” adalah untuk membuat mask menggunakan fungsi ‘cv2.inRange()’ berdasarkan rentang warna yang telah ditentukan sebelumnya.

#Menerapkan mask pada gambar asli
Kodingan “result_orange,result_red dan result yellow” merupakan kode untuk menggabungkan gambar asli dengan mask menggunakan operasi bitwise AND, menghasilkan gambar yang hanya menampilkan bagian yang sesuai dengan mask

#Operasi morfologi untuk membersikan mask
Kodingan “kernel, cleaned_mask _orange sampai green” kode untuk operasi morfologi(opening) dengan kernel yang berbentuk elips dan membersihkan mask dari noise atau piksel yang tidak diinginkan

#Mencari kontur
“Contours_orange, sampai dengan green” merupakan kode untuk kontur mask yang telah di bersiihkan menggunakan fungsi dari ‘cv2,findContours()’.

#Menampilkan gambar
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


Yang terakhir, "kodingan diatas" adalah kode membuat subplot dengan ukuran 2x2 dan untuk menampilkan gambar pada subplot. Gambar yang ditampilkan termasuk gambar asli, mask merah, orange dan hijau
