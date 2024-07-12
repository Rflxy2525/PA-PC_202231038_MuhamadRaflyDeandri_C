# PA-PC_202231038_MuhamadRaflyDeandri_C

```python
import cv2
import matplotlib.pyplot as plt # memvisualisasi data
import numpy as np # membaca angka
```
Kodingan di atas mengimpor tiga pustaka:cv2 untuk pemrosesan gambar, matplotlib.pyplot untuk visualisasi data, dan numpy untuk operasi numerik.

```python
img = cv2.imread("fotorafly.jpg")
img.shape
[baris, kolom] = img.shape[:2]
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img_median = img.copy()
img_median_after = cv2.medianBlur(img_median, 11)
fig, axis = plt.subplots(1, 2, figsize = (10, 10))
ax = axis.ravel()
ax[0].imshow(img, cmap='gray')
ax[0].set_title('citra asli')
ax[1].imshow(img_median_after, cmap='gray')
ax[1].set_title('after filter median')
plt.show()
```
Kodingan di atas melakukan serangkaian langkah pemrosesan gambar, dimulai dengan membaca gambar dari file bernama fotorafly.jpg. Gambar yang dibaca kemudian dikonversi dari format warna BGR (Blue, Green, Red) ke format RGB (Red, Green, Blue) untuk keperluan visualisasi yang lebih akurat. Setelah konversi, gambar tersebut diproses menggunakan filter median untuk mengurangi noise, yaitu gangguan pada gambar yang dapat mempengaruhi kualitas visual dan analisis. Hasil dari proses ini adalah dua gambar: gambar asli dan gambar yang telah diolah dengan filter median. Kedua gambar ini kemudian ditampilkan secara berdampingan dalam dua subplot yang terpisah, memungkinkan perbandingan visual yang jelas dan langsung antara gambar asli dan gambar yang telah melalui proses pengurangan noise.

```python
img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
plt.imshow(img_gray, cmap='gray')
```
Kodingan di atas melakukan konversi gambar berwarna menjadi gambar grayscale dan menampilkannya menggunakan pustaka Matplotlib.

```python
copyCitra1 = img_gray.copy().astype(float)
m1, n1 = copyCitra1.shape
output1 = np.empty([m1, n1])
print("shape copy citra 1 : ", copyCitra1.shape)
print("shape output citra 1 : ", output1.shape)
print("m1 : ", m1)
print("n1 : ", n1)
print()
```
Kodingan diatas pertama-tama menyalin gambar grayscale ke dalam variabel baru yaitu copyCitra1 dan mengonversinya menjadi tipe data float untuk memungkinkan operasi numerik yang lebih presisi. Selanjutnya, dimensi dari gambar salinan ini diambil dan digunakan untuk membuat array kosong output1 dengan ukuran yang sama, yang akan digunakan untuk menyimpan hasil pemrosesan. Terakhir, informasi mengenai dimensi dari gambar salinan dan array kosong dicetak agar memberitahukan pemahaman yang jelas tentang struktur data yang sedang diproses.

```python
for baris in range (0, m1-1) :
    for kolom in range (0, n1-1) :
        a1 = baris
        b1 = kolom
        jumlah = copyCitra1[a1-1, b1-1] + copyCitra1[a1-1, b1] + copyCitra1[a1-1, b1+1] +\
            copyCitra1[a1, b1-1] + copyCitra1[a1, b1] + copyCitra1[a1, b1+1] +\
            copyCitra1[a1+1, b1-1] + copyCitra1[a1+1, b1] + copyCitra1[a1+1, b1+1]
        output1[a1, b1] = 1/9 * jumlah
fig, axis = plt.subplots(1, 2, figsize = (10, 10))
ax = axis.ravel()
ax[0].imshow(img_gray, cmap='gray')
ax[0].set_title('Original Image')
ax[1].imshow(output1, cmap='gray')
ax[1].set_title('Mean Filtered Image')
plt.show()
```
Kodingan diatas melakukan filter rata-rata pada gambar grayscale dengan menghitung rata-rata dari nilai piksel di sekitar setiap piksel dalam gambar. Proses ini dilakukan melalui dua loop for yang mengiterasi setiap piksel dalam gambar, menjumlahkan nilai dari piksel tersebut dan delapan tetangganya, dan menghitung rata-rata nilai-nilai tersebut untuk menghasilkan gambar yang telah difilter. Setelah pemrosesan selesai, gambar asli dan gambar hasil filter ditampilkan berdampingan menggunakan Matplotlib, memungkinkan perbandingan visual yang jelas untuk melihat efek dari filter rata-rata dalam menghaluskan gambar.
