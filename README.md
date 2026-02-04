# Deteksi-Man-in-the-Middle

Perkenalan
Serangan man-in-the-middle ( MITM ) merupakan salah satu ancaman paling berbahaya dalam keamanan jaringan. Dalam serangan ini, penyerang memposisikan diri di antara titik akhir komunikasi yang sah untuk mencegat, memodifikasi, atau mengalihkan lalu lintas. Dari perspektif tim biru , mendeteksi serangan ini membutuhkan pendekatan berlapis yang menggabungkan pemantauan jaringan, validasi sertifikat, dan analisis perilaku. 

Di ruangan ini, kita akan mempelajari dasar-dasar serangan Man-in-the-Middle ( MITM ) dan cara mengenali tanda-tandanya dalam lalu lintas jaringan.

Tujuan pembelajaran
Ruangan ini berfokus pada tujuan pembelajaran berikut:

Memahami vektor dan teknik serangan MITM yang umum.
Pelajari cara mengidentifikasi indikator kompromi terkait serangan MITM ( Man-in-the-Middle).
Alat pemantauan jaringan utama untuk mendeteksi pola lalu lintas yang mencurigakan.
Latih prosedur respons insiden untuk skenario MITM ( Man-in-the-Middle).

-Koneksi Laboratorium
Skenario
Sebuah peringatan pemantauan jaringan rutin di  Acme Corp mengungkapkan pola lalu lintas yang tidak biasa yang menunjukkan kemungkinan serangan Man-in-the-Middle ( MITM ) di dalam LAN perusahaan. Selama beberapa hari, penyerang diam-diam mencegat komunikasi, mengalihkan koneksi, dan menangkap kredensial pengguna.
Di ruangan ini, Anda akan berperan sebagai Analis SOC yang menyelidiki insiden ini. Dengan menggunakan tangkapan paket dan log yang disediakan, Anda akan mengungkap bukti tiga teknik MITM berantai . 

ARP Spoofing (penyadapan jaringan).
Pemalsuan DNS (pengalihan).
SSL Stripping (penangkapan kredensial).
Akses Laboratorium
Sebelum melanjutkan, mulailah lab dengan mengklik tombol Mulai Mesin di bawah. Mesin akan dimulai dalam tampilan terpisah dan akan membutuhkan waktu sekitar dua menit untuk memuat. Jika mesin tidak terlihat, Anda dapat mengklik tombol Tampilkan Tampilan Terpisah di bagian atas tugas.

Catatan Penting
Untuk menyelesaikan ruangan ini, kita akan mengandalkan lalu lintas jaringan yang diberikan kepada kita di mitmfolder di Desktop. Namun, ada cara lain untuk memeriksa dan menyelesaikan ruangan ini.

Berkas log lengkap bernama mitm_attack.log, yang berisi seluruh rangkaian serangan, ditempatkan di folder yang sama.
Log yang sama dimasukkan ke dalam Splunk, yang dapat diakses di MACHINE_IP:8000, dan log tersebut dimasukkan ke dalam index=network_logs.

<img width="893" height="610" alt="image" src="https://github.com/user-attachments/assets/092773c0-36d7-4bec-a0b8-f4047602eedc" />

# Serangan MITM - Gambaran Umum
Serangan MITM : Gambaran Umum
Serangan Man-in-the-Middle ( MITM ) adalah serangan siber di mana penyerang secara diam-diam mencegat dan berpotensi mengubah komunikasi antara dua pihak, seperti pengguna dan layanan, tanpa sepengetahuan mereka. Penyerang dapat menguping untuk mencuri data sensitif seperti kredensial dan informasi kartu kredit atau menyuntikkan konten berbahaya. Serangan ini dapat menargetkan organisasi atau individu mana pun, terutama di mana enkripsi atau otentikasi lemah.

<img width="1046" height="696" alt="image" src="https://github.com/user-attachments/assets/51667b9c-dc1e-42da-b0c6-3a88c8217c14" />

Cara Kerja Serangan MITM
Serangan MITM umumnya melibatkan dua langkah utama:

