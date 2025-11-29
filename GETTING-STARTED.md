# Getting Started - Digital Forensics Case Project

## 📚 Untuk Mahasiswa

### Selamat Datang!
Selamat datang di case-based project Digital Forensics. Repository ini berisi 3 case investigasi yang dirancang untuk memberikan pengalaman hands-on dalam digital forensics menggunakan data real dari public datasets.

## 🎯 Tujuan Pembelajaran

Setelah menyelesaikan project ini, Anda akan:
1. ✅ Memahami fundamental digital forensics
2. ✅ Mampu bekerja dalam tim untuk investigasi forensik
3. ✅ Mampu menganalisis evidence digital (sesuai case yang ditugaskan)
4. ✅ Mampu menggunakan tools forensik industri
5. ✅ Mampu menulis laporan investigasi forensik yang profesional
6. ✅ Mampu mempresentasikan hasil investigasi

## 👥 Mode Pengerjaan

### Kelompok (3-4 orang)
- **Setiap kelompok mengerjakan 1 case yang BERBEDA**
- **Durasi: 3 minggu untuk semua case**
- **Assignment case ditentukan oleh instruktur**
- **Semua kelompok bekerja paralel dalam periode yang sama**

### Pembagian Kerja Kelompok (Rekomendasi):
1. **Team Lead:** Koordinasi, timeline management
2. **Technical Analyst 1:** Hands-on analysis
3. **Technical Analyst 2:** Supporting analysis
4. **Report Writer:** Dokumentasi dan laporan

**⚠️ PENTING:** Semua anggota harus memahami seluruh case!

## 📋 Prerequisites

### Knowledge Requirements
- Pemahaman dasar tentang:
  - Networking (TCP/IP, HTTP, DNS)
  - Operating Systems (Windows & Linux)
  - Command Line Interface
  - Security concepts
  - Programming (Python - basic)

### Software Requirements

#### Essential (Wajib):
1. **VirtualBox** atau **VMware**
   - Download: https://www.virtualbox.org/
   - Untuk menjalankan analysis VMs

2. **Python 3.8+**
   - Download: https://www.python.org/
   - Untuk menjalankan analysis scripts

3. **Wireshark**
   - Download: https://www.wireshark.org/
   - Untuk network analysis (Case 1)

#### Recommended:
4. **FlareVM** (Windows Analysis VM)
   - Setup guide: https://github.com/mandiant/flare-vm
   - Untuk malware analysis (Case 2)

5. **REMnux** (Linux Analysis VM)
   - Download: https://remnux.org/
   - Alternative untuk malware analysis

## 🚀 Quick Start

### Step 1: Setup Environment

```bash
# Clone atau download repository ini
cd case-forensics

# Install Python dependencies
pip install -r tools/forensic-toolkit/requirements.txt

# Verify installation
python --version
pip list | grep scapy
```

### Step 2: Tunggu Assignment dari Instruktur

Instruktur akan menugaskan case ke setiap kelompok:

**Assignment Process:**
1. Pembentukan kelompok (3-4 orang)
2. Instruktur assign case ke setiap kelompok
3. Kelompok yang berbeda mendapat case yang berbeda
4. Semua kelompok mulai bersamaan

**Case Distribution:**
- **Kelompok 1-3:** Case 1 (Network Intrusion)
- **Kelompok 4-6:** Case 2 (Malware Analysis)
- **Kelompok 7-9:** Case 3 (Log Analysis)

*Catatan: Distribution dapat disesuaikan berdasarkan jumlah kelompok*

### Step 3: Read Case Documentation

```bash
# Baca README di folder case yang ditugaskan
cd cases/case-1-network-intrusion/  # atau case yang ditugaskan
cat README.md
```

### Step 4: Organize Team Work

**Week 1: Setup & Initial Analysis**
- Setup environment (semua anggota)
- Download dataset
- Initial assessment
- Pembagian tugas detail

**Week 2: Deep Analysis**
- Technical analysis
- Evidence collection
- IoC extraction
- Progress meeting

**Week 3: Report & Presentation**
- Finalisasi analisis
- Report writing
- Presentation prep
- Practice session

### Step 5: Download Dataset

Setiap case memiliki link ke public dataset:
- Case 1: CICIDS2017 dataset
- Case 2: MalwareBazaar samples
- Case 3: SecRepo logs

**⚠️ IMPORTANT:**
- Pastikan download dari sumber yang legitimate
- Untuk malware samples, handle dengan hati-hati!
- **JANGAN di host machine

### Step 5: Start Investigation

