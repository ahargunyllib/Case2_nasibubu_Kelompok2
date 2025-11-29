# **Laporan Kontribusi Individu**

**Nama:** Shinta Oktavia Ramadhani  
**NIM:** 235150207111036  
**Kelompok:** Nasibubu / Kelompok 2   
**Kasus:** Malware Analysis \- Agent Tesla  
**Tanggal:** 29 November 2025

## **1\. Peran Saya dalam Tim**

**Peran Utama:** Penulis Laporan  
**Tanggung Jawab:**

* Menulis dan menyusun seluruh laporan akhir berdasarkan temuan dan analisis tim bersama rekan **report writer** ( Catherine Nathania).  
* Mengorganisir dan menyunting laporan untuk memastikan konsistensi dan kejelasan dalam penyajian data.  
* Menyusun bagian Executive Summary dan memberikan masukan untuk bagian rekomendasi.

---

## **2\. Tugas yang Telah Diselesaikan**

### **Minggu 1: Setup & Analisis Awal**

* **Tugas 1: Pembagian Tugas dan Memilih Dataset**  
  * Waktu yang Dihabiskan: 1 jam   
  * Output: Dataset AgentTesla dan setiap masing masing anggota memiliki jobsdesk  
* **Tugas 2: Penyusunan Struktur Laporan**  
  * Waktu yang Dihabiskan: 1 jam  
  * Output: Menyusun template dan struktur laporan berdasarkan format yang telah ditentukan.

### **Minggu 2: Analisis Mendalam**

* **Tugas 3: Penyuntingan Bab I \- Executive Summary**  
  * Waktu yang Dihabiskan: 1 jam  
  * Output: Menyusun ringkasan eksekutif yang menjelaskan temuan utama secara singkat dan jelas.  
* **Tugas 4: Penyusunan Bab III \- Static Analysis Results**  
  * Waktu yang Dihabiskan: 1 jam  
  * Output: Menyusun hasil analisis statis terhadap file atau sampel malware untuk memperoleh wawasan tentang struktur file dan teknik anti-analisis yang digunakan.

### **Minggu 3: Laporan & Presentasi**

* **Tugas 5: Penyusunan Bab V \- Network Analysis**  
  * Waktu yang Dihabiskan: 1 jam  
    Output: Menyusun hasil analisis aspek jaringan dari serangan, yang termasuk dalam observasi Command-and-Control (C2), serta pola komunikasi yang digunakan oleh malware.  
* **Tugas 6: Penyusunan Bab VII \- MITRE ATT\&CK Mapping**  
  * Waktu yang Dihabiskan: ½ jam  
  * Output: Menyusun taktik yang digunakan oleh malware, misalnya: Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, dan lainnya berdasarkan hasil temuan oleh tim teknis.  
* **Tugas 6: Penyusunan Bab IX \- Rekomendasi**  
  * Waktu yang Dihabiskan: ½ jam  
  * Output: Menyusun bagian rekomendasi berdasarkan hasil analisis, mencakup langkah-langkah perbaikan dan pencegahan.

---

## **3\. Alat dan Teknik yang Digunakan**

### **Alat**

1. **Microsoft Word**  
   * Tujuan: Menggunakan untuk menyusun dan menyunting laporan.  
   * Fitur Utama: Pengaturan gaya teks, header, dan format referensi.  
   * Output: Laporan akhir yang siap untuk diserahkan.  
2. **VirusTotal**  
   * Tujuan: Menganalisis file yang mencurigakan dan mendapatkan informasi terkait file hash.  
   * Fitur Utama: Mengupload file dan memeriksa potensi ancaman.  
   * Output: Daftar file hash yang relevan dengan analisis malware.

### **Teknik Analisis**

* **PE Structure Analysis**: Digunakan untuk memeriksa struktur file PE malware, memastikan apakah ada indikasi manipulasi atau penggunaan teknik anti-analisis.  
* **Strings Analysis**: Digunakan untuk mencari string yang berhubungan dengan perintah atau komunikasi yang dilakukan oleh malware.

---

## **4\. Temuan Utama Saya**

### **Temuan 1: Identifikasi Keluarga Malware**

* **Deskripsi:** Saya mengidentifikasi keluarga malware yang digunakan dalam serangan ini, dengan mengaitkan pola yang ada pada malware yang dikenal.  
* **Bukti:** Referensi pada analisis statis dan dinamis yang dilakukan pada malware.  
* **Signifikansi:** Memahami keluarga malware ini memungkinkan tim untuk lebih memahami ancaman dan cara malware tersebut beroperasi.  
* **Kontribusi Saya:** Saya menyusun bagian yang menjelaskan tentang identifikasi malware dan keterkaitannya dengan ancaman yang ada.

### **Temuan 2: Mekanisme Persistensi Malware**

* **Deskripsi:** Malware ini mengimplementasikan mekanisme persistensi yang memungkinkan ia bertahan meskipun komputer direstart.  
* **Bukti:** Modifikasi pada registry dan file system yang ditemukan selama analisis dinamis.  
* **Signifikansi:** Penting untuk memastikan bahwa malware ini tidak dapat dengan mudah dihapus setelah serangan awal.  
  **Kontribusi Saya:** Saya membantu menjelaskan bagaimana malware berfungsi untuk bertahan dalam sistem.

---

## **5\. Bagian Laporan yang Saya Kontribusikan**

