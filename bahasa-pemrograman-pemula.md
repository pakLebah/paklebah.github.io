# Bahasa Pemrograman Untuk Pemula

Saya sering mendapat pertanyaan dari orang yg berniat belajar pemrograman atau ingin menjadi pemrogram tentang bahasa pemrograman apa yg paling cocok dipelajari oleh seorang pemula. Umumnya pemrogram profesional akan menyarankan untuk memilih bahasa yg sedang banyak digunakan dengan alasan supaya nanti lebih mudah mencari kerja dengan modal keahlian bahasa yg sedang laku di pasar kerja. Atau bisa jadi juga seorang pemrogram senior akan menyarankan untuk memilih bahasa yg dikuasainya dengan alasan supaya nanti dia lebih mudah membantu si penanya dalam belajar.

Kedua saran di atas tentu sah-sah saja dan alasannya pun bisa diterima. Tetapi saya kurang sepakat dengan saran yg demikian. Seorang pemula itu belum menjadi pemrogram alias masih mau akan menjadi pemrogram sehingga bisa dikatakan dia belum paham apa-apa tentang pemrograman. Maka, menurut saya, yg lebih baik adalah menyarankan bahasa pemrograman yg membantu atau memudahkan pemula dalam memahami berbagai prinsip dan konsep pemrograman secara umum. Yg penting bukan bahasanya, tetapi bagaimana bahasa yg digunakan bisa lebih mudah dipelajari dan dipahami oleh pemula.

Tidak ada bahasa pemrograman yg betul-betul terbaik. Setiap bahasa pemrograman memiliki kelebihan dan kekurangan masing-masing. Pemrogram memilih bahasa pemrogramannya lebih karena faktor kebutuhan atau kecocokan yg subyektif. Walaupun secara kemampuan bisa dibilang semua bahasa pemrograman itu setara, tetapi tidak semua bahasa pemrograman itu sama. Ada bahasa yg rumit dan sulit dipahami, namun ada pula bahasa yg sederhana dan mudah dipahami sehingga cocok bagi para pemula. Bahasa pemrograman yg disarankan bagi pemula sebaiknya yg memiliki sifat bahasa sebagai berikut:

### 1. Kosakatanya mendekati bahasa manusia (dalam hal ini bahasa Inggris).

Hal utama yg perlu dipahami dalam pemrograman adalah konsep-konsep dan prinsip-prinsip dasar pemrograman. Bahasa pemrograman yg kosakatanya rumit dengan simbol-simbol dan aksesoris yg tampak "aneh" (bagi pemula) membuat pemula harus berpikir lebih keras untuk memahaminya dibandingkan dengan bahasa pemrograman yg tata bahasanya mirip bahasa manusia. Perhatikan contoh berikut:

"Hello World" dengan bahasa C++:
```c++
#include <iostream>
using namespace std;

int main() 
{
    cout << "Hello World!";
    return 0;
}
```

"Hello World" dengan bahasa Python:
```python
print "Hello World"
```

Jika anda belum pernah menulis atau membaca kode program, menurut anda contoh kode program mana yg lebih mudah dipahami, bahasa C++ atau Python? Tentu dengan asumsi anda paham bahasa Inggris.

### 2. Memiliki sistem tipe data yg statis atau tetap.

Tipe data dalam bahasa pemrograman itu seperti satuan dalam matematika. Dua hal yg berbeda satuannya, tidak bisa dioperasikan langsung, harus dikonversi lebih dahulu. Contoh, `1 cm + 1 m` tidak bisa dihitung langsung, salah satu satuannya harus dikonversi ke satuan yg lain, baru bisa dioperasikan. Semua yg pernah belajar matematika tingkat SD tentu paham. Bahasa pemrograman yg menerapkan prinsip yg sama akan lebih mudah dipahami pemula. Perhatikan contoh berikut:

Operasi penjumlahan di bahasa JavaScript:    
- Perintah `"3" + 4 + 5` (huruf "3" ditambah angka 4 ditambah angka 5) menghasilkan teks `"345"` di mana `4` dan `5` dianggap huruf sehingga keduanya disambungkan, bukan dijumlahkan.
- Tetapi perintah `3 + 4 + "5"` (angka 3 ditambah angka 4 ditambah huruf "5") menghasilkan teks `"75"` di mana `3` dan `4` dianggap angka sehingga keduanya dijumlahkan, bukan disambungkan.

