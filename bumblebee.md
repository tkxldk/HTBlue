# Bumblebee

![image](https://github.com/tkxldk/HTBlue/assets/89120989/c4311f80-cf1f-4fd8-94da-f87067508d60)

## POC

![image](https://github.com/tkxldk/HTBlue/assets/89120989/77b41d99-b8c0-4c68-a296-251cc31a84f3)

1. Dari zip didapatkan 2 file, yakni access.log dan phpbb.sqlite3


> Soal 1 -> apoole1
2. "What was the username of the external contractor?", jawabannya dapat kita lihat dengan membuka file database yang diberikan.

`SELECT name FROM sqlite_master WHERE type='table'`

Setelah itu akan muncul daftar tabel yang ada pada database tersebut dan disana ada nama tabel phpbb_users yang menarik perhatian saya.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/f61abe91-74bc-4cd7-b36b-ec8c6c52f468)

`SELECT * FROM phpbb_users`

Lalu gunakan query di atas untuk menampilakan semua isi dari tabel tersebut dan ketika discroll ke bawah didapatkan nama `apoole1` yang sesuai dengan hint.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/7e6ce311-81e5-41e4-a278-981b5220de72)


> Soal 2 -> 10.10.0.78
3. "What IP address did the contractor use to create their account?", jawabannya dapat dilihat di gambar sebelumnya

![image](https://github.com/tkxldk/HTBlue/assets/89120989/63fe4828-cb99-4dfd-9f34-cfd74db4f683)


> Soal 3 -> 9
4. "What is the post_id of the malicious post that the contractor made?", untuk menjawabnya kita perlu menggunakan query yang pertama untuk melihat keseluruhan tabelnya. Dan saya menemukan terdapat tabel bernama phpbb_posts dan di dalamnya terdapat 3 baris dan salah satu post_textnya terdapat sebuah HTML code yang di dalamnya tertuliskan javascript yang kemungkinan besar meruapkan malicious code.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/88363eba-127a-434d-8ad7-55d6e2db49bb)

![image](https://github.com/tkxldk/HTBlue/assets/89120989/18b5efe6-196a-4b6a-a03a-e2c549d450d6)


> Soal 4 -> 10.10.0.78
5. "What is the full URI that the credential stealer sends its data to?", pada post_text yang sebelumnya didapatkan saya menemukan adanya IP address

![image](https://github.com/tkxldk/HTBlue/assets/89120989/c6633aa4-1e2e-46ac-9bb8-9e09378edacc)

Disini saya memperkirakan ketika user login, maka login form tersebut akan muncul dan disubmit ke IP tersebut (10.10.0.78).


> Soal 5 -> 26/04/2023 10:53:12
6. "When did the contractor log into the forum as the administrator? (UTC)", untuk mendapatkannya kita perlu menganalisis access log dan didapatkan database bernama phpbb_log yang berisikan successful login attempt untuk administrator, namun terdapat IP yang berbeda dengan yang lainnya. IP tersebut merupakan IP yang diperkirakan malicious.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/e13916e7-b147-489d-8d18-b45d17e0bc7a)

7. Karena sudah didapatkan log_time, maka kita hanya harus mengubahnya menjadi jam yang kita mengerti menggunakan online tools (https://www.epochconverter.com/). Jam yang kita gunakan adalah GMT, sehingga kita menggunakan Wednesday, April 26, 2023 10:53:12 AM.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/3a9405d7-f52e-4cda-9313-f15982542eb5)


> Soal 6 -> Passw0rd1
8. "In the forum there are plaintext credentials for the LDAP connection, what is the password?", awalnya saya mencoba untuk memasukkan query pada databasenya untuk menemukan "%ldap%", namun dikarenakan keterbatasan skill, saya melakukan strings secara langsung pada databasenya dan mencari ldap.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/b3495ab8-fca4-4f60-af84-67011d9151c3)


> Soal 7 -> Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36
9. "What is the user agent of the Administrator user?", untuk mendapatkan jawabannya, kita dapat melihat pada file access.log dan memastikan IP yang digunakan

![image](https://github.com/tkxldk/HTBlue/assets/89120989/2a414262-4961-47fc-b417-b6c377246f18)


> Soal 8 -> 26/04/2023 10:53:51
10. "What time did the contractor add themselves to the Administrator group? (UTC)", kita dapat melihat kembali ke phpbb_log, disana terdapat log yang dimana user ditambahkan. Menggunakan langkah yang sama dengan sebelumnya juga, ubah jamnya menjadi jam yang kita pahami, sehingga menjadi Wednesday, April 26, 2023 10:53:51 AM.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/0e692bdb-21eb-44bb-9723-d83582e0e424)

![image](https://github.com/tkxldk/HTBlue/assets/89120989/b55b3eea-481c-4797-8035-6e0fe85654b9)


> Soal 9 -> 26/04/2023 11:01:38
11. "What time did the contractor download the database backup? (UTC)", kita dapat melihatnya di access.log untuk melihat kapan contractor mendownloadnya. Dari sekian log yang berhubungan dengan backup, saya menemukan adanya "store" yang menarik perhatian saya, sehingga saya membuat asumsi bahwa store adalah download. 26/Apr/2023:12:01:38 +0100 = GMT +1, kurangi waktunya 1 jam.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/f17cda6e-88c2-46f7-8f4b-3b70ceee326a)


> Soal 10 -> 34707
12. "What was the size in bytes of the database backup as stated by access.log?", kita dapat menemukannya pada log sebelumnya.

![image](https://github.com/tkxldk/HTBlue/assets/89120989/635bb504-4786-4079-a5c5-1767b81e0ac6)