Pencegatan : Penyerang menyusup ke dalam aliran komunikasi, seringkali dengan mengeksploitasi kelemahan dalam protokol jaringan atau dengan menggunakan teknik seperti ARP , DNS , atau pemalsuan IP.
Manipulasi/Dekripsi : Penyerang mencoba mengakses atau memodifikasi komunikasi, mendekripsi data yang dikodekan atau menyuntikkan konten berbahaya, seperti respons situs web yang diubah atau formulir login palsu.
Jenis-Jenis Serangan MITM yang Umum
Packet sniffing: Merekam paket data yang tidak terenkripsi yang dipertukarkan melalui jaringan, seringkali pada Wi-Fi terbuka.
Pembajakan sesi: Mencuri dan menggunakan token sesi untuk meniru identitas pengguna.
SSL stripping: Menurunkan kualitas koneksi HTTPS menjadi HTTP yang tidak aman untuk mencuri atau mengubah data yang ditransfer.
DNS spoofing: Mengalihkan lalu lintas situs web yang sah ke domain palsu dengan memanipulasi respons DNS .
Pemalsuan IP: Membuat paket IP berbahaya yang tampak berasal dari sistem tepercaya.
Titik akses Wi-Fi ilegal: Membuat jaringan palsu untuk mencegat lalu lintas pengguna.
Contoh di Dunia Nyata
Pada tahun 2017, Equifax mengalami pelanggaran data besar akibat serangan MITM (Man-in- the-Middle), yang mengungkap data sensitif lebih dari 100 juta pengguna.
Serangan-serangan tingkat tinggi mencakup injeksi kode oleh ISP dan aktor negara yang mencegat lalu lintas pencarian melalui pemalsuan SSL.
MITM dan Rantai Pembunuhan Siber
Untuk menganalisis dan menanggapi peristiwa keamanan secara efektif, seorang analis harus mengontekstualisasikan peringatan dalam model operasi musuh yang lebih luas. Indikator yang terisolasi menjadi signifikan ketika dipetakan ke Taktik, Teknik, dan Prosedur (TTP) penyerang. Model yang banyak diadopsi untuk ini adalah Cyber ​​Kill Chain, sebuah kerangka kerja yang mengurutkan tahapan tipikal dari intrusi siber tingkat lanjut.

Kerangka kerja ini terdiri dari tujuh fase yang berbeda:

Pengintaian : Pihak lawan mengumpulkan informasi intelijen tentang target untuk mengidentifikasi kelemahan.
Persenjataan : Pihak lawan menggabungkan eksploitasi dengan muatan berbahaya ke dalam paket yang dapat dikirimkan.
Pengiriman : Pihak musuh mengirimkan paket senjata ke lingkungan yang ditargetkan.
Eksploitasi : Kode musuh diaktifkan, dan memanfaatkan kerentanan perangkat lunak, perangkat keras, atau manusia untuk mendapatkan akses awal.
Instalasi : Pihak penyerang menginstal malware atau membuat pintu belakang permanen pada aset yang disusupi.
Komando & Kontrol ( C2 ) : Pihak lawan membangun saluran rahasia untuk berkomunikasi dengan dan mengendalikan aset yang disusupi.
Tindakan pada Tujuan : Pihak lawan mengeksekusi tujuan utamanya, seperti pengambilan data, penghancuran, atau pergerakan lateral.
Menempatkan MITM dalam Rantai Pembunuhan Siber
Man-in-the-Middle adalah teknik serbaguna yang terutama dimanfaatkan oleh pihak musuh selama fase Eksploitasi dan Instalasi.

Sebagai Teknik Eksploitasi: Serangan MITM mengeksploitasi kepercayaan dan keterbatasan desain yang melekat pada protokol jaringan inti seperti ARP dan DNS . Dengan memanipulasi protokol ini, penyerang dapat mencegat saluran komunikasi. Tindakan pencegatan sesi ini merupakan bentuk eksploitasi, karena melanggar integritas jaringan dan memberi musuh pijakan awal untuk menguping atau melakukan manipulasi aktif.
Sebagai Vektor Instalasi: Setelah penyerang berhasil membangun posisi MITM ( Man-in-the-Middle), mereka mengendalikan aliran data dan dapat menggunakannya sebagai mekanisme pengiriman muatan berbahaya. Misalnya, penyerang dapat menyuntikkan eksploitasi peramban, dropper malware, atau trojan akses jarak jauh (RAT) ke dalam unduhan yang sah dan tidak terenkripsi. Tindakan ini sesuai dengan fase Instalasi, di mana musuh membangun persistensi atau menyebarkan alat berbahaya tambahan ke sistem korban.
Mendeteksi serangan MITM (Man-in -the-Middle) adalah temuan yang sangat penting. Hal ini menandakan bahwa musuh secara aktif terlibat dalam tahap tengah intrusi, yang memberikan peluang penting bagi SOC ( Security Operations Center) untuk campur tangan dan mengganggu rantai serangan sebelum tujuan akhir tercapai.

