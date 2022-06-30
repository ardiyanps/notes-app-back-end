Membuat akun aws
https://aws.amazon.com/

- Anda akan diarahkan ke halaman pendaftaran akun. Silakan isi email dan nama akun AWS Anda. Jika selesai, klik tombol Verify email address.
- Selanjutnya cek inbox email yang didaftarkan, tuliskan kode verifikasi yang Anda dapat pada halaman registrasi yang tampak, dan klik tombol Verify.
- Setelah verifikasi email berhasil, buatlah password untuk akun AWS Anda dan klik tombol Continue.
- Anda akan diarahkan ke halaman Contact Information. Pada opsi Account Type pilih Personal. Lalu isikan data pribadi Anda dengan lengkap. Setelah selesai, klik Continue.
- Di halaman selanjutnya, Anda diharuskan mengisi informasi pembayaran melalui kartu debit/kredit. Anda juga bisa menggunakan virtual credit card yang disediakan beberapa bank di Indonesia. Jika sudah, maka Anda bisa langsung klik Verify and Continue.
- Jika kartu debit/kredit Anda valid, maka Anda akan diarahkan ke halaman selanjutnya. Silakan masukkan nomor telepon Anda dan isi security check sesuai pada layar Anda masing-masing, lalu klik Send SMS.
- Masukkan kode verifikasi yang dikirim Amazon ke ponsel Anda. Lalu klik Verify Code. Bila Verifikasi berhasil Anda akan diarahkan ke halaman Support Plan.
- Di halaman ini ada beberapa opsi Plan. Basic Plan, Developer Plan, dan Business Plan. Silakan pilih yang Basic Plan dengan klik tombol Free dan Complete sign up.
- Selamat! Akun AWS Anda sudah selesai dibuat. Dengan itu, Anda bisa mulai menggunakan banyak layanan AWS seperti Amazon EC2. Jika Anda ingin masuk ke console, silakan klik Go to the AWS Management Console.

Membuat IAM Users
https://aws.amazon.com/

- Klik tombol Sign In to the Console
- Pilih opsi masuk menggunakan Root user, tuliskan email akun AWS Anda, dan pilih tombol Next.
- Karena Ohio (Amerika Serikat) letaknya cukup jauh dengan Indonesia, kita akan mengubah Region ke yang lebih dekat agar mendapatkan latensi rendah. Untuk mengubahnya, silakan klik teks “Ohio” dan pilih Regionnya menjadi “Asia Pacific (Singapore) ap-southeast-1”.
  Catatan: Anda juga bisa memilih region ap-southeast-3 (Jakarta) yang barus saja hadir. Namun, kami rekomendasikan Anda tetap gunakan region ap-southeast-1 (Singapore) agar selaras dengan modul pembelajaran kelas ini.
- Yuk, sekarang kita mulai buat IAM Users. Silakan klik All services, kemudian lihat kategori Security, Identity, & Compliance.
- Pilih menu IAM. 
- Setelah itu, Anda akan diarahkan pada IAM dashboard.
- Lihat panel samping kiri, pilih menu Users.
- Kemudian klik tombol Add user. Anda akan diarahkan ke halaman pembuatan user baru.
Silakan berikan nilai:

User name : <isi dengan username yang Anda inginkan>
Access type : AWS Management Console access.
Console password : Custom password. Kemudian isi password Anda.
Require password reset : uncheck. 

Setelah semua terisi, klik Next: Permissions.
- Berdasarkan pilihan yang ada, kita akan memilih opsi pertama. Namun untuk menggunakannya, kita perlu membuat user group terlebih dahulu. Silakan klik Create group.
- Isi Group name dengan “Developer”. Kemudian berikan permission untuk AmazonEC2FullAccess. Anda bisa memanfaatkan search box untuk mencari permission-nya.
- Setelah semuanya terisi dan terpilih dengan benar, klik Create group.
- Lanjut klik Next: Tags.
- klik Next: Review.
- Jika semua sudah sesuai, klik Create User.
Voila! User berhasil dibuat. Silakan unduh .csv untuk mendapatkan kredensial user baru. Gunakan kredensial tersebut untuk masuk ke AWS Management Console.

Simpanlah berkas .csv pada tempat yang aman. Untuk melihat kredensialnya, Anda bisa buka berkas .csv yang diunduh dengan menggunakan Notepad ataupun Text Editor lainnya.

