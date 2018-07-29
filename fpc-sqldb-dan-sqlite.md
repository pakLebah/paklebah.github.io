# Free Pascal, SQLdb, dan SQLite

Kemampuan RAD (*Rapid Application Development*) bahasa Pascal –tepatnya [Delphi][1] atau [Lazarus][2]– dikenal sangat mudah untuk membuat aplikasi *database*. Namun ternyata banyak juga pemrogram Pascal yg masih kesulitan membuat program *database* dengan Pascal tanpa bantuan RAD. Beberapa rekan pemrogram Pascal di komunitas [Pascal Indonesia][16] masih sering bertanya bagaimana membuat aplikasi *database* jika tidak menggunakan fitur RAD di Delphi atau Lazarus.

#### Kelemahan RAD

Salah satu kelemahan dari pemrograman RAD ala Delphi atau Lazarus adalah kemudahan yg menyembunyikan cara kerja sebenarnya di balik kemudahan tersebut. Pemrogram tinggal *drag-n-drop* komponen ke atas *form*, klik sana-sini, atur-atur propertinya, tulis kode-kode seperlunya, lalu *voila*... program pun bekerja. Nyaris semuanya bekerja secara otomatis. Apa yg terjadi di balik komponen dan bagaimana komponen bekerja, banyak pemrogram yg tidak paham. Komponen visual ala [VCL][6] atau [LCL][7] itu seperti kotak televisi yg kita terima apa adanya tanpa perlu tahu apa isi di dalamnya, yg penting televisi itu bekerja, titik. Mudah dan memanjakan, tetapi tidak memberikan ilmu.

Kelemahan tersebut baru terasa ketika pemrogram harus meninggalkan pola pemrograman RAD. Contohnya adalah ketika pemrogram harus menggunakan komponen *database* di aplikasi web atau *console*, yg tidak memiliki GUI (*Graphical User Interface*). Di pemrograman RAD, akses ke *database* bisa dilakukan nyaris tanpa menulis kode program. Cukup dengan menghubungkan komponen-komponennya, sesuaikan *setting* sana-sini, tuliskan *query*-nya, lalu data pun muncul dalam tabel (*grid*). Tanpa GUI, komponennya masih bisa digunakan sebagai *class*, tapi pemrogram RAD biasanya bingung bagaimana menggunakan komponen secara "manual". Mereka bingung bagaimana melakukan koneksi ke *database*, menjalankan *query* dan mengambil datanya, menampilkan data yg diterima ke pengguna, dan lain sebagainya. 

#### SQLdb dan SQLite

Nah... untuk itu, mari kita belajar membuat aplikasi *database* **sederhana** dengan cara "manual" menggunakan *class* yg tersedia di [Free Pascal][3]. Kita akan gunakan *class-class* dari *unit* [SQLdb][4] dan *database*-nya kita gunakan [SQLite][5] (versi 3). Kita menggunakan SQLdb karena merupakan bagian dari paket Free Pascal sehingga jika kita sudah memasang Free Pascal maka SQLdb pun (seharusnya) juga telah tersedia. Bagi pengguna Delphi, bisa menggunakan komponen [dbExpress][8] yg prinsip kerjanya agak mirip dengan SQLdb yaitu akses ke *database* melalui pustaka asli (*native*) yg disediakan *database* yg bersangkutan. Kita menggunakan SQLite karena SQLite mudah pemasangannya, kecil, cepat, ringan, dan mendukung fitur-fitur SQL yg baku dan umum. Di Linux atau Unix terbaru, SQLite biasanya sudah terpasang. Sementara di Windows, pemasangannya juga cukup [mudah][9].

Sebelum kita mulai menulis program, pastikan terlebih dulu sudah terpasang Free Pascal dan SQLite di komputer kita. Lebih baik jika kita menggunakan versi yg terbaru. Untuk penyunting program, silakan gunakan aplikasi apa pun yg Anda suka untuk menulis program Pascal. Mungkin Lazarus yg paling umum, tetapi saya sendiri menggunakan [VS Code][10].

