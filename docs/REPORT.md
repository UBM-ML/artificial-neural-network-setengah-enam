# Laporan Kelompok — ANN Bake-Off

> Isi semua bagian di bawah. Hapus _italic placeholder_ setelah diisi.

## Identitas Kelompok

- **Nama Kelompok:** _isi di sini_
- **Anggota:**
  1. _Joel Prasetya Pradipta — 32230020 — Single layer_
  2. _Richard Sidharta — 32230069 — mlp tanh_
  3. _Richard Stefano — 32230002 — mlp tanh_
  4. _Ruben Wijaya — 32230048 — mlp sigmoid_
  5. _Harlan Luthi Permana — 32230033 — mlp sigmoid_
  6. _Cristian Everson Jong — 32230057 — mlp relu_
  7. _Yogi Tansyah — 32220162 — comparison_

---

## 1. Ringkasan Hasil Eksperimen

_Tabel hasil akhir dari notebook `05_comparison.ipynb`. Boleh copy-paste tabel markdown atau screenshot._

| Varian | Arsitektur | Aktivasi | Test Accuracy | Test Loss | Jumlah Parameter |
|---|---|---|---|---|---|
| 01 | Single layer | — | 0.864583 | 0.416680 | 15 |
| 02 | 1 hidden (16) | Sigmoid | 0.916667	 | 0.251070	 | 131 |
| 03 | 1 hidden (16) | Tanh | 0.968750 | 0.113794	 | 131 |
| 04 | 2 hidden (32→16) | ReLU | 0.989583 | 0.034608 | 739 |

---

## 2. Analisis & Diskusi

Pilih **minimal 3 pertanyaan** dari daftar pertanyaan diskusi di `README.md` dan jawab di sini.

1. Kapasitas Model: Single-layer vs Multi-layerSecara teori, model multi-layer (MLP) memiliki kapasitas yang jauh lebih tinggi dibandingkan single-layer. Hal ini didasarkan pada Universal Approximation Theorem yang dikemukakan oleh Cybenko (1989) dan Hornik (1991). Mereka membuktikan bahwa jaringan dengan minimal satu hidden layer dapat mendekati fungsi kontinu apa pun, sedangkan single-layer (Perceptron) hanya terbatas pada pemisahan linear. Pada dataset ini, penggunaan multi-layer memungkinkan model menangkap hubungan non-linear antar fitur (seperti panjang dan lebar sepal/petal) secara lebih akurat daripada model linear sederhana.
   
2. Kecepatan Konvergensi: ReLU vs SigmoidHasil eksperimen menunjukkan bahwa Varian 04 (ReLU) konvergen jauh lebih cepat dibandingkan Varian 02 (Sigmoid). Hal ini terbukti secara empiris melalui grafik loss yang menukik tajam sejak epoch awal. Secara ilmiah, Nair & Hinton (2010) menjelaskan bahwa ReLU ($f(x) = \max(0, x)$) tidak mengalami saturasi pada sisi positif, sehingga gradiennya tetap konstan (bernilai 1). Sebaliknya, Glorot & Bengio (2010) dalam penelitiannya tentang kesulitan training jaringan saraf, menunjukkan bahwa Sigmoid sering mengalami vanishing gradient karena nilai turunannya yang sangat kecil (maksimal 0.25), sehingga memperlambat pembaruan bobot secara signifikan.
   
4. Fenomena Overfitting pada Model DalamBerdasarkan klaim Slide 1.9 dan didukung oleh buku literatur Goodfellow et al. (2016), model yang terlalu dalam pada dataset kecil cenderung mengalami overfitting. Saat model terlalu kompleks, ia mulai "menghafal" noise pada data training alih-alih mempelajari pola umum. Secara visual, ini ditandai dengan training accuracy yang terus naik mendekati 100%, namun validation accuracy justru stagnan atau menurun. Model kehilangan kemampuan generalisasi karena kapasitasnya melebihi kompleksitas data yang tersedia.
   
5. Dampak Penambahan Hidden Layer Ekstra (Layer 3 & 4)Menambah hidden layer ke-3 atau ke-4 tidak selalu meningkatkan akurasi, bahkan seringkali justru menurunkan performa. Eksperimen tambahan menunjukkan adanya hukum diminishing returns. Selain risiko overfitting, penambahan layer berlebih tanpa teknik regulasi yang tepat akan memperparah masalah vanishing gradient, terutama jika menggunakan aktivasi berbasis saturasi. Glorot & Bengio (2010) menyatakan bahwa semakin dalam jaringan, semakin sulit sinyal kesalahan (error) mengalir kembali ke layer awal, yang mengakibatkan layer-layer pertama tidak belajar dengan efektif.
   
6. Efisiensi Tanh (Zero-Centered)Klaim pada Slide 2.7 bahwa Tanh mempercepat pembelajaran karena sifatnya yang zero-centered terbukti benar dalam eksperimen ini (Varian 03 mencapai akurasi $\ge 0.90$ lebih cepat dari Varian 02). LeCun et al. (1998) dalam jurnal "Efficient BackProp" menjelaskan bahwa fungsi aktivasi yang zero-centered (rata-rata output mendekati nol) membuat proses gradient descent lebih efisien. Jika output aktivasi selalu positif (seperti Sigmoid), gradien pada bobot akan memiliki tanda yang sama, menyebabkan pergerakan optimasi yang berliku-liku (zig-zag). Tanh menghindari hal ini dengan rentang $[-1, 1]$, sehingga arah pembaruan bobot lebih seimbang dan langsung menuju titik minimum.

## 3. Refleksi Proses Kerja Kelompok

_300–500 kata. Ceritakan:_
Untuk Pembagian tugas sudah seperti diatas ada yang kerja berdua ada yang sendiri tergantung tingkat kesulitan dan kapabilitas dari setiap anggota jadi dibagi secara merata dan saling support satu sama lain, satu satunya kesusahan yang dialami mungkin dari penggunaan github aja yang blm terbiasa apalagi integrasi dengan colab menurut kami agak ribet aja namun setelah penyesuaian dari beberapa project menurut kami sudah lebih better, dan pelajaran yang bisa dibawa ke project ML berikutnya banyak dari pemanfaatan epoch kemudian banyak teknik teknik yang bisa kami aplikasikan juga ke project kami.
---

## 4. Kontribusi Tiap Anggota

| Anggota | Kontribusi Konkret | % Effort |
|---|---|---|
| _Joel Prasetya Pradipta_ | _Single Layer & Laporan_ | _19%_ |
| _Richard Sidharta_ | _mlp tanh_ | _14%_ |
| _Richard Stefano_ | _mlp tanh_ | _14%_ |
| _Ruben Wijaya_ | _mlp sigmoid_ | _13%_ |
| _Harlan Luthi Permana_ | _mlp sigmoid_ | _13%_ |
| _Cristian Everson Jong_ | _mlp relu_ | _14%_ |
| _Yogi Tansyah_ | _Comparison_ | _14%_ |
_Total harus 100%._

---

## 5. Referensi

_Cybenko, G. (1989). Approximation by superpositions of a sigmoidal function.

Glorot, X., & Bengio, Y. (2010). Understanding the difficulty of training deep feedforward neural networks.

Goodfellow, I., Bengio, Y., & Courville, A. (2016). Deep Learning.

LeCun, Y., et al. (1998). Efficient BackProp.

Nair, V., & Hinton, G. E. (2010). Rectified Linear Units Improve Restricted Boltzmann Machines._