- Untuk login menggunakan IAM user, silakan logout dari root user Anda. 
- Kemudian kunjungi alamat login link yang terdapat pada berkas .csv. 
- Isilah username dan password IAM user sesuai yang Anda buat. Kemudian klik Sign in.
- Well Done! Anda berhasil masuk dengan akun IAM User. Selanjutnya kita bisa mulai membuat dan menjalankan Amazon EC2.


Membuat dan menjalankan Amazon EC2 Instance

- Untuk membuat EC2 Instance, silakan akses menu All Services -> Compute -> EC2.
- Atau, Anda bisa juga mencarinya menggunakan kolom pencarian yang ada di bar atas.
- Gulir jendela browser ke bawah dan Anda akan melihat tombol Launch Instance.
- Klik tombol tersebut dan pilih Launch instance untuk membuat EC2 instance.

Silakan isi formulir yang tersedia dengan nilai dan instruksi berikut.

1. Name and tags: Web Server
2. Application and OS Images: Ubuntu Server (LTS terbaru) Free tier eligible.
3. Instance type: t2.micro (Free tier eligible)
4. Key pair (login):
    - Klik Create new key pair.
    - Key pair name: notes-api-webserver.
    - Klik Create key pair.
    - Pastikan berkas notes-api-webserver.pem terunduh.
    - Simpan berkas pem yang terunduh pada lokasi yang aman. Karena berkas ini digunakan ketika hendak mengoperasikan instance melalui SSH, jadi jangan sampai hilang yah. Agar mudah, taruh saja berkas tersebut di dalam folder proyek notes-app-back-end.

5. Network settings:
    - Klik Edit.
    - Security group name: app-server-sg.
    - Description: Allow custom TCP port 5000
    - Klik Add security group rule.
    - Isi security group baru dengan nilai:
        - Type: Custom TCP
        - Port range: 5000
        - Source type: Anywhere
        - Description: Application Port

6. Klik Launch Instance.
7. Voila! EC2 instance berhasil dibuat dan berjalan! Anda bisa melihat statusnya dengan mengeklik tombol View Instances.

Penjelasan: Di bagian Network settings kita menentukan cara atau jalur apa saja untuk mengakses EC2 Instance yang dibuat. Secara default, AWS menambahkan SSH pada security group. Jalur SSH ini digunakan nanti oleh kita untuk mengoperasikan EC2 secara remote.

Selain SSH, kita juga menambahkan security group lainnya agar web server kita dapat diakses secara publik. Yakni membuka TCP port 5000 (sesuai dengan yang digunakan oleh web server), dan source-nya Anywhere.

Anda bisa lihat status dari instance tersebut adalah Running. Selanjutnya kita akan coba mengoperasikan instance melalui SSH.


Mengoperasikan EC2 Instance Melalui SSH

- Kembali ke halaman EC2 instance.
- Pada halaman daftar instance, pilih instance yang baru saja kita buat.
- Pilih tombol Connect yang berada di atas,
- Di sini Anda bisa melihat beberapa opsi dalam mengakses EC2 Instance. Untuk mendapatkan informasi bagaimana mengakses melalui SSH, pilih tab SSH client.
- Silakan salin perintah yang berada di example, lalu paste perintah tersebut pada Terminal/PowerShell/CMD di folder tempat Anda meletakkan berkas pem.
- Tekan Enter untuk mengeksekusi perintah.
Whops! Ada eror. Dari pesan eror tersebut menjelaskan bahwa berkas notes-api-webserver.pem miliki permission yang terlalu terbuka. Ini tidak aman untuk digunakan sebagai kunci dalam mengakses EC2 instance.

Solusinya, kita perlu mengubah permission pada berkas .pem tersebut. Silakan eksekusi perintah berikut (sesuaikan dengan sistem operasi yang Anda gunakan).
- Linux/macOS
    - chmod 400 notes-api-webserver.pem
- Windows
    $path = ".\notes-api-webserver.pem"
    # Reset to remove explicit permissions
    icacls.exe $path /reset
    # Give current user explicit read-permission
    icacls.exe $path /GRANT:R "$($env:USERNAME):(R)"
    # Disable inheritance and remove inherited permissions
    icacls.exe $path /inheritance:r
