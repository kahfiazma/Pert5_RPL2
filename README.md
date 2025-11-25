Spring Boot adalah framework Java yang dibangun di atas Spring Framework untuk 
mempermudah proses pembuatan aplikasi berbasis Spring. 
Jika framework Spring biasa membutuhkan banyak konfigurasi manual (misalnya file 
XML atau setup Bean secara manual), maka Spring Boot menyederhanakan semua itu 
dengan: 
• Konfigurasi otomatis (Auto Configuration) 
• Starter dependencies (starter packs) 
• Embedded server (misalnya Tomcat, Jetty, dsb, langsung bisa jalan tanpa setup 
tambahan) 
Keuntungan Spring Boot: 
• Cepat dan Mudah Dimulai 
Tidak perlu konfigurasi panjang. Cukup beberapa baris kode, aplikasi sudah 
bisa dijalankan. 
• Auto Configuration 
Spring Boot otomatis menyesuaikan konfigurasi berdasarkan dependency 
yang kamu pakai (contohnya: jika kamu pakai spring-boot-starter-web, 
otomatis disiapkan controller, dispatcher servlet, dsb). 
• Starter Dependencies 
Paket siap pakai seperti: 
o spring-boot-starter-web (untuk web API) 
o spring-boot-starter-data-jpa (untuk database) 
o spring-boot-starter-security (untuk keamanan) 
Jadi tidak perlu mencari dan mencocokkan library satu per satu. 
• Embedded Server 
Tidak perlu install atau deploy ke Tomcat/Jetty secara manual — bisa 
langsung dijalankan dari IDE atau command line. 
• Microservices Ready 
Sangat cocok untuk membuat microservices, karena ringan, independen, dan 
mudah dijalankan secara terpisah. 
• Monitoring & Metrics 
Dilengkapi fitur Actuator untuk memantau kesehatan aplikasi (health check, 
metrics, logs, dsb). 

