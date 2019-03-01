# Persiapan Belajar Pemrograman

Seperti halnya melakukan apa pun, belajar pemrograman juga perlu persiapan. Seseorang tidak bisa *ujug-ujug* buka aplikasi penyunting, menulis kode program, langsung sukses, dan mendadak jadi aplikasi. Itu mustahil. Namun anehnya, ada saja pemula yg melakukan seperti itu. Dia belum paham bahasa pemrograman yg digunakan, mencomot kode program dari internet (bermodal *google*), ditulis (ditempel atau di-*paste* lebih tepatnya) begitu saja ke penyunting, tanpa paham apa yg ditulisnya, lalu berharap program bekerja. Tentu saja hampir pasti itu gagal.

Dan ketika gagal, dia ribut bertanya di grup pemrograman. Karena dia tidak paham kode program yg didapatnya, tentu saja dia tidak paham apa yg seharusnya dia tanyakan. Bahkan ketika pesan kesalahan yg muncul begitu jelas, dia pun tidak bisa paham. Maka jawaban apa pun atas pertanyaannya, dia juga tidak akan bisa paham. Bagaimana bisa paham jika dia tidak mengerti apa-apa tentang pemrograman? Lalu dia berkesimpulan bahwa pemrograman itu sulit. Padahal penyebab kegagalannya lebih karena dia tidak belajar dengan persiapan yg baik dan benar.

Nah, apa saja persiapan yg harus dilakukan untuk belajar pemrograman? Mari kita ulas satu per satu.

## 1. Pilih Bahasa Pemrograman Untuk Pemula

Ini sudah saya jelaskan di artikel sebelumnya, [Bahasa Pemrograman Untuk Pemula][12]. Bahasa pemrograman yg saya sarankan bagi pemula adalah bahasa Pascal. Tentu bahasa Pascal yg modern, bukan yg kuno.

## 2. Pahami Konsep dan Prinsip Dasar Pemrograman

Ini sudah saya jelaskan panjang lebar di buku kecil saya, [Bekal Belajar Pemrograman][13]. Di buku tersebut saya membahas tentang konsep dan prinsip dasar dalam pemrograman, termasuk pola pikir pemrogram itu sendiri.

## 3. Pelajari Panduan Bahasa Pemrograman

Di grup pemrograman [Pascal Indonesia][1], saya pernah sampaikan, *"Jangan sekali-kali menulis sebaris pun kode program jika belum paham tata cara penulisan bahasa pemrograman (syntax) yg digunakan."* Logikanya, bagaimana mungkin seseorang bisa menulis kode program dengan benar jika cara menulisnya saja belum tahu? Mustahil. Ibaratnya, kita ingin bicara dalam bahasa Inggris tapi kita tidak tahu sedikit pun kosakata dan tata bahasa Inggris. Apa mungkin bisa?

Panduan bahasa pemrograman umumnya berupa buku (cetak). Sebelum mulai menulis program, bacalah terlebih dahulu buku panduan bahasa pemrograman yg digunakan. Tentu bacalah buku yg membahas versi bahasa yg terbaru dan masih digunakan saat ini, jangan versi *jadul* yg sudah tidak dipakai lagi. Misalnya belajar bahasa Pascal, bacalah buku yg membahas [bahasa Pascal modern][2], jangan buku yg membahas bahasa Pascal *jadul* seperti [Turbo Pascal][3].

Namun jaman sekarang, buku panduan tidak harus dalam bentuk buku cetak. Panduan dalam bentuk buku digital (*ebook*) yg tersedia daring justru lebih mudah didapatkan. Bisa juga tersedia dalam bentuk wiki yg dilengkapi dengan fitur pencarian. Berikut beberapa panduan bahasa Pascal yg bisa dipelajari:

<img align="right" src="img/delphi_handbook.jpg">

* Buku kecil panduan [bahasa Pascal dengan Free Pascal][20].
* Buku [*Essential Pascal*][6] oleh Marco Cantù.
* Buku [*Object Pascal Handbook*][7] oleh Marco Cantù.
* Panduan daring [bahasa Pascal dari tutorialspoint.com][18]
* Panduan daring [bahasa Pascal dari pp4s.co.uk][19]

Berikut adalah daftar referensi (acuan) bahasa Pascal:
* Dokumen bahasa [Free Pascal][4].
* Dokumen wiki [Free Pascal dan Lazarus IDE][5].
* Dokumen wiki [Delphi][8] dari Embarcadero.

