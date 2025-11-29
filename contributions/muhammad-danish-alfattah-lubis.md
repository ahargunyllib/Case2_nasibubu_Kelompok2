# Individual Contribution Report

**Name:** Muhammad Danish Alfattah Lubis

**Student ID:** 235150207111008 

**Group:** 2

**Case:** Malware Analysis – Telegram C2 Malware

**Date:** 28 November 2025

---

## 1. My Role in the Team
**Primary Role:** Documentation & IoC / Detection Rules Specialist  
**Responsibilities:**
- Mengolah output teknis menjadi laporan yang terstruktur
- Membuat dan menyusun IoC list berdasarkan hasil analisis
- Mengembangkan YARA Rules & Snort Rules untuk deteksi malware
- Membantu penyusunan struktur laporan
- Berkoordinasi dengan tim untuk menyatukan hasil analisis teknis

---

## 2. Tasks Completed

### Week 1 – Setup & Coordination
- [✅] **Task 1: Membuat struktur laporan awal & pembagian tugas**
  - Time spent: 1 hour
  - Output: Draft laporan dan struktur kolaborasi kerja tim

- [✅] **Task 2: Menyusun format dan struktur repository**
  - Time spent: 1 hour
  - Output: Template dokumentasi dan susunan folder IoC/rules

---

### Week 2 – Deep Analysis & IoC Development
- [✅] **Task 3: Mengolah data hasil Sysinternals Strings & PeStudio**
  - Time spent: 2 hours
  - Output: Ekstraksi indikator artefak (URL, domain, API, SQL commands)

- [✅] **Task 4: Membuat IoC List dalam format CSV**
  - Time spent: 1 hour
  - Output: File IoC lengkap dan terstruktur untuk GitHub

---

### Week 3 – Detection Rules & Report Finalization
- [✅] **Task 5: Develop YARA Rule & Snort Rule untuk deteksi malware**
  - Time spent: 2.5 hours
  - Output:
    - `Malware_HnaZtD_TelegramC2.yar`
    - `telegram-c2.rules`

- [✅] **Task 6: Menyusun bagian laporan final**
  - Time spent: 2 hours
  - Output: Analisis IoC, grafik alur analisis

**Total Time Invested:** **9.5 hours**

---

## 3. Tools & Techniques Used

### Tools
| Tool | Kegunaan | Output |
|-------|----------|---------|
| Excel/CSV | Menyusun IoC list | IoC-LIST.csv |
| VSCode / GitHub | Menyusun rules & struktur repo | Folder IoC & Rule |
| PeStudio | Validasi indikator dan strings berbahaya | Evidence & Indicators |
| Sysinternals Strings | Referensi awal indikator | Raw data String |

### Analysis Techniques
- IoC extraction & classification
- Signature‑based detection modeling
- Static analysis support
- Threat intelligence documentation format

---

## 4. My Key Findings

### Finding 1: Telegram API sebagai Command‑and‑Control (C2)
- **Description:** Malware berkomunikasi dengan Telegram API untuk exfiltrasi data
- **Evidence:** URL: `https://api.telegram.org/bot/sendDocument`
- **Significance:** Membuktikan penggunaan Telegram sebagai komunikasi rahasia
- **My Contribution:** Mendokumentasikan dan memasukkan ke IOC CSV

### Finding 2: SQL Query Behavior dalam malware
- **Description:** Terdapat query database internal yang memodifikasi data
- **Evidence:** 
  - `select * from Mesajlar1`
  - `delete from Oda101`
- **Significance:** Malware berpotensi menghapus / mencuri data
- **My Contribution:** Menuliskan ke dalam kategori Behaviour IoC

### Finding 3: Metadata Debug Path Exposure
- **Description:** Malware menyimpan path debug PDB asli
- **Evidence:** `HnaZtD.pdb`
- **Significance:** Mengindikasikan asal development
- **My Contribution:** Dokumentasi dan penambahan ke CSV & YARA

---

## 5. Report Sections I Contributed To

| Section | Contribution | Percentage |
|---------|-------------|-------------|
| Executive Summary | Ringkasan hasil IoC | 20% |
| Technical Analysis | IoC breakdown dan rules | 30% |
| Evidence Collection | IoC list, rule files | 40% |
| Timeline | Alur kerja dokumentasi | 20% |
| IoC List | **Full creation and formatting** | **100%** |
| Recommendations | Deteksi dan monitoring | 20% |
| Presentation Slides | - | - |

---

## 6. Collaboration Activities

### Team Meetings
- Meeting 1: Penyusunan alur & tanggung jawab
- Meeting 2: Integrasi analisis data
- Meeting 3: Penyusunan final report & slide

### Communication
- Primary channel: WhatsApp
- Response rate: Fast (≤1 hour)
- Collaboration support:
  - Format IoC CSV
  - Integrasi YARA & Snort rules
  - Penyusunan dokumentasi final

---

## 7. Challenges & Solutions

### Challenge 1: Data terlalu banyak pada file strings
- **Solution:** Menyaring secara manual dan cross‑reference via PeStudio
- **Outcome:** IoC clean dan ringkas

### Challenge 2: Membuat rule detection dari awal
- **Solution:** Mempelajari template rule industri
- **Outcome:** Rules final teruji dan digunakan report

---

## 8. Skills Developed

### Technical
- YARA rule writing
- Network rule (Snort) development
- IoC documentation
- Static analysis workflow

### Soft Skills
- Collaboration & communication
- Documentation writing
- Structured thinking

---

## 9. What I Learned
- Proses nyata malware static analysis
- Cara mengubah artefak teknis menjadi evidence
- Pentingnya IoC sebagai output threat intelligence

---

## 10. Self‑Evaluation
**Contribution Level:** High  
**Effort Level:** 9/10  
**Work Quality:** 9/10  

**Brief justification:** Saya menghasilkan output utama berupa IoC dan rules yang menjadi bagian inti deteksi malware.

---

## 11. Peer Evaluation
**Ghufron Bagaskara**
- Strength: Memiliki kemampuan analisis teknis yang kuat
- Contribution: Sangat tinggi pada bagian investigasi dan evidence

---

## 12. Evidence of Work
- `ioc-list.csv`
- `Malware_HnaZtD_TelegramC2.yar`
- `telegram-c2.rules`

---

## 13. Presentation Contribution
- -

---

## 14. Additional Comments
Project ini meningkatkan kemampuan saya dalam forensic documentation dan malware detection methodology.

---

## Declaration
Saya menyatakan bahwa laporan ini benar sesuai kontribusi saya pribadi.  

**Signature:** Muhammad Danish Alfattah Lubis
**Date:** 29-11-2025