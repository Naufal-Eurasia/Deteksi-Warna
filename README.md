# Deteksi-Warna
Program deteksi warna tomat yang matang sama tidak matang
```python
import cv2
import numpy as np

def detect_tomato_ripeness(image_path):
    # Baca gambar
    image = cv2.imread(image_path)
    if image is None:
        print("Gambar tidak ditemukan.")
        return

    # Konversi gambar ke ruang warna HSV
    hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Rentang warna untuk tomat matang (merah)
    lower_red1 = np.array([0, 100, 100])   # Rentang pertama merah
    upper_red1 = np.array([10, 255, 255])
    lower_red2 = np.array([160, 100, 100]) # Rentang kedua merah
    upper_red2 = np.array([180, 255, 255])

    # Mask untuk mendeteksi warna merah
    mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
    mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
    red_mask = mask_red1 + mask_red2

    # Hitung proporsi piksel merah
    red_pixels = cv2.countNonZero(red_mask)
    total_pixels = image.shape[0] * image.shape[1]
    red_percentage = (red_pixels / total_pixels) * 100

    # Tampilkan hasil
    print(f"Persentase warna merah: {red_percentage:.2f}%")
    if red_percentage > 30:  # Ambang batas warna merah
        print("Tomat matang.")
    else:
        print("Tomat belum matang.")

    # Tampilkan gambar asli dan mask
    cv2.imshow("Gambar Asli", image)
    cv2.imshow("Mask Warna Merah", red_mask)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

# Jalankan program
image_path = "tomato.jpg"  # Ganti dengan path gambar tomat
detect_tomato_ripeness(image_path)
```
Penjelasan:
Input Gambar: Program membaca gambar tomat menggunakan (cv2.imread).

Konversi ke HSV: Warna dideteksi dengan menggunakan HSV.

Mask Warna Merah: Dua rentang warna merah digunakan untuk mendeteksi tomat matang (karena merah memiliki dua wilayah dalam HSV).

Perhitungan Persentase: Program menghitung persentase piksel merah untuk menentukan kematangan tomat dan persentasenya.

# Hasil: Jika proporsi warna merah melebihi ambang batas (misalnya 30%), tomat dianggap matang.

![image](https://github.com/user-attachments/assets/32175ac3-62a1-44e0-9886-151e8c647065)