Perilaku operator `+` di JavaScript tidak konsisten, namun tidak ada pesan kesalahan apa pun. JavaScript memiliki aturannya sendiri untuk operator `+` yg berbeda dengan prinsip matematika yg sudah jadi aksioma (kebenaran umum).

Operasi penjumlahan di bahasa Kotlin:    
Perintah `"3" + 4 + 5` menghasilkan pesan kesalahan yg menyatakan *"operator `+` tidak bisa bekerja pada tipe data yg berbeda"* yg artinya huruf dan angka tidak bisa dijumlahkan. Pesan yg mudah dipahami dan masuk akal. Perintah yg benar adalah salah satu dari berikut:
- Mengubah huruf menjadi angka sehingga bisa dijumlahkan dengan perintah `"3".toInt() + 4 + 5` (huruf "3" diubah jadi angka 3 dengan perintah `toInt()` lalu dijumlahkan dengan angka 4 dan angka 5) yg menghasilkan angka `12`. 
- Mengubah angka menjadi huruf sehingga bisa disambungkan dengan perintah `"3" + 4.toString() + 5.toString()` (huruf "3" disambung dengan angka 4 yg diubah jadi huruf "4" dengan perintah `toString()` lalu disambung dengan angka 5 yg diubah jadi huruf "5") menghasilkan teks `"345"`.

Perilaku operator `+` di Kotlin konsisten dan sesuai dengan prinsip matematika sehingga pembelajar tidak perlu memahami kebenaran baru yg bersifat khusus serta bertentangan dengan kebenaran yg telah umum diterima.

### 3. Bahasa yg bisa dipelajari secara bertahap.

Pemula yg belajar pemrograman dari awal tentu tidak perlu dibuat bingung dengan berbagai hal yg memang belum waktunya dipelajari, apalagi direpotkan dengan jargon-jargon pemrograman yg sedang *hype*, yg kadang istilahnya saja susah dipahami. Belajar yg mudah, nyaman, dan menyenangkan adalah belajar secara bertahap dari yg sederhana menuju ke rumit sesuai dengan perkembangan pemahaman si pembelajar. Perhatikan contoh berikut:

Kode program perulangan dalam bahasa Java:
```java
class Loop {
    public static void main(String[] args) {
        for (int i = 1; i <= 10; ++i) {
            System.out.println("i = " + i);
        }
    }
}
```

Pemula yg baru saja belajar perulangan dengan perintah `for` dalam bahasa Java, mau tidak mau harus menulis lengkap baris kode program di atas walaupun dia tidak paham apa itu `class`, `public`, dan `static` yg merupakan bagian dari konsep OOP (*object oriented programming*) yg belum dipelajarinya. Pokoknya ditulis aja dulu, pahamnya nanti saja.

Kode program perulangan dalam bahasa PHP:
```php
<?php 
  for ($i = 0; $i <= 10; $i++) {
      echo "The number is: $i <br>";
  } 
?>
```

Berbeda dengan pemula yg baru saja belajar perulangan dengan perintah `for` dalam bahasa PHP. Dia hanya perlu menuliskan kode program yg memang relevan dengan apa yg sudah dan sedang dipelajarinya. Tidak ada kode-kode yg "asing" yg harus ditulis tapi tidak dipahami. Pemula PHP tidak punya "beban kode" dalam proses belajar.

### 4. Tata bahasanya melatih kedisiplinan.

Karena belum terbiasa menulis kode program yg panjang dan rumit, pemula biasanya kurang disiplin dan kurang teliti. Contoh yg paling umum adalah bikin variabel di mana-mana, kadang dengan nama yg sama (baik sengaja atau tidak). Ketika program tidak bekerja sesuai dengan yg diharapkan karena ada kesalahan lingkup (*scope*), lalu bingung sendiri mencari salahnya di mana. Ada beberapa bahasa yg menerapkan tata deklarasi yg lebih ketat dan disiplin, contohnya adalah bahasa Pascal. Perhatikan contoh berikut:

