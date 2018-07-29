# Free Pascal, SQLdb, dan SQLite

Kemampuan RAD (*Rapid Application Development*) bahasa Pascal –tepatnya [Delphi][1] atau [Lazarus][2]– dikenal sangat memudahkan dalam pembuatan aplikasi *database*. Namun ternyata banyak juga pemrogram Pascal yg masih kesulitan membuat program *database* dengan Pascal tanpa bantuan RAD. Beberapa rekan pemrogram Pascal di komunitas [Pascal Indonesia][16] masih sering bertanya bagaimana membuat aplikasi *database* jika tidak menggunakan fitur RAD di Delphi atau Lazarus.

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

Cukup singkat, jelas, dan mudah dimengerti, bukan? Bagian utama program berisi pasangan `try...finally` yg mencoba membuka berkas data `chinook.db` sebagai parameter pada pemanggilan fungsi `openDB()`, menampilkan tabel melalui prosedur `showTables()`, dan perulangan `repeat...until` yg menjalankan *query* melalui prosedur `runQuery` hingga selesai yg ditunjukkan oleh peubah `quit`. Sebelum program berakhir, pastikan *database* ditutup melalui prosedur `closeDB()`.

> **CATATAN:** Kita asumsikan berkas data `chinook.db` berada dalam *folder* yg sama dengan program sehingga cukup disebut nama berkasnya saja. Namun jika berbeda lokasi, sertakan tujuan (*path*) berkas dengan benar. 

### Komponen Yg Dibutuhkan

Pemrograman *database* dengan SQLdb dan SQLite membutuhkan setidaknya 2 *unit*, yaitu:
- *unit* `sqldb.pas` berisi komponen-komponen berikut:
  - [`TSQLConnection`][18] untuk koneksi ke sistem *database*.
  - [`TSQLTransaction`][19] untuk manajemen transaksi data.
  - [`TSQLQuery`][20] untuk menjalankan perintah SQL.
- *unit* `sqlite3conn.pas` berisi komponen berikut:
  - [`TSQLite3Connection`][21] untuk akses data ke berkas SQLite. *Class* ini adalah turunan dari *class* `TSQLConnection` dengan implementasi khusus untuk SQLite (versi 3).

Di Lazarus, penambahan unit dilakukan otomatis jika kita meletakkan komponen-komponen visual SQLdb dari palet SQLdb ke *form*. Namun kali ini kita harus menambahkan sendiri di blok [`uses`][17] di program Pascal kita. Masih ada beberapa *unit* lain dari paket komponen SQLdb untuk kegunaan dan manfaat yg berbeda, misalnya `db.pas`, namun itu tidak dibutuhkan dalam program kita ini.

