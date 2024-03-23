# advprog-modul6

---
#### Nama: Rakha Abid Bangsawan
#### NPM: 2206081585
#### Kelas: Adpro-C
---

## Tutorial 6
### Commit 1 Refletion Notes
Metode <code>handle_connection</code> bertanggung jawab untuk memproses koneksi TCP yang masuk. Method ini memiliki parameter yang mana meminjam ownership dari TcpStream yang merepresentasikan koneksi dari client. Dapat dilihat bahwa terdapat syntax mut yang berarti stream dapat dimodifikasi jika diperlukan. Selanjutnya ada BufReader yang diinisialisasi menggunakan referensi dari stream, yaitu connection dari client sehingga dapat menyediakan kemampuan buffering, yang dapat meningkatkan kinerja Input/Output dengan mengurangi operasi read pada stream. Selanjutnya pada variable `http_request`, `buf_reader` yang dibuat sebelumnya kita jalankan metode `lines()` yang mengembalikan iterator atas baris-baris masukan dari stream. Selanjutnya kita `map()` untuk membongkar Result yang dikembalikan oleh `lines()`, mengasumsikan bahwa itu aman dilakukan karena kesalahan I/O akan ditangani di tempat lain. Hasil dari map itu akan kita `take_while()` untuk mengumpulkan baris sampai sebuah baris kosong ditemukan yang menandakan akhir dari HTTP request. Terakhir, `collect()` mengumpulkan baris-baris menjadi Vec\<String> yang disebut http_request. Selanjutnya HTTP request yang sudah didapatkan bisa dicetak agar kita dapat melihat isi dalamnya apa.

### Commit 2 Reflection Notes
Pada commit ke-2 ini, kita menambahkan beberapa kode baru ke method <code>handle_connection</code>.
```
let status_line = "HTTP/1.1 200 OK";
let contents = fs::read_to_string("hello.html").unwrap();
let length = contents.len();
let response = format!("{status_line}\r\nContent-Length: {length}\r\n\r\n{contents}");
```

- `status_line` menyatakan bahwa respons adalah OK dengan kode status 200.
- `fs::read_to_string()` digunakan untuk membaca konten dari file "hello.html" dan menyimpannya di dalam contents.
- Panjang konten dihitung menggunakan `contents.len()` untuk mengisi header Content-Length.
- Kemudian, respons HTTP dibentuk menggunakan format!(), yang mencakup status line, panjang konten, dan isi konten.

Selanjutnya ada kode tambahan juga, yaitu:
```
stream.write_all(response.as_bytes()).unwrap();
```
Setelah respons HTTP dibangun selanjutnya akan ditulis ke stream menggunakan metode write_all(). Respons dikonversi menjadi byte array menggunakan as_bytes() sebelum ditulis.

![Commit 2 screen capture](/assets/images/commit_2.png)