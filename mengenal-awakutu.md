# Mengenal Awakutu

> Seseorang tidak layak disebut pemrogram jika belum menguasai teknik awakutu (*debugging*).    
*~Pak Lebah*

Itu yg saya katakan pada seseorang yg bertanya di grup pemrograman Pascal tentang mengapa program yg dibuatnya tidak bisa bekerja sesuai yg dia harapkan. Padahal pesan kesalahan yg ditampilkan oleh penyunting sudah cukup jelas, tapi dia tidak mampu memahami maksud dari pesan kesalahan tersebut. Dia memang masih belajar pemrograman, tapi ketidak-mampuannya dalam memahami hal-hal yg sederhana dan mendasar seperti itu membuat saya kecewa pada para pembelajar masa kini. Dan pertanyaan seperti itu bukan yg pertama dan saya yakin juga bukan yg terakhir yg akan saya lihat di grup pemrograman (mana pun).

Seperti yg sudah saya jelaskan dalam buku kecil saya tentang [Bekal Belajar Pemrograman][1], pemrogram itu tugasnya adalah berpikir untuk menyelesaikan masalah dengan program komputer. Ada 3 kata kunci di situ, yaitu: *berpikir*, *masalah*, dan *program* (komputer). Pemrogram harus bisa berpikir, tentu berpikir dengan baik sesuai logika yg benar. Dengan kemampuan berpikir, pemrograman harus bisa memahami masalah dengan baik, lalu mencari jalan keluar (solusi) yg terbaik untuk masalah tersebut. Kemudian pemrograman harus bisa menerjemahkan atau mengejawantahkan jalan keluar tersebut menjadi program komputer.

## JENIS KESALAHAN

Maka menjadi seorang pemrogram harus selalu siap menghadapi masalah dan menyelesaikannya. Secara umum, ada 3 jenis kesalahan yg dihadapi pemrogram dalam pembuatan program, yaitu:

### 1. Kesalahan Penulisan

Ini adalah kesalahan yg paling sering terjadi namun paling mudah diatasi. Kesalahan ini terjadi karena pemrogram kurang menguasai cara menyusun program yg benar sesuai bahasa (*syntax error*) atau alat (*build error*) pemrograman yg digunakan. Pemrogram yg kurang menguasai cara menyusun program biasanya karena kurang membaca tata bahasa dan tata kelola alat pemrograman yg digunakan. Pastikan kita sudah membaca panduan penyusunan program dari bahasa atau alat yg kita gunakan.

Kesalahan ini paling mudah diatasi karena kompilator (*compiler*) akan memberikan pesan kesalahan yg cukup jelas. Misalnya kurang titik koma di baris sekian kolom sekian, atau kelebihan tanda kurung di baris sekian kolom sekian, ada variabel `x` yg tidak dikenali, dan lain-lain, yg biasanya dalam bahasa Inggris. Jika pemrogram tidak mampu memahami pesan kesalahan dan memperbaikinya, baik karena tidak paham penulisan program yg benar atau tidak paham bahasa Inggris, sebaiknya dia kembali ke titik nol lagi yaitu belajar dari awal cara menulis program sesuai bahasa pemrograman yg digunakan. Bila perlu sekalian juga belajar bahasa Inggris.

Penyunting modern telah mampu menunjukkan kesalahan penulisan sebelum kompilator bekerja. Misalnya dengan menandai bagian yg salah dengan garis bawah merah bergerigi, seperti dalam aplikasi Microsoft Word. Penyunting modern juga mampu memberikan saran perbaikan untuk kesalahan penulisan yg umum terjadi. Pengguna tinggal setujui saran yg muncul maka penyunting akan memperbaiki kesalahan secara otomatis (*auto-fix*). Fasilitas demikian biasa disebut dengan *[linter][4]*. Gambar di bawah ini adalah contoh fasilitas *linter* yg disediakan oleh ekstensi [OmniPascal][2] di penyunting [VS Code][3].

![](img/omnipascal_linter.png)

### 2. Kesalahan Algoritma

Ini adalah kesalahan akibat ketidak-mampuan pemrogram menerjemahkan solusi menjadi algoritma program yg tepat. Solusi masalah sudah didapat tetapi algoritma program yg disusun tidak sesuai dengan solusi tersebut. Dalam kasus ini, kompilator juga tidak bisa membantu karena bisa jadi penulisan kode programnya sudah benar, algoritmanya saja yg masih salah. Sumber kesalahannya ada di sisi pemrogram maka hanya pemrogram yg bisa memperbaikinya, baik pemrogram aslinya atau pemrogram yg lain.

> **Ingat!** Komputer melakukan apa yg kita perintahkan, bukan melakukan apa yg kita inginkan.

Misalnya, solusinya menyatakan data harus diurutkan dari kecil ke besar, tapi algoritma yg dibuat mengurutkan data dari besar ke kecil. Maka tentu saja hasil kode program tidak sesuai dengan solusi yg diinginkan.

Kesalahan algoritma bisa terjadi secara tidak sengaja atau sengaja. Penyebabnya bisa jadi sepele tapi bisa jadi rumit juga. Kesalahan tidak sengaja misalnya seharusnya ditulis variabel `data1` tapi salah ketik menjadi `data2` atau salah baca menjadi `datal`. Penyebabnya tampak sepele tapi menemukan kesalahan itu dalam kode program belum tentu semudah penyebabnya. Kesalahan yg sengaja misalnya karena belum betul-betul paham solusinya tapi segera membuat program sehingga salah algoritmanya. Kesalahan jenis ini akan lebih sulit memperbaikinya, bahkan kadang kode program harus ditulis ulang lagi dari awal dengan algoritma yg benar.

### 3. Kesalahan Solusi

Ini adalah kesalahan akibat solusi yg diambil kurang tepat untuk menyelesaikan masalah. Tidak ada penyunting atau *linter* yg bisa membantu menyelesaikan masalah ini. Kesalahan ini terjadi bahkan sebelum kode program ditulis, maka solusinya adalah kembali lagi ke proses berpikir dan pencarian solusi masalah yg tepat. Jika solusi yg diambil bukan dari pemrogram (misalnya dari atasan pemrogram) maka harus dikembalikan lagi ke yg menentukan solusi tersebut.

## AWAKUTU


———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/6).  
Thank you. 😊

---
<span style="float: left">← [Home](index.md)</span> <span style="float: right">[Top](#top) ↑</span>

[1]: https://pak.lebah.web.id/ebook/pascal.id_kulgram1.pdf
[2]: https://marketplace.visualstudio.com/items?itemName=Wosi.omnipascal
[3]: https://code.visualstudio.com
[4]: https://en.wikipedia.org/wiki/Lint_programming_tool