| Bagian | Kontribusi Saya | Persentase |
| :---- | :---- | :---- |
| Executive Summary | Menulis ringkasan eksekutif berdasarkan hasil temuan teknis (Malware family identification, Risk assessment, Impact summary, Key recommendations) | 100% |
| Technical Analysis | Membantu menyusun analisis teknis  (PE structure analysis, Strings analysis, Imported functions, Anti-analysis techniques detected, Embedded resources) | 30% |
| Evidence Collection | Menyusun bukti digital dalam laporan. | 20% |
| IoC List | Menyusun daftar indikator kompromi berdasarkan hasil analisis dalam laporan berdasarkan temuan teknis. | 15% |
| Recommendations | Menulis rekomendasi untuk langkah-langkah perbaikan dan pencegahan. | 100% |
| Presentation Slides | Lingkungan SetUp | 5% |
| Timeline | Persiapan \- Menyicil laporan \- Finalisasi | 75% |

---

## **6\. Kegiatan Kolaborasi**

### **Pertemuan Tim yang Diikuti**

* **Pertemuan 1 (12 November 2025\)**: Membahas struktur laporan dan pembagian tugas. Saya memberikan masukan tentang format laporan.  
* **Pertemuan 2 (19 November 2025\)**: Mendiskusikan temuan analisis malware, saya membantu menjelaskan temuan dalam bentuk laporan.  
* **Pertemuan 3 (26 November 2025\)**: Menyusun rekomendasi, saya memberikan masukan tentang langkah-langkah yang perlu diambil berdasarkan analisis.

### **Komunikasi**

* **Saluran Utama:** WhatsApp  
* **Waktu Respons:** Biasanya dalam 2 jam.  
* **Komunikasi Proaktif:** Saya sering memulai diskusi terkait format laporan dan mengingatkan untuk membuat laporan individu, serta progress masing masing

### **Membantu Anggota Tim**

* Membantu Catherine Nathania dalam menyusun Report Kelompok dan pemeriksaan kelengkapan data.  
* Berbagi pengetahuan tentang: Penyusunan daftar IoC.  
* Mereview: Bagian teknis laporan terkait analisis PE dan jaringan.

---

## **7\. Tantangan & Solusi**

### **Tantangan 1: Penyusunan Laporan yang Komprehensif**

* **Masalah:** Laporan membutuhkan banyak data teknis yang harus disusun dengan bahasa yang mudah dipahami.  
* **Dampak:** Memperlambat proses penyusunan laporan.  
  **Solusi Saya:** Mengorganisir laporan menjadi bagian-bagian yang lebih terstruktur dan mudah dipahami.  
* **Hasil:** Laporan menjadi lebih terorganisir dan dapat dipahami oleh pembaca dengan berbagai tingkat pemahaman.

---

## **8\. Keterampilan yang Dikembangkan**

### **Keterampilan Teknis**

* **Analisis PE**: Saya semakin menguasai analisis struktur file PE untuk identifikasi malware.  
* **Penggunaan Alat Forensik**: Penggunaan VirusTotal dan alat lainnya untuk analisis malware secara lebih efisien.

### **Keterampilan Sosial**

* **Kolaborasi Tim**: Saya belajar cara berkomunikasi lebih efektif dalam tim, terutama dalam mengorganisir bagian laporan dan berbagi informasi teknis.

---

## **9\. Apa yang Saya Pelajari**

### **Pengetahuan Teknikal**

* **Pemahaman Malware**: Saya belajar lebih banyak tentang bagaimana malware beroperasi di sistem dan bagaimana mengidentifikasi serta mencegahnya.  
* **Forensik Digital**: Saya memperdalam pemahaman saya mengenai analisis statis dan dinamis malware.

### **Metodologi Forensik**

* **Teknik Pengumpulan Bukti**: Saya memahami pentingnya pengumpulan bukti yang tepat untuk menganalisis dan melaporkan serangan siber secara akurat.

### **Kolaborasi Tim**

* **Kerja Sama Tim**: Saya belajar bagaimana berkolaborasi dalam proyek besar dan bagaimana mengkoordinasikan tugas dengan anggota tim lainnya.

---

## **10\. Evaluasi Diri**

### **Kekuatan dalam Proyek Ini**

* **Pengorganisasian Laporan**: Saya mampu mengorganisir laporan dengan baik dan memastikan semua bagian terstruktur dengan rapi.  
* **Kolaborasi**: Saya dapat bekerja dengan baik dalam tim dan memberikan masukan yang konstruktif.

### **Area untuk Peningkatan**

* **Proaktif dalam Tugas**: Saya bisa lebih proaktif dalam mengambil inisiatif tanpa menunggu instruksi.  
* **Detail Teknis**: Saya bisa lebih mendalami bagian teknis laporan agar lebih mendalam.

### **Penilaian Diri**

**Tingkat Kontribusi:** Sangat Tinggi  
 **Tingkat Usaha:** 10/10  
 **Kualitas Pekerjaan:** 9.5/10

**Justifikasi Singkat:** Saya memberikan kontribusi utama dalam menyusun laporan akhir, namun masih perlu meningkatkan pengetahuan teknis lebih lanjut.

---

**Deklarasi**  
Saya menyatakan bahwa informasi yang diberikan dalam laporan kontribusi ini akurat dan mencerminkan pekerjaan dan kontribusi saya dalam proyek kelompok ini.

**Tanda Tangan:** \-  
**Tanggal:** 29 November 2025

