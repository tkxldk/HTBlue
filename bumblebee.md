# Bumblebee

1. Dari zip didapatkan 2 file, yakni access.log dan phpbb.sqlite3

2. Untuk soal pertama diminta "What was the username of the external contractor?", jawabannya dapat kita lihat dengan membuka file database yang diberikan.
`SELECT name FROM sqlite_master WHERE type='table'`
Setelah itu akan muncul daftar tabel yang ada pada database tersebut dan disana ada nama tabel phpbb_users yang menarik perhatian saya.
`SELECT * FROM phpbb_users`
Lalu gunakan query di atas untuk menampilakan semua isi dari tabel tersebut dan ketika discroll ke bawah didapatkan nama apoole1 yang sesuai dengan hint.
