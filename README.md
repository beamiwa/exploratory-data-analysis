# LINK DASHBOARD
Klik : [DASHBOARD](https://public.tableau.com/app/profile/beami/viz/criminalreport/CriminalCasesReport)

# CRIME IN BOSTON ANALYSIS
by Beami Mbani Wibawa

# LATAR BELAKANG
Berdasarkan [washingtonpost](https://www.washingtonpost.com/outlook/we-dont-know-why-violent-crime-is-up-but-we-know-theres-more-than-one-cause/2021/07/09/467dd25c-df9a-11eb-ae31-6b7c5c34f0d6_story.html), tingkat pembunuhan di AS meningkat, meskipun lambat dan tanpa banyak perhatian media, sebelum pandemi. Dari tahun 2019 hingga 2020, angka tersebut meningkat sebesar 13 persen. Maka Boston Police Departement (BPD) ingin meningkatkan pelayanannya dalam menindaklanjuti kriminalitas di Boston agar masyarakat merasa aman dan nyaman. Untuk mencapai hal tersebut, saya akan melakukan analisis berdasarkan data historikal dari dokumentasi laporan insiden kriminal yang disediakan oleh Boston Police Department yang terjadi di tahun 2015-2018. Dengan adanya analisis data historikal ini diharapkan dapat memberikan insight yang nantinya dapat dijadikan rekomendasi dalam menentukan perlengkapan dan tindakan yang akan diambil oleh BPD untuk meningkatkan pelayanan dalam menjaga keamanan.

# DATASET
- Sumber : [Crime in Boston](https://drive.google.com/drive/folders/1uPzXi8Qkf_lSxs7UbTAANxZwGe2PzREm). Terdapat 2 dataset yang harus di analisis dan diolah.
- 1 dataset akan diberi variabel crime 
- 1 dataset lainnya akan diberi variabel codes

Dataset crime berisikan dokumentasi mengenai laporan insiden kriminal yang disediakan oleh Departemen Kepolisian Boston (BPD), dengan rincian awal berupa insiden yang ditanggapi oleh petugas BPD dari laporan masyarakat sipil, yang mencakup kumpulan pelanggaran yang dilaporkan dari tanggal 15 Juni 2015-3 September 2018. Dapat dilihat bahwa pada tahun 2015 dan 2018 datanya tidak penuh. tahun 2015 hanya dimulai pada bulan juni (7 bulan) dan 2018 (hanya 9 bulan)

# TUJUAN
- Meningkatkan pelayanan patroli di Boston berdasarkan banyaknya jenis pelanggaran
- Menentukan perlengkapan dan tindakan yang dapat diambil dan dipersiapkan oleh Boston Police Departement berdasarkan banyaknya jenis pelanggaran

# RUMUSAN MASALAH
- Offense group apa yang paling sering terjadi? dan sering terjadinya di district mana?
- Apa UCR part yang paling sering terjadi di berbagai district?
- Apa jenis insiden kriminal berdasarkan UCR part yang paling sering terjadi?
- Berapa persen perbandingan antara kasus insiden kriminal dengan adanya penembakan dan tidak ada penembakan?
- Bagaimana perubahan trend kriminalitas dari waktu ke waktu?

# EXPLORING DATA 
## Load Dataset Crime
Dataset crime menjelaskan mengenai rincian laporan insiden kejahatan di Boston.
## Penjelasan kolom pada dataset crime
| kolom | Penjelasan |
| --- | --- |
| INCIDENT_NUMBER | berisikan number insiden kriminal yang dilaporkan oleh masyarakat sipil kepada Boston Police Department (BPD) |
| OFFENSE_CODE | kode-kode pelanggaran berupa angka |
| OFFENSE_CODE_GROUP | berisikan grup-grup pelanggaran dari [UCR_PART] |
| OFFENSE_DESCRIPTION | berisikan nama pelanggaran berdasarkan kode angka [OFFENSE_CODE] |
| DISTRICT | berisikan daerah terjadinya insiden kriminal |
| REPORTING_AREA | berisikan tentang area pelaporan, darimana insiden kriminal itu dilaporkan |
| SHOOTING | berisikan indikasi terjadinya penembakan |
| OCCURRED_ON_DATE | berisikan tanggal dan waktu paling awal insiden kriminal itu bisa terjadi |
| YEAR | berisikan tahun berasal dari [OCCURRED_ON_DATE] |
| MONTH | berisikan bulan berasal dari [OCCURRED_ON_DATE] |
| DAY_OF_WEEK | berisikan hari berasal dari [OCCURRED_ON_DATE] |
| HOUR | berisikan jam berasal dari [OCCURRED_ON_DATE] |
| UCR_PART | berisikan Nomor Bagian Pelaporan Kejahatan Universal (1,2,3) berdasarkan [Group] |
| | UCR (Uniform Crime Report) adalah laporan tahunan yang dikeluarkan oleh FBI yang menyajikan data tentang kategori kejahatan tertentu yang dilaporkan ke polisi (dictionary.com) |
| | Terdapat 2 part dari UCR berdasarkan [sumber](https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses):
| | Part I (Kejahatan Berat) = Criminal Homicide - The killing of another person (Murder and Nonnegligent Manslaughter & Manslaughter), Rape, Robbery (Armed Robbery-Any Weapon & Strong    Arm-No Weapon), Aggravated Assault (Gun, Knife or Cutting Instrument, Other Dangerous Weapons, Hands, Fists, Feet, etc. Aggravated), Burglary (Forcible Entry, Unlawful Entry-No Force, Attempted Forcible Entry), Larceny , Motor Vehicle Theft , Arson, Human Trafficking - Commercial Sex Acts, Human Trafficking - Involuntary Servitude |
| | Part II (Kejahatan Ringan)  = Other Assaults, Forgery and Counterfeiting , Fraud, Embezzlement, Stolen Property, Vandalism, Weapons, Prostitution and Commercialized Vice , Sex Offenses , Drug Abuse Violation, Gambling , Offenses Against Family and Children, Driving Under the Influence , Liquor Laws, Disorderly Conduct, Vagrancy , All Other Offenses (All violations of state or local laws not specifically identified as Part I or Part II offenses,except traffic violations. This classification includes: • Admitting minors to improper places • Bigamy and polygamy • Blackmail and extortion • Contempt of court • Kidnapping • Possession of drug paraphernalia • Riot and rout, etc. • Attempts to commit any of the above), Curfew and Loitering Law Violation (Juvenile), Runaways (Juvenile) |
| | Part III = menurut [sumber](https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses), terdapat pernyataan bahwa "All Other Offenses (All violations of state or local laws not specifically identified as Part I or Part II offenses,except traffic violations". |
| STREET | berisikan nama jalan tempat insiden kriminal itu terjadi |
| Lat | berisikan latitude dalam peta berasal dari [Street] |
| Long | berisikan longitude dalam peta berasal dari [Street] |
| Location | berisikan gabungan [Latitude] dan [Longitude] berasal dari [Street] |
## Load Dataset Codes
Dataset codes menjelaskan mengenai kode-kode pelanggaran.
## Penjelasan Kolom Dataset Codes
Tabel Codes, berfungsi sebagai informasi tambahan. 
| kolom | Penjelasan |
| --- | --- |
| CODE | kode-kode pelanggaran berupa angka (sama seperti kolom OFFENSE_CODE di dataset crime.csv) |
| NAME | Deskripsi pelanggaran |
## Merge Dataset Crime dan Codes 
## Penjelasan kolom pada dataset yang telah di merge 
| Kolom | Penjelasan |
| --- | --- | 
| Incident Number | berisikan number insiden kriminal yang dilaporkan oleh masyarakat sipil kepada Boston Police Department (BPD) |
| Offense Code | kode-kode pelanggaran berupa angka |
| Group | berisikan grup-grup pelanggaran dari [UCR Part] |
| Description | berisikan nama pelanggaran berdasarkan kode angka [Offense Code] |
| District | berisikan daerah terjadinya insiden kriminal |
| Area | berisikan tentang area pelaporan, darimana insiden kriminal itu dilaporkan |
| Shooting | berisikan indikasi terjadinya penembakan |
| Date | berisikan tanggal dan waktu paling awal insiden kriminal itu bisa terjadi |
| Year | berisikan tahun berasal dari [Date] |
| Month | berisikan bulan berasal dari [Date] |
| Day | berisikan hari berasal dari [Date] |
| Hour | berisikan jam berasal dari [Date] |
| UCR Part | berisikan Nomor Bagian Pelaporan Kejahatan Universal (1,2,3) berdasarkan [Group] |
| | UCR (Uniform Crime Report) adalah laporan tahunan yang dikeluarkan oleh FBI yang menyajikan data tentang kategori kejahatan tertentu yang dilaporkan ke polisi (dictionary.com) |
| | Terdapat 2 part dari UCR (https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses): |
| | Part I (Kejahatan Berat) = Criminal Homicide - The killing of another person (Murder and Nonnegligent Manslaughter & Manslaughter), Rape, Robbery (Armed Robbery-Any Weapon & Strong    Arm-No Weapon), Aggravated Assault (Gun, Knife or Cutting Instrument, Other Dangerous Weapons, Hands, Fists, Feet, etc. Aggravated), Burglary (Forcible Entry, Unlawful Entry-No Force, Attempted Forcible Entry), Larceny , Motor Vehicle Theft , Arson, Human Trafficking - Commercial Sex Acts, Human Trafficking - Involuntary Servitude |
| | Part II (Kejahatan Ringan)  = Other Assaults, Forgery and Counterfeiting , Fraud, Embezzlement, Stolen Property, Vandalism, Weapons, Prostitution and Commercialized Vice , Sex Offenses , Drug Abuse Violation, Gambling , Offenses Against Family and Children, Driving Under the Influence , Liquor Laws, Disorderly Conduct, Vagrancy , All Other Offenses (All violations of state or local laws not specifically identified as Part I or Part II offenses,except traffic violations. This classification includes: • Admitting minors to improper places • Bigamy and polygamy • Blackmail and extortion • Contempt of court • Kidnapping • Possession of drug paraphernalia • Riot and rout, etc. • Attempts to commit any of the above), Curfew and Loitering Law Violation (Juvenile), Runaways (Juvenile) |
| | Part III = menurut (https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses , terdapat pernyataan bahwa "All Other Offenses (All violations of state or local laws not specifically identified as Part I or Part II offenses,except traffic violations". |
| Street | berisikan nama jalan tempat insiden kriminal itu terjadi |
| Latitude | berisikan latitude dalam peta berasal dari [Street] |
| Longitude | berisikan longitude dalam peta berasal dari [Street] |
| Location | berisikan gabungan [Latitude] dan [Longitude] berasal dari [Street] |

# DATA CLEANING
Mengecek unique value dari tiap kolom
Berdasarkan Pengamatan Unik Value, dapat dilihat bahwa :
- Pada INCIDENT NUMBER ada format penulisan yang berbeda dari yang lain, yaitu 142052550. Format penulisan incident number ini diawali oleh angka 1 dan dengan pola I\d{9}, sedangkan secara umum format penulisan incident number diawali oleh huruf 'I' dan mengikuti pola I\d{9}(-\d{2})
- Pada GROUP terdapat format penulisan yang berbeda, yaitu menggunakan kapital semua (HOME INVASION, HUMAN TRAFFICKING, HUMAN TRAFFICKING - INVOLUNTARY SERVITUDE, INVESTIGATE PERSON) sedangkan yang lain tidak. 
## cek date apakah memiliki pola 'yyyy-mm-dd hh:mm:ss'
## Analisis Format Penulisan Incident Number
## Analisis Format Penulisan Group
## cek deskriptif
Berdasarkan pengamatan deskriptif, dapat dilihat bahwa:
- pada Latitude dan Longitude terdapat nilai -1.000000 (termasuk outlier)
- pada kolom area terdapat blank value
- pada location terdapat nilai (0.00000000, 0.00000000) (termasuk outlier)
## Cek outlier pada latitude
## Cek outlier pada longitude
## Ubah blank value pada area
## ubah outlier pada location
## Data Duplicate Handling
## Missing value handling

# ANALISIS DATA BERDASARKAN RUMUSAN MASALAH

# **Offense group apa yang paling sering terjadi? dan sering terjadinya di district mana?**
## Insight
- Berdasarkan top ten of offense group, tindakan polisi dalam mengatasi kriminalitas yang sering dilakukan adalah 'Motor Vehicle Accident Response/Penanganan Kecelakaan Kendaraan Bermotor' yaitu berjumlah 37.132. Motor Vehicle Accident Response termasuk ke dalam UCR Part III, yaitu termasuk ke dalam kategori insiden kriminal traffic violations/pelanggaran lalu lintas. Grup pelanggaran 'motor vehicle accident response' yang berjumlah paling banyak diantara grup pelanggaran lainnya ini sering sekali terjadi di district B2 pada waktu pagi hari yaitu di sekitar jam 5 AM-12 PM.

# **Apa UCR part yang sering terjadi di berbagai district?**
## Insight
- Di district E13 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district A7 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district C11 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district B2 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district B3 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district E18 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district C6 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district E5 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district A1 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district D14 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district D4 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1
- Di district A15 paling sering terjadi insiden kriminal dari UCR part 3 dan paling sedikit UCR part 1

# **Apa jenis insiden kriminal berdasarkan UCR part yang paling sering terjadi?**
## Insight
-  Insiden kriminal yang paling banyak dilaporkan dari UCR part one meliputi pencurian dari gedung sebanyak 8.864 kasus, pencurian dari MV - Non aksesories sebanyak 8.361 kasus, pencurian penguntilan sebanyak 7.781 kasus, pencurian dari semuanya sebanyak 5.654 kasus.
- Insiden kriminal berdasarkan UCR Part two yang paling banyak terjadi meliputi vandalisme (perbuatan merusak hasil karya seni / barang berharga) sebanyak 14.588 kasus dan serangan sebanyak 13.855 kasus. Selanjutnya, ada ancaman secara fisik sebanyak 8.783 kasus, penipuan 4.301 kasus.
- Insiden kriminal yang paling banyak dilaporkan dari UCR Part three adalah kegiatan investigasi terhadap individu sebanyak 17.963 kasus, pemberian tindakan medis untuk individu yang terluka dari sebuah insiden kriminal sebanyak 17.810 kasus, perbuatan merusak harta benda dan kabur dengan kendaraan bermotor sebanyak 14.364 kasus, adu mulut sebanyak 12.942 kasus, tilang terhadap kendaraan bermotor sebanyak 10.736 kasus dan kegiatan investigasi terhadap harta benda sebanyak 10.584 kasus.

# **Berapa persen perbandingan antara kasus insiden kriminal dengan adanya penembakan dan tidak ada penembakan?**
## Insight
Kolom shooting terdiri dari value 'Y' yang menyatakan insiden kriminal yang dicatat disertai terjadinya penembakan, persentasenya sebesar 99.67% sedangkan yang diberikan value 'N' yaitu yang tidak disertai penembakan berpresentase 0.33%

# **Bagaimana perubahan trend kriminalitas dari waktu ke waktu?**
Berdasarkan data klinis yang dikumpulkan oleh National Confidential Inquiry into Suicide and Safety in Mental Health (NCISH), Pelanggaran/tindak kriminal lebih mungkin terjadi pada akhir pekan, sebagian besar pada hari Sabtu [sumber: Jurnal "Do homicide rates increase during weekends and national holidays?",2019](https://www.researchgate.net/publication/332279464_Do_homicide_rates_increase_during_weekends_and_national_holidays)
Untuk itu saya akan mencoba uji hipotesis dengan one sample z-test dengan hipotesis :
- H0 : persentase tindakan kriminal yang terjadi pada weekend = 0.28 (2/7 (jumlah weekend/jumlah hari))
- Ha : persentase tindakan kriminal yang terjadi pada weekend != 0.28 (2/7 (jumlah weekend/jumlah hari))
- Hasil:
pvalue =2.9689318061383294e-55, pvalue < 0.05, berhasil menolak Ho')
kita punya cukup bukti untuk mengatakan bahwa tindakan kriminal yang terjadi pada weekend tidak sama dengan 0.28
(proporsi berbeda signifikan)
## Insight
- Berdasarkan hasil uji one sample z-test dapat diambil kesimpulan bahwa tindakan kriminal sering terjadi di weekday dibandingkan di weekend
- Persentase tindakan kriminal yang terjadi pada weekend tidak lebih banyak dibandingkan weekday, dibuktikan dengan Uji Hipotesis dan Pie Chart yang ditampilkan. Hal ini juga dipengaruhi faktor bahwa weekend hanya berjumlah 2 hari yaitu hari sabtu dan hari minggu, sedangkan weekday terdapat 5 hari dalam seminggu.
- jumlah insiden kriminal yang terjadi di hari sabtu dan hari minggu berjumlah sekitar 40.000-43.000, lebih rendah dibandingkan weekday yaitu sekitar 46.000 - 49.000 kasus
- berdasarkan hari per minggu, rata-rata kriminalitas paling sering terjadi di hari jumat dan paling sedikit di hari minggu.  Di hari senin jumlahnya lebih sedikit dibandingkan hari weekday lainnya. Rata-rata terjadi 39-42 kasus per hari saat weekday dan 32-35 kasus per hari saat weekend

# Rekomendasi:
1. Sistem pencatatan bedasarkan incident number diharapkan lebih rapi lagi. 1 Incident number diharapkan dapat mewakili satu pelaporan dengan offense group yang berbeda.
2. Tidak ada perbedaan signifikan antara tingkat kriminalitas per harinya, sehingga diharapkan untuk kepolisian Boston Police Department membuat program yang direncanakan yang sama untuk di setiap harinya, tanpa perlu adanya patroli khusus di hari-hari tertentu.
3. Selama periode 15 Juni 2015-3 September 2018, angka kriminalitas di kota Boston cenderung stabil. Namun hal tersebut bisa juga karena upaya yang diterapkan oleh Boston Police Department belum efektif untuk menekan turunnya angka kriminalitas di kota Boston. Maka dari itu, direkomendasikan untuk melakukan upaya tambahan sesuai konstitusi negara Amerika Serikat maupun negara bagian Massachusetts.
4. Direkomendasikan agar penanganan kriminalitas dilakukan tanpa campur tangan senjata api sehingga membuat masyarakat nyaman karena tindakan polisi yang sebelumnya cenderung terlihat represif terhadap pelaku kejahatan yang dapat terlihat dari adanya penanganan kriminalitas dengan penembakan sebesar 99.67%.
5. Distrik B2 merupakan distrik dengan tingkat kriminalitas tertinggi dibandingkan dengan 11 distrik lainnya di Boston. Sehingga diharapkan polisi Boston harus mengerahkan lebih banyak polisi untuk berpatroli dan menjaga distrik ini. Di Distrik B2 sering terjadi kelompok kejahatan 'respon kecelakaan kendaraan bermotor' pada pagi hari sekitar pukul 5 pagi hingga 12 siang. Diharapkan pihak kepolisian memasang CCTV untuk memantau arus lalu lintas di titik rawan pelanggaran lalu lintas ini. Boston memiliki teknologi untuk menata ulang jalanannya. Di jalan pintar, kami menggunakan teknologi - seperti kamera dan sensor - untuk mempelajari lebih lanjut tentang bagaimana orang menavigasi dan berinteraksi di jalan-jalan kota. Pekerjaan terbaru kami berfokus pada keselamatan jalan raya. Namun untuk kamera tilang elektronik seperti lampu merah dan kamera kecepatan, masih ilegal di Boston. Diharapkan tilang elektronik ini dapat dipertimbangkan oleh pihak kepolisian untuk diajukan sebagai hal yang legal kepada pemerintah.
6. Tindakan kepolisian yang paling banyak dilakukan selama periode waktu 15 Juni 2015-3 September 2018 adalah investigasi, baik kepada orang maupun harta benda. Maka kepolisian Boston dapat menambahkan jumlah staff di divisi investigasi, agar apabila ada banyak kasus, kepolisian tidak kekurangan staff. kemudian yang terbanyak kedua adalah tindakan kepolisian berupa bantuan medis kepada individu di tempat kejadian perkara, maka diharapkan polisi memiliki skill pemberian pertolongan pertama yang dapat dilakukan di TKP sambil menunggu petugas medis tiba. Kepolisian Boston dapat mengadakan program pelatihan pertolongan pertama seperti DRSABC, yaitu kepanjangan dari Danger, Response, Shout, Airway, Breathing, Circulation. 
