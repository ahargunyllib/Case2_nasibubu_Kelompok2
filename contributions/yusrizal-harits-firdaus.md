# Individual Contribution Report

**Name:** Yusrizal Harits Firdaus

**Student ID:** 235150207111011

**Group:** 2

**Case:** Malware Analysis – Telegram C2 Malware

**Date:** 29 November 2025

---

## 1. My Role in the Team

**Primary Role:** Dynamic Analysis Specialist

**Responsibilities:**
- Melakukan eksekusi dan monitoring malware menggunakan sandbox (ANY.RUN) bersama rekan satu tim (Billy).
- Menganalisis log jaringan untuk mengidentifikasi pola komunikasi C2 (Command & Control).
- Mengidentifikasi dan mengekstraksi Indicator of Compromise (IoC) seperti IP, Domain, dan Token API.

---

## 2. Tasks Completed

### Week 1: Setup & Initial Analysis
- [x] Task 1: Konfigurasi lingkungan analisis dan akuisisi sampel malware
  - Time spent: 4 hours
  - Output: Akun sandbox siap digunakan dan file malware berhasil diunggah dengan aman.
  
- [x] Task 2: Observasi awal (Initial Triage) perilaku malware
  - Time spent: 6 hours
  - Output: Log aktivitas awal dan identifikasi tipe file yang mencurigakan.

### Week 2: Deep Analysis
- [x] Task 3: Analisis Dinamis Mendalam (Deep Dive Dynamic Analysis)
  - Time spent: 10 hours
  - Output: Laporan detil mengenai perubahan Registry, Filesystem, dan Network traffic (PCAP).
  
- [x] Task 4: Ekstraksi IoC dan Pemetaan Serangan
  - Time spent: 8 hours
  - Output: Tabel IoC berisi endpoint Telegram, user-agent, dan payload data yang dieksfiltrasi.

### Week 3: Report & Presentation
- [x] Task 5: Penulisan Laporan Teknis (Bagian Dynamic & Network)
  - Time spent: 7 hours
  - Output: Draft bab analisis teknis dan penyusunan bukti gambar (screenshot).
  
- [x] Task 6: Pembuatan Slide Presentasi
  - Time spent: 3 hours
  - Output: Slide visualisasi alur serangan dan temuan utama.

**Total Time Invested:** 38 hours

---

## 3. Tools & Techniques Used

### Tools
1. **ANY.RUN**
   - Purpose: Platform sandbox utama untuk eksekusi malware yang aman.
   - Key features: Interactive monitoring, Network stream analysis.
   - Output: Process graph, PCAP files, dan laporan perilaku JSON/PDF.

2. **Text Editor / Notepad++ (untuk Log Analysis)**
   - Purpose: Menganalisis string mentah dari output malware.
   - Key features: Search & filter pola spesifik.
   - Output: Identifikasi string token Telegram dan chat ID.

### Analysis Techniques
- **Dynamic Analysis:** Menjalankan malware di lingkungan terkontrol untuk melihat interaksinya dengan OS secara langsung.
- **Network Traffic Analysis:** Membedah paket jaringan untuk melihat isi komunikasi antara malware dan server Telegram.

---

## 4. My Key Findings

### Finding 1: Pemanfaatan Platform Legitim (Telegram) sebagai C2
- **Description:** Malware tidak menggunakan server C2 khusus, melainkan menyalahgunakan API bot Telegram.
- **Evidence:** Ditemukan request HTTP POST ke `api.telegram.org/bot<token>/sendMessage`.
- **Significance:** Teknik ini membuat traffic malware sulit diblokir oleh firewall standar karena terlihat seperti traffic legal.
- **My contribution:** Mengisolasi request spesifik yang berisi data curian dan memvalidasi token bot yang digunakan.

### Finding 2: Aktivitas Spyware dan Pencurian Kredensial
- **Description:** Malware secara aktif memindai browser dan aplikasi email untuk mengambil data login tersimpan.
- **Evidence:** Log akses file pada direktori `AppData\Local\Google\Chrome\User Data`.
- **Significance:** Mengonfirmasi bahwa tujuan utama malware adalah pencurian informasi (Infostealer/Spyware).
- **My contribution:** Memetakan path file sistem yang diakses malware untuk dimasukkan ke dalam laporan IoC.

---

## 5. Report Sections I Contributed To

| Section | My Contribution | Percentage |
|---------|----------------|------------|
| Executive Summary | Merangkum dampak teknis untuk pembaca non-teknis | 40% |
| Technical Analysis | Menyusun narasi alur eksekusi malware | 60% |
| Evidence Collection | Seleksi dan anotasi screenshot bukti dari Sandbox | 50% |
| Recommendations | Menyusun saran mitigasi berdasarkan temuan dinamis | 30% |

---

## 6. Collaboration Activities

### Team Meetings Attended
- Meeting 1 (18 Nov): Perencanaan strategi analisis — menyepakati penggunaan ANY.RUN.
- Meeting 2 (22 Nov): Cross-check temuan — memvalidasi data yang ditemukan Billy dengan hasil observasi saya.
- Meeting 3 (25 Nov): Finalisasi — memastikan konsistensi istilah teknis dalam laporan.