> **Catatan**: Free Pascal dan Delphi adalah sama-sama dialek bahasa (*Object*) Pascal modern dengan tingkat kompatibilitas yg tinggi (lebih dari 90%). Bagi pemula keduanya bisa dibilang sama saja. Buku panduan Delphi bisa digunakan di Free Pascal, dan sebaliknya. Perbedaan keduanya baru muncul pada kemampuan bahasa Pascal tingkat menengah ke atas.

Semua panduan di atas ditulis dalam bahasa Inggris. Jika bahasa Inggris masih menjadi kendala, silakan belajar bahasa Inggris terlebih dahulu. Pemrograman adalah ilmu yg berasal dari negeri yg berbahasa Inggris, jika ingin paham ilmunya maka harus paham bahasanya. Walaupun tersedia buku cetak dalam bahasa Indonesia, umumnya isi buku sudah cukup jauh tertinggal sehingga pemula tidak bisa menikmati fitur-fitur bahasa terbaru yg lebih canggih.

## 4. Pasang Aplikasi Penyunting atau IDE

Menulis kode program tentu butuh aplikasi penyunting (*editor*), tapi bukan penyunting biasa seperti aplikasi Notepad. Gunakanlah aplikasi penyunting khusus pemrograman yg menyediakan fitur-fitur yg membantu dan memudahkan dalam menulis kode program, atau biasa disebut IDE (*integrated development environment* atau lingkungan pengembangan terpadu). Dan yg terpenting adalah harus menyediakan fitur dan alat bantu untuk [awakutu][9]. Fitur awakutu **sangat penting** bagi pemula. Pemula harus menghindari penyunting yg tidak menyediakan alat awakutu.

> *"Seseorang tidak layak disebut pemrogram jika belum menguasai teknik awakutu (debugging)."*    
> *~Pak Lebah*

Untuk pengguna Free Pascal, hindari penyunting teks (*console*) bawaan Free Pascal. Sekarang sudah abad 21, gunakanlah penyunting grafis (GUI atau *graphical user interface*). Penyunting teks bawaan Free Pascal lebih ditujukan untuk pemrogram yg sudah pintar di lingkungan teks (CLI atau *command line interface*) dan fitur yg disediakan sangat terbatas sehingga sangat tidak cocok bagi pemula. Saya sarankan gunakan [Lazarus IDE][10] (untuk Free Pascal) atau [Delphi][14] yg memiliki banyak fitur canggih. Atau minimal, gunakanlah [Free Pascal dengan Visual Studio Code][11].