Kita kali ini akan belajar dari sebuah contoh program yg sudah saya siapkan. Silakan unduh kode program dan berkas *database* dari *gist* di [sini][11]. Klik tombol `Download ZIP` di sisi kanan atas laman tersebut, atau langsung unduh saja dari [sini][12], lalu bongkar (*extract*) berkas `.zip` yg diperoleh. Sudah? Mari kita bahas... 

## Contoh Data

*Database* yg akan kita gunakan dalam program, saya ambil dari contoh yg disediakan oleh situs [SQLite Tutorial][14] di [sini][15]. Contoh *database* berupa berkas bernama `chinook.db` dengan struktur data seperti dalam diagram berikut:

![](http://www.sqlitetutorial.net/wp-content/uploads/2015/11/sqlite-sample-database-color.jpg)

*Database* tersebut berisi 11 tabel dengan beberapa ribu baris data. Jumlah yg cukup bagi kita untuk belajar mengolah data dengan perintah-perintah SQL. Namun dalam tulisan ini saya hanya akan membahas pemrograman *database* dengan komponen SQLdb di Free Pascal. Sedang pemrograman dengan bahasa SQL di SQLite bisa Anda pelajari secara mandiri di situs [SQLite Tutorial][14].

## Contoh Program

Contoh program hanya terdiri dari 1 berkas saja bernama `chinook.lpr`. Saya namakan demikian karena program tersebut hanya untuk mengakses berkas data `chinook.db` saja. Mari kita bahas isi dari program tersebut.

### Bagian Utama

Kita mulai dari bagian utama program. Silakan lompat ke baris nomor [235][13], kode yg kita perhatikan adalah sebagai berikut:

```pascal
//# main program
begin
  try
    if openDB('chinook.db') then
    begin
      showTables(false);
      repeat runQuery until quit;
    end;
  finally
    closeDB;
  end;
end.
```

Cukup singkat, jelas, dan mudah dimengerti, bukan? Bagian utama program berisi pasangan `try...finally` yg mencoba membuka berkas *database* `chinook.db` melalui fungsi `openDB()`, menampilkan tabel melalui prosedur `showTables()`, dan perulangan yg menjalan *query* melalui prosedur `runQuery` hingga selesai. Sebelum program berakhir, pastikan *database* ditutup melalui prosedur `closeDB()`.

### Komponen Yg Dibutuhkan

Pemrograman *database* dengan SQLdb dan SQLite membutuhkan setidaknya 2 *unit*, yaitu:
- *unit* `sqldb.pas` berisi komponen-komponen berikut:
  - `TSQLConnection` untuk koneksi ke sistem *database*.
  - `TSQLTransaction` untuk manajemen transaksi data.
  - `TSQLQuery` untuk menjalankan perintah SQL.
- *unit* `sqlite3conn.pas` berisi komponen berikut:
  - `TSQLite3Connection` untuk akses data ke berkas SQLite.

Pastikan kedua unit itu harus kita tambahkan di baris [`uses`][17] di program Pascal kita. Masih ada beberapa *unit* lain dari paket komponen SQLdb untuk kegunaan yg berbeda, namun itu tidak dibutuhkan dalam program kita ini. Di Lazarus, penambahan unit dilakukan otomatis jika kita meletakkan komponen-komponen visual SQLdb ke *form* dari palet SQLdb.

![](http://wiki.freepascal.org/images/8/82/sqldbcomponents.png)

_____
[1]: https://www.embarcadero.com/products/delphi/starter/
[2]: http://www.lazarus-ide.org
[3]: https://www.freepascal.org
[4]: https://www.freepascal.org/docs-html/fcl/sqldb/usingsqldb.html
[5]: https://www.sqlite.org
[6]: http://docwiki.embarcadero.com/RADStudio/XE6/en/VCL_Overview
[7]: http://wiki.freepascal.org/LCL
[8]: http://docwiki.embarcadero.com/RADStudio/Berlin/en/DbExpress_Framework
[9]: http://www.sqlitetutorial.net/download-install-sqlite/
[10]: https://paklebah.github.io/fpc-dan-vscode.html
[11]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add
[12]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add/archive/f6005b6a27caa0ade96abed1310c951921d56d0b.zip
[13]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L235
[14]: http://www.sqlitetutorial.net
[15]: http://www.sqlitetutorial.net/sqlite-sample-database/
[16]: http://facebook.com/groups/Pascal.ID
[17]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L5
