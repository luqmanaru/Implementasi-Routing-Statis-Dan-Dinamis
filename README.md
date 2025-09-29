# Implementasi-Routing-Statis-Dan-Dinamis

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Contributors](https://img.shields.io/badge/contributors-1-green.svg)
![Forks](https://img.shields.io/badge/forks-0-lightgrey.svg)
![Stars](https://img.shields.io/badge/stars-0-yellow.svg)

Proyek ini berisi implementasi konfigurasi jaringan komputer dengan fokus pada routing statis dan dinamis menggunakan protocol RIP dan analisis perbandingannya dengan OSPF.

## 🌐 Topologi Jaringan

### Soal 1: Routing Statis

```
PC1 ---- R1 ---- R2 ---- PC2
```
<img width="827" height="588" alt="image" src="https://github.com/user-attachments/assets/8a51d97b-f634-441c-85b9-bc4d5c161cd7" />

| Perangkat | Interface | IP Address | Subnet Mask |
|-----------|-----------|------------|-------------|
| PC1 | - | 192.168.1.2 | 255.255.255.0 |
| R1 | GigabitEthernet0/0 | 192.168.1.1 | 255.255.255.0 |
| R1 | GigabitEthernet0/1 | 10.10.10.1 | 255.255.255.252 |
| R2 | GigabitEthernet0/0 | 192.168.2.1 | 255.255.255.0 |
| R2 | GigabitEthernet0/1 | 10.10.10.2 | 255.255.255.252 |
| PC2 | - | 192.168.2.2 | 255.255.255.0 |

### Soal 2: Routing Dinamis dengan RIP

```
PC1 ---- R1 ---- R2 ---- PC2
```

| Perangkat | Interface | IP Address | Subnet Mask |
|-----------|-----------|------------|-------------|
| PC1 | - | 192.168.1.2 | 255.255.255.0 |
| R1 | GigabitEthernet0/0 | 192.168.1.1 | 255.255.255.0 |
| R1 | GigabitEthernet0/1 | 10.0.0.1 | 255.255.255.0 |
| R2 | GigabitEthernet0/0 | 192.168.2.1 | 255.255.255.0 |
| R2 | GigabitEthernet0/1 | 10.0.0.2 | 255.255.255.0 |
| PC2 | - | 192.168.2.2 | 255.255.255.0 |

### Soal 3: Multi-Router dengan RIP

```
    PC1         PC2
     |           |
    R1 -- R3 -- R2
     |     |     |
    PC3   PC4   PC5
                |
               PC6
```
<img width="827" height="547" alt="image" src="https://github.com/user-attachments/assets/3536675e-0299-4041-8ef7-c2859735cb0a" />

| Perangkat | Interface | IP Address | Subnet Mask |
|-----------|-----------|------------|-------------|
| PC1 | - | 192.168.1.2 | 255.255.255.0 |
| PC2 | - | 192.168.1.3 | 255.255.255.0 |
| R1 | GigabitEthernet0/0 | 192.168.1.1 | 255.255.255.0 |
| R1 | GigabitEthernet0/1 | 10.0.0.1 | 255.255.255.0 |
| R1 | GigabitEthernet0/2 | 10.0.1.1 | 255.255.255.0 |
| PC3 | - | 192.168.2.2 | 255.255.255.0 |
| PC4 | - | 192.168.2.3 | 255.255.255.0 |
| R2 | GigabitEthernet0/0 | 192.168.2.1 | 255.255.255.0 |
| R2 | GigabitEthernet0/1 | 10.0.0.2 | 255.255.255.0 |
| R2 | GigabitEthernet0/2 | 10.0.2.1 | 255.255.255.0 |
| PC5 | - | 192.168.3.2 | 255.255.255.0 |
| PC6 | - | 192.168.3.3 | 255.255.255.0 |
| R3 | GigabitEthernet0/0 | 192.168.3.1 | 255.255.255.0 |
| R3 | GigabitEthernet0/1 | 10.0.1.2 | 255.255.255.0 |
| R3 | GigabitEthernet0/2 | 10.0.2.2 | 255.255.255.0 |

---

## 📝 Penjelasan Konfigurasi

### Soal 1: Routing Statis

Pada soal ini, kita mengimplementasikan routing statis antara dua router. Konfigurasi meliputi:
- Pengaturan IP address pada interface router
- Penambahan static route untuk mengarahkan traffic ke jaringan tujuan
- Pengaturan IP address pada PC beserta default gateway

Keuntungan menggunakan subnet /30 untuk koneksi antar router:
- Lebih hemat IP karena hanya membutuhkan 2 IP address
- Lebih efisien daripada menggunakan subnet /24 yang terlalu besar
- Tidak mempengaruhi kinerja routing selama konfigurasi benar

### Soal 2: Routing Dinamis dengan RIP

Pada soal ini, kita mengimplementasikan routing dinamis menggunakan protocol RIP (Routing Information Protocol). Konfigurasi meliputi:
- Pengaturan IP address pada interface router
- Aktivasi RIP version 2
- Penambahan network yang terhubung ke RIP
- Menonaktifkan auto-summary untuk mendukung VLSM

Masalah umum pada RIP dan solusinya:
1. Router belum diaktifkan untuk RIP: Pastikan semua router telah dikonfigurasi dengan perintah `router rip`
2. Ada jalur yang belum terdaftar: Tambahkan semua network yang terhubung dengan perintah `network`
3. IP address salah atau interface belum aktif: Periksa konfigurasi IP dan pastikan interface aktif dengan `no shutdown`
4. Pengaturan PC salah: Pastikan default gateway pada PC mengarah ke router yang benar

Kelemahan RIP untuk jaringan besar:
- Hanya mendukung maksimal 15 hop
- Konvergensi lambat saat terjadi perubahan jaringan

Keunggulan OSPF dibandingkan RIP:
- Memilih jalur terbaik berdasarkan cost, bukan hanya hop count
- Konvergensi lebih cepat saat terjadi perubahan
- Dapat diorganisir dalam area-area untuk skalabilitas
- Lebih efisien dalam penggunaan bandwidth karena hanya mengirimkan update saat ada perubahan

### Soal 3: Multi-Router dengan RIP

Pada soal ini, kita mengimplementasikan jaringan dengan tiga router yang saling terhubung menggunakan RIP. Konfigurasi meliputi:
- Pengaturan IP address pada interface router
- Aktivasi RIP version 2
- Penambahan semua network yang terhubung ke RIP
- Menonaktifkan auto-summary untuk mendukung VLSM

---

**luqmanaru**
