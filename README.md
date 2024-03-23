# advprog-modul6

---
#### Nama: Rakha Abid Bangsawan
#### NPM: 2206081585
#### Kelas: Adpro-C
---

## Tutorial 6
### Commit 1 Refletion Notes
Metode <code>handle_connection</code> bertanggung jawab untuk memproses koneksi TCP yang masuk. Method ini memiliki parameter yang mana meminjam ownership dari TcpStream yang merepresentasikan koneksi dari client. Dapat dilihat bahwa terdapat syntax mut yang berarti stream dapat dimodifikasi jika diperlukan. Selanjutnya ada BufReader yang diinisialisasi menggunakan referensi dari stream, yaitu connection dari client sehingga dapat menyediakan kemampuan buffering, yang dapat meningkatkan kinerja Input/Output dengan mengurangi operasi read pada stream. Selanjutnya pada variable `http_request`, `buf_reader` yang dibuat sebelumnya kita jalankan metode `lines()` yang mengembalikan iterator atas baris-baris masukan dari stream. Selanjutnya kita `map()` untuk membongkar Result yang dikembalikan oleh `lines()`, mengasumsikan bahwa itu aman dilakukan karena kesalahan I/O akan ditangani di tempat lain. Hasil dari map itu akan kita `take_while()` untuk mengumpulkan baris sampai sebuah baris kosong ditemukan yang menandakan akhir dari HTTP request. Terakhir, `collect()` mengumpulkan baris-baris menjadi Vec\<String> yang disebut http_request. Selanjutnya HTTP request yang sudah didapatkan bisa dicetak agar kita dapat melihat isi dalamnya apa.