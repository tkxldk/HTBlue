# Bumblebee

![image](https://github.com/tkxldk/HTBlue/assets/89120989/c4311f80-cf1f-4fd8-94da-f87067508d60)

## POC

![image](https://github.com/tkxldk/HTBlue/assets/89120989/77b41d99-b8c0-4c68-a296-251cc31a84f3)

1. Dari zip didapatkan 2 file, yakni access.log dan phpbb.sqlite3


2. Untuk soal pertama diminta "What was the username of the external contractor?", jawabannya dapat kita lihat dengan membuka file database yang diberikan.

`SELECT name FROM sqlite_master WHERE type='table'`

Setelah itu akan muncul daftar tabel yang ada pada database tersebut dan disana ada nama tabel phpbb_users yang menarik perhatian saya.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/f61abe91-74bc-4cd7-b36b-ec8c6c52f468)

`SELECT * FROM phpbb_users`

Lalu gunakan query di atas untuk menampilakan semua isi dari tabel tersebut dan ketika discroll ke bawah didapatkan nama `apoole1` yang sesuai dengan hint.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/7e6ce311-81e5-41e4-a278-981b5220de72)

3. Lanjut ke soal nomor 2 "What IP address did the contractor use to create their account?", jawabannya dapat dilihat di gambar sebelumnya

![image](https://github.com/tkxldk/HTBlue/assets/89120989/63fe4828-cb99-4dfd-9f34-cfd74db4f683)

4. Ok, soal nomor 3 "What is the post_id of the malicious post that the contractor made?", untuk menjawabnya kita perlu menggunakan query yang pertama untuk melihat keseluruhan tabelnya. Dan saya menemukan terdapat tabel bernama phpbb_posts dan di dalamnya terdapat 3 baris dan salah satunya terdapat sebuah HTML code yang di dalamnya tertuliskan javascript yang kemungkinan besar malicious.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/88363eba-127a-434d-8ad7-55d6e2db49bb)

5. Selanjutnya nomor 4 "What is the full URI that the credential stealer sends its data to?", 
