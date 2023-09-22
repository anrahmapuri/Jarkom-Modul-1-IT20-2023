# Jarkom-Modul-1-IT20-2023

WRITE UP PRAKTIKUM JARKOM - MODUL 1 
IT20

Annisa Rahmapuri - 5027211018
Abdul Zaki Syarul Rahmat - 502721120

Nomor 1 - Addressing
Deskripsi : Pada nomor 1 ini user diminta untuk mencari paket yang mengupload sebuah file dan juga paket yang merupakan respons nya. Kemudian menginputkan sequence number (raw) dan acknowledge number (raw) dari kedua paket tersebut
Cara Pengerjaan : 
Untuk melakukan hal tersebut kita dapat melakukan filtering terlebih dahulu pada wireshark untuk mencari paket yang merupakan paket ftp dengan menggunakan query “ftp”. Kemudian kita dapat mencari list paket-paket tersebut. Untuk mempermudah pencarian, paket tersebut dapat diurutkan menurut waktunya secara ascending (dari yang paling awal ke akhir)

Setelah ditelusuri terdapat paket yang menggunakan “STOR”, salah satu perintah dalam protokol FTP untuk mengunggah sebuah file, dan jika diurutkan sesuai dengan waktu (ascending) make paket tepat setelahnya adalah paket respons dari request STOR

Di sebelah sebelah kiri bawah kita dapat membuka bagian TCP. Di bagian tersebut kita dapat menemukan sequence number dan acknowledge number masing-masing paket
Paket request STOR

Paket respons

Masukkan jawaban tersebut ke netcat


Nomor 2 - Stream
Deskripsi : User diminta untuk mencari web server yang digunakan melalui file packet capture
Cara pengerjaan : 
Pertama-tama, lakukan filtering pada wireshark untuk menampilkan paket http dengan query “http”

Periksa paket yang merupakan respons dari protokol HTTP seperi HTTP 200 dan 403

Dibagian HTTP sebelah kiri bawah, kita dapat menemukan server yang digunakan, yaitu gunicor (Green Unicorn)

Masukkan jawaban ke netcat 


Nomor 3 
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut:
Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702? 21 paket
Protokol layer transport apa yang digunakan? UDP
Penjelasan : 
Gunakan filter ip.addr == 239.255.255.250 and udp.port == 3702
ip.addr == 239.255.255.250 → filter untuk mencari paket-paket yang memiliki alamat IP sumber (ip.src) atau alamat IP tujuan (ip.dst) 239.255.255.250 
udp.port == 3702 → filter untuk port UDP sumber (udp.srcport) atau port UDP tujuan (udp.dstport) 3702.
Hasil yang terfilter → 21 paket dengan protokol UDP 



Nomor 4 
Berapa nilai checksum yang didapat dari header pada paket nomor 130?
Penjelasan :
Buka file → lihat detail paket no 130 
Cari checksumnya → 0x18e5

Akses nc 10.21.78.111 7272
`	

Nomor 5 - Analysis
Deskripsi : Pada kategori Analisis nomor 5 ini kita diminta untuk menganalisa file packet capture yang diberikan dan mencari beberapa informasi terkait
Cara pengerjaan : 
Kita diberikan dua file, satu file zip dan pcap, disini kita akan mencari password dari zip terlebih dahulu yang berada di file pcap. Lakukan filtering untuk menampilkan paket yang menggunakan protokol SMTP dengan query “smtp”









Follow TCP Stream paket-paket tersebut dengan cara klik kanan > Follow > TCP Stream

Setelah ditelusuri, dapat ditemukan password yang masih terenkripsi dengan enkripsi Base64. Kita dapat mendekripsinya menggunakan tools yang ada di internet

Setelah didekripsi, ditemukan password sebagai berikut, password berikut merupakan password dari file zip yang diberikan

File zip tersebut mengandung alamat netcat yang akan kita gunakan nantinya untuk mendapatkan flag

Kembali ke Wireshark, hilangkan filtering yang kita gunakan, maka disebelah kanan bawah akan tampil total paket yang ada

Kemudian disebelah kiri ada keterangan untuk paket SMTP menggunakan port 25

Untuk IP Addressnya dapat dilihat paket SMTP di bagian source nya

Masukkan informasi-informasi tersebut ke nc


Nomor 6 - Addressing
Deskripsi : Pada soal nomor 6 ini kita diminta untuk mencari pesan tersembunyi yang tersimpan di dalam file packet capture
Cara pengerjaan : 
Di soal dijelaskan bahwa source address 7812 is invalid. Ini adalah sebuah clue, kita dapat langsung menuju ke paket nomor 7812

Pada soal terdapat hint bahwa “source address adalah kunci” maka kita dapat melihat source IP Address pada paket tersebut yaitu 104.18.14.101

Hint lainnya mengatakan bahwa pesan merupakan pesan cipher dengan tipe a1z26 dengan ketentuan bahwa rentang huruf yang digunakan Huruf A-R, 1-18 dengan jawaban 6 huruf. Jika kita decode dengan petunjuk tersebut, maka akan di dapatkan 10-4.18.14.10-1 atau JDRNJA


Masukkan teks yang sudah di decode kedalam netcat