![](http://wiki.freepascal.org/images/8/82/sqldbcomponents.png)

> **INFO:** Selain SQLite, SQLdb juga menyediakan komponen untuk koneksi ke berbagai jenis sistem *database* seperti yg ditunjukan dalam gambar palet SQLdb di atas. Misalnya ke MS SQL, mySQL, MariaDB, Firebird, PostgreSQL, Oracle, atau ODBC, dan lain sebagainya.

### Membuka Koneksi Database

Hal pertama dalam olah data adalah tentu saja membuka koneksi ke sistem *database* yg digunakan. Untuk melakukan itu, perhatikan fungsi `openDB()` yg dimulai pada baris [21][22]. Kodenya adalah sebagai berikut:

```pascal
function openDB(const dbName: string): boolean;
begin
  // create components
  sqlite3 := TSQLite3Connection.Create(nil);
  dbTrans := TSQLTransaction.Create(nil);
  dbQuery := TSQLQuery.Create(nil);
  slNames := TStringList.Create;

  // setup components
  sqlite3.Transaction   := dbTrans;
  dbTrans.Database      := sqlite3;
  dbQuery.Transaction   := dbTrans;
  dbQuery.Database      := sqlite3;
  slNames.CaseSensitive := false;

  // setup db
  sqlite3.DatabaseName := dbName;
  sqlite3.HostName     := 'localhost';
  sqlite3.CharSet      := 'UTF8';

  // open db
  if FileExists(dbName) then
  try
    sqlite3.Open;
    result := sqlite3.Connected;
  except
    on E: Exception do
    begin
      sqlite3.Close;
      writeln(sqlDBError(E.Message));
    end;
  end
  else
  begin
    result := false;
    writeln('Database file "',dbName,'" is not found.');
  end;
end;
```

Sebelum bisa menggunakan komponen, kita harus membuat obyek dari *class*-nya terlebih dahulu. Itu yg dilakukan dalam blok komentar `//create component` yg berisi pembuatan obyek `sqlite3`, `dbTrans`, `dbQuery`, dan `slNames` yg deklarasi variabelnya ada pada blok `var` di baris nomor [8][23]. `slNames` adalah sebuah `TStringList` untuk menampung daftar nama yg nanti akan kita butuhkan.

Selanjutnya adalah mengatur properti-properti penting di tiap obyek komponen tersebut. Itu dilakukan dalam blok komentar `//setup components` yg berisi pengaturan properti `Transaction` dan `Database` di obyek `sqlite3`, `dbTrans`, dan `dbQuery`. Perhatikan dengan baik bagaimana pengisian propertinya. Properti ketiga obyek tersebut harus saling terhubung dengan benar agar bisa saling bekerja sama.

Kemudian adalah mengatur properti koneksi database pada obyek `sqlite3` yg dilakukan dalam blok komentar `// setup db`. Properti `DatabaseName` berisi tujuan (*path*) lengkap ke berkas data, nilainya diambil dari parameter `dbName`. Properti `HostName` diisi `localhost` karena SQLite bekerja lokal (tanpa *server*). Properti `CharSet` diisi `UTF8` karena itu adalah *encoding* yg paling umum digunakan. Perlu diingat bahwa ini adalah pengaturan untuk SQLite, yg belum tentu sama pada sistem *database* yg lain. Sistem *database* yg berbeda bisa jadi membutuhkan pengaturan properti yg berbeda pula.

Setelah semua obyek dibuat, dihubungkan, dan diatur dengan benar, maka kita bisa membuka koneksi ke *database* dengan menjalankan prosedur `Open` di obyek `sqlite3`. Itu dilakukan dalam blok komentar `// open db`. Menjalankan prosedur `Open` perlu dilakukan dalam pasangan `try...except` agar jika terjadi kegagalan bisa ditangani. Dalam hal ini jika ada kegagalan maka kita hanya menutup koneksi dan menampilkan pesan kesalahan yg diberikan oleh *database*.

Namun dalam program di atas, pasangan `try...except` dilakukan dalam pengecekan berkas data dengan fungsi `FileExists()`. Ini perlu dilakukan karena berkas data SQLite bersifat lokal sehingga jika berkas data tidak ada maka kita bisa menampilkan pesan yg sesuai dan tidak perlu repot-repot membuka koneksi ke *database*. Selain itu juga karena SQLdb akan membuat berkas data baru jika berkas yg diminta tidak ditemukan. Pengecekan keberadaan berkas mencegah hal tersebut.

Fungsi `openDB` mengembalikan nilai bertipe `boolean`. Nilai kembalian fungsi berasal dari status koneksi obyek `sqlite3` properti `Connected` yg dipadukan dengan kembalian fungsi `FileExists()`. Jika kembalian fungsi bernilai `true` maka koneksi ke *database* sukses, sebaliknya jika bernilai `false` maka koneksi gagal.

### Menjalankan Perintah SQL











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
[18]: https://www.freepascal.org/docs-html/fcl/sqldb/tsqlconnection.html
[19]: https://www.freepascal.org/docs-html/fcl/sqldb/tsqltransaction.html
[20]: https://www.freepascal.org/docs-html/fcl/sqldb/tsqlquery.html
[21]: http://wiki.freepascal.org/TSQLite3Connection
[22]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L21
[23]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L8