### Communication
- **Primary channel:** WhatsApp Group & Discord.
- **Response rate:** Sangat responsif (kurang dari 1 jam).
- **Proactive communication:** Rutin membagikan screenshot progres analisis realtime saat menemukan anomali baru.

### Helping Team Members
- Berkolaborasi intensif dengan Billy (Nugraha Billy Viandy) dalam memecah tugas analisis dinamis agar tidak tumpang tindih namun saling melengkapi.
- Membantu tim menyusun narasi logis dari data mentah sandbox menjadi cerita serangan yang runut.

---

## 7. Challenges & Solutions

### Challenge 1: Eksekusi Malware Gagal (Silent Exit)
- **Problem:** Malware mendeteksi lingkungan virtual atau memerlukan interaksi pengguna (password zip).
- **Impact:** Tidak ada aktivitas berbahaya yang terekam pada percobaan awal.
- **My solution:** Berkoordinasi dengan tim untuk menggunakan parameter eksekusi yang benar (input password arsip) dan restart sesi sandbox.
- **Outcome:** Malware berhasil berjalan penuh (detonasi sukses).

### Challenge 2: Volume Log yang Besar
- **Problem:** Sandbox menghasilkan ribuan baris log event sistem.
- **Impact:** Kesulitan menemukan event kunci di antara noise sistem operasi Windows.
- **My solution:** Fokus pada filter event network dan pembuatan proses baru (process creation) saja.
- **Outcome:** Analisis menjadi lebih cepat dan fokus pada perilaku malicious saja.

---

## 8. Skills Developed

### Technical Skills
- **Malware Sandbox Proficiency:** Meningkatkan kemampuan konfigurasi dan interpretasi hasil dari cloud sandbox.
- **IoC Extraction:** Menjadi lebih mahir dalam memilah mana artefak yang berguna untuk pertahanan (Blue Team) dan mana yang hanya noise.

### Soft Skills
- **Collaborative Analysis:** Belajar melakukan analisis paralel dengan rekan tim tanpa duplikasi kerja yang tidak perlu.
- **Technical Reporting:** Kemampuan menuangkan hasil log teknis ke dalam bahasa laporan akademis yang terstruktur.

---

## 9. What I Learned

### Technical Knowledge
1. **Living off the Land (LotL):** Bagaimana malware memanfaatkan tool atau layanan yang sudah ada (seperti Telegram) untuk menyembunyikan jejak.
2. **Persistence Mechanism:** Cara malware mencoba bertahan di sistem meskipun komputer di-restart.

### Forensic Methodology
1. **Chain of Custody (Digital):** Pentingnya menjaga keaslian bukti (hash file) selama proses analisis.
2. **Verification:** Bahwa satu tool saja tidak cukup; hasil sandbox perlu diverifikasi dengan logika manual.

### Team Collaboration
1. Sinergi antara dua analis (saya dan Billy) mempercepat proses validasi hipotesis serangan secara signifikan dibandingkan bekerja sendiri.

---

## 10. Self-Evaluation

### Strengths in This Project
- Ketelitian dalam mengidentifikasi pola jaringan kecil yang mencurigakan.
- Kemampuan kolaborasi yang kuat dengan rekan satu sub-topik (Billy).
- Konsistensi dalam dokumentasi progres harian.

### Areas for Improvement
- Efisiensi waktu dalam triase awal malware bisa ditingkatkan.
- Perlu eksplorasi lebih lanjut mengenai analisis statis (reverse engineering code) untuk melengkapi analisis dinamis.

### Overall Self-Assessment
**Contribution Level:** Medium to High
**Effort Level:** 9/10
**Quality of Work:** 9/10

**Brief Justification:**
Saya berkontribusi secara penuh dalam inti teknis proyek ini (analisis dinamis). Bersama Billy, saya memastikan data yang disajikan dalam laporan akurat, terbukti, dan dapat dipertanggungjawabkan. Saya juga aktif dalam penyusunan laporan akhir hingga selesai.

---

## 11. Peer Evaluation

(Opsional)

---

## 12. Evidence of Work

### Screenshots
- Screenshot 1: *Process Tree Graph* (Menunjukkan parent-child process malware).
- Screenshot 2: *Network Stream HTTP POST* (Bukti komunikasi ke API Telegram).

### Documents
- Document 1: `Malware_Analysis_Report_Draft.docx` (Draft kontribusi laporan).

---

## 13. Presentation Contribution

### Slides I Contributed
- Slide 5: Hasil Analisis Dinamis(Behavior)

### My Presentation Section
- **Section:** Rekomendasi Tindakan
- **Duration:** 4–5 menit
- **Key points:**
  1. **Tindakan Segera:** Isolasi host, Blokir IP C2 (92.223.116.254), dan Hapus file di `%APPDATA%`.
  2. **Pencegahan Jangka Panjang:** Implementasi SSL/TLS Inspection untuk melihat payload HTTPS dan penggunaan EDR untuk deteksi Process Injection.

---

## 14. Additional Comments

Pengerjaan proyek ini bersama kelompok sangat produktif karena kami bisa saling memvalidasi temuan (cross-verification) secara realtime, sehingga akurasi laporan meningkat.

---
