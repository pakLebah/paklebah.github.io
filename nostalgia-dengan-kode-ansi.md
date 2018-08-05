# Bernostalgia Dengan Kode ANSI

Beberapa hari yg lalu, saat jalan-jalan di dunia maya melalui blog (*blogwalking*) dan media sosial, tanpa sengaja saya *nyasar* ke sebuah artikel di [sini][1]. Sebuah tulisan tentang pemrograman layar teks (*console*) di bahasa [Python][2] dengan memanfaatkan [kode ANSI][3]. Saya jadi teringat waktu masih belajar pemrograman [Pascal][4] dengan [Turbo Pascal][5] di kampus dulu. Kala itu jadi sebuah kesenangan, sekaligus kebanggaan, jika bisa membuat aplikasi di [DOS][6] yg warna-warni, walaupun kadang tampilan program jadi *norak* karena selera seni saya yg pas-pasan.

Gara-gara artikel itu, saya jadi ingin bernostalgia membuat aplikasi *console* yg warna-warni. Jika dulu saya membuatnya dengan Turbo Pascal dan teknik [*interrupt* 10H][7], kini saya akan membuatnya dengan Free Pascal dan kode ANSI. Tentu saja menggunakan aplikasi penyunting [VS Code][8] di MacBook Pro kesayangan saya. Saya rencanakan gagasan tersebut sebagai proyek *ngoprek* di akhir pekan kali ini.

Kode ANSI sebenarnya bukan hal yg baru, usianya bahkan lebih tua dari DOS. Namun standar pengolahan tampilan teks tersebut masih tetap berlaku di sistem operasi modern hingga hari ini, termasuk [Windows 10][9] (walaupun perlu diaktifkan terlebih dahulu). Sementara teknik *interrupt* 10H sudah tidak didukung lagi di sistem operasi modern karena membutuhkan akses langsung ke perangkat keras.

Setelah beberapa jam *ngoprek* program sambil membaca standar kode ANSI dari berbagai sumber, akhirnya sebuah *unit* bernama [`ansiCRT.pas`][18] dan sebuah program demo pun saya buat. Kode program sumber saya simpan di *gist* di [sini][10]. Bagi yg berminat, silakan dipelajari. Tampilan programnya sebagai berikut:

![](https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1/raw/e693b93fc283efc8bd382f0abb017c5ce5ca65f2/ansicrt_demo.png)

Menggunakan kode ANSI sangatlah mudah, cukup menulis rangkaian kode *escape* ke kanal keluaran baku (`stdout`). Misalnya untuk mengatur warna teks menjadi merah, kodenya cukup satu baris seperti berikut:

```pascal
write(#27'[31m');
```

Memindahkan kursor ke baris 10 kolom 10, kodenya juga cukup satu baris seperti berikut:

```pascal
write(#27'[10;10H');
```

*Unit* `ansiCRT.pas` sudah menyimpan sebagian besar kode ANSI yg saya anggap penting. Dan semua itu sudah dibungkus sebagai fungsi dan prosedur yg siap pakai dalam program Anda. Jika Anda merasa perlu menambahkan kode ANSI lainnya, silakan unduh kode program di atas lalu ubah/tambah sesuai keinginan atau kebutuhan Anda.

### Masalah Dengan Penerapan Kode ANSI

Ada sedikit kabar buruk untuk pengguna Windows. Seperti yg saya singgung sebelumnya, walaupun Windows sudah mendukung kode ANSI namun masih perlu diaktifkan terlebih dulu. Dalam *unit* `ansiCRT.pas` sudah saya sediakan fungsi [`EnableANSIMode`][14] untuk platform Windows tapi masih belum ada isinya, sebab saya bukan pengguna Windows sehingga saya tidak bisa mencoba sendiri kode programnya. Caranya tidak sulit, Anda cukup memanggil Windows API [`GetStdHandle`][11], [`GetConsoleMode`][12], dan [`SetConsoleMode`][13]. Jika Anda berhasil menyelesaikan fungsi `EnableANSIMode` tersebut, saya harap Anda berkenan berbagi kode untuk disertakan dalam *unit* `ansiCRT.pas` ini.