# Mendeteksi ARP Spoofing
Sebelum menyelidiki serangan ARP spoofing, penting untuk memahami apa itu protokol ARP , tujuannya, dan bagaimana penyerang menyalahgunakannya untuk melakukan serangan Man-in-the-Middle.

Apa itu Protokol ARP ?
ARP (Address Resolution Protocol) memetakan alamat IP ke alamat MAC dalam jaringan lokal. Ketika sebuah perangkat ingin mengirim data ke IP lain, perangkat tersebut pertama-tama bertanya: "Siapa yang memiliki IP ini?" Perangkat yang tepat akan membalas dengan alamat MAC-nya.

Pemalsuan ARP
Dalam serangan ARP spoofing, penyerang mengirimkan balasan ARP palsu untuk mengelabui perangkat agar mengaitkan alamat MAC penyerang dengan IP yang sah, biasanya gateway default. Hal ini memungkinkan penyerang untuk mencegat, memodifikasi, atau mengalihkan lalu lintas.

Mengapa ARP Spoofing Berhasil?
ARP tidak memiliki otentikasi . Perangkat apa pun dapat mengirim is-atpesan yang tidak diminta. Penyerang mengeksploitasi kerentanan ini dengan mengirimkan balasan ARP palsu kepada korban dan gateway:

192.16.10.100penyerang 02:fe:BB:cd:55:55 mengklaim bahwa itu adalah gerbang masuknya.
Hasil:

Persediaan ARP korban terkontaminasi.
Semua lalu lintas yang ditujukan untuk gateway mengalir melalui penyerang terlebih dahulu (MITM).
Indikator Serangan
Kita dapat mencari indikator-indikator kunci berikut saat menyelidiki log atau lalu lintas jaringan untuk potensi serangan Man-in-the-Middle menggunakan ARP spoofing.

Pemetaan MAC-ke-IP Ganda : Beberapa alamat MAC mengklaim alamat IP yang sama. Menunjukkan peniruan identitas.
Balasan ARP yang tidak diminta : Jumlah balasan ARP yang tinggi tanpa adanya permintaan yang cocok ("ARP gratis").
Volume Lalu Lintas ARP Abnormal: Sejumlah besar paket ARP dalam interval waktu yang singkat.
Pengalihan Rute Lalu Lintas yang Tidak Biasa : Lalu lintas dialihkan melalui MAC penyerang.
Pola Pengalihan Gateway: Beberapa MAC tujuan untuk IP gateway yang sama.
Perulangan Probe/Reply ARP : Banyak permintaan ARP dengan Who has 192.168.1.x? Tell 192.168.1.ypola tertentu.
Informasi Jaringan
Untuk kasus yang diselidiki, kami memiliki informasi berikut tentang jaringan tersebut: 

Peran	AKU P	MAC	Catatan
Gerbang	192.168.10.1	-	Router asli
Penyerang	-	-	-
Korban	-	-	-
Domain	corp-login.acme-corp.local	-	 
Analisis Lalu Lintas Jaringan
Mari kita mulai penyelidikan kita dengan memeriksa lalu lintas ARP dan melihat bagaimana kita dapat mengidentifikasi dan mendeteksi pemalsuan ARP dalam lalu lintas jaringan. Buka folder network-traffic.pcapyang terletak the mitm_trafficdi Desktop, dan ikuti langkah-langkah yang disebutkan di bawah ini:

Mempersempit lalu lintas ARP
Karena ARP adalah protokol yang menjadi perhatian, kita dapat mulai dengan mengisolasinya menggunakan filter berikut. Ini akan memungkinkan kita untuk memeriksa permintaan/balasan dan memperhatikan volume atau pola yang tidak normal. 

Filter :arp

<img width="1016" height="469" alt="image" src="https://github.com/user-attachments/assets/a2cc7205-3ee5-4d98-a30a-b6c9707f70a5" />

Anda akan melihat permintaan dan balasan ( who-hasdan is-at) yang mengarah ke permintaan dan respons ARP. Kita dapat memeriksa hasilnya untuk setiap permintaan atau respons yang tidak normal dan berulang.

Catatan Penting : Tekan CTRL + ALT + 1 untuk mengunci waktu yang ditampilkan.

Permintaan ARP
Mari kita lihat permintaan ARP, seperti yang ditunjukkan di bawah ini. 

Menyaring:arp.opcode == 1

<img width="1007" height="577" alt="image" src="https://github.com/user-attachments/assets/9e5207ce-8997-4909-b041-f4e0b2745614" />

Ini menunjukkan semua permintaan ARP yang ditangkap dari berbagai host.