```pascal
program Loop;

var
  i: integer;

begin
  for i := 1 to 100 do
  begin
    if i mod 3 = 0 then
      writeln('Fizz')
    else if i mod 5 = 0 then
      writeln('Buzz')
    else if (i mod 3 = 0) and (i mod 5 = 0) then
      writeln('FizzBuzz')
    else
      writeln(i);
  end;
end.
```

Bagi pemrogram yg terbiasa dengan bahasa C++ misalnya, kode program bahasa Pascal di atas terkesan bertele-tele (*verbose*). Tapi bagi pemula, tata bahasa Pascal di atas memaksa untuk disiplin dalam penulisan kode program. Dari baris pertama sudah jelas bahwa berkas ini berisi program utama bernama `Loop`, ada blok deklarasi variabel dengan penanda `var`, blok kumpulan perintah ada dalam pasangan penanda `begin`...`end;`, serta program utama ada dalam pasangan penanda `begin`...`end`.

Bahkan bagi orang yg belum pernah menulis program komputer, contoh kode program dengan bahasa Pascal di atas lebih mudah dimengerti daripada contoh kode program dengan bahasa lainnya di atas. Itulah sebabnya saya katakan, menulis kode program dalam bahasa Pascal itu seperti menulis puisi.

> *"I'm not writing computer program, I'm writing digital poetry."*    
> *~Mr Bee*

### 5. Alat bantunya tersedia di mana saja.

Belajar pemrograman tidak hanya memahami bahasa saja, tetapi juga harus bisa menggunakan alat bantu pemrograman. Bahasa pemrograman tidak bisa jadi aplikasi tanpa alat bantu pemrograman. Alat bantu pemrograman antara lain *compiler* atau *interpreter* untuk mengubah kode program menjadi kode komputer, penyunting atau *editor* atau IDE (*integrated development environment*) untuk menulis kode program dengan berbagai fasilitas yg memudahkan, alat [awakutu][1] atau *debugger* untuk penelusuran kode program, dan *linker* untuk merangkai berbagai kode program menjadi aplikasi siap pakai.

Alat bantu pemrograman adalah aplikasi komputer juga. Namun tidak semua alat bantu pemrograman tersedia di berbagai jenis komputer, baik secara sistem operasi maupun sistem arsitektur komputer. Memilih bahasa pemrograman untuk belajar sebaiknya yg alat bantunya tersedia di berbagai jenis komputer, paling tidak di sistem komputer yg digunakan. Contoh, jika anda pengguna sistem operasi Windows maka hindari memilih bahasa Swift karena tidak tersedia alat bantu pemrograman Swift di Windows. Alat bantu pemrograman bahasa Swift hanya tersedia secara lengkap di sistem operasi MacOS saja.

### 6. Tersedia banyak sumber pembelajaran.

Belajar bahasa pemrograman –atau bahkan belajar apa pun di jaman sekarang– tentu perlu adanya dukungan sumber-sumber pembelajaran yg membantu proses belajar. Misalnya buku (terutama yg berbahasa Indonesia), berbagai contoh program, artikel tutorial, panduan video, forum tanya-jawab, orang-orang yg ahli, pelatihan atau kursus, materi pelajaran di sekolah atau kampus, dan sebagainya. Semakin banyak sumber pembelajaran, pemula semakin terbantu dalam belajar.

Bahasa pemrograman yg terkenal dan banyak digunakan biasanya memiliki sumber-sumber pembelajaran yg banyak pula. Contohnya JavaScript yg sekarang sedang jadi bahasa paling populer di industri perangkat lunak. Tetapi bahasa lama yg dulu pernah terkenal dan pernah banyak digunakan biasanya juga memiliki sumber-sumber pembelajaran yg banyak karena sejatinya bahasa lama tidak pernah benar-benar mati, apalagi bahasa lama yg masih digunakan secara profesional dan diajarkan di sekolah dan kampus. Misalnya seperti bahasa C, bahasa Perl, bahasa Pascal, dan lain-lain.

