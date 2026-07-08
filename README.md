# 🔋 ESP32 Daly Smart BMS BLE Reader

Sistem monitoring **Daly Smart BMS** berbasis **ESP32** menggunakan komunikasi **Bluetooth Low Energy (BLE)** dengan library **NimBLE-Arduino**.

Project ini memungkinkan ESP32 terhubung langsung ke Daly Smart BMS melalui Bluetooth, membaca berbagai parameter baterai secara real-time, serta menampilkan hasil pembacaan melalui **Serial Monitor**. Cocok digunakan sebagai dasar pengembangan sistem monitoring baterai berbasis IoT, data logger, Home Assistant, maupun aplikasi monitoring energi.

---

## 📌 Fitur Utama

* 📡 Scan otomatis perangkat Daly Smart BMS
* 🔗 Koneksi BLE otomatis berdasarkan MAC Address
* 🔄 Auto reconnect ketika koneksi terputus
* ✅ Verifikasi checksum setiap paket data
* 🔋 Monitoring tegangan total baterai
* ⚡ Monitoring arus Charge/Discharge
* 📊 Monitoring State of Charge (SOC)
* 🔬 Monitoring tegangan setiap sel (hingga 48 sel)
* 🌡 Monitoring temperatur BMS
* ⚖ Monitoring status Cell Balancing
* 🔌 Monitoring status Charge MOS & Discharge MOS
* 🔄 Penyusunan otomatis paket multi-frame tegangan sel
* 💻 Monitoring melalui Serial Monitor

---

## 📊 Data yang Dibaca

| CMD  | Informasi                           |
| ---- | ----------------------------------- |
| 0x90 | Total Voltage, Current, SOC         |
| 0x91 | Tegangan Sel Maksimum & Minimum     |
| 0x92 | Temperatur Maksimum & Minimum       |
| 0x93 | Status BMS, MOS, Remaining Capacity |
| 0x94 | Konfigurasi Baterai                 |
| 0x95 | Tegangan Sel Individual             |
| 0x97 | Status Cell Balancing               |

---

## 🔧 Hardware yang Dibutuhkan

* ESP32 Development Board
* Daly Smart BMS BLE
* Baterai Lithium
* Arduino IDE / PlatformIO

---

## 📚 Library

Library yang digunakan:

* NimBLE-Arduino

---

## 🔌 UUID BLE Daly Smart BMS

| Service               | UUID                                   |
| --------------------- | -------------------------------------- |
| Service UUID          | `0000FFF0-0000-1000-8000-00805F9B34FB` |
| Notify Characteristic | `0000FFF1-0000-1000-8000-00805F9B34FB` |
| Write Characteristic  | `0000FFF2-0000-1000-8000-00805F9B34FB` |

---

## ⚙️ Konfigurasi

Ubah alamat MAC Bluetooth sesuai dengan perangkat Daly Smart BMS yang digunakan.

```cpp
#define BMS_MAC_ADDRESS "50:18:08:01:15:51"
```

---

## ⌨️ Perintah Serial

| Tombol | Fungsi                       |
| ------ | ---------------------------- |
| c      | Connect ke BMS               |
| d      | Disconnect                   |
| 0      | Basic Status                 |
| 1      | Min/Max Cell Voltage         |
| 2      | Temperature                  |
| 3      | BMS State                    |
| 4      | Battery Configuration        |
| 5      | Cell Voltage                 |
| 6      | Cell Balance                 |
| r      | Reset pembacaan Cell Voltage |

---

## 📂 Struktur Program

### BLE Manager

* Scan perangkat BLE
* Koneksi ke Daly BMS
* Auto reconnect
* Subscribe notification

### Packet Parser

* Verifikasi checksum
* Parsing seluruh frame Daly
* Penyusunan paket multi-frame

### Data Decoder

* Decode seluruh command Daly
* Konversi data ke satuan yang mudah dibaca
* Menampilkan hasil ke Serial Monitor

---

## ⚙️ Cara Kerja

1. ESP32 melakukan scan perangkat BLE.
2. Daly Smart BMS ditemukan berdasarkan MAC Address.
3. ESP32 melakukan koneksi ke BMS.
4. Subscribe ke karakteristik notifikasi.
5. Mengirim request data ke BMS.
6. Menerima paket data BLE.
7. Memverifikasi checksum.
8. Mendekode setiap frame data.
9. Menampilkan informasi baterai pada Serial Monitor.
10. Mengulangi proses polling setiap 1 detik.

---

## 📷 Contoh Output

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

## 🚀 Pengembangan Lanjutan

Beberapa fitur yang dapat ditambahkan:

* 📡 MQTT
* 🌐 Web Server Monitoring
* ☁️ Blynk IoT
* 🏠 Home Assistant
* 📈 InfluxDB + Grafana
* 📱 Telegram Bot
* 📤 Firebase Realtime Database
* 💾 SD Card Data Logger
* 📺 OLED / TFT Display
* 🌍 Modbus TCP / RTU
* 🔔 Alarm Over Voltage & Under Voltage

---

## 📦 Use Case

Project ini cocok untuk:

* 🔋 Monitoring baterai Lithium
* ⚡ Solar Power System (PLTS)
* 🚐 Campervan
* 🚲 Sepeda listrik
* 🛵 Motor listrik
* 🚗 Kendaraan listrik
* 🏡 Home Energy Storage
* 🌐 IoT Battery Monitoring
* 📊 Data Logger Baterai

---

## 🛠 Instalasi

1. Install Arduino IDE atau PlatformIO.
2. Install library **NimBLE-Arduino**.
3. Ubah MAC Address sesuai BMS.
4. Upload program ke ESP32.
5. Buka Serial Monitor pada baudrate **115200**.
6. ESP32 akan melakukan scan dan terhubung ke Daly Smart BMS secara otomatis.

---

## ⚠️ Catatan Penting

* Hanya mendukung **Daly Smart BMS versi Bluetooth (BLE)**.
* Pastikan alamat MAC Bluetooth sudah benar.
* Mendukung hingga **48 sel baterai**.
* Polling data dilakukan setiap **1 detik**.
* Tegangan sel dikirim dalam beberapa frame dan akan digabungkan secara otomatis sebelum ditampilkan.

---

## 📧 Contact Us

* 📷 Instagram : https://www.instagram.com/frendi.co/
* 💬 WhatsApp : https://wa.me/+6287888227410
* 📧 Email : [frendirobotech@gmail.com](mailto:frendirobotech@gmail.com)
* 📧 Email Alternatif : [frendix45@gmail.com](mailto:frendix45@gmail.com)

---

## 👨‍💻 Author

**Dikembangkan oleh:** Imam Sa'id Nurfrendi

**Komunitas:** Reog Robotic & Robotech Electronics

**Lisensi:** MIT License