Respons ARP
Serangan ARP poisoning palsu biasanya menggunakan is-atbalasan yang tidak diminta (balasan cuma-cuma/tidak diminta). Ini adalah indikator yang kuat. Mari kita lihat respons ARP, seperti yang ditunjukkan di bawah ini:

Menyaring:arp.opcode == 2

<img width="1011" height="570" alt="image" src="https://github.com/user-attachments/assets/b2d94fd8-9c92-44df-bb25-0857bac989fe" />

Filter ini menampilkan respons ARP dari berbagai host. Pemeriksaan lebih dekat akan mengungkapkan beberapa respons, termasuk respons yang tidak perlu. Balasan yang sah biasanya sesuai dengan permintaan "who-has" terbaru. Aktivitas mencurigakan ditunjukkan oleh banyak balasan tanpa permintaan yang terlihat atau iklan berulang dari alamat IP yang sama dari alamat MAC yang mencurigakan.

Tanggapan ARP yang Tidak Beralasan
Host yang mencurigakan mengirimkan banyak balasan ARP yang tidak diminta (gratuitous) , terutama ke beberapa tujuan. ARP gratuitous yang berulang dapat mengindikasikan penyerang mempertahankan status "poison" (kondisi di mana paket yang digunakan tidak diinginkan). Kita juga dapat memfilter paket-paket gratuitous tersebut, seperti yang ditunjukkan di bawah ini:

Filter :arp.isgratuitous

<img width="1019" height="508" alt="image" src="https://github.com/user-attachments/assets/1c74c71a-8dc2-470c-b469-f7096ef221ad" />

Lalu lintas ARP yang terkait dengan Gateway
Kita memiliki informasi tentang alamat IP dan MAC yang terkait dengan gateway. Mari kita terapkan filter berikut untuk memeriksa lalu lintas ARP yang terkait dengan gateway, seperti yang ditunjukkan di bawah ini:

Filter :arp && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:aa:bb:cc:00:01

<img width="958" height="271" alt="image" src="https://github.com/user-attachments/assets/417b5905-656b-4a29-bd7a-cd789e1271bb" />

Melihat outputnya, kita hanya dapat melihat respons ARP . Sekarang mari kita persempit pencarian ke IP Gateway untuk menyelidiki lebih lanjut tentang alamat MAC yang terkait dengan IP tersebut, menggunakan filter berikut seperti yang ditunjukkan di bawah ini:

Filter :arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1

<img width="1291" height="667" alt="image" src="https://github.com/user-attachments/assets/ffa17a65-3dff-45d3-bb83-c5e2d5290c19" />

Output ini terlihat menarik. Jika diperhatikan lebih detail, kita melihat beberapa balasan ARP yang mengarahkan IP Gateway ke alamat MAC yang mencurigakan. Frekuensi balasan ARP ini menunjukkan bahwa ini memang merupakan pemalsuan ARP . Mari kita konfirmasi dengan menerapkan filter lain, seperti yang ditunjukkan di bawah ini:

Menyaring:arp.opcode ==2 && _ws.col.info contains "192.168.10.1 is at"

<img width="932" height="479" alt="image" src="https://github.com/user-attachments/assets/9d7da7b4-3023-4511-9b06-6b49eba715b2" />

Filter ini memiliki dua bagian. Bagian pertama berfokus pada respons ARP dan bagian kedua  _ws.col.info contains "192.168.10.1 is at"memfilter konten yang ditampilkan di kolom informasi. Ini menyaring respons ARP, yang mengarahkan IP Gateway 192.168.10.1 ke alamat MAC. Tetapi jika kita perhatikan lebih dekat, kita dapat melihat bahwa penyerang menggunakan spoofing ARP untuk mengarahkan IP ke alamat MAC-nya. Kita juga dapat menggunakan filter ini arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1, yang menunjukkan hasil yang sama.

Memeriksa alamat MAC yang mencurigakan
Setelah kita mengidentifikasi aksi ARP spoofing, mari kita persempit pencarian ke alamat MAC penyerang yang telah mengaitkan dirinya dengan alamat IP Gateway, menggunakan filter berikut:

Menyaring:arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:fe[REDACTED]

<img width="937" height="356" alt="image" src="https://github.com/user-attachments/assets/cc867d21-15b4-46b8-b0aa-02eb813fdfd2" />

Hasil tersebut dengan jelas menegaskan bahwa penyerang melakukan pemalsuan ARP .

Periksa Pemetaan IP-ke-MAC yang Duplikat
Hal terakhir yang dapat kita periksa dan konfirmasi adalah dengan memfilter berdasarkan "Periksa pemetaan alamat MAC duplikat ke satu alamat IP". 

