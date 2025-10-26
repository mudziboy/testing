# Bot Telegram Seller XL
Bot Telegram untuk keperluan penjualan/otomatisasi tembak paket, dengan fitur backup database ke Google Drive (opsional).

## 🚀 Instalasi

### 1. Clone Repository
```bash
git clone https://github.com/mudziboy/testing.git
cd testing
```

### 2. Edit Konfigurasi
Edit file `core/setup.json` dengan isi seperti berikut (sesuaikan token, userid, username, dan API):
```json
{
  "token": "token_bot_utama",
  "notifikasi": "token_bot_notifikasi",
  "notifikasi_username": "username_bot_notifikasi",
  "admin": {
    "userid": 123456789,
    "username": "username_admin"
  },
  "api": {
    "base_url": "https://api.st.tunnel.sistemtopup.shop",
    "email": "email@gmail.com",
    "password": "password"
  },
  "qris_string": "",
  "qris_path": "core/qris.png"
}
```

### 3. Ganti QRIS
**PENTING:** Sebelum menjalankan bot, ganti file `core/qris.png` dengan gambar QRIS milik Anda:
- Pastikan format file adalah PNG
- Ukuran disarankan minimal 500x500 piksel untuk kualitas yang baik
- Nama file harus tetap `qris.png` dan berada di dalam folder `core/`

### 4. (Opsional) Backup Google Drive dengan rclone
Jika ingin fitur backup database otomatis ke Google Drive:
- Install rclone:
    - **Linux:**  
      ```bash
      sudo apt install rclone
      ```
    - **Termux:**  
      ```bash
      pkg install rclone
      ```
- Buat file `core/backup.json` berisi service account Google Drive:
```json
{
  "type": "service_account",
  "project_id": "bot-1735382210111",
  "private_key_id": "xxx",
  "private_key": "-----BEGIN PRIVATE KEY-----\\n....\\n-----END PRIVATE KEY-----\\n",
  "client_email": "....@....iam.gserviceaccount.com",
  "client_id": "....",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/....",
  "universe_domain": "googleapis.com"
}
```
> **Catatan:**  
> Service account Google Drive hanya bisa backup ke Shared Drive (bukan My Drive).  
> Invite email service account ke Shared Drive, lalu atur `team_drive` di `rclone config` jika perlu.

### 5. Install Python & Requirements
- Install python3 (minimal 3.7)
- Install dependensi dari `requirements.txt`:
```bash
python3 -m venv venv
```
```bash
source venv/bin/activate
```
```bash
pip install -r requirements.txt
```

### 6. Jalankan Bot
```bash
python3 bot.py
```

#### **Jalankan di Background (opsional, agar tetap berjalan di server/termux)**
Gunakan [screen](https://linux.die.net/man/1/screen):
```bash
screen -S bot_telegram
python3 bot.py
```
- Untuk keluar dari screen tanpa mematikan bot, tekan:
  ```
  CTRL+A lalu CTRL+D
  ```
- Untuk masuk lagi ke screen:
  ```bash
  screen -r bot_telegram
  ```

---

## ✨ Selesai!
Bot siap digunakan.  
Jika ada masalah atau pertanyaan, silakan buka issue pada repository ini.

## FITUR BOT
ADMIN MENU
```
- Seting user 
  ├── Daftar User
  ├── Tambah User
  ├── Edit User (username, saldo, status)
  └── Hapus User
- Setting Produk
  ├── Daftar Produk
  └── Edit Produk (nama produk, kategori, harga, deskripsi, status)
- Setting Bot
  ├── setting status bot (open, close, maintenance)(private, public)
  ├── Kirim notifikasi ke user yang terdaftar
  ├── seting cara pembelian
  └── setting cara deposit
- Deposit Api
  └── Deposit Saldo panel web
```
USER MENU
```
- Otp Login
  └── cek sesi nomor, kirim otp, verifikasi otp, cek pulsa, cek kuota, pembelian produk
- Transaksi Terjadwal
  └── Jadwalkan transaksi otomatis di tanggal dan jam yang sudah di atur
- Sidompul Cek Kuota
  └── cek kuota untuk XL & Axis
- Deposit 
  └── Depsoit user mengubah qris statis menjadi qris dinamis
- Transaksi Pending
  └── daftar transaksi pending yang ada di transaksi terjadwal
- Riwayat transaksi
  └── notifikasi transaksi sukses akan di kirim pada bot notifikasi
```
  
