<img width="1920" height="1080" alt="Screenshot (271)" src="https://github.com/user-attachments/assets/8baf3c58-b803-45be-b802-0fa45bd83a83" />
Saya menambahkan satu PC baru (PC-C) di S1 pada port Fa0/8, lalu saya aktifkan kembali port tersebut (no shutdown) dan memasukkannya ke VLAN 30 (Guest). Setelah itu konfigurasi VLAN dan trunk tetap saya lanjutkan seperti instruksi modul.

<img width="1920" height="1080" alt="Screenshot (272)" src="https://github.com/user-attachments/assets/e2299af5-f1a6-49b1-aa10-dbe29b967bcf" />
Saya melakukan ping dari S1 ke S2 dan awalnya hanya berhasil 60%, lalu setelah saya ulang hasilnya 100% yang menandakan koneksi VLAN 1 sudah stabil. Ketika saya ping dari S1 ke PC-A hasilnya 0% karena PC-A berada di VLAN berbeda, sementara S1 hanya berada di VLAN 1 sehingga tanpa router komunikasi antar VLAN memang tidak bisa dilakukan.

<img width="1920" height="1080" alt="Screenshot (274)" src="https://github.com/user-attachments/assets/de589563-3335-4d09-b2e8-e38c9f706f78" />
Hasil show ip interface brief menunjukkan hanya VLAN 1 di S1 yang aktif, sedangkan VLAN 99 masih down karena belum ada port yang masuk ke VLAN tersebut. Ping ke 192.168.1.12 gagal karena IP itu sudah dipindah dari VLAN 1 ke VLAN 99 sehingga S1 tidak bisa menjangkaunya lagi.

<img width="1920" height="1080" alt="Screenshot (275)" src="https://github.com/user-attachments/assets/43cdeb52-face-47f2-ae73-8f7cc17966ee" />
Hasil konfigurasi menunjukkan bahwa trunk pada Fa0/1 sudah berjalan dan seluruh VLAN (1,10,20,99,1000) ikut melewati trunk tersebut. Saat saya melakukan ping dari S1 ke S2, percobaan pertama hanya berhasil 60%, lalu percobaan kedua berhasil 100%, menandakan trunk sudah stabil. PC di VLAN 10 hanya bisa saling ping sesama VLAN 10, tetapi tidak bisa ping ke switch karena switch menggunakan VLAN 99. Perbedaan VLAN inilah yang membuat ping antar perangkat beda VLAN tidak berhasil.

<img width="1920" height="1080" alt="Screenshot (277)" src="https://github.com/user-attachments/assets/596ac0f0-935c-46af-bf80-49c93fbfc3f8" />
Pada tampilan Command Prompt PC-A terlihat bahwa ping ke PC-B (192.168.10.4) berhasil karena keduanya berada di VLAN yang sama, yaitu VLAN 10, sehingga komunikasi masih dalam satu broadcast domain. Namun saat PC-A mencoba ping ke 192.168.1.11 dan 192.168.1.12, seluruh paket gagal. Penyebabnya bukan karena kesalahan konfigurasi, tetapi karena kedua alamat tersebut berada pada VLAN berbeda (VLAN 1 atau VLAN 99), sedangkan PC-A berada di VLAN 10. Dalam tugas ini belum ada mekanisme untuk menghubungkan antar VLAN, sehingga wajar jika perangkat antar VLAN tidak saling menjangkau.

Jawaban dari pertanyaan TA = 
untuk memungkinkan host di VLAN 10 berkomunikasi dengan host di VLAN 99 dibutuhkan kemampuan inter-VLAN, yang biasanya disediakan oleh perangkat Layer 3. Namun pada materi ini fokus pada konsep dasar VLAN dan trunking tanpa router, komunikasi antar VLAN memang tidak diharapkan berhasil. Adapun manfaat utama VLAN tetap berlaku, yaitu meningkatkan keamanan, membatasi broadcast domain, mengoptimalkan kinerja jaringan, dan membuat pengelolaan jaringan lebih terstruktur.