Follow the tasks dalam case README yang ditugaskan:
1. Initial Assessment (Semua anggota)
2. Technical Analysis (Dibagi per anggota)
3. Evidence Collection (Kolaboratif)
4. Report Writing (Koordinasi)
5. Presentation Prep (Semua anggota)

## 📝 Submission Guidelines

### Struktur Submission

```
CaseX_NamaKelompok_Kelompok#/
├── report/
│   ├── main-report.pdf          # Laporan utama
│   ├── executive-summary.pdf    # Ringkasan untuk manajemen
│   └── technical-appendix.pdf   # Detail teknis (optional)
├── evidence/
│   ├── screenshots/             # Screenshot findings
│   ├── pcap-files/             # Filtered PCAP (jika ada)
│   └── log-samples/            # Sample logs analyzed
├── ioc/
│   └── ioc-list.csv            # Indicators of Compromise
├── scripts/
│   └── analysis-scripts/       # Scripts yang digunakan
├── presentation/
│   └── slides.pdf              # Presentasi kelompok
└── contribution/
    └── individual-contribution.md  # Kontribusi masing-masing anggota
```

### Format Laporan

Gunakan template yang disediakan di:
```
submissions/template/REPORT-TEMPLATE.md
```

Template mencakup:
- Executive Summary
- Technical Analysis
- Timeline
- IoC List
- Recommendations
- Appendices

### Deadline & Submission

- **All Cases:** 3 minggu dari assignment
- **Presentasi:** Minggu ke-4 (setelah submission)

**Submit via:**
- ZIP file dengan nama: `CaseX_NamaKelompok_Kelompok#.zip`
- Upload ke platform yang ditentukan instruktur
- Atau email ke instruktur

**Presentasi:**
- Durasi: 15-20 menit per kelompok
- Format: Semua anggota harus hadir dan presentasi
- Q&A: 5-10 menit

## 🎓 Grading Criteria

### Breakdown Penilaian

| Komponen | Bobot | Kriteria |
|----------|-------|----------|
| Metodologi | 20% | Penggunaan metodologi yang tepat, systematic approach, teamwork |
| Analisis Teknis | 30% | Kedalaman analisis, akurasi findings, penggunaan tools |
| Evidence Collection | 20% | Dokumentasi bukti, chain of custody, completeness |
| Laporan | 20% | Struktur, kejelasan, profesionalitas, grammar |
| Presentasi | 10% | Delivery, Q&A, team coordination |

### Komponen Nilai:
- **Nilai Kelompok (80%):** Hasil kerja bersama (report, analysis, presentation)
- **Nilai Individu (20%):** Kontribusi dan pemahaman individu (dinilai saat Q&A dan review kontribusi)

### Grading Scale

- **A (85-100):** Excellent
  - Analisis sangat komprehensif dan akurat
  - Laporan profesional dan detail
  - Rekomendasi actionable dan prioritas jelas
  - Evidence terdokumentasi dengan baik

- **B (70-84):** Good
  - Analisis baik dengan minor gaps
  - Laporan jelas dan terstruktur
  - Rekomendasi relevant
  - Evidence adequate

- **C (60-69):** Satisfactory
  - Analisis basic namun kurang mendalam
  - Laporan memenuhi requirement minimum
  - Rekomendasi generic
  - Evidence incomplete

- **D (<60):** Needs Improvement
  - Analisis tidak lengkap atau tidak akurat
  - Laporan tidak terstruktur
  - Rekomendasi tidak relevan
  - Evidence kurang

## 💡 Tips untuk Sukses

### Team Collaboration Tips
1. **Clear Role Assignment** - Tetapkan peran sejak awal
2. **Regular Meetings** - Meeting progress minimal 2x seminggu
3. **Use Collaboration Tools** - GitHub, Notion, Trello, dll
4. **Document Everything** - Setiap anggota catat kontribusinya
5. **Communication** - Group chat aktif, responsive

### General Tips
1. **Start Early** - Jangan tunggu last minute!
2. **Read Everything** - Baca semua dokumentasi dengan teliti
3. **Take Notes** - Dokumentasikan setiap langkah analisis
4. **Ask Questions** - Jangan ragu bertanya ke instruktur
5. **Help Each Other** - Share knowledge dalam kelompok

### Analysis Tips
1. **Follow the Evidence** - Biarkan data guide analisis Anda
2. **Be Systematic** - Gunakan metodologi yang terstruktur
3. **Document Everything** - Screenshot, command output, findings
4. **Cross-Validate** - Verifikasi findings dari multiple sources
5. **Think Like Attacker** - Understand the adversary mindset

### Report Writing Tips
1. **Write for Audience** - Executive summary untuk management, technical details untuk analysts
2. **Be Clear and Concise** - Avoid jargon kecuali necessary
3. **Use Visuals** - Screenshots, diagrams, charts
4. **Proofread** - Check grammar, spelling, formatting
5. **Tell a Story** - Make timeline and narrative clear

