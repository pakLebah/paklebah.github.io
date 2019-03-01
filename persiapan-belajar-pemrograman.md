# Persiapan Belajar Pemrograman

Seperti halnya melakukan apa pun, belajar pemrograman juga perlu persiapan. Seseorang tidak bisa *ujug-ujug* buka aplikasi penyunting, menulis kode program, langsung sukses, dan mendadak jadi aplikasi. Itu mustahil. Namun anehnya, ada saja pemula yg melakukan seperti itu. Dia belum paham bahasa pemrograman yg digunakan, mencomot kode program dari internet (bermodal *google*), ditulis (ditempel atau di-*paste* lebih tepatnya) begitu saja ke penyunting, tanpa paham apa yg ditulisnya, lalu berharap program bekerja. Tentu saja hampir pasti itu gagal.

Dan ketika gagal, dia ribut bertanya di grup pemrograman. Karena dia tidak paham kode program yg didapatnya, tentu saja dia tidak paham apa yg seharusnya dia tanyakan. Bahkan ketika pesan kesalahan yg muncul begitu jelas, dia pun tidak bisa paham. Maka jawaban apa pun atas pertanyaannya, dia juga tidak akan bisa paham. Bagaimana bisa paham jika dia tidak mengerti apa-apa tentang pemrograman? Lalu dia berkesimpulan bahwa pemrograman itu sulit. Padahal penyebab kegagalannya lebih karena dia tidak belajar dengan persiapan yg baik dan benar.

Nah, apa saja persiapan yg harus dilakukan untuk belajar pemrograman? Mari kita ulas satu per satu.

## 1. Pilih Bahasa Pemrograman Untuk Pemula

Ini sudah saya jelaskan di artikel sebelumnya, [Bahasa Pemrograman Untuk Pemula][12]. Bahasa pemrograman yg saya sarankan bagi pemula adalah bahasa Pascal. Tentu bahasa Pascal yg modern, bukan yg kuno.

## 2. Pahami Konsep dan Prinsip Dasar Pemrograman

Ini sudah saya jelaskan panjang lebar di buku kecil saya, [Bekal Belajar Pemrograman][13]. Di buku tersebut saya membahas tentang konsep dan prinsip dasar dalam pemrograman, termasuk pola pikir pemrogram itu sendiri.

## 3. Baca Panduan Bahasa Pemrograman

Di grup pemrograman [Pascal Indonesia][1], saya pernah sampaikan, *"Jangan sekali-kali menulis sebaris pun kode program jika belum paham tata cara penulisan bahasa pemrograman (syntax) yg digunakan."* Logikanya, bagaimana mungkin seseorang bisa menulis kode program dengan benar jika cara menulisnya saja belum tahu? Mustahil. Ibaratnya, kita ingin bicara dalam bahasa Inggris tapi kita tidak tahu sedikit pun kosakata dan tata bahasa Inggris. Apa mungkin bisa?

Panduan bahasa pemrograman umumnya berupa buku (cetak). Sebelum mulai menulis program, bacalah terlebih dahulu buku panduan bahasa pemrograman yg digunakan. Tentu bacalah buku yg membahas versi bahasa yg terbaru dan masih digunakan saat ini, jangan versi *jadul* yg sudah tidak dipakai lagi. Misalnya jika belajar bahasa Pascal maka bacalah buku yg membahas [bahasa Pascal modern][2], jangan buku yg membahas bahasa *jadul* seperti [Turbo Pascal][3].

<img align="left" style="margin: 10px 10px 10px 0" src="img/delphi_handbook.jpg">

Namun jaman sekarang, buku panduan tidak harus dalam bentuk buku cetak. Panduan dalam bentuk buku digital (*ebook*) yg tersedia daring justru lebih mudah didapatkan. Bisa juga tersedia dalam bentuk wiki yg dilengkapi dengan fitur pencarian. Berikut beberapa panduan bahasa Pascal yg bisa dipelajari:

• Buku [*Essential Pascal*][6] oleh Marco Cantù.    
• Buku [*Object Pascal Handbook*][7] oleh Marco Cantù.    
• Dokumen panduan resmi [Free Pascal][4].    
• Dokumen wiki [Free Pascal dan Lazarus IDE][5].    
• Dokumen wiki [Delphi][8] dari Embarcadero.

> **Catatan**: Free Pascal dan Delphi adalah sama-sama dialek bahasa (*Object*) Pascal modern dengan tingkat kompatibilitas yg tinggi (lebih dari 90%). Bagi pemula keduanya bisa dibilang sama saja. Buku panduan Delphi bisa digunakan di Free Pascal, dan sebaliknya. Perbedaan keduanya baru muncul pada kemampuan bahasa Pascal tingkat menengah ke atas.

Jika bahasa Inggris jadi kendala, silakan belajar bahasa Inggris dulu. Pemrograman adalah ilmu yg berasal dari negeri yg berbahasa Inggris, jika ingin paham ilmunya maka harus paham bahasanya.

## 4. Pasang Aplikasi Penyunting atau IDE

Menulis kode program tentu butuh aplikasi penyunting (*editor*), tapi bukan penyunting biasa seperti aplikasi Notepad. Gunakanlah aplikasi penyunting khusus pemrograman yg menyediakan fitur-fitur yg membantu dan memudahkan dalam menulis kode program, atau biasa disebut IDE (*integrated development environment* atau lingkungan pengembangan terpadu). Dan yg terpenting adalah harus menyediakan fitur dan alat bantu untuk [awakutu][9]. Fitur awakutu **sangat penting** bagi pemula. Pemula harus menghindari penyunting yg tidak menyediakan alat awakutu.

Untuk pengguna Free Pascal, hindari penyunting teks (*console*) bawaan Free Pascal. Sekarang sudah abad 21, gunakanlah penyunting grafis (GUI atau *graphical user interface*). Penyunting teks bawaan Free Pascal lebih ditujukan untuk pemrogram yg sudah pintar di lingkungan teks (CLI atau *command line interface*) dan fitur yg disediakan sangat terbatas sehingga sangat tidak cocok bagi pemula. Saya sarankan gunakan [Lazarus IDE][10] (untuk Free Pascal) atau [Delphi][14] yg memiliki banyak fitur canggih. Atau minimal, gunakanlah [Free Pascal dengan Visual Studio Code][11].

[![Delphi demo video.](img/delphi_rio_thumb.png)](https://player.vimeo.com/video/300656745)

———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/7).  
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
