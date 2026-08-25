# 🐍🪜 Game Ular Tangga Interaktif (Web Edition)

Dokumen ini berisi **Game Design Document (GDD)** lengkap dan **Skema Cara Bermain** untuk proyek Web Game Ular Tangga Interaktif.

---

## 📋 Table of Contents
1. [Overview Proyek](#-overview-proyek)
2. [Game Design Document (GDD)](#-game-design-document-gdd)
   - [1. Konsep & Tujuan](#1-konsep--tujuan)
   - [2. Target Audiens & Platform](#2-target-audiens--platform)
   - [3. Fitur Utama](#3-fitur-utama)
   - [4. Mekanika Permainan (Game Mechanics)](#4-mekanika-permainan-game-mechanics)
   - [5. Arsitektur & Spesifikasi Teknis](#5-arsitektur--spesifikasi-teknis)
   - [6. Desain Visual & Audio](#6-desain-visual--audio)
3. [🎮 Skema & Cara Bermain](#-skema--cara-bermain)
   - [Persiapan Permainan](#persiapan-permainan)
   - [Alur Permainan (Game Loop)](#alur-permainan-game-loop)
   - [Aturan Khusus](#aturan-khusus)
   - [Kondisi Kemenangan](#kondisi-kemenangan)
4. [🛠️ Cara Menjalankan Proyek](#-cara-menjalankan-proyek)

---

## 🌟 Overview Proyek

Game Ular Tangga Interaktif ini adalah modernisasi dari permainan papan tradisional *Snakes and Ladders*. Dikembangkan menggunakan teknologi standar web modern (HTML5 Canvas, CSS3 Glassmorphism, JavaScript ES6, dan Audio Synthesis via Tone.js), game ini dapat dimainkan langsung di peramban (browser) tanpa menginstal aplikasi tambahan.

Game ini mendukung **Mode Manusia vs Manusia (PvP)** untuk bermain bersama teman secara lokal dan **Mode Manusia vs AI (PvE)** untuk bermain melawan komputer.

---

## 📄 Game Design Document (GDD)

### 1. Konsep & Tujuan
* **Judul Game**: Ular Tangga Interaktif (Interactive Snakes & Ladders)
* **Genre**: Board Game / Casual / Strategy
* **Konsep Utama**: Permainan papan klasik 100 kotak di mana pemain berlomba mencapai kotak 100 menggunakan lemparan dadu, memanfaatkan tangga untuk naik lebih cepat dan menghindari ular yang menurunkan posisi.
* **Tujuan Pemain**: Menjadi pemain pertama yang mencapai tepat di Kotak 100.

### 2. Target Audiens & Platform
* **Target Audiens**: Semua umur (Anak-anak, remaja, hingga dewasa).
* **Platform Utama**: Web Browser (Desktop, Laptop, Tablet, Smartphone).
* **Persyaratan Browser**: Browser modern dengan dukungan HTML5 Canvas dan Web Audio API (Google Chrome, Mozilla Firefox, Microsoft Edge, Apple Safari).

### 3. Fitur Utama
* 🤖 **Dua Mode Permainan**:
  * **Mode Manusia (2 Players)**: Permainan bergilir 2 pemain lokal pada satu perangkat.
  * **Mode AI (Player vs Computer)**: Pemain melawan kecerdasan buatan (bot) yang mengeksekusi giliran secara otomatis.
* 🎵 **Sistem Audio Sintetis (Tone.js)**:
  * Efek suara dadu bergulir (*percussion click*).
  * Efek suara setiap langkah bidak (*step pop sound*).
  * Efek suara naik tangga (*ascending melodic chime*).
  * Efek suara terkena ular (*descending glissando sound*).
  * Efek suara kemenangan (*victory fanfare*).
* 🎨 **Desain Visual Modern (Glassmorphism)**:
  * Latar belakang dinamis dengan animasi *floating blobs* & ikon elemen game melayang.
  * Papan permainan transparan bertema *glassmorphism* dengan kontras tinggi.
  * Render Ular dan Tangga secara dinamis menggunakan HTML5 Canvas API.
* 🧹 **Clean Interface**:
  * Panel kontrol minimalis tanpa log teks tebal untuk menjaga konsentrasi pemain dan estetika visual.

### 4. Mekanika Permainan (Game Mechanics)

#### A. Sistem Papan (Board System)
* Grid berukuran **10x10** (total 100 kotak).
* Penomoran kotak mengikuti pola **Zig-zag (Boustrophedon)**:
  * Baris 1 (Kotak 1 - 10): Kiri ke Kanan
  * Baris 2 (Kotak 11 - 20): Kanan ke Kiri
  * Baris 3 (Kotak 21 - 30): Kiri ke Kanan, dst.
  * Kotak 1 berada di sudut kiri bawah, Kotak 100 berada di sudut kiri atas.

#### B. Dadu & Pergerakan (Dice & Movement)
* Dadu bernilai acak antara **1 hingga 6**.
* Animasi pengocokan dadu selama ~600ms sebelum nilai akhir muncul.
* Pergerakan bidak dilakukan secara bertahap (step-by-step) untuk pengalaman visual yang interaktif.

#### C. Tangga & Ular (Ladders & Snakes)
* **Tangga (Ladder)**:
  * Memindahkan bidak dari pangkal tangga di kotak bawah langsung ke puncak tangga di kotak atas.
  * Memberikan keuntungan mempercepat perjalanan pemain.
* **Ular (Snake)**:
  * Memindahkan bidak dari kepala ular di kotak atas turun langsung ke ekor ular di kotak bawah.
  * Menjadi rintangan yang menurunkan kemajuan pemain.

### 5. Arsitektur & Spesifikasi Teknis
* **HTML5**: Menyediakan struktur halaman, canvas render, dan elemen UI kontrol.
* **CSS3**: Layouting fleksibel (Flexbox/Grid), animasi `@keyframes`, styling *Glassmorphism* (`backdrop-filter: blur`), dan *smooth transitions*.
* **JavaScript (Vanilla ES6)**:
  * Pengelolaan status permainan (*state management*).
  * Logika giliran (*turn logic*) & deteksi AI.
  * Animasi pergerakan bidak async/await.
  * Penggambaran SVG/Canvas ular dan tangga secara eksplisit berdasarkan koordinat grid.
* **Tone.js (CDN)**: Pustaka Web Audio untuk menghasilkan gelombang suara audio sintetis tanpa ketergantungan file MP3/WAV eksternal.

### 6. Desain Visual & Audio
* **Palette Warna**:
  * Gradient Background: Pastel Cyan, Yellow, Violet (`linear-gradient(135deg, #a8ff78, #78ffd6, #f6d365, #fda085)`).
  * Player 1: Merah Cerah / Coral (`#FF4D4D`).
  * Player 2 / AI: Biru Cerah / Cobalt (`#3388FF`).
* **Audio Feedback**: Respons langsung dari setiap aksi pengguna untuk meningkatkan *gameplay experience*.

---

## 🎮 Skema & Cara Bermain

```
[ Papan Permainan (1-100) ]
        │
        ├── Pilih Mode Permainan (Manusia vs Manusia / Manusia vs AI)
        │
        ├── Giliran Player 1: Klik "Lempar Dadu" ──► Bergerak Sesuai Dadu
        │                                             │
        │                                             ├── Mendarat di Tangga ──► Naik ke Atas
        │                                             ├── Mendarat di Ular   ──► Turun ke Bawah
        │                                             └── Mendarat di Normal ──► Selesai Giliran
        │
        ├── Giliran Player 2 / AI ───────────────────► Bergerak Sesuai Dadu (Otomatis jika AI)
        │                                             │
        │                                             ├── Mendarat di Tangga ──► Naik ke Atas
        │                                             ├── Mendarat di Ular   ──► Turun ke Bawah
        │                                             └── Mendarat di Normal ──► Selesai Giliran
        │
        └── Seseorang Mencapai Kotak 100 ────────────► PEMENANG DITETAPKAN 🎉
```

### Persiapan Permainan
1. Buka file `index.html` pada web browser Anda.
2. **Aktifkan Audio**: Klik di bagian mana saja pada layar sekali (misalnya klik tombol mode atau dadu) untuk memberikan izin pada browser mengaktifkan suara.
3. **Pilih Mode Permainan**:
   * Pilih 👥 **Mode Manusia** jika ingin bermain bersama teman secara bergiliran.
   * Pilih 🤖 **Mode AI** jika ingin bermain melawan komputer.

### Alur Permainan (Game Loop)
1. Permainan dimulai dengan kedua bidak berada di posisi **Kotak 1**.
2. **Lempar Dadu**:
   * Pemain yang mendapat giliran menekan tombol **"Lempar Dadu"**.
   * Suara kocokan dadu akan terdengar dan angka 1–6 akan muncul.
3. **Melangkah**:
   * Bidak pemain akan bergerak maju satu demi satu sesuai angka dadu.
   * Setiap langkah memicu efek suara ketukan.
4. **Mekanisme Ular & Tangga**:
   * Jika bidak berhenti tepat di **pangkal tangga**, bidak akan otomatis meluncur naik ke puncak tangga disertai efek nada menaik (*Ladder Chime*).
   * Jika bidak berhenti tepat di **kepala ular**, bidak akan meluncur turun ke ekor ular disertai efek nada meluncur turun (*Snake Slide*).
5. **Perantian Giliran**:
   * Pada **Mode Manusia**: Giliran berpindah ke Pemain 2 untuk menekan tombol dadu.
   * Pada **Mode AI**: Setelah Pemain 1 selesai melangkah, AI akan melempar dadu dan melangkah secara otomatis setelah jeda singkat (1 detik).

### Aturan Khusus
* **Aturan Memantul (Bounce Back on 100)**:
  * Untuk menang, pemain harus mendarat **TEPAT** di Kotak 100.
  * Jika posisi pemain di 97 dan mendapat angka dadu 5, pemain melangkah 3 kali ke Kotak 100, lalu memantul mundur 2 kali ke Kotak 98.

### Kondisi Kemenangan
* Pemain pertama (Manusia atau AI) yang mendarat tepat di **Kotak 100** dinyatakan sebagai **PEMENANG**.
* Musik/efek suara kemenangan (*Victory Fanfare*) akan dibunyikan dan pesan ucapan selamat akan ditampilkan di layar.
* Tombol **"Reset Permainan"** dapat ditekan kapan saja untuk memulai ulang dari awal.

---

## 🛠️ Cara Menjalankan Proyek

1. Simpan kode permainan ke dalam file bernama `index.html`.
2. Buka file `index.html` menggunakan browser favorit Anda (Chrome, Edge, Firefox, Safari).
3. Pastikan perangkat Anda terhubung ke internet saat pertama kali membuka file agar library **Tone.js** dapat teruat otomatis melalui CDN.
4. Selamat bermain! 🎲🐍🪜