## 📚 Learning Resources

### Books
- **Practical Malware Analysis** - Michael Sikorski
- **The Art of Memory Forensics** - Michael Ligh
- **Network Forensics** - Sherri Davidoff
- **Incident Response & Computer Forensics** - Jason Luttgens

### Online Courses
- **SANS Digital Forensics** - https://www.sans.org/
- **Cybrary Forensics Courses** - https://www.cybrary.it/
- **Udemy Digital Forensics** - Various courses

### Communities
- **Reddit r/computerforensics** - https://reddit.com/r/computerforensics
- **DFIR Discord** - Digital Forensics community
- **SANS DFIR Summit** - Annual conference

### Tools Documentation
- **Wireshark User Guide** - https://www.wireshark.org/docs/
- **Volatility Documentation** - https://volatilityfoundation.org/
- **YARA Documentation** - https://yara.readthedocs.io/

## ❓ FAQ

### Q: Boleh bekerja dalam group?
**A:** YA! Project ini WAJIB dikerjakan dalam kelompok 3-4 orang.

### Q: Apakah setiap kelompok case-nya sama?
**A:** TIDAK. Setiap kelompok akan ditugaskan case yang berbeda oleh instruktur.

### Q: Bagaimana pembagian kerja dalam kelompok?
**A:** Kelompok bebas mengatur, tapi semua anggota harus paham keseluruhan case.

### Q: Apakah ada penilaian individu?
**A:** Ya, 20% dari nilai berdasarkan kontribusi dan pemahaman individu (Q&A session).

### Q: Dataset tidak bisa didownload, bagaimana?
**A:** Hubungi instruktur untuk alternative source atau akses ke mirror.

### Q: Boleh diskusi dengan kelompok lain yang case berbeda?
**A:** Boleh diskusi umum, tapi TIDAK boleh sharing solusi atau findings.

### Q: Berapa halaman minimum untuk laporan?
**A:** Tidak ada minimum, focus pada quality. Typical: 20-30 halaman untuk kelompok.

### Q: Boleh menggunakan tools selain yang direkomendasikan?
**A:** Ya! Selama Anda dokumentasikan tools yang digunakan dan justify pemilihan.

### Q: Malware sample aman untuk didownload?
**A:** Ya dari sumber yang legitimate (MalwareBazaar). Tapi HARUS dalam VM isolated!

### Q: Laporan harus dalam Bahasa Indonesia atau Inggris?
**A:** Either is fine. Yang penting jelas dan profesional.

## 🆘 Getting Help

### Jika Mengalami Kesulitan:

1. **Check Documentation**
   - Baca README case dengan teliti
   - Check tools documentation
   - Search online for error messages

2. **Ask Instructor**
   - Email: [instructor-email]
   - Office Hours: [schedule]
   - Discussion Forum: [link]

3. **Community Resources**
   - DFIR Discord
   - Reddit communities
   - Stack Overflow

## ⚠️ Important Reminders

### Ethics & Legal
- ✅ Only use public datasets for educational purposes
- ✅ Analyze malware ONLY in isolated VMs
- ✅ Follow institutional policies
- ✅ Respect privacy and confidentiality
- ❌ NEVER use skills for illegal activities
- ❌ NEVER analyze malware on personal computers
- ❌ NEVER distribute malware

### Academic Integrity
- ✅ Work together as a team
- ✅ Cite sources properly
- ✅ Use provided templates
- ✅ Share knowledge within your group
- ❌ No plagiarism from other groups
- ❌ No sharing complete solutions between groups
- ❌ No copying from previous years

## 📞 Contact

**Instruktur:**
- Name: [Instructor Name]
- Email: [Email]
- Office: [Location]
- Office Hours: [Schedule]

**Teaching Assistants:**
- TA 1: [Name] - [Email]
- TA 2: [Name] - [Email]

---

## 🎉 Ready to Begin?

1. ✅ Kelompok sudah terbentuk?
2. ✅ Environment setup complete?
3. ✅ Case sudah ditugaskan oleh instruktur?
4. ✅ Read this guide?
5. ✅ Downloaded dataset?
6. ✅ Team roles sudah dibagi?

**Then let's start investigating! 🔍**

```bash
# Masuk ke folder case yang ditugaskan
cd cases/case-1-network-intrusion/
# atau case-2-malware-analysis/
# atau case-3-log-analysis/

# Read the case README
cat README.md

# Start team meeting!
# Good luck! 🚀
```

---

**Last Updated:** November 2025  
**Version:** 1.0