### 7. Mempunyai komunitas pemrogram yg besar.

Satu hal penting yg sangat membantu pemula dalam belajar adalah komunitas pemrogram yg besar (hingga ribuan anggota) dan aktif. Tidak seperti buku atau tutorial sebagai sumber pembelajaran yg searah dan pasif, komunitas adalah sumber pembelajaran multi-arah dan aktif. Banyak hal bermanfaat yg bisa kita ambil dari komunitas **dan** banyak hal berguna yg bisa kita sumbangkan ke komunitas. Dalam komunitas yg baik, biasanya terbangun interaksi yg menyenangkan antar anggota komunitas.

Dari komunitas, semua anggota bisa saling berbagi manfaat yg seringkali tidak bisa didapatkan dari sumber pembelajaran yg lain. Misalnya membangun relasi dengan orang-orang tertentu (terkait karir), mendapatkan pelajaran berharga dari pengalaman orang lain, memperoleh pengetahuan-pengetahuan non-teknis yg penting, seperti lowongan kerja, tawaran kerjasama, dan lain sebagainya. Sebuah komunitas yg baik adalah yg sebagian besar anggotanya aktif berkontribusi.

## Apa Bahasa Pemrograman yg Paling Cocok Bagi Pemula?

![SAY NO TO TURBO PASCAL!](https://pak.lebah.web.id/img/no_tp.gif)

Menurut saya, jawaban untuk pertanyaan di atas adalah **bahasa Pascal**. Namun bahasa Pascal yg saya maksud **bukan** Turbo Pascal. Saya justru [menentang penggunaan Turbo Pascal][3] di jaman modern ini. Bahasa Pascal yg saya maksud adalah [bahasa (Object) Pascal yg modern][2]. Mari kita uji jawaban saya berdasarkan 7 sifat bahasa yg telah saya sebutkan di atas.

1. Kosakatanya mendekati bahasa manusia? ✔︎ Terpenuhi.    
2. Memiliki sistem tipe data yg statis? ✔︎ Terpenuhi.    
3. Bahasa yg bisa dipelajari secara bertahap? ✔︎ Terpenuhi.
4. Tata bahasanya melatih kedisiplinan? ✔︎ Terpenuhi.
5. Alat bantunya tersedia di mana saja? ✔︎ Terpenuhi.
6. Tersedia banyak sumber pembelajaran? ✔︎ Terpenuhi.
7. Mempunyai komunitas pemrogram yg besar? ✔︎ Terpenuhi.

Jelas bahasa Pascal bisa memenuhi semua sifat bahasa yg cocok bagi pemula. Bisa jadi itu sebabnya bahasa Pascal masih diajarkan di sekolah dan kampus di berbagai belahan dunia hingga hari ini, khususnya di kawasan Asia dan Eropa Timur, termasuk di Indonesia. Para akademisi di kawasan tersebut tentu memahami berbagai kelebihan bahasa Pascal sehingga memutuskan Pascal tetap diajarkan di jalur pendidikan formal.

Pokok dari ilmu pemrograman adalah algoritma, bukan bahasanya. Algoritma yg sama bisa diterapkan di berbagai bahasa yg berbeda. Konsep dan prinsip pemrograman pun sama saja walaupun penerapannya berbeda di berbagai bahasa. Jika seorang pemrogram telah memahami konsep dan prinsip pemrograman serta menguasai satu bahasa pemrograman dengan baik, maka belajar bahasa kedua akan lebih mudah daripada saat belajar bahasa pertama (saat masih pemula). Dengan demikian, pemula tidak perlu khawatir untuk memulai belajar pemrograman dari bahasa yg cocok bagi pemula walaupun mungkin bahasa tersebut kurang populer di dunia kerja.

———  
💬 I welcome your comment [here](https://github.com/pakLebah/paklebah.github.io/issues/7).  
Thank you. 😊

---
<span style="float: left">← [Home](index.md)</span> <span style="float: right">[Top](#top) ↑</span>

[1]: https://paklebah.github.io/mengenal-awakutu.html
[2]: https://pak.lebah.web.id/pascal5.html
[3]: https://pak.lebah.web.id/saynototp.html