Fitur yg disediakan kode ANSI cukup kaya, mungkin lebih kaya dari yg disediakan *unit* CRT di Pascal. Namun ternyata tidak semua layar teks mendukung seluruh fitur yg ada di standar kode ANSI, khususnya fitur-fitur yg dianggap lanjut (atau mungkin tidak penting). Misalnya, *emulator* layar teks di VS Code tidak mendukung pengaturan teks berkedip (*blink*), layar teks di macOS tidak mendukung warna 24-bit, dan lain sebagainya. Jadi kita perlu hati-hati memilih fitur kode ANSI jika ingin mendukung banyak jenis layar teks.

Kendala lain adalah pembacaan data dari kode ANSI yg mengembalikan nilai. Misalnya perintah mengambil posisi kursor terakhir (lihat fungsi [`WhereXY`][15]) atau ukuran layar (lihat fungsi [`ScreenSize`][16]). Kita tidak bisa menggunakan prosedur bawaan `read` dari Pascal karena prosedur tersebut menunggu hingga pengguna menekan tombol `Enter` yg tentu saja akan mengganggu. Cara mengatasinya adalah dengan membuat fungsi sendiri yg bisa membaca data langsung dari keluaran baku (`stdout`). Saya sudah sediakan fungsi [`readStdOut`][17] untuk tujuan itu. Masalahnya, hingga tulisan ini dibuat, saya belum sempat menyelesaikannya. Jika Anda berminat (atau tertantang) untuk meneruskan, silakan dilanjutkan.

### Apa Bedanya Dengan *Unit* CRT?

Tidak ada. Pada dasarnya manfaat kode ANSI sama saja dengan *unit* CRT di Pascal, yaitu sama-sama mengatur antarmuka di layar teks. *Unit* [`ansiCRT.pas`][18] ini sekadar proyek *ngoprek* iseng saya di akhir pekan. Namun ada beberapa fitur kode ANSI yg tidak tersedia di *unit* CRT. Misalnya, pengaturan gaya teks seperti teks miring (*italics*) atau garis bawah (*underline*), pewarnaan hingga 256 atau 24-bit, penggulungan layar, dan sebagainya. Jika *unit* ini mampu menyediakan seluruh fitur kode ANSI maka *unit* ini punya lebih banyak fitur dari *unit* CRT serta bisa menjadi pustaka tambahan untuk pemrograman layar teks di dunia Pascal.

Anda berminat? Mari kita lanjutkan *bareng-bareng*. 

———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/5).  
Thank you. 😊

---
<span style="float: left">← [Home](index.md)</span> <span style="float: right">[Top](#top) ↑</span>

[1]: http://www.lihaoyi.com/post/BuildyourownCommandLinewithANSIescapecodes.html
[2]: https://www.python.org
[3]: https://en.wikipedia.org/wiki/ANSI_escape_code
[4]: https://www.freepascal.org
[5]: https://pak.lebah.web.id/tp_no.html
[6]: https://en.wikipedia.org/wiki/DOS
[7]: https://en.wikipedia.org/wiki/INT_10H
[8]: https://paklebah.github.io/fpc-dan-vscode.html
[9]: https://docs.microsoft.com/en-us/windows/console/console-virtual-terminal-sequences
[10]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1
[11]: https://docs.microsoft.com/en-us/windows/console/getstdhandle
[12]: https://docs.microsoft.com/en-us/windows/console/getconsolemode
[13]: https://docs.microsoft.com/en-us/windows/console/setconsolemode
[14]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1#file-ansicrt-pas-L184
[15]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1#file-ansicrt-pas-L295
[16]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1#file-ansicrt-pas-L314
[17]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1#file-ansicrt-pas-L208
[18]: https://gist.github.com/pakLebah/c5e2bbd0b93c863b2122660111db68d1#file-ansicrt-pas