[![Delphi demo video.](img/delphi_rio_thumb.png)](https://player.vimeo.com/video/300656745)

## 5. Mulai Belajar Membuat Program

Pemrograman selain merupakan ilmu, juga menerupakan keahlian (*skill*). Yg namanya keahlian harus dipraktekkan secara terus-menerus untuk menjaga, mengasah, dan meningkatkan kemampuan yg dimiliki. Membaca buku saja –sebanyak apa pun buku yg dibaca– namun tanpa praktek sama sekali, tidak akan membuat pemula menjadi pemrogram yg ahli. Sama seperti belajar berenang, membaca selemari buku teknik berenang namun tidak pernah masuk ke kolam renang, tidak akan membuat pembacanya mendadak jadi perenang yg andal. Demikian pula pemrograman.

Setelah buku dibaca dan penyunting terpasang, selanjutnya adalah mulai membuat program. Paling mudah adalah mengikuti panduan dari buku yg dipelajari. Salah satu kiat sederhana agar lebih cepat memahami bahasa pemrograman adalah tidak melakukan salin-tempel (*copy-paste*) kode program dari internet atau buku (jika disertakan berkas kode programnya). Sebaiknya ketik ulang saja setiap program yg ingin dicoba. Selain membuat lebih paham bahasanya, ketik ulang juga akan membuat pemula menjadi terbiasa dengan penyunting yg digunakan berikut fitur-fiturnya.

Satu hal yg penting diingat adalah belajarlah hingga tuntas, berdasarkan buku panduan yg digunakan. Ikuti dan pahami contoh program yg tersedia sejak yg paling awal hingga yg paling akhir. Jangan belajar bahasa pemrograman setengah-setengah lalu beralih ke bahasa pemrograman yg lain karena bisa jadi akan membingungkan dan justru makin menyulitkan pemahaman. Saya sarankan untuk ikuti dua buku panduan karya Marco Cantù di atas, mulai dari *Essential Pascal* lalu lanjut ke *Object Pascal Handbook*.

## 6. Luangkan Waktu Untuk Berlatih Secara Rutin

Kembali ke analogi berenang, apakah dengan berlatih renang hanya 1-2 kali akan membuat jadi perenang andal? Tentu tidak. Pemrogram yg sudah jago pun akan menurun keahliannya jika lama tidak membuat program. Apalagi pemula, harus selalu luangkan waktu secara rutin untuk membangun kemampuannya. Saran saya minimal berlatih seminggu sekali, misalnya sehari di akhir pekan digunakan khusus untuk berlatih pemrograman. Jika seorang pemula betul-betul ingin menjadi pemrogram yg andal, maka jadwalkan latihan rutin dan berlatihlah secara disiplin.

Berlatih membuat program apa? Apa saja. Pokoknya buatlah program dengan bahasa yg sedang dipelajari. Namun yg namanya pemula tentu tidak harus bikin program yg muluk-muluk dan rumit. Mulai dari yg sederhana saja dulu, disesuaikan dengan tingkat kemampuan yg sudah dipelajari. Supaya berlatihnya tidak membosankan, ada beberapa materi yg cocok untuk latihan pemula, yaitu:

![Bola pantul](https://gist.githubusercontent.com/pakLebah/1748ea96b95ccbe5c21bf5b22b84e0a6/raw/a39be5604039621584ee71ff2ce590dc0063af88/z_ubounce.gif)

* **Olah matematika.** Berlatih matematika penting untuk mengasah kemampuan logika numerik pemrogram. Bisa dimulai dengan menyelesaikan soal-soal di situs [Project Euler][15], mulailah dari soal-soal yg mudah.

* **Olah grafis sederhana.** Berlatih grafis penting untuk mengasah kemampuan logika visual pemrogram. Bisa dimulai dengan membuat fraktal, penampil persamaan matematika, animasi partikel (seperti video di atas), membuat gambar dengan program, dsb. Bisa dilengkapi dengan interaksi baik papan ketik atau tetikus. Yg kreatiflah.

<img align="right" src="https://raw.githubusercontent.com/git-bee/gaple/master/gaple.gif">

* **Membuat *game* sederhana.** Berlatih membuat *game* penting untuk mengasah kemampuan membangun aplikasi yg terpadu sebab *game* melibatkan hampir seluruh kemampuan pemrograman, mulai dari matematika, visual, interaksi, antarmuka, olah data, dan memadukan semuanya menjadi sebuah permainan yg menarik. Mulailah dari *game* yg sederhana, misalnya Tic Tac Toe, atau Dakon, atau Silang Pentol, atau [Gaple][16], dan sebagainya.

* **Bermain *game* dengan program.** Siapa bilang belajar pemrograman tidak bisa dengan *game*? Bayangkan anda bermain perang-perangan di luar angkasa dengan pesawat luar angkasa, tapi... pesawatnya tidak dikendalikan dengan tombol atau tetikus, melainkan dengan kode program. Menarik bukan? Silakan mencobanya di [CodinGame][17].

## 7. Bergabung dengan Komunitas Pemrograman

Nah, apakah anda juga seorang pemula atau berniat belajar pemrograman? Anda boleh ikuti saran-saran saya di atas. Dan saya tunggu karya anda di grup [Pascal Indonesia][1]. Selamat belajar!

———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/8).  
Thank you. 😊

---
<span style="float: left">← [Home](index.md)</span> <span style="float: right">[Top](#top) ↑</span>

[1]: https://www.facebook.com/groups/pascal.id/
[2]: https://pak.lebah.web.id/pascal5.html
[3]: https://pak.lebah.web.id/saynototp.html
[4]: https://freepascal.org/docs.html
[5]: http://wiki.freepascal.org
[6]: http://www.marcocantu.com/epascal/
[7]: http://forms.embarcadero.com/sDownloadMarcoseBook
[8]: http://docwiki.embarcadero.com/RADStudio/Rio/en/Main_Page
[9]: https://paklebah.github.io/mengenal-awakutu.html
[10]: https://www.lazarus-ide.org/
[11]: https://paklebah.github.io/fpc-dan-vscode.html
[12]: https://paklebah.github.io/bahasa-pemrograman-pemula.html
[13]: https://pak.lebah.web.id/ebook/pascal.id_kulgram1.pdf
[14]: https://www.embarcadero.com/products/delphi
[15]: https://projecteuler.net/archives
[16]: https://github.com/git-bee/gaple
[17]: https://www.codingame.com/
[18]: https://www.tutorialspoint.com/pascal/
[19]: http://pp4s.co.uk/main/tutorials.html
[20]: https://pak.lebah.web.id/ebook/bahasa-pascal.pdf