Filter : arp.duplicate-address-detected || arp.duplicate-address-frame

<img width="1046" height="461" alt="image" src="https://github.com/user-attachments/assets/d352a3fe-946c-497a-903b-b2280a208ca1" />

Hasil ini menunjukkan bahwa penyerang berhasil melakukan ARP spoofing dan memposisikan dirinya di antara korban dan gateway. Mari kita lanjutkan ke tugas berikutnya dan periksa bagaimana penyerang dapat melakukan serangan DNS spoofing untuk mendapatkan pengalihan.

Jawablah pertanyaan-pertanyaan di bawah ini.
Berapa banyak paket ARP dari alamat MAC gateway yang teramati?
ketik perintah di wireshark di pencarian dan lihat di bagian displayed bawah  : arp && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:aa:bb:cc:00:01 
<img width="1366" height="608" alt="image" src="https://github.com/user-attachments/assets/f4a318ed-8471-4fe2-8aa3-1ddbbb7b9e31" />


jawaban 10

Memeriksa
Alamat MAC apa yang digunakan penyerang untuk menyamar sebagai gateway?
ketik di pencarian wire shark : arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1 && eth.src 
<img width="1360" height="624" alt="image" src="https://github.com/user-attachments/assets/0da42a99-264d-44fd-a272-b04c3ebf0831" />

jawaban : 02:fe:fe:fe:55:55

Memeriksa
Berapa banyak balasan ARP gratis yang diamati untuk 192.168.10.1?
cara hampir sama ketik di pencarian wire shark : arp.isgratuitous
lihat ip yang sama seperti  192.168.10.1 ada berapa lihat di tampilan wireshark 
<img width="1360" height="624" alt="image" src="https://github.com/user-attachments/assets/eae99123-6a1d-400f-8ed0-e4c6a81fd421" />

jawaban : 2

Memeriksa
Berapa banyak alamat MAC unik yang mengklaim IP yang sama (192.168.10.1)?
cara hampir sama seperti yang di atas 
di pencarian wire shark : arp.isgratuitous

jawaban : 2

Memeriksa
Berapa total paket ARP spoofing yang teramati dari penyerang?
dengan mengetik di pencarian wireshark : arp.duplicate-address-detected || arp.duplicate-address-frame
lalu lihat detail displayed paling bawah sebelah pojok kanan : 14

jawaban : 14

# Mengungkap Praktik DNS Spoofing
Protokol DNS yang Disederhanakan
Pertama, mari kita pahami  DNS . Anggap saja seperti daftar kontak di ponsel Anda. Anda tidak mengingat nomor telepon teman-teman Anda; Anda hanya mengetuk nama mereka. Demikian pula, DNS menerjemahkan nama situs web yang mudah dipahami manusia (seperti  ) menjadi alamat IPwww.google.com yang mudah dipahami komputer .

DNS Spoofing (atau DNS Cache Poisoning) terjadi ketika penyerang merusak sistem ini. Mereka memberikan "nomor telepon" yang salah kepada komputer Anda untuk situs web yang ingin Anda kunjungi.

Ini adalah teknik ampuh untuk melancarkan serangan Man-in-the-Middle (MITM) . Begini cara kerjanya:

Korban mencoba mengunjungi bank mereka di my-real-bank.com.
Penyerang , yang sudah berada di jaringan lokal (mungkin melalui ARP spoofing), mencegat permintaan DNS korban .
Modus Spoofing: Penyerang dengan cepat mengirimkan respons DNS palsu ke korban. Respons palsu ini menyatakan, " my-real-bank.comberada di alamat IP saya: ATTACKER_IP".
Pencegatan: Komputer korban mempercayai respons palsu ini dan menyimpannya di cache DNS-nya. Ketika korban mencoba terhubung ke bank mereka, tanpa disadari mereka terhubung langsung ke server penyerang, yang mungkin menampung replika sempurna dari situs perbankan yang sebenarnya.
Penyerang kini in the middledapat merekam semua yang diketik korban, termasuk nama pengguna dan kata sandinya.

<img width="1055" height="713" alt="image" src="https://github.com/user-attachments/assets/2909f0f0-1ef0-42f0-9abb-f26f090913de" />

Indikator Serangan
Kita dapat mencari indikator-indikator kunci berikut saat menyelidiki log atau lalu lintas jaringan untuk potensi serangan Man-in-the-Middle menggunakan DNS  spoofing.