- Kemudian coba ulangi perintah yang sebelumnya ada pada example.
- Tada! Kita berhasil terhubung dengan EC2 instance melalui SSH. Anda bisa bebas mengoperasikan instance layaknya komputer Anda sendiri.
- Untuk keluar dari EC2 instance, Anda bisa gunakan perintah exit.


Mengonfigurasi Kebutuhan pada EC2 Instances
- Mengunduh Repository
Untuk mengunduh remote repository pada EC2 instance, tentu kita juga perlu memasang sistem git di EC2 instance. Good news! AMI yang kita gunakan (Ubuntu) telah terpasang sistem git secara built-in. Sehingga kita tidak perlu instal git secara mandiri. 

Untuk memastikan hal tersebut, silakan akses kembali EC2 instance menggunakan SSH di PowerShell/CMD/Terminal.
- ssh -i "notes-api-webserver.pem" ubuntu@ec2-54-1710.ap-southeast-1.compute.amazonaws.com
- Kemudian tuliskan perintah git --version.
- sudo apt-get install git 
- git clone <remote repository URL>
- Masuk ke folder proyek tersebut dengan menggunakan perintah.
    - cd notes-app-back-end 

Memasang Node.js dan Menjalankan Web Server di EC2 Instance
- Karena untuk menjalankan web server yang kita buat membutuhkan Node.js, tentu kita perlu memasang Node.js pada EC2 instance juga. Jadi ayo kita melangkah!

Sebelum Anda mulai memasang Node.js, pastikan versi yang digunakan Node.js di komputer Anda sama dengan Node.js yang akan dipasang di EC2 instance. Ini berguna untuk mencegah terjadinya bugs yang ditimbulkan oleh perbedaan versi Node.js, apalagi bila perbedaan versi tersebut cukup jauh. Untuk itu, kita cek dulu yuk versi Node.js apa yang digunakan pada komputer kita.

Silakan buka Terminal/CMD/PowerShell baru pada komputer Anda, lalu jalankan perintah node -v.
- Oke, catat yah versi yang muncul. Pastikan kita menggunakan versi yang sama untuk dipasang di EC2 instance.

Agar mudah mengatur versi Node.js yang digunakan pada EC2 instance, kita akan menggunakan tools yang bernama nvm. Melalui nvm ini, kita bisa dengan mudah mengubah versi Node.js yang ingin digunakan. Tools ini sangat membantu proses upgrade atau downgrade Node.js secara mudah.

Untuk memasang nvm pada Ubuntu, silakan eksekusi perintah berikut:

- curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
Tunggu hingga proses unduh dan instalasi selesai.
- Penting: Agar nvm dapat digunakan, silakan keluar dulu dari SSH dengan perintah exit. Kemudian akses kembali EC2 instance.

Selanjutnya pasang Node.js versi yang sesuai dengan komputer Anda dengan perintah:

nvm install <versi nodejs>
Contoh, bila ingin memasang versi v14.15.4, maka tuliskan:

nvm install v14.15.4
- Good job! Pastikan Node.js berhasil terpasang dengan mengeksekusi perintah node -v.
Well done! Node.js berhasil terpasang. Kini Anda bisa menjalankan web server. Pastikan Anda berada di dalam folder notes-app-back-end. Jika belum, silakan masuk ke foldernya dengan perintah:

- cd notes-app-back-end
- Lalu, pasang seluruh module/package dependencies yang digunakan pada proyek kita dengan mengeksekusi perintah npm install.

- Lanjut, jalankan proyek dengan perintah npm run start.

- Wah tampaknya server sudah berjalan nih. Coba kita cek melalui browser. Silakan kunjungi alamat ip http://172.31.26.251:5000 yang merupakan IP server EC2 instance (lihat alamat IP pada Terminal). Apakah ada respons dari server?

Memperbaiki Bugs

Kita kira server sudah dapat dijalankan dengan baik oleh nodemon pada EC2 instance. Tapi nyatanya masih belum bisa diakses secara publik. Lantas bagaimana solusinya?

Setelah ditelaah lebih dalam, ternyata IP yang kita kunjungi tadi bukanlah IP publik dari EC2 instance yang dapat diakses secara umum. Lalu bagaimana cara mengetahui IP publik dari EC2 instance yang kita buat? Mudah! Silakan kunjungi kembali halaman daftar EC2 instance pada AWS Management Console, lalu pilih EC2 instance yang Anda buat.