Program ini merupakan sebuah aplikasi berbasis Spring Boot yang digunakan 
untuk mengelola data mahasiswa melalui tampilan berbasis console. Framework utama 
yang digunakan adalah Spring Boot, sedangkan pengelolaan data dilakukan 
menggunakan Spring Data JPA yang terhubung dengan database MySQL, dengan 
penerapan sederhana dari konsep MVC (Model-View-Controller). Tujuan dari program 
ini adalah mempermudah proses penyimpanan, pengambilan, dan pengecekan data 
mahasiswa tanpa harus menulis query SQL secara manual, karena seluruh proses 
tersebut sudah ditangani otomatis oleh Spring Boot dan JPA. 
Program diawali dari kelas utama Pertemuan5SpringBootApplication yang 
diberi anotasi @SpringBootApplication. Anotasi ini merupakan gabungan dari tiga 
anotasi 
penting, 
yaitu 
@Configuration, 
@EnableAutoConfiguration, 
dan 
@ComponentScan, yang memungkinkan Spring Boot melakukan pendeteksian serta 
pengaturan otomatis terhadap semua komponen di dalam proyek, seperti controller, 
model, dan repository. Di dalam kelas ini terdapat method main() yang menjalankan 
perintah SpringApplication.run(...) untuk menginisialisasi aplikasi dan mengaktifkan 
konteks Spring. Setelah semua komponen siap, method run() yang berasal dari interface 
CommandLineRunner akan dipanggil secara otomatis. Di dalam method tersebut, 
program akan menjalankan tampilkanMenu() dari objek mhsController, yang berperan 
sebagai pengendali utama dalam aplikasi. 
Berikutnya, kelas MahasiswaController yang diberi anotasi @Controller berisi 
seluruh logika aplikasi yang berinteraksi langsung dengan pengguna melalui console. 
Kelas ini memiliki ketergantungan terhadap MahasiswaRepository, komponen yang 
bertugas berkomunikasi dengan database. Ketergantungan tersebut disuntikkan oleh 
Spring menggunakan anotasi @Autowired. Di dalam controller terdapat method 
tampilkanMenu(), yang berfungsi menampilkan daftar pilihan kepada pengguna. Menu 
tersebut memiliki beberapa opsi, yaitu menampilkan seluruh data mahasiswa, 
menambah mahasiswa baru, mengecek koneksi ke database, dan keluar dari program. 
Input dari pengguna dibaca menggunakan objek Scanner, dan setiap pilihan akan 
memanggil method yang sesuai dengan fungsi yang diinginkan. 
Apabila pengguna memilih untuk menampilkan seluruh data mahasiswa, 
method tampilkanSemuaMahasiswa() akan dijalankan. Method ini mengambil seluruh 
data dari database melalui fungsi findAll() pada MahasiswaRepository, kemudian 
menampilkannya di console. Jika data kosong, akan muncul pesan bahwa tidak ada data 
mahasiswa. Jika pengguna memilih untuk menambahkan mahasiswa baru, program 
akan menjalankan method tambahMahasiswa(), yang meminta input berupa NPM, 
nama, semester, dan IPK. Setelah data dimasukkan, program membuat objek dari kelas 
ModelMahasiswa dan menyimpannya ke database dengan memanggil fungsi save() 
dari repository. Selain itu, method cekKoneksi() digunakan untuk memastikan koneksi 
ke database berfungsi dengan baik dengan mencoba menjalankan findAll() dan 
menangani kemungkinan kesalahan koneksi. 
Kelas ModelMahasiswa berfungsi sebagai representasi dari tabel mahasiswa di 
dalam database. Kelas ini diberi anotasi @Entity dan @Table(name = "mahasiswa"), 
yang menandakan bahwa kelas tersebut merupakan entitas database. Di dalamnya 
terdapat atribut seperti id, npm, nama, semester, dan ipk, yang masing-masing 
dihubungkan dengan kolom pada tabel menggunakan anotasi @Column. Kolom id 
dilengkapi anotasi @Id dan @GeneratedValue(strategy = GenerationType.IDENTITY) 
agar nilainya dihasilkan otomatis oleh database. Kelas ini juga memiliki konstruktor, 
getter, setter, serta method toString() yang digunakan untuk menampilkan data 
mahasiswa dalam format teks yang mudah dibaca. 
Sementara itu, MahasiswaRepository adalah sebuah interface yang diberi 
anotasi @Repository. Interface ini memperluas JpaRepository<ModelMahasiswa, 
Long>, sehingga secara otomatis mendapatkan berbagai operasi dasar terhadap 
database seperti findAll(), save(), dan deleteById() tanpa perlu menulis query SQL 
secara eksplisit. Dengan pendekatan ini, pengelolaan data menjadi lebih efisien, mudah 
dibaca, dan tidak memerlukan logika database tambahan di dalam kode program. 
Selain 
kelas 
utama, 
terdapat 
juga 
file 
konfigurasi 
bernama 
application.properties yang berisi pengaturan koneksi ke database MySQL. File ini 
mencakup informasi penting seperti URL database, username, password, serta 
pengaturan Hibernate seperti spring.jpa.hibernate.ddl-auto=update, yang berfungsi 
membuat atau memperbarui struktur tabel secara otomatis sesuai dengan entitas yang 
ada di program. Pengaturan spring.jpa.show-sql=true digunakan agar setiap query SQL 
yang dijalankan oleh Hibernate dapat ditampilkan di console, sehingga memudahkan 
proses debugging. 
Seluruh dependensi atau pustaka eksternal dikelola menggunakan Maven 
melalui file pom.xml. Di dalamnya terdapat dependensi penting seperti spring-boot
starter-data-jpa untuk pengelolaan data, spring-boot-starter-web untuk keperluan 
pengembangan aplikasi web (jika dikembangkan lebih lanjut), mysql-connector-java 
untuk koneksi ke MySQL, dan spring-boot-starter-test untuk pengujian aplikasi. Selain 
itu, terdapat plugin spring-boot-maven-plugin yang memungkinkan aplikasi dijalankan 
langsung melalui perintah mvn spring-boot:run tanpa konfigurasi tambahan. 
Secara keseluruhan, alur program berjalan dengan cara berikut: saat aplikasi 
dijalankan, Spring Boot akan melakukan konfigurasi otomatis dan memuat semua 
komponen yang diberi anotasi. Setelah itu, method run() pada kelas utama akan 
dijalankan untuk memanggil controller yang menampilkan menu interaktif kepada 
pengguna. Pengguna dapat memilih opsi untuk melihat, menambahkan, atau mengecek 
koneksi data mahasiswa. Semua proses interaksi data dilakukan melalui repository 
yang berkomunikasi dengan database menggunakan JPA dan Hibernate. Dengan 
struktur ini, aplikasi menjadi lebih efisien, terstruktur, serta mudah dikembangkan lebih 
lanjut, misalnya dengan menambahkan antarmuka web tanpa perlu mengubah logika 
dasar program. 
Langkah-langkah Eksekusi Program 
• Program dijalankan → main() di Pertemuan5SpringBootApplication memulai 
konteks Spring Boot. 
• Spring Boot melakukan auto configuration dan mendeteksi semua komponen 
(@Controller, @Entity, @Repository). 
• Setelah semua bean siap, method run() otomatis dijalankan karena class ini 
mengimplementasi CommandLineRunner. 
• Di dalam run(), program memanggil mhsController.tampilkanMenu(). 
• Menu console muncul di layar: 
o Opsi 1: memanggil tampilkanSemuaMahasiswa() → ambil data dari 
DB lewat findAll(). 
o Opsi 2: memanggil tambahMahasiswa() → ambil input dari user → 
simpan ke DB lewat save(). 
o Opsi 3: memanggil cekKoneksi() → mencoba findAll() untuk tes 
koneksi. 
o Opsi 4: keluar dari program. 
• Selama program berjalan, Hibernate dan Spring Data JPA menangani semua 
interaksi SQL secara otomatis.
