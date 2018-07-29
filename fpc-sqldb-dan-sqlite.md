# Free Pascal, SQLdb, dan SQLite

---

### Daftar Isi

* Pendahuluan
   * [Kelemahan RAD](#kelemahan-rad)
   * [SQLdb dan SQLite](#sqldb-dan-sqlite)
* [Contoh Data](#contoh-data)
* [Contoh Program](#contoh-program)
   * [Unit Yg Dibutuhkan](#unit-yg-dibutuhkan)
   * [Bagian Utama](#bagian-utama)
   * [Membuka Koneksi Database](#membuka-koneksi-database)
   * [Menampilkan Daftar Tabel](#menampilkan-daftar-tabel)
      * [Kesalahan Kecil Dalam TSQLite3Connection](#kesalahan-kecil-dalam-tsqlite3connection)
   * [Menjalankan Perintah SQL](#menjalankan-perintah-sql)
      * [Mengambil Data](#mengambil-data)
      * [Mengubah Data](#mengubah-data)
      * [Menampilkan Struktur Tabel](#menampilkan-struktur-tabel)
   * [Menutup Koneksi Database](#menutup-koneksi-database)
* [Demo Program](#demo-program)
* [Kesimpulan](#kesimpulan)

---

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

### Unit Yg Dibutuhkan

Pemrograman *database* dengan SQLdb dan SQLite membutuhkan setidaknya 2 *unit*, yaitu:

- *unit* `sqldb.pas` berisi komponen-komponen berikut:
  - [`TSQLConnection`][18] untuk koneksi ke sistem *database*.
  - [`TSQLTransaction`][19] untuk manajemen transaksi data.
  - [`TSQLQuery`][20] untuk menjalankan perintah SQL.
- *unit* `sqlite3conn.pas` berisi komponen berikut:
  - [`TSQLite3Connection`][21] untuk akses data ke berkas SQLite. *Class* ini adalah turunan dari *class* `TSQLConnection` dengan implementasi khusus untuk SQLite (versi 3).

Di Lazarus, penambahan unit dilakukan otomatis jika kita meletakkan komponen-komponen visual SQLdb dari palet SQLdb ke *form*. Namun kali ini kita harus menambahkan sendiri di blok [`uses`][17] di program Pascal kita. Masih ada beberapa *unit* lain dari paket komponen SQLdb untuk kegunaan dan manfaat yg berbeda, misalnya `db.pas`, namun itu tidak dibutuhkan dalam program kita ini.

![](http://wiki.freepascal.org/images/8/82/sqldbcomponents.png)

> **INFO:** Selain SQLite, SQLdb juga menyediakan komponen untuk koneksi ke berbagai jenis sistem *database* seperti yg ditunjukan dalam gambar palet SQLdb di atas. Misalnya ke mySQL (atau MariaDB), Firebird, PostgreSQL, Oracle, MS SQL (melalui ODBC), dan lain sebagainya.

### Bagian Utama

Selanjutnya kita mari bahas dari bagian utama program. Silakan lompat ke baris nomor [235][13], kode yg kita perhatikan adalah sebagai berikut:

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

Cukup singkat, jelas, dan mudah dimengerti, bukan? Bagian utama program berisi pasangan `try...finally` yg mencoba membuka berkas data `chinook.db` sebagai parameter pada pemanggilan fungsi `openDB`, menampilkan tabel melalui prosedur `showTables`, dan perulangan `repeat...until` yg menjalankan *query* melalui prosedur `runQuery` hingga selesai yg ditunjukkan oleh peubah `quit`. Sebelum program berakhir, pastikan *database* ditutup melalui prosedur `closeDB`.

> **CATATAN:** Kita asumsikan berkas data `chinook.db` berada dalam *folder* yg sama dengan program sehingga cukup disebut nama berkasnya saja. Namun jika berbeda lokasi, sertakan tujuan (*path*) berkas dengan benar. 

### Membuka Koneksi Database

Hal pertama dalam olah data adalah tentu saja membuka koneksi ke sistem *database* yg akan digunakan. Untuk melakukan itu, perhatikan fungsi `openDB` yg dimulai pada baris [21][22]. Kodenya adalah sebagai berikut:

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

Sebelum bisa menggunakan komponen, kita harus membuat obyek dari *class*-nya terlebih dahulu. Itu yg dilakukan dalam blok komentar `// create components` yg berisi pembuatan obyek `sqlite3`, `dbTrans`, `dbQuery`, dan `slNames` yg deklarasi variabelnya ada pada blok `var` di baris nomor [8][23]. `slNames` adalah sebuah `TStringList` untuk menampung daftar nama yg nanti akan kita butuhkan.

Selanjutnya adalah mengatur properti-properti penting di tiap obyek komponen tersebut. Itu dilakukan dalam blok komentar `//setup components` yg berisi pengaturan properti `Transaction` dan `Database` di obyek `sqlite3`, `dbTrans`, dan `dbQuery`. Perhatikan dengan baik bagaimana pengisian propertinya. Properti ketiga obyek tersebut harus saling terhubung dengan benar agar bisa saling bekerja sama.

Kemudian adalah mengatur properti koneksi database pada obyek `sqlite3` yg dilakukan dalam blok komentar `// setup db`. Properti `DatabaseName` berisi tujuan (*path*) lengkap ke berkas data, nilainya diambil dari parameter `dbName`. Properti `HostName` diisi `localhost` karena SQLite bekerja lokal (tanpa *server*). Properti `CharSet` diisi `UTF8` karena itu adalah *encoding* yg paling umum digunakan. Perlu diingat bahwa ini adalah pengaturan untuk SQLite, yg belum tentu sama pada sistem *database* yg lain. Sistem *database* yg berbeda bisa jadi membutuhkan pengaturan properti yg berbeda pula.

Setelah semua obyek dibuat, dihubungkan, dan diatur dengan benar, maka kita bisa membuka koneksi ke *database* dengan menjalankan prosedur `Open` di obyek `sqlite3`. Itu dilakukan dalam blok komentar `// open db`. Menjalankan prosedur `Open` perlu dilakukan dalam pasangan `try...except` agar jika terjadi kegagalan bisa ditangani. Dalam hal ini jika ada kegagalan maka kita hanya menutup koneksi dan menampilkan pesan kesalahan yg diberikan oleh *database*.

Namun dalam program di atas, pasangan `try...except` dilakukan dalam pengecekan berkas data dengan fungsi `FileExists`. Ini perlu dilakukan karena berkas data SQLite bersifat lokal sehingga jika berkas data tidak ada maka kita bisa menampilkan pesan yg sesuai dan tidak perlu repot-repot membuka koneksi ke *database*. Selain itu juga karena SQLdb akan membuat berkas data baru jika berkas yg diminta tidak ditemukan. Pengecekan keberadaan berkas data mencegah hal tersebut.

Fungsi `openDB` mengembalikan nilai bertipe `boolean`. Nilai kembalian fungsi berasal dari status koneksi obyek `sqlite3` properti `Connected` yg dipadukan dengan kembalian fungsi `FileExists`. Jika kembalian fungsi bernilai `true` maka koneksi ke *database* sukses, sebaliknya jika bernilai `false` maka koneksi gagal.

### Menampilkan Daftar Tabel

Apabila koneksi ke *database* berhasil, program menampilkan daftar tabel yg ada dalam berkas data yg dibuka. Ini dilakukan oleh prosedur `showTables`. Prosedur `showTables` dimulai pada baris nomor [77][26] dengan kode sebagai berikut:

```pascal
procedure showTables(const clear: boolean = true);
var
  i,j: integer;
begin
  if clear then ClrScr;

  // get and print list of tables
  sqlite3.GetTableNames(slNames,false);
  if slNames.Count > 0 then
  begin
    writeln('> "',sqlite3.DatabaseName,'" has ',slNames.Count,' table(s):');

    j := 0;
    for i := 0 to slNames.Count-1 do
      // fix included system tables bug
      if LowerCase(Copy(slNames[i],1,7)) <> 'sqlite_' then
      begin
        j := j+1;
        writeln(j,'. ',slNames[i]);
      end;
    writeln('Found ',j,' data table(s).');
  end
  else
    writeln('> "',sqlite3.DatabaseName,'" has no tables.');
end;
```

Yg pertama dilakukan adalah membersihkan layar jika diperlukan, berdasarkan parameter `clear`. Kemudian mengambil daftar nama tabel data dengan memanggil prosedur `GetTableNames` dari obyek `sqlite3`. Prosedur tersebut mengembalikan daftar tabel melalui parameter pertama bertipe `TStringList` di mana kita sudah siapkan variabel `slNames` untuk menampungnya. Parameter kedua bertipe `boolean` untuk kondisi penyertaan tabel sistem (bersifat internal dan tersembunyi). Kita berikan nilai `false` ke parameter kedua yg artinya program tidak butuh tabel sistem disertakan dalam daftar.

Selanjutnya, program melihat apakah berkas data yg kita buka memiliki tabel atau tidak, dengan cara mengecek jumlah baris melalui properti `Count` di obyek `slNames`. Jika memiliki tabel (properti `Count` bernilai lebih dari 0) maka program menampilkan informasi jumlah tabel, diikuti tampilan daftar nama tabel yg ditampung dalam obyek `slNames` dengan perulangan `for...do`.

#### Kesalahan Kecil Dalam TSQLite3Connection

Namun rupanya ada sedikit kesalahan (*bug*) dalam komponen `TSQLite3Connection` karena prosedur `GetTableNames` dengan parameter kedua bernilai `false` masih mengembalikan sebagian tabel sistem. Dalam kasus ini, seharusnya mengembalikan 11 tabel data, ternyata mengembalikan 13 tabel di mana 2 di antaranya adalah tabel sistem. Kesalahan ini terekam dalam video demo program di bawah dan baru saya sadari setelah menontonnya. Kesalahan ini harus kita benahi.

SQLite menamai tabel sistemnya dengan awalan `sqlite_`. Maka untuk menyembunyikan tabel sistem yg terikut dalam daftar `slNames` cukup mudah, yaitu dengan hanya menampilkan tabel yg namanya tidak berawalan `sqlite_` (7 huruf pertama). Blok seleksi `if...then` dalam perulangan `for...do` di atas yg melakukan itu. Lalu kita tambahkan informasi berapa jumlah tabel data yg sebenarnya. Dengan pengecekan itu maka jumlah tabel data yg tampil pun sesuai dengan berkas data, yaitu 11 tabel.

### Menjalankan Perintah SQL

Kini program siap menerima perintah SQL dari masukan pengguna. Ini dilakukan oleh prosedur `runQuery` yg berada di baris [202][27], yg kodenya sebagai berikut:

```pascal
procedure runQuery;
var
  p: integer;
  q,s: string;
begin
  if sqlite3.Connected then
  begin
    // query input
    writeln('_____');
    writeln('Enter SQL query:');
    write('» ');
    readln(q);
    q := Trim(q);

    // filter input to process custom commands
    if q <> '' then
    begin
      // read first word
      p := Pos(' ',q);
      if p = 0 then p := Length(q) else p := p-1;
      s := LowerCase(Copy(q,1,p));

      // run query
      if (s = 'quit') or (s = 'exit') then quit := true
      else if (s = 'clear') and (p = Length(q)) then ClrScr
      else if (s = 'tables') and (p = Length(q)) then showTables
      else if (s = 'schema') then showSchema(q)
      else if s = 'select' then openQuery(q)
      else execQuery(q);
    end;
  end;
end;
```

Prosedur `runQuery` selalu mengecek apakah program masih tersambung ke *database* melalui properti `Connected` dari obyek `sqlite3` karena tidak mungkin menjalankan perintah SQL jika program terputus dari *database*. Selanjutnya menampilkan *prompt* untuk menerima masukan dari pengguna. Masukan pengguna ditampung sebagai `string` dalam variabel `q`. Ini dilakukan dalam blok komentar `// query input`.

Jika ada masukan dari pengguna, yaitu `q` tidak berupa `string` kosong, maka program menguji jenis perintah apa yg diberikan pengguna lalu memanggil perintah yg sesuai. Jenis perintah ditentukan dari kata pertama dalam kalimat perintah. Pengambilan kata pertama dilakukan dalam blok komentar `// read first word`. Pengujian ini diperlukan karena program kita tidak hanya menerima perintah SQL tapi juga beberapa perintah khusus yg tidak disediakan SQLite, yaitu:

- `quit` atau `exit` untuk menghentikan program.
- `clear` untuk membersihkan layar.
- `tables` untuk menampilkan daftar tabel data.
- `schema <table>` untuk menampilkan struktur tabel.

Perintah SQL perlu dibedakan juga karena SQLdb punya perintah yg berbeda untuk membaca data dan mengubah data. Perintah SQL untuk membaca data umumnya adalah `select`, maka itu harus kita deteksi dalam masukan pengguna. Perintah SQL selain `select` kita anggap perintah untuk mengubah data. Pengujian jenis perintah dilakukan dalam blok komentar `// run query`.

#### Mengambil Data

Jika kata pertama masukan pengguna adalah `select` maka program akan memanggil prosedur `openQuery` dengan parameter `sql` bertipe `string`. Prosedur `openQuery` bekerja dengan obyek `dbQuery` yg dimulai dari baris [127][28] dengan kode sebagai berikut:

```pascal
procedure openQuery(const sql: string);
var
  i: integer;
begin
  try
    // fetch data
    dbQuery.SQL.Text := sql;
    dbQuery.Open;

    if dbQuery.Active then
    begin
      ClrScr;
      writeln('> Fetching: "',sql,'"');

      // get and print headers
      dbQuery.GetFieldNames(slNames);
      for i := 0 to slNames.Count-1 do write('| ',UpperCase(slNames[i]),' ');
      writeln;

      // iterate rows
      while not dbQuery.EOF do
      begin
        // print cell by column
        for i := 0 to dbQuery.FieldCount-1 do
          write('| ',dbQuery.Fields.Fields[i].AsString,' ');
        writeln;

        dbQuery.Next;
      end;

      // print summary
      writeln('Found ',dbQuery.RecordCount,' record(s).');
    end;

    dbQuery.Close;
  except
    on E: Exception do writeln(sqlDBError(E.Message));
  end;
end;
```

Masukan dari pengguna tidak bisa dijamin selalu benar, oleh karena itu perintah SQL yg diberikan pengguna harus dijalankan dalam pasangan `try...except` untuk menangkap kesalahan yg terjadi dan menampilkan pesan kesalahan dari *database*. Kemudian program memberikan perintah SQL dari parameter `sql` ke properti `SQL.Text`, lalu menjalankan prosedur `Open`. Ini dilakukan dalam blok komentar `// fetch data`.

Jika prosedur `Open` sukses, ditunjukkan dengan properti `Active` bernilai `true`, maka program akan menampilkan tabel data. Diawali dengan menampilkan daftar nama kolom tabel, yg dilakukan dalam blok komentar `// get and print headers`, yaitu dengan menjalankan prosedur `GetFieldNames` yg kembaliannya ditampung dalam `slNames`. Kemudian perulangan `for...do` untuk menampilkan daftar nama kolom sebagai baris pertama.

Selanjutnya program melakukan perulangan untuk mengambil setiap baris data yg ada, dari baris pertama hingga baris terakhir. Caranya adalah perulangan `while...do` dengan mengecek akhir baris melalui properti `EOF` (*end of file*). Tampilkan data pada setiap baris dengan perulangan `for..do` untuk membaca data di tiap kolomnya. Jumlah kolom ada di properti `FieldCount` dan indeks kolom dimulai dari `0`. Jangan lupa memanggil prosedur `Next` di akhir perulangan `while...do` agar perulangan tidak tertahan (*stuck*) di baris pertama.

Setelah tabel, program menampilkan info ringkasan tabel berupa jumlah baris data yg diterima. Jumlah baris data ada di properti `RecordCount`. Dan terakhir adalah menutup perintah SQL dengan memanggil prosedur `Close`. Selesailah rangkaian proses menampilkan data dari perintah `select`.

#### Mengubah Data

Jika perintah dari pengguna bukan 5 perintah yg sudah ditentukan di atas, maka program menganggap itu adalah perintah untuk mengubah data. Program menjalankan prosedur `execQuery` dengan parameter `sql` bertipe `string`. Prosedur `execQuery` dimulai dari baris nomor [103][29] dengan kode sebagai berikut:

```pascal
procedure execQuery(const sql: string);
begin
  try
    // execute command
    dbQuery.SQL.Text := sql;
    dbTrans.Active := true;
    dbQuery.ExecSQL;

    // print info
    writeln('> Executing: "',sql,'"');
    writeln('Affected ',dbQuery.RowsAffected,' record(s).');

    // commit changes
    dbTrans.Commit;
  except
    on E: Exception do
    begin
      // rollback changes
      dbTrans.Rollback;
      writeln(sqlDBError(E.Message));
    end;
  end;
end;
```

Mengubah data harus dilakukan dalam transaksi agar jika ada kesalahan data bisa dibatalkan. Dalam SQLdb, transaksi data ditangani oleh *class* `TSQLTransaction` yg dalam program ini berupa obyek `dbTrans`. Sebagaimana prosedur `runQuery`, prosedur `execQuery` juga dilakukan dalam pasangan `try...except` untuk menangkap kesalahan perintah dari pengguna.

Prosedur `execQuery` dimulai dengan memberikan perintah SQL dari parameter `sql` ke properti `SQL.Text` di obyek `dbQuery`. Lalu memulai transaksi dengan memberikan nilai `true` pada properti `Active` di obyek `dbTrans`. Kemudian menjalankan prosedur `ExecSQL` di obyek `dbQuery`. Ini yg dilakukan dalam blok komentar `// execute command`.

Jika perintah SQL berhasil dijalankan maka properti `RowsAffected` di obyek `dbQuery` akan berisi jumlah baris data yg berubah akibat perintah tersebut. Info ini kita tampilkan ke pengguna. Kemudian pastikan perubahan data tersimpan ke berkas data dengan memanggil prosedur `Commit` di obyek `dbTrans`.

Jika perintah SQL ternyata gagal maka ini ditangkap oleh blok `except` yg melakukan pembatalan perubahan data dengan memanggil prosedur `Rollback` di obyek `dbTrans`. Kemudian menampilkan pesan kesalahan ke pengguna.

#### Menampilkan Struktur Tabel

SQLdb telah menyediakan beberapa prosedur untuk mengambil info struktur tabel, misalnya prosedur `GetTableNames` dan `GetFieldNames` di atas. Namun itu hanya mengembalikan namanya saja, tidak termasuk tipe data kolom dan info-info lainnya. Untungnya, SQLite menyediakan fitur membaca struktur tabel melalui perintah SQL. Mari kita gunakan fitur tersebut.

Menampilkan info struktur tabel dilakukan dengan perintah `schema` diikuti nama tabel. Perintah itu ditangani oleh prosedur `showSchema` yg dimulai pada baris nomor [167][30] dengan kode sebagai berikut:

```pascal
procedure showSchema(const sql: string);
var
  i,p: integer;
  t: string;
begin
  // check table name
  p := Pos(' ',sql);
  if p = 0 then writeln('ERROR: Schema requires a table name.');
  if p = 0 then exit;

  // check table existence
  sqlite3.GetTableNames(slNames,false);
  t := LowerCase(Copy(sql, p+1, Length(sql)-p));
  p := slNames.IndexOf(t);
  if p = -1 then writeln('ERROR: Table "',t,'" is not found.');
  if p = -1 then exit;

  // fetch table schema
  try
    ClrScr;
    writeln('> Schema of "',t,'"');

    // schema command
    dbQuery.SQL.Text := 'select name, sql from sqlite_master '+
                        'where type="table" and name="'+t+'"';
    dbQuery.Open;

    // print schema
    writeln(dbQuery.Fields.Fields[1].AsString);
    dbQuery.Close;
  except
    on E: Exception do writeln(sqlDBError(E.Message));
  end;
end;
```

Karena perintah `schema` membutuhkan nama tabel, hal pertama yg dicek adalah parameter kedua. Jika tidak disertakan nama tabel maka perintah dihentikan. Ini dilakukan dalam blok komentar `// check table name`. Selanjutnya adalah mengecek keberadaan tabel yg diminta dalam daftar nama tabel. Jika tabel yg diminta tidak ditemukan maka perintah dihentikan. Ini dilakukan dalam blok komentar `// check table existence`.

Jika tabel dipastikan ada dan tersedia maka dilakukan pembacaan struktur tabel dengan perintah SQL `select` ke tabel sistem bernama `sqlite_master`. Caranya sama dengan cara [mengambil data][31] di atas. Bedanya tidak perlu dilakukan perulangan karena data yg dikembalikan *database* bisa dipastikan hanya 1 baris saja.

Setelah menjalankan perintah SQL dari pengguna, program kembali menungggu perintah SQL selanjutnya. Demikian seterusnya hingga pengguna memberikan perintah `quit` atau `exit` untuk menghentikan program. Jika perintah tersebut diterima maka program memanggil prosedur `closeDB` dan program berakhir.

### Menutup Koneksi Database

Fungsi `openDB` tidak selalu berhasil melakukan koneksi ke *database*. Karena satu dan lain hal, kegagalan koneksi bisa saja terjadi. Seperti yg ditunjukkan dalam [bagian utama][25] program, ketika fungsi `openDB` gagal (mengembalikan nilai `false`), atau perulangan `repeat...until` selesai, maka program akan masuk ke bagian `finally` di mana ada pemanggilan prosedur `closeDB`. Mari kita perhatikan apa isi dari prosedur tersebut. 

Prosedur `closeDB` dimulai pada baris nomor [60][24] dengan kode sebagai berikut:

```pascal
procedure closeDB;
begin
  // disconnect
  if sqlite3.Connected then
  begin
    dbTrans.Commit;
    dbQuery.Close;
    sqlite3.Close;
  end;

  // release
  slNames.Free;
  dbQuery.Free;
  dbTrans.Free;
  sqlite3.Free;
end;
```

Cukup singkat saja. Ada 2 hal yg dilakukan dalam prosedur `closeDB`, yaitu pertama adalah memutuskan koneksi ke *database* jika koneksi sedang aktif (yg ditunjukkan oleh properti `Connected` di obyek `sqlite3`). Pemutusan dilakukan dengan menjalankan prosedur `Close` pada obyek `dbQuery` dan `sqlite3`. Namun sebelum itu, dilakukan perintah `Commit` pada obyek `dbTrans` untuk menyimpan segala perubahan data yg telah terjadi ke *database*.

Selanjutnya adalah melepas sumber daya yg digunakan obyek-obyek komponen yg telah dibuat sebelumnya. Caranya dengan memanggil prosedur `Free` pada obyek `slNames`, `dbQuery`, `dbTrans`, dan `sqlite3`. Dalam RAD, pelepasan sumber daya ini juga dilakukan otomatis oleh "pemilik" (*owner*) komponen, yg biasanya adalah *form* tempat komponen berada. Namun kali ini harus kita lakukan manual karena tidak ada "pemilik" komponen.

## Demo Program

Berikut demo program `chinook.lpr` dalam bentuk video (`.gif`) yg direkam saat dijalankan dari VS Code.

![](https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add/raw/f6005b6a27caa0ade96abed1310c951921d56d0b/z_chinook.gif)

## Kesimpulan

Dari uraian di atas, cukup jelas bahwa menulis program *database* secara "manual" tidak semudah *drag-n-drop* di RAD, tapi juga tidak sulit. Mungkin kodenya agak sedikit lebih panjang, tapi alurnya jelas dan mudah. Contoh program ini saya buat sesederhana mungkin dengan operasi dasar yg umum digunakan agar lebih mudah dipahami. Untuk operasi olah data dengan perintah SQL yg lebih rumit, silakan pelajari dari tautan-tautan yg disertakan. Namun demikian, mekanisme dasarnya tidak jauh berbeda dengan yg saya jelaskan di sini.

Contoh program ini masih sangat bisa dikembangkan lebih jauh atau ditambah fitur-fitur lain yg lebih menarik. Tekniknya juga bisa diterapkan dalam aplikasi web atau non-GUI lainnya. Semula contoh program ini akan saya buat sebagai aplikasi web dengan menggunakan *unit* [WebCRT][32]. Namun agar pembaca tidak terganggu dengan kode-kode web yg sebenarnya tidak terkait dengan olah data, maka saya urungkan rencana itu dan jadikan sebagai aplikasi *console* saja.

Demikian. Semoga bermanfaat.

———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/4).  
Thank you. 😊

---
<span style="float: left">← [Home](index.md)</span> <span style="float: right">[Top](#top) ↑</span>

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
[24]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L60
[25]: #bagian-utama
[26]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L77
[27]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L202
[28]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L127
[29]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L103
[30]: https://gist.github.com/pakLebah/277e0875a9ff50b9186fa9e166667add#file-chinook-lpr-L167
[31]: #mengambil-data
[32]: https://github.com/pakLebah/webCRT
