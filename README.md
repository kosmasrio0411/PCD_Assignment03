# PCD_Assignment03

Tugas ini berisi implementasi **segmentation by thresholding** dan **morphological processing** pada citra tanpa library pemrosesan citra. OpenCV hanya digunakan untuk **I/O** (baca gambar, konversi ke grayscale).
Operasi yang diimplementasikan:

* Thresholding otomatis **Otsu**
* **Erosion**, **Dilation**, **Opening**, **Closing**
* Opsional: **Hit-and-Miss**, **Thinning**, **Thickening**, **Skeletonization**
* **Structuring Element (SE)** fleksibel: square, cross, atau circular (disk); ukuran bisa diatur

---

## Fitur Utama

* Implementasi Otsu manual (tanpa `cv2.threshold`)
* Operasi morfologi manual berbasis NumPy (tanpa `cv2.morphologyEx`)
* SE bisa dipilih bentuk dan ukurannya:

  * `np.ones((k, k))` untuk square
  * Cross 3×3: `[[0,1,0],[1,1,1],[0,1,0]]`
  * Disk (lingkaran) via fungsi `circular_se(radius)`
* Perbandingan **hasil segmentasi sebelum vs sesudah** morphology (visual + metrik jumlah piksel)

---

## Output

Notebook akan menampilkan:

* Citra grayscale dan hasil **binary (Otsu)**
* Hasil **Erosion**, **Dilation**, **Opening**, **Closing**
* Opsional: **Thinning**, **Thickening** (dan Skeleton jika diaktifkan)
* Tabel/metrik ringkas perubahan piksel terhadap `binary`
* 
---

## Catatan Analisis

* **Tanpa morphology** (binary saja): masih mungkin ada noise kecil, lubang di objek, atau kontur bergerigi.
* **Dengan morphology**:

  * **Opening** efektif menghapus noise eksternal tanpa merusak bentuk utama.
  * **Closing** menutup lubang/celah kecil di dalam objek sehingga objek lebih solid.
* **Pemilihan SE itu krusial**:

  * **Disk** menjaga kontur alami (objek organik).
  * **Square** agresif untuk noise besar namun bisa membuat kontur tampak kotak.
  * **Cross** menjaga struktur ortogonal, menghindari penyatuan diagonal.
  * Ukuran SE lebih besar membersihkan lebih kuat namun berisiko menghilangkan detail halus.