Beberapa respons DNS untuk kueri yang sama : Sebuah resolver yang sah dan sebuah responder palsu membalas kueri yang sama. Ini adalah indikator tunggal yang paling dapat diandalkan.
Respons DNS dari sumber yang tidak terduga : Balasan DNS tiba dari alamat IP yang tidak sesuai dengan resolver yang dikonfigurasi (seperti 8.8.8.8 atau server DNS Anda ).
Nilai TTL (Time-To-Live) yang mencurigakan : Penyerang menggunakan TTL yang sangat rendah (1 - 30 detik) untuk menjaga agar entri yang diracuni berumur pendek dan menegaskan kembali kendali.
Respons DNS yang tidak diminta : Balasan DNS muncul tanpa adanya permintaan DNS yang sesuai dari korban.
Analisis Lalu Lintas Jaringan
Mari kita mulai penyelidikan kita dengan memeriksa lalu lintas DNS dan bagaimana kita dapat mengidentifikasi dan mendeteksi pemalsuan DNS dalam lalu lintas jaringan. Buka file  network-traffic.pcapyang terletak di mitm_trafficfolder di Desktop, dan ikuti langkah-langkah yang disebutkan di bawah ini:

Mempersempit lalu lintas DNS
Karena DNS adalah protokol yang menjadi perhatian, kita dapat mulai dengan mengisolasinya menggunakan filter berikut. Ini akan memungkinkan kita untuk memeriksa permintaan/balasan dan memperhatikan volume atau pola yang tidak normal. 

Filter :dns

<img width="1185" height="397" alt="image" src="https://github.com/user-attachments/assets/9503a838-6923-475a-a255-ef21b3a8e3b3" />

Output tersebut berisi permintaan DNS dan respons yang sesuai.

Penyaringan lalu lintas yang sah
Server DNS yang sah (seperti milik Google 8.8.8.8) merespons dari alamat IP eksternal yang dikenal. Dengan memfilter respons dari IP ini, kita dapat melihat normalseperti apa jawabannya untuk perbandingan.

Filter :dns.flags.response == 1 && ip.src == 8.8.8.8

<img width="1272" height="452" alt="image" src="https://github.com/user-attachments/assets/fb832a6d-ff0b-4c3d-8507-d87e707660e5" />

asilnya menunjukkan balasan DNS yang valid dari server DNS yang sah .

Periksa Respons DNS
Mari kita lihat respons DNS , menggunakan filter di bawah ini. 

Filter :dns.flags.response==1

<img width="1229" height="545" alt="image" src="https://github.com/user-attachments/assets/248a5b9e-8260-4651-ae60-f2aa96dfcfa0" />

Dalam output tersebut, kita dapat mencari respons dari alamat IP selain server DNS biasa . Jika diperhatikan lebih teliti, kita menemukan satu respons DNS dari IP selain  8.8.8.8. Ini adalah temuan yang menarik. Meskipun kita telah menemukan permintaan DNS yang aneh yang mengindikasikan potensi upaya pemalsuan DNS, kita akan mencatat hal ini dan kembali membahasnya nanti.

Respons DNS dari Server DNS
Filter berikut akan menampilkan respons DNS dari server DNS. 

Filter :dns.flags.response == 1 && ip.src == 8.8.8.8

<img width="1301" height="639" alt="image" src="https://github.com/user-attachments/assets/f0e0508f-8cd2-4561-80aa-f4a6c3541c82" />

Permintaan DNS untuk Domain kami
Sekarang mari kita perhatikan dengan saksama lalu lintas DNS untuk domain yang kita minati, corp-login.acme-corp.local, menggunakan filter berikut:

Filter :dns && dns.qry.name == "corp-login.acme-corp.local"

<img width="1259" height="470" alt="image" src="https://github.com/user-attachments/assets/f84c378b-524a-4dac-a7ec-e650422c8405" />

Sekarang mari kita saring permintaan DNS untuk domain yang kita minati, yang berasal dari server DNS , menggunakan filter seperti yang ditunjukkan di bawah ini:

Filter :dns.flags.response == 1 && ip.src == 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local"

<img width="1256" height="556" alt="image" src="https://github.com/user-attachments/assets/5f1da0be-17b9-47c5-be89-e52a6ba0099e" />

Hasilnya juga terlihat sangat normal, seperti yang diharapkan. 

Respons DNS selain dari Server DNS .
Pada hasil sebelumnya, kita telah menelusuri lalu lintas DNS yang berasal dari server DNS untuk domain yang kita minati. Mari kita terapkan filter berikut untuk melihat apakah ada permintaan DNS yang berasal dari server selain server DNS8.8.8.8 :

Filter :dns.flags.response == 1 && ip.src != 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local"