Pada instance summary, kita bisa lihat public IPv4 address. Apakah dengan IP tersebut kita bisa mengakses web server? Kita coba saja kunjungi alamat public dari IPv4 address Anda, dan pastikan pada SSH nodemon sedang berjalan mengeksekusi web server yah.

Argh! Ternyata masih belum bisa diakses. Bagaimana ini? Apalagi yang salah?

Well. Ternyata kita tidak bisa menggunakan host dengan nilai localhost untuk menjalankan Hapi server pada EC2 instance. Kita perlu menjelaskan secara eksplisit private IP yang digunakan oleh instance, di mana IP tersebut pada summary instance dijelaskan bernilai 172.31.36.19.

Tetapi menetapkan nilai host dengan alamat IP yang eksplisit seperti itu bukanlah hal yang baik. Kenapa? Karena ketahuilah nilai IP (baik public atau private) dapat berubah. Perubahan bisa terjadi karena pindah server atau me-restart server. Kita tidak dapat menjamin kapan perubahan tersebut bisa terjadi. Apakah Anda mau setiap kali IP berubah, kode Anda juga harus diubah? Repot sekali bukan. Lalu bagaimana solusinya?

Solusinya adalah gunakan IP beralamat 0.0.0.0. Alamat tersebut merupakan alamat spesial yang digunakan agar komputer dapat diakses melalui seluruh alamat IP yang digunakan pada komputer tersebut. Misalnya begini, bila komputer Anda tersambung ke jaringan Wi-Fi dengan IP 192.168.100.25 dan LAN dengan IP 172.31.90.21, maka 0.0.0.0 dapat diakses melalui kedua alamat IP tersebut. Sudah paham?

Dengan begitu di production kita dapat menggunakan alamat spesial ini untuk menghindari masalah perubahan IP. Karena bila alamat IP berubah, maka nilai 0.0.0.0 tetap aman untuk digunakan.

Oh ya! Bila kita mengubah nilai localhost menjadi 0.0.0.0, bagaimana nasib ketika proses development kita menginginkan ia hanya dapat dijalankan di localhost? Apakah kita ubah saja nilai ip-nya secara manual pada EC2 instance tanpa melalui remote repository? Ah, itu bukan praktik yang baik.

Lalu, adakah cara yang dapat membedakan penggunaan nilai ketika proses development dan production di EC2 instance? Jawabannya ada! Masih ingatkan dengan global objek process.env? Di sana kita dapat meletakan suatu nilai ketika proses node dijalankan. Yuk langsung saja perbaiki proyek web server kita.

- Kembali ke VSCode dan buka berkas server.js.

- Ubah nilai properti host menjadi seperti ini: 

 const server = Hapi.server({
  port: 5000,
  host: process.env.NODE_ENV !== 'production' ? 'localhost' : '0.0.0.0',
  routes: {
    cors: {
      origin: ['*'],
    },
  },
});
Dengan begitu, properti host akan bernilai sesuai dengan environment yang ditetapkan.

- Selanjutnya kita tetapkan environment pada npm runner script. Buka berkas package.json, dan atur npm runner script menjadi seperti ini:

"scripts": {
  "start-prod": "NODE_ENV=production node ./src/server.js",
  "start-dev": "nodemon ./src/server.js",
  "lint": "eslint ./src"
},
Kita tidak perlu menetapkan NODE_ENV pada start-dev karena nodemon secara default menggunakan nilai development pada NODE_ENV. Karena itu juga, pada proses production kita tidak menggunakan nodemon lagi, cukup gunakan node saja.

- Simpan seluruh perubahan, kemudian commit seluruh perubahan yang ada dengan perintah:

- git add .
- git commit -m "fix bugs host value"
- Kemudian push perubahannya pada remote repository dengan perintah:

- git push origin master 

- Selanjutnya, akses kembali EC2 instance melalui SSH dan masuk ke folder notes-app-back-end.

- Update proyek web server dengan perubahan yang sudah dilakukan sebelumnya dengan menggunakan perintah:

- git pull origin master

- Coba jalankan kembali servernya, namun kali ini menggunakan proses production. Eksekusi perintah npm run start-prod.

- Silakan akses server melalui browser dengan menggunakan alamat IP publik beserta port 5000.

