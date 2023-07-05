
# Project UAS

        Nama  : Muhammad Wahyu Ilham 
        NIM   : 202131097
        Kelas : Pengolahan Citra Kelas F

Dalam membuat Project kali ini saya mendapat kesempatan untuk membuat Deteksi Gambar Menggunakan Contour

## Apa itu Deteksi Gambar Menggunakan Contour
Deteksi kontur adalah proses pengenalan dan ekstraksi garis lengkung yang membentuk batas objek dalam sebuah gambar. Kontur sering kali digunakan untuk mengidentifikasi dan memisahkan objek dari latar belakang dalam analisis gambar.

Cara kerja deteksi kontur umumnya melibatkan langkah-langkah berikut:

- Praproses Gambar: Gambar awal sering kali perlu diproses sebelum deteksi kontur dilakukan. Praproses ini dapat melibatkan langkah-langkah seperti konversi ke skala abu-abu, peningkatan kontras, penghalusan, atau segmentasi gambar untuk memisahkan objek dari latar belakang.

- Ambang Biner: Langkah pertama dalam deteksi kontur adalah mengonversi gambar menjadi citra biner. Ini dilakukan dengan menerapkan ambang biner di atas atau di bawah ambang tertentu. Piksel yang berada di atas ambang ini dianggap sebagai piksel objek, sementara piksel di bawah ambang ini dianggap sebagai piksel latar belakang.

- Operasi Morfologi (Opsional): Untuk meningkatkan hasil deteksi kontur, operasi morfologi seperti dilasi (dilation) atau erosi (erosion) dapat diterapkan pada citra biner. Dilasi dapat digunakan untuk mengisi celah atau memperluas kontur, sedangkan erosi dapat digunakan untuk menghaluskan kontur dan menghilangkan detail kecil.

- Deteksi Kontur: Setelah langkah-langkah pra-pemrosesan selesai, metode deteksi kontur seperti algoritma Canny atau metode diferensial dapat diterapkan. Metode diferensial menghitung perbedaan intensitas piksel di sekitar setiap piksel dalam gambar untuk mengidentifikasi tepi dan kontur. Algoritma Canny, di sisi lain, menggunakan pendekatan multi-langkah yang melibatkan deteksi tepi awal, penguatan tepi, dan penapisan non-maksimum untuk menghasilkan kontur yang akurat.

- Pengolahan Kontur: Setelah kontur berhasil dideteksi, langkah selanjutnya adalah mengolah kontur yang ditemukan. Hal ini dapat melibatkan pengelompokan kontur yang saling terhubung, mengukur atribut kontur seperti luas atau panjangnya, menggambar bounding box atau poligon yang mengelilingi kontur, atau ekstraksi fitur lebih lanjut.

Deteksi kontur sering digunakan dalam berbagai aplikasi, termasuk pengenalan objek, deteksi gerakan, analisis citra medis, pengenalan tulisan tangan, visi komputer, dan banyak lagi.

## Penjelasan program
- Import Library
```bash
    import cv2 ## Import Library opencv
  from matplotlib import pyplot as plt ## import Library matplotlib.pyplot dengan nama plt
  import numpy as np ##Import Library numpy dengan nama np
```
- Show Image
```bash
    img = cv2.imread('gambar1.jpg') ## Membaca gambar gambae1.jpg dengan variabel img
  img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) ## Mengubah gambar img menjadi warna gray
 
  plt.imshow(img) ## Menampilkan gambar
  plt.show() ## Menampilkan gambar
```
- Deteksi Contour
```bash
 gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY) ## Mengubah gambar menjadi warna gray  

  thresh = cv2.adaptiveThreshold(
    gray, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY_INV, 21, 5) ## Terapkan ambang batas (threshold) untuk membuat citra biner 

  contours, _ = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE) ## Mencari Kontur dalam citra biner 

  detected_contours = img.copy() ## digunakan untuk membuat salinan (copy) dari citra asli (img) ke variabel detected_contours

  cv2.drawContours(detected_contours, contours, -500, (0, 255, 0), -500) ## Untuk menggambar kontur pada salinan citra asli
  
  plt.imshow(detected_contours)
  plt.title('Image With Contours') ## Menampilkan Keterangan pada gambar
  plt.show() ## Menampilkan gambar
```
- Extraks Contour
```bash
contours, _ = cv2.findContours(
    thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE) ## untuk menemukan kontur dalam citra biner (thresh) menggunakan fungsi "cv2.findContours" dari pustaka OpenCV.

  highlight = np.ones_like(img) ## untuk membuat sebuah array numpy dengan dimensi yang sama seperti citra img, yang diisi dengan nilai 1.

  cv2.drawContours(highlight, contours, -500, (255, 255, 255), -255) ## untuk menggambar kontur pada citra yang disimpan dalam variabel highlight menggunakan fungsi "cv2.drawContours" dari pustaka OpenCV.
 
  plt.imshow(highlight)
  plt.title('Highlight contour with color') ## Menampilkan Keterangan pada gambar
  plt.show() ## Menampilkan gambar 
```


```bash
  contours = {"Original Image": img, "Image with contours": detected_contours,
            "Color contours": highlight} ## untuk membuat sebuah kamus (dictionary) dengan tiga entri yang berisi citra-citra yang relevan dalam proses deteksi kontur.

  plt.subplots_adjust(wspace=.2, hspace=.2) ## untuk mengatur jarak antara subplot dalam sebuah plot menggunakan pustaka Matplotlib.
  plt.tight_layout() ## untuk secara otomatis mengatur tata letak subplot dan elemen-elemen dalam plot menggunakan pustaka Matplotlib.

  for i, (key, value) in enumerate(contours.items()): ## untuk melakukan iterasi melalui item-item dalam kamus contours menggunakan fungsi enumerate().
    plt.subplot(2, 2, i + 1) ## untuk membuat subplot dalam plot menggunakan pustaka Matplotlib.
    plt.tick_params(labelbottom=False) ## untuk mengatur parameter sumbu x pada plot menggunakan pustaka Matplotlib.
    plt.tick_params(labelleft=False) ## untuk mengatur parameter sumbu y pada plot menggunakan pustaka Matplotlib.
    plt.title("{}".format(key)) ## untuk mengatur judul pada plot menggunakan pustaka Matplotlib.
    plt.imshow(value) ## untuk menampilkan citra pada subplot menggunakan pustaka Matplotlib.

  plt.show() ## Menampilkan gambar 

```

    Sekian dari Saya Muhammad Wahyu Ilham. diatas merupakan penjelasan singkat mengenai Deteksi countour dan sebuah codingan program yang telah saya buat. 

    Terima kasih Kepada Dosen saya Bu Dwina telah mengajarkan pengolahan citra ini selama satu semester. Dan terima kasih kepada Kakak dan Abang yang selalu membantu saya di lab ketika sedang melakukan praktikum :)

    



