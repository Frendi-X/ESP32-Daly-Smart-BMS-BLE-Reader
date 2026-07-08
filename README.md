# ESP32 Daly Smart BMS BLE Reader

Program berbasis **ESP32** untuk membaca data **Daly Smart BMS** melalui **Bluetooth Low Energy (BLE)** menggunakan library **NimBLE-Arduino**.

ESP32 akan melakukan pemindaian perangkat BLE, menghubungkan diri ke Daly Smart BMS berdasarkan alamat MAC, mengirim permintaan data, menerima notifikasi BLE, kemudian mendekode protokol komunikasi Daly dan menampilkan seluruh informasi baterai melalui **Serial Monitor**.

---

## ✨ Fitur

* Scan otomatis perangkat Daly Smart BMS.
* Koneksi BLE otomatis menggunakan alamat MAC.
* Reconnect otomatis apabila koneksi terputus.
* Verifikasi checksum setiap paket data.
* Penyusunan otomatis paket tegangan sel (multi-frame).
* Mendukung hingga **48 sel baterai**.
* Mendeteksi otomatis nomor frame Daly (0-based maupun 1-based).
* Polling data secara otomatis setiap 1 detik.

---

## 📊 Data yang Dibaca

### CMD 0x90 - Status Dasar

* Total Voltage
* Accumulated Voltage
* Current
* State of Charge (SOC)

### CMD 0x91 - Tegangan Sel

* Tegangan sel tertinggi
* Nomor sel tertinggi
* Tegangan sel terendah
* Nomor sel terendah
* Selisih tegangan antar sel

### CMD 0x92 - Temperatur

* Temperatur maksimum
* Sensor temperatur maksimum
* Temperatur minimum
* Sensor temperatur minimum

### CMD 0x93 - Status BMS

* Status baterai
* Charge MOS
* Discharge MOS
* Remaining Capacity

### CMD 0x94 - Konfigurasi Baterai

* Jumlah sel
* Jumlah sensor temperatur
* Status charger
* Status load
* Charge cycle

### CMD 0x95 - Tegangan Setiap Sel

Menampilkan tegangan seluruh sel dalam satuan:

* mV
* Volt

Contoh:

```text
Cell 01 : 3385 mV (3.385 V)
Cell 02 : 3387 mV (3.387 V)
Cell 03 : 3386 mV (3.386 V)
```

### CMD 0x97 - Cell Balancing

Menampilkan status balancing setiap sel.

Contoh:

```text
Cell 01 : Open
Cell 02 : Closed
Cell 03 : Closed
```

---

# 🔧 Hardware

* ESP32
* Daly Smart BMS BLE
* Modul Bluetooth bawaan Daly

---

# 📚 Library

Install library berikut melalui Arduino IDE:

* NimBLE-Arduino

---

# ⚙️ Konfigurasi

Ubah alamat MAC Bluetooth sesuai BMS yang digunakan.

```cpp
#define BMS_MAC_ADDRESS "50:18:08:01:15:51"
```

---

# 📡 UUID BLE

## Service

```
0000FFF0-0000-1000-8000-00805F9B34FB
```

## Notify Characteristic

```
0000FFF1-0000-1000-8000-00805F9B34FB
```

## Write Characteristic

```
0000FFF2-0000-1000-8000-00805F9B34FB
```

---

# ⌨️ Perintah Serial

| Tombol | Fungsi                          |
| ------ | ------------------------------- |
| c      | Connect ke BMS                  |
| d      | Disconnect                      |
| 0      | Status Dasar                    |
| 1      | Tegangan Sel Maksimum & Minimum |
| 2      | Temperatur                      |
| 3      | Status BMS                      |
| 4      | Konfigurasi Baterai             |
| 5      | Tegangan Semua Sel              |
| 6      | Status Cell Balancing           |
| r      | Reset pembacaan tegangan sel    |

---

# 📷 Contoh Output

```text
--- DALY FRAME CMD=0x90 ---

Total Voltage : 51.2 V
Current       : -8.5 A
SOC           : 82.3 %

--- DALY FRAME CMD=0x91 ---

Max Cell : 3.391 V
Min Cell : 3.385 V
Difference : 6 mV

--- DALY FRAME CMD=0x95 ---

Cell 01 : 3385 mV (3.385 V)
Cell 02 : 3387 mV (3.387 V)
Cell 03 : 3386 mV (3.386 V)
...
```

---

# 📂 Struktur Program

```
ESP32
   │
   ├── Scan BLE
   │
   ├── Connect ke Daly BMS
   │
   ├── Subscribe Notification
   │
   ├── Kirim Request CMD
   │
   ├── Terima Data BLE
   │
   ├── Verifikasi Checksum
   │
   ├── Decode Frame Daly
   │
   └── Tampilkan ke Serial Monitor
```

---

# 🚀 Fitur Utama

* Komunikasi BLE menggunakan NimBLE (lebih ringan dibanding BLE bawaan ESP32)
* Parsing seluruh frame Daly Smart BMS
* Pembacaan tegangan sel otomatis
* Auto reconnect
* Validasi checksum
* Mendukung hingga 48 sel baterai
* Mudah dikembangkan untuk MQTT, WiFi, OLED, LCD, atau Home Assistant

---

# 📄 Lisensi

Proyek ini bersifat **open source** dan bebas digunakan, dimodifikasi, maupun dikembangkan lebih lanjut sesuai kebutuhan.