- Voila! Akhirnya kita bisa melihat pesan not found yang dihasilkan oleh Hapi. Ini artinya server kita sudah berhasil berjalan di EC2 dan dapat diakses oleh publik. Selamat yah!


Process Manager
Saat ini web server kita sudah bisa diakses secara publik melalui internet. Untuk memastikan web server berfungsi dengan baik, silakan hubungkan aplikasi client dengan URL web server terbaru kita.

Silakan coba-coba fungsionalitas dari aplikasi tersebut. Pastikan semua berjalan dengan normal.

Selama web server sedang digunakan, pastikan juga proses node pada EC2 selalu tetap berjalan yah.

BIla proses node tersebut terhenti, itu bisa dikarenakan Anda tak sengaja menghentikannya atau session SSH berakhir, maka web server pun akan terhenti. Bila web server terhenti, maka otomatis aplikasi client tidak dapat digunakan.

Bayangkan bila ini terjadi pada implementasi di dunia nyata? Tentu akan merepotkan bisnis Anda. Karena agar server dapat berjalan kembali kita perlu masuk ke SSH dan menjalankan kembali perintah npm run start-prod. Sungguh tahapan yang tidak praktis. Kita tidak ingin menghabiskan waktu dan tenaga untuk melakukan hal itu berulang kali.

Bila Anda tidak bersedia untuk menjaga server tetap hidup, berarti sebagai gantinya kita harus mencari seseorang yang mau melakukannya. Tapi pertanyaannya, siapa yang mau? Ada kok, terlebih lagi ia mau bekerja tanpa bayaran. Perkenalkan, Process Manager.

Process Manager dapat menangani permasalahan di atas. Dengan menggunakan Process Manager, Anda tidak perlu khawatir bila aplikasi Node.js terhenti disebabkan oleh crash, ia akan menjalankan ulang prosesnya secara otomatis hampir tanpa downtime. Selain itu, Process Manager dapat membantu menyeimbangkan muatan proses pada CPU yang tersedia di server, hal ini biasa disebut sebagai load balancing. Dengan begitu, aplikasi server dapat diakses secara lebih cepat dibandingkan dijalankan menggunakan node process secara langsung.

- Memasang Node.js Process Manager pada EC2 instance
- PM2 merupakan salah satu Node.js Process Manager yang populer digunakan. Kita akan menggunakan pm2 ini untuk memantau web server yang ada di EC2 instance.

- Silakan akses kembali EC2 instance melalui SSH. Kemudian pasang pm2 dengan perintah npm install -g pm2.

- Setelah proses install selesai, masuk ke directory notes-app-back-end dengan perintah cd notes-app-back-end. Jalankan node process menggunakan pm2 dengan perintah:

- pm2 start npm --name "notes-api" -- run "start-prod" 

Pm2 berhasil menjalankan web server dan ia akan memantau prosesnya. Bila proses itu terhenti entah karena terjadi crash atau apa pun, ia akan secara otomatis menjalankan ulang proses. Dengan begitu, Anda tidak perlu khawatir server Anda mengalami downtime lagi.

- Di pm2, kita dapat me-restart proses secara manual dengan cara:
pm2 restart notes-api
- Atau, menghentikan prosesnya dengan cara:
pm2 stop notes-api
- Untuk menjalankan kembali proses, gunakan perintah:
pm2 start notes-api

Ikhtisar
Anda berada di akhir dari modul Deploy Web Services. Mari kita uraikan materi yang sudah Anda pelajari untuk mempertajam pemahaman.

Anda dapat membuat akun AWS.
Anda sudah mengenal apa itu Amazon EC2.
Anda dapat membuat dan meluncurkan Amazon EC2.
Anda dapat menggunakan Amazon EC2 dengan teknik remote melalui SSH.
Anda dapat menggunakan Git pada proyek web service yang dibuat.
Anda dapat membuat akun Github.
Anda dapat mengunggah repository git ke Github.
Anda dapat menyiapkan kebutuhan deployment pada Amazon EC2.
Anda dapat men-deploy web service ke Amazon EC2.
Anda dapat memasang Process Manager pada Amazon EC2.
Dengan ringkasan tersebut, diharapkan Anda dapat memahami semua materi yang telah disampaikan. Jika belum, Anda bisa ulas kembali materi yang diberikan pada modul ini. Untuk Anda yang sudah merasa mantap, yuk lanjut ke modul berikutnya!