<img width="1217" height="172" alt="image" src="https://github.com/user-attachments/assets/f41d9887-4700-4c2f-9cbd-2225ee1e7d9d" />

Inilah tampilan dari DNS spoofing. Ini menunjukkan sebuah sistem di dalam jaringan bertindak sebagai server DNS palsu, mengirimkan respons DNS palsu .

Ringkasan Analisis
Analisis pada dua tugas sebelumnya menunjukkan:

Serangan Man-in-the-Middle multi-tahap yang berhasil di mana penyerang pertama-tama merusak pemetaan ARP untuk gateway (192.168.10.1)
Kemudian disusul dengan balasan DNS palsu untuk corp-login.acme-corp.local yang mengarahkan korban ke IP penyerang.
Mari kita lanjutkan ke tugas berikutnya: memahami mengapa SSL stripping digunakan dan menemukan bukti SSL stripping yang mengakibatkan pencurian data korban.

Jawablah pertanyaan-pertanyaan di bawah ini.
Berapa banyak respons DNS yang diamati untuk domain corp-login.acme-corp.local?

211

Memeriksa
Berapa banyak permintaan DNS yang teramati dari IP selain 8.8.8.8?

2

Memeriksa
Alamat IP apa yang dikembalikan oleh respons DNS palsu penyerang untuk domain tersebut?

192.168.10.55

# Mendeteksi Aksi Penyadapan SSL
SSL stripping adalah teknik man-in-the-middle di mana penyerang mencegat dan memodifikasi lalu lintas untuk menghapus atau mencegah enkripsi TLS antara klien dan server. Hal ini menyebabkan klien berkomunikasi melalui HTTP, bukan HTTPS. Penyerang mempertahankan sesi yang aman (HTTPS) dengan server sambil meneruskan HTTP biasa ke korban, sehingga memungkinkan penyadapan dan pengambilan kredensial.

Cara Kerjanya
Korban memulai permintaan HTTPS ke sebuah situs web.
Penyerang mencegat permintaan menggunakan ARP spoofing atau titik akses palsu.
Penyerang terhubung ke situs web melalui HTTPS tetapi meneruskan respons ke korban melalui HTTP .
Korban tanpa sadar berinteraksi melalui HTTP , sehingga mengekspos data sensitif dalam bentuk teks biasa.
Indikator SSL stripping
Permintaan Awal vs. Respons:  Permintaan awal pengguna mungkin untuk HTTPS(port 443), tetapi paket-paket berikutnya segera beralih ke port yang tidak terenkripsi HTTP(port 80) untuk domain yang sama.
Pengalihan/Penulisan Ulang Tautan : Memantau pengalihan ( Kode Status HTTP 301, 302) yang secara terus-menerus mengarahkan permintaan HTTPS ke sumber daya HTTP .
Kesalahan Sertifikat : Meskipun penyerang biasanya mencoba menyembunyikan hal ini, proses jabat tangan TLS/SSL awal mungkin gagal atau menampilkan sertifikat yang ditandatangani sendiri jika penyerang menggunakan teknik proksi yang lebih langsung.
 
Analisis Lalu Lintas Jaringan
Mari kita lanjutkan penyelidikan kita dengan memeriksa lalu lintas jaringan yang sama, yaitu file pcap di Wireshark. Dalam tugas ini, kita akan melihat lalu lintas SSL dan melihat apakah kita dapat mengidentifikasi salah satu indikator yang disebutkan di atas. 

Mempersempit  lalu lintas SSL
Untuk tugas ini, HTTPS adalah protokol yang menjadi fokus. Kita mulai dengan mengisolasinya menggunakan filter berikut. Ini akan memungkinkan kita untuk memeriksa permintaan SSL dan memperhatikan volume atau pola yang tidak normal. 

Filter :tls || ssl

<img width="1024" height="467" alt="image" src="https://github.com/user-attachments/assets/ae493aa1-1833-4575-8f7f-f087dcdec138" />

Filter ini akan menampilkan semua lalu lintas yang terkait dengan SSL.

Periksa lalu lintas SSL server kami.
Mari kita terapkan filter berikut untuk menampilkan jabat tangan TLS yang telah terjalin ke server kita, yang membuktikan bahwa situs tersebut biasanya menggunakan TLS untuk komunikasi.

filter :tls.handshake.type == 1 && tls.handshake.extensions_server_name == "corp-login.acme-corp.local"

<img width="1092" height="446" alt="image" src="https://github.com/user-attachments/assets/4fcc1993-2e6c-4b15-a780-cc7abc544927" />

Salah satu pengamatan kunci dari output di atas adalah konfirmasi bahwa domain yang bersangkutan menggunakan TLS untuk komunikasi.

Tampilkan pengalihan DNS yang mendahului penghapusan.
Hipotesis kami tentang SSL stripping adalah bahwa hal itu dilakukan setelah penyerang berhasil melakukan DNS spoofing, mengarahkan korban ke IP penyerang. Pada tugas sebelumnya, kami telah mengidentifikasi alamat IP penyerang yang melakukan DNS spoofing. Mari kita isolasi respons DNS dari penyerang untuk menunjukkan bahwa korban diarahkan ke IP penyerang, seperti yang ditunjukkan di bawah ini:

Filter : dns.flags.response == 1 && ip.src == 192.168.10.55 && dns.qry.name == "corp-login.acme-corp.local"

<img width="1187" height="138" alt="image" src="https://github.com/user-attachments/assets/cb088ac7-acd9-4ce1-91f7-c9c89da4b3d7" />

Hasil di atas menunjukkan dua insiden di mana IP penyerang mengirimkan respons DNS palsu untuk domain yang diminati. 

Verifikasi TLS hilang
Salah satu indikator utama dari SSL stripping adalah bahwa, setelah spoofing, domain tersebut tidak lagi melakukan jabat tangan TLS ke server yang sah, yang memvalidasi tidak adanya lalu lintas TLS dari korban ke server sebenarnya. Mari kita terapkan filter berikut pada IP server dan IP penyerang, seperti yang ditunjukkan di bawah ini:

Filter :http && ip.src == 192.168.10.10 && ip.dst == 192.168.10.55

<img width="1086" height="177" alt="image" src="https://github.com/user-attachments/assets/9f5f9371-a227-4b25-889c-56f55eb196c1" />
Kita dapat melihat dengan jelas bahwa korban terhubung ke server setelah SSL stripping dan berhasil login. 

<img width="1635" height="444" alt="image" src="https://github.com/user-attachments/assets/6ad5c209-0285-4e93-a124-764408cd016e" />

Kita juga dapat mengidentifikasi kredensial pengguna dalam bentuk teks biasa, yang menegaskan bahwa penyerang berhasil memperoleh kredensial korban. Meskipun ada indikator SSL stripping lainnya yang juga perlu kita perhatikan. Dalam skenario ini, kami hanya mengamati satu indikator, di mana lalu lintas HTTPS portal kami di-strip menjadi HTTP .

Ringkasan
Mari kita lihat ringkasan investigasi, termasuk kronologi serangan.

Pemalsuan ARP (peracunan cache):
Serangan ARP spoofing dimulai , penyerang mengirimkan ARP yang tidak diminta  is-atdengan mengklaim alamat IP gateway.
Pemalsuan DNS (respons DNS palsu):
Permintaan DNS korban untuk corp-login.acme-corp.local.
Respons DNS palsu dari penyerang, jawaban domain →  192.168.10.55.
Penghapusan SSL ( penurunan versi TLS / pengambilan kredensial):
Korban memulai koneksi ke IP yang telah diresolusi, HTTP ke penyerang (efek penghapusan SSL).
Kredensial POST teramati (teks biasa).

Jawablah pertanyaan-pertanyaan di bawah ini.
Berapa banyak permintaan POST yang teramati untuk domain kami corp-login.acme-corp.local?

1

Memeriksa
Apa kata sandi korban yang ditemukan dalam teks biasa setelah serangan ssl stripping berhasil? 

Secret123!

# Kesimpulan & Ringkasan Ruangan
Di ruangan ini, kami mengeksplorasi beberapa serangan man-in-the-middle umum yang dirangkai dalam sebuah skenario dan cara mengidentifikasi jejaknya dalam lalu lintas jaringan. 

Harap dicatat bahwa log serupa ditempatkan di folder log mitm_network dan telah diimpor terlebih dahulu ke Splunk agar Anda dapat mencobanya.

Beberapa konsep utama yang dibahas di ruangan ini adalah:

Terdeteksi dengan menemukan alamat MAC duplikat untuk IP yang berbeda di cache ARP ( arp -a) atau dengan mendeteksinya di Wireshark.
DNS Spoofing: Terungkap dengan menemukan beberapa respons DNS yang saling bertentangan .
SSL Stripping: Terungkap dengan menemukan data sensitif, seperti kata sandi, yang dikirim dalam bentuk teks biasa melalui HTTP  ke situs web yang seharusnya aman.
Jika Anda menyukai ruangan ini, lihat juga ruangan Deteksi Eksfiltrasi Data kami , yang memeriksa dan mengidentifikasi upaya filtrasi melalui berbagai saluran jaringan.
