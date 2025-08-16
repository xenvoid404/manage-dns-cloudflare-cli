# Management DNS Cloudflare CLI

<div align="center">

[![Shell Script](https://img.shields.io/badge/Shell-Script-89e051?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://github.com/xenvoid404/manage-dns-cloudflare-cli)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)](https://cloudflare.com)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Version](https://img.shields.io/badge/Version-1.0.0-green?style=for-the-badge)](https://github.com/xenvoid404/manage-dns-cloudflare-cli/releases)

</div>

Script shell untuk mengelola DNS records Cloudflare melalui command line interface (CLI). Tool ini memungkinkan Anda untuk mengambil, membuat, memperbarui, dan menghapus DNS records dengan mudah menggunakan file JSON.

Script ini bisa dijalankan di lingkungan **Termux**, **Virtual Private Server (VPS)**, dan juga **Komputer**.

## 1. Fitur Utama

-   **Get Records**: Mengambil semua DNS records dan menyimpannya dalam format JSON
-   **Create Records**: Membuat DNS records baru dari file JSON dengan SSL provisioning otomatis
-   **Update Records**: Memperbarui DNS records yang sudah ada
-   **Delete Records**: Menghapus DNS records berdasarkan ID
-   **Auto SSL Provisioning**: Menggunakan temporary worker untuk memastikan SSL certificate ter-provision dengan benar

## 2. Instalasi

### Instalasi Menggunakan curl

Jalankan perintah berikut untuk mengunduh dan menginstal script:

```bash
apt install curl jq -y && curl -L -o dns https://raw.githubusercontent.com/xenvoid404/manage-dns-cloudflare-cli/refs/heads/master/dns && chmod +x ./dns && ls
```

## 3. Konfigurasi

Setelah mengunduh script, Anda **WAJIB** mengatur konfigurasi kredensial akun Cloudflare anda.

1. Buka file dns yang baru saja diunduh dengan editor teks. (misalnya nano):

```bash
nano ./dns
```

2. Cari bagian Konfigurasi Awal di baris paling atas skrip.
3. Ubah nilai variabel berikut dengan data Anda:

```bash
# Konfigurasi Awal (WAJIB DIISI)
CF_EMAIL="example@gmail.com"          # Ganti dengan email Cloudflare Anda
CF_API_KEY="YOUR_CLOUDFLARE_API_KEY"  # Ganti dengan Global API Key Cloudflare
ZONE_ID="YOUR_ZONE_ID"                # Ganti dengan Zone ID domain Anda
```

### Cara Mendapatkan Kredensial Cloudflare

1. **Email**: Email yang digunakan untuk login ke akun Cloudflare
2. **Global API Key**:
    - Login ke [Cloudflare Dashboard](https://dash.cloudflare.com)
    - Klik profil Anda → "My Profile" → "API Tokens"
    - Scroll ke bawah dan klik "View" pada "Global API Key"
3. **Zone ID**:
    - Pilih domain di Cloudflare Dashboard
    - Scroll ke bawah, salin "Zone ID"

## 4. Penggunaan

> **⚠️ Penting**:
>
> -   Semua perintah script harus dijalankan di direktori yang sama dengan tempat file script berada
> -   File JSON berisi data DNS juga sebaiknya disimpan di direktori yang sama dengan script

### • Get Record DNS

Mengambil semua record DNS dan menyimpannya ke records.json.

```bash
./dns get
```

### • Create (Membuat) Record DNS

Membuat satu atau lebih record DNS baru berdasarkan data dari file JSON.

```bash
./dns create records.json
```

### • Update (Memperbarui) Record DNS

Memperbarui record DNS yang ada. Pastikan field id untuk setiap record ada di dalam file JSON Anda.

```bash
./dns update records.json
```

### • Delete (Menghapus) Record DNS

Menghapus record DNS. Operasi ini juga membutuhkan field id di dalam file JSON.

```bash
./dns delete records.json
```

## 5. Tips Penggunaan

### Mendapatkan File JSON Lengkap

Sebelum melakukan operasi create, update, atau delete, disarankan untuk menjalankan perintah `get` terlebih dahulu:

```bash
./dns get
```

Ini akan menghasilkan file `records.json` dengan struktur yang lengkap dan benar. Anda dapat menggunakan file ini sebagai template untuk operasi selanjutnya.

### Contoh File JSON

Untuk melihat contoh struktur file JSON, Anda dapat mengecek folder `example` di repository ini:

-   📁 [Folder Example](https://github.com/xenvoid404/manage-dns-cloudflare-cli/tree/master/example)

## 📋 Format JSON

Struktur file JSON untuk DNS records:

```json
[
    {
        "id": "record_id_disini",
        "type": "A",
        "name": "subdomain",
        "content": "192.168.1.1",
        "ttl": 300,
        "proxied": false
    },
    {
        "type": "CNAME",
        "name": "www",
        "content": "example.com",
        "ttl": 1,
        "proxied": true
    }
]
```

### Catatan Penting tentang Field `id`:

-   **Create**: Field `id` **tidak perlu** disertakan
-   **Update/Delete**: Field `id` **wajib** ada dan harus valid
-   **Get**: Akan menghasilkan semua records dengan field `id` yang lengkap

## 6. Troubleshooting

### Error "Command not found"

Pastikan script memiliki permission execute:

```bash
chmod +x ./dns
```

### Error "File not found"

Pastikan file JSON berada di direktori yang sama dengan script dan nama file sudah benar.

### Error Authentication

Periksa kembali konfigurasi `CF_EMAIL`, `CF_API_KEY`, dan `ZONE_ID` di dalam script.

### Error Dependencies

Jika `curl` atau `jq` tidak terinstal:

```bash
apt install curl jq -y
```

## 7. Kontribusi

Kontribusi sangat diterima! Silakan:

1. Fork repository ini
2. Buat feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

## 8. Lisensi

Project ini dilisensikan di bawah MIT License - lihat file [LICENSE](LICENSE) untuk detail.

## 9. Author

**Xenvoid 404**

-   GitHub: [@xenvoid404](https://github.com/xenvoid404)
-   Repository: [manage-dns-cloudflare-cli](https://github.com/xenvoid404/manage-dns-cloudflare-cli)

## 10. Support

Jika Anda mengalami masalah atau memiliki pertanyaan:

-   🐛 [Report Bug](https://github.com/xenvoid404/manage-dns-cloudflare-cli/issues)
-   💡 [Request Feature](https://github.com/xenvoid404/manage-dns-cloudflare-cli/issues)
-   💬 [Discussions](https://github.com/xenvoid404/manage-dns-cloudflare-cli/discussions)

---

⭐ **Jika script ini membantu Anda, jangan lupa untuk memberikan star di repository ini!**
