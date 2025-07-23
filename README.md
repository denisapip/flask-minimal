# flask-minimal

flask-minimal adalah project starter sederhana berbasis Flask, dibuat untuk mempermudah kamu membangun aplikasi web yang bersih, simpel, dan efisien. Semua kode utama ada di satu file (`app.py`), dilengkapi dengan struktur HTML dasar serta file statis untuk styling dan JavaScript.


## Fitur
- Aplikasi berbasis satu file utama (`app.py`) yang memudahkan proses belajar dan pengembangan.
- Sudah tersedia struktur HTML dasar dengan tampilan yang minimalis dam JavaScript.
- Setup yang cepat dan tidak rumit, cocok untuk pemula maupun pengembangan cepat.
- Mudah dikembangkan sesuai kebutuhan proyek anda.

## Persiapan
```bash
sudo apt update
sudo apt install python3 python3-venv python3-pip -y
```

## Instalasi

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/flask-minimal.git
   cd flask-minimal
   ```

2. Create a virtual environment (recommended):
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run the app:
   ```bash
   python app.py
   ```

Setelah dijalankan, kamu bisa mengakses aplikasi melalui browser dengan membuka http://localhost:5000.

## Penggunaan

Project ini bisa langsung digunakan sebagai pondasi untuk membuat aplikasi web. Semua route dan logika program ada di dalam `app.py`, sehingga mudah untuk dimodifikasi. Kamu bisa menambahkan template, route baru, atau file statis lainnya sesuai dengan kebutuhanmu.

## Kustomisasi
Kamu bisa menyesuaikan bagian-bagian berikut:

 - Struktur HTML di `templates/index.html`
 - Tampilan dan gaya di `static/style.css`
 - Interaktivitas atau efek di `static/script.js`

Semua elemen ini bisa kamu ubah agar sesuai dengan desain dan fungsionalitas yang diinginkan.

## Lisensi
Project ini menggunakan lisensi MIT, yang berarti kamu bebas menggunakannya, memodifikasi, dan mengembangkan lebih lanjut.

## Kontribusi
Silakan fork repository ini dan kirim pull request jika kamu memiliki perbaikan atau penambahan fitur. Kalau ada ide atau saran, kamu juga bisa membuat issue agar bisa didiskusikan bersama.

Project ini dibuat dengan tujuan untuk tetap sederhana dan efisien, sangat cocok untuk memulai pengembangan aplikasi web kecil atau membuat prototype dengan cepat tanpa banyak kerumitan.


##OTOMATISASI

#Solusi: Jadikan Flask App kamu sebagai systemd Service

1. Cek struktur folder kamu dulu

Misalnya kamu berada di:

cd /home/ubuntu/flask-minimal/

Dan kamu jalankan Flask dengan:

source venv/bin/activate
python app.py

Maka kita tinggal bungkus itu ke dalam service.

2. Buat file systemd

Buat file baru:

sudo nano /etc/systemd/system/flaskapp.service

Isi dengan ini:

[Unit]
Description=Flask Minimal App
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/flask-minimal
Environment="PATH=/home/ubuntu/flask-minimal/venv/bin"
ExecStart=/home/ubuntu/flask-minimal/venv/bin/python app.py
Restart=always

[Install]
WantedBy=multi-user.target

>  Ganti /home/ubuntu/ sesuai dengan direktori tempat kamu clone repo-nya kalau beda.

3. Aktifkan servicenya

sudo systemctl daemon-reload
sudo systemctl enable flaskapp
sudo systemctl start flaskapp

Cek status:

sudo systemctl status flaskapp

Kalau berhasil, akan muncul active (running).

4. Reboot dan Coba Akses

Sekarang coba:

sudo reboot

Tunggu sebentar, lalu buka:

http://<public-ip-ec2>:5000

Harusnya langsung bisa diakses tanpa login lagi!


Kalau Gagal

Cek log dengan:

journalctl -u flaskapp -e

Pastikan port 5000 dibuka di Security Group AWS EC2
