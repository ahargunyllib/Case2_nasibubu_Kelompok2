# Laporan Analisis Statis - Detailed Report

## Informasi File Executable

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| **Nama File** | HnaZtD.exe | Nama internal executable |
| **Ukuran File** | 725 KB | Ukuran file di disk |
| **Tipe File** | PE32 Executable (GUI) | Windows 32-bit GUI application |
| **Arsitektur** | Intel 386 (x86) | 32-bit Intel compatible |
| **Framework** | .NET/Mono Assembly | Aplikasi berbasis .NET Framework |
| **MD5 Hash** | 5c22381ff243c8b3fc6984842168f2c7 | Hash MD5 untuk identifikasi |
| **SHA-256 Hash** | c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027 | Hash SHA-256 untuk verifikasi |
| **Timestamp** | Thu Aug 25 07:20:50 2061 | Timestamp kompilasi (anomali: tahun 2061!) |
| **Linker Version** | 48.0 | Versi linker yang digunakan |

### Anomali Terdeteksi
⚠️ **Timestamp kompilasi menunjukkan tahun 2061** - Ini tidak mungkin dan merupakan indikator manipulasi timestamp atau teknik anti-forensik.

---

## Ringkasan Eksekutif

Berikut adalah hasil analisis statis dari beberapa file output tools terhadap file executable yang dianalisis. File ini teridentifikasi sebagai aplikasi manajemen penginapan (Pansiyon) berbasis .NET dengan indikasi penggunaan packer UPX. Temuan utama disajikan dalam bentuk tabel dan poin.


## 1. objdump_disasm.txt - Disassembly Code
**Deskripsi:** Hasil disassembly dari bagian kode executable (.text section).

| Temuan Utama | Detail |
|--------------|--------|
| **Instruksi** | x86 assembly khas Windows |
| **Entry Point** | 0x004b0076 |
| **Code Section** | .text (0x402000 - 0x4b007c) |
| **Ukuran Code** | 713,728 bytes (0xae400) |
| **Pattern** | Tidak ditemukan kode yang jelas ter-obfuscate atau berbahaya |

**Penjelasan Detail:**

Disassembly adalah proses mengubah kode mesin (machine code) menjadi instruksi assembly yang dapat dibaca manusia. Pada file ini, hasil disassembly menunjukkan:

**Karakteristik Kode:**
- Menggunakan instruksi x86 standar yang umum pada aplikasi Windows
- Entry point berada di alamat 0x004b0076 (dalam range .text section)
- Tidak ditemukan instruksi mencurigakan seperti:
  - Self-modifying code
  - Teknik anti-debugging explicit
  - Direct system calls untuk injection
  - Instruksi obfuscation tingkat tinggi

**Catatan Penting:**
- File ini menggunakan packer UPX, sehingga kode yang terlihat mungkin hanya stub unpacker
- Kode asli aplikasi kemungkinan masih terkompresi dan akan di-unpack saat runtime
- Analisis dinamis diperlukan untuk melihat kode sebenarnya setelah unpacking


## 2. objdump_headers.txt - PE Headers & Sections
**Deskripsi:** Informasi header dan section PE (Portable Executable).

### Header PE32

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| **Magic** | 010b (PE32) | Format PE 32-bit |
| **Subsystem** | 0x00000002 | Windows GUI Application |
| **Image Base** | 0x00400000 | Base address di memory |
| **Entry Point** | 0x000b0076 | RVA dari entry point |
| **Section Alignment** | 0x00002000 (8KB) | Alignment section di memory |
| **File Alignment** | 0x00000400 (1KB) | Alignment di file |
| **OS Version** | 4.0 | Target minimum Windows |
| **Subsystem Version** | 6.0 | Windows Vista+ |

### DLL Characteristics

| Fitur Keamanan | Status | Keterangan |
|----------------|--------|------------|
| **HIGH_ENTROPY_VA** | ✅ Aktif | 64-bit address space randomization |
| **DYNAMIC_BASE** | ✅ Aktif | ASLR (Address Space Layout Randomization) |
| **NX_COMPAT** | ✅ Aktif | Data Execution Prevention (DEP) |
| **NO_SEH** | ✅ Aktif | Tidak menggunakan SEH |
| **TERMINAL_SERVICE_AWARE** | ✅ Aktif | Terminal Services compatible |

### Section Details

| Nama | VMA | Size | File Offset | Karakteristik |
|------|-----|------|-------------|---------------|
| **.text** | 0x00402000 | 0xae07c | 0x00000400 | Code section (executable, readable) |
| **.rsrc** | 0x004b2000 | 0x0239c | 0x000ae800 | Resource section (readonly, data) |
| **.reloc** | 0x004b6000 | 0x0000c | 0x000b0c00 | Relocation section (readonly, data) |

### Import Table

| DLL | Function | Keterangan |
|-----|----------|------------|
| **mscoree.dll** | _CorExeMain | .NET Runtime Entry Point |

**Penjelasan Detail:**

**Karakteristik .NET Application:**
File ini adalah aplikasi .NET yang dikompilasi menjadi native PE. Bukti:
- Import hanya dari `mscoree.dll` (Microsoft Common Object Runtime Execution Engine)
- Fungsi `_CorExeMain` adalah entry point standar untuk .NET executable
- Terdapat CLR Runtime Header di Data Directory (Entry 14)

**Debug Information:**
- Debug directory menunjuk ke file PDB: `C:\Users\Administrator\Desktop\Client\Temp\hJafkVGgZB\src\obj\Debug\HnaZtD.pdb`
- Path ini mengindikasikan kompilasi dalam mode Debug
- GUID debug: 2846d6f7de3f4f03bcd220ac60bb6937

**Resource Directory:**
File memiliki 3 tipe resource:
- Type 0x03 (Icon group)
- Type 0x0e (Icon)
- Type 0x10 (Version info)

**Kesimpulan Header:**
- Tidak ada anomali struktural pada header PE
- Section standar dan ukuran wajar
- Fitur keamanan modern aktif (ASLR, DEP)
- Aplikasi .NET legitimate dengan debug info


## 3. packer_detection.txt - Packer Analysis
**Deskripsi:** Deteksi signature packer/compression tools.

| Temuan | Status | Level Risiko |
|--------|--------|--------------|
| **Packer Terdeteksi** | ✅ UPX | ⚠️ Sedang |
| **Signature** | UPX packer signature detected | - |
| **Implikasi** | File terkompresi/obfuscated | - |

**Penjelasan Detail:**

**Tentang UPX (Ultimate Packer for eXecutables):**
- UPX adalah packer open-source yang legal dan umum digunakan
- Fungsi utama: mengkompresi executable untuk mengurangi ukuran file
- Dapat di-unpack dengan tool `upx -d`

**Mengapa UPX Digunakan:**

✅ **Penggunaan Legitimate:**
1. Mengurangi ukuran file untuk distribusi
2. Menghemat bandwidth dan storage
3. Mempercepat download

⚠️ **Penggunaan Berbahaya:**
1. Menyembunyikan kode malicious dari antivirus
2. Mempersulit analisis statis
3. Menghindari signature-based detection
4. Obfuscation code untuk anti-reversing

**Implikasi pada File Ini:**
- Kode .NET asli terkompresi dan tidak dapat dilihat sepenuhnya
- String dan resource dapat ter-obfuscate
- Entry point mengarah ke unpacking stub, bukan kode aplikasi asli
- Analisis statis terbatas karena kode masih packed

**Rekomendasi:**
1. **Unpack file** menggunakan: `upx -d HnaZtD.exe`
2. Setelah unpacking, lakukan analisis ulang untuk melihat kode asli
3. Gunakan .NET decompiler (dnSpy, ILSpy) pada file yang sudah di-unpack
4. Lakukan analisis dinamis di sandbox untuk melihat behavior runtime

**Status Risiko:**
- ⚠️ **Sedang** - Packer legitimate tapi sering disalahgunakan
- Perlu unpacking dan analisis lanjutan untuk memastikan tidak ada malicious code


## 4. rabin2_info.txt - Binary Metadata & Security Features
**Deskripsi:** Metadata binary dan analisis fitur keamanan.

### Informasi Binary

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| **Architecture** | x86 | 32-bit Intel |
| **Binary Type** | PE | Portable Executable |
| **Bits** | 32 | 32-bit application |
| **Class** | PE32 | PE32 format |
| **Base Address** | 0x400000 | Load address di memory |
| **Binary Size** | 724,992 bytes | Ukuran file binary |
| **Language** | CIL (Common Intermediate Language) | .NET bytecode |
| **Machine** | i386 | Intel 386+ compatible |
| **OS** | Windows | Target platform Windows |
| **Subsystem** | Windows GUI | GUI application |
| **Endian** | Little | Little-endian byte order |

### Fitur Keamanan

| Fitur | Status | Fungsi Proteksi |
|-------|--------|-----------------|
| **Canary** | ✅ True | Stack overflow protection |
| **NX (DEP)** | ✅ True | Data Execution Prevention |
| **PIC** | ✅ True | Position Independent Code (ASLR support) |
| **RELOCS** | ❌ False | No relocation table |
| **Stripped** | ❌ False | Debug symbols masih ada |
| **Static** | ❌ False | Dynamically linked |
| **Signed** | ❌ False | Tidak ada digital signature |
| **Crypto** | ❌ False | No cryptographic operations detected |

### Informasi Debug

| Parameter | Nilai |
|-----------|-------|
| **Debug File** | C:\Users\Administrator\Desktop\Client\Temp\hJafkVGgZB\src\obj\Debug\HnaZtD.pdb |
| **GUID** | 2846D6F7DE3F4F03BCD220AC60BB69371 |
| **Build Mode** | Debug (not stripped) |
| **Line Numbers** | False |
| **Local Symbols** | False |

### Checksum & Compilation

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| **Computed Checksum** | 0x000b580d | Checksum yang dihitung |
| **Header Checksum** | 0x00000000 | Tidak ada checksum di header |
| **Compilation Time** | Thu Aug 25 07:20:50 2061 | ⚠️ Timestamp anomali! |
| **Overlay** | False | Tidak ada data overlay |

**Penjelasan Detail:**

**Fitur Keamanan Aktif:**

1. **Canary (Stack Protector)**
   - Proteksi terhadap buffer overflow attacks
   - Mendeteksi stack corruption sebelum return

2. **NX/DEP (Data Execution Prevention)**
   - Memory pages ditandai non-executable
   - Mencegah eksekusi shellcode di stack/heap

3. **PIC/ASLR Support**
   - Address randomization untuk mempersulit exploitation
   - Setiap run, memory layout berbeda

**Kelemahan Keamanan:**

1. **Tidak Ada Digital Signature**
   - File tidak ditandatangani secara digital
   - Tidak dapat diverifikasi publisher/author
   - Lebih mudah untuk dipalsukan

2. **Debug Symbols Masih Ada**
   - File tidak di-strip
   - Memudahkan reverse engineering
   - Informasi debugging tersedia

3. **No Checksum di Header**
   - Integritas file tidak dapat diverifikasi via PE header
   - Checksum header = 0x00000000

**Path Debug Suspicious:**
```
C:\Users\Administrator\Desktop\Client\Temp\hJafkVGgZB\src\obj\Debug\HnaZtD.pdb
```
- Path menunjuk ke folder temporary (`Temp`)
- Folder dengan nama random (`hJafkVGgZB`)
- Indikasi build automated atau temporary compilation

**Anomali Timestamp:**
⚠️ **Waktu kompilasi: 2061** - Ini tidak mungkin dan merupakan red flag yang menunjukkan:
- Manipulasi timestamp untuk menghindari deteksi
- Anti-forensic technique
- Reproducible build dengan timestamp fake


## 5. rabin2_strings.txt - String Analysis
**Deskripsi:** String yang diekstrak dari binary (via rabin2) - Total 12,517 strings.

### Ringkasan String Terdeteksi

| Kategori | Jumlah | Contoh |
|----------|--------|--------|
| **UI Components** | ~200+ | button1-12, label1-12, listView1-2, comboBox1, groupBox1-2 |
| **Form Names** | 10+ | FrmAnaForm, FrmOdalar, FrmMesajlar, FrmStoklar, FrmGelirGider |
| **.NET Classes** | 500+ | System.Data, System.IO, System.Linq, System.Windows.Forms |
| **SQL Strings** | 5+ | Connection strings, SQL queries |
| **Resource Files** | 10+ | Pansiyon_kayıt1.*.resources |
| **Variables** | 100+ | Txt*, Btn*, Lbl*, Dt* (Hungarian notation) |

### Identifikasi Aplikasi

**Nama Aplikasi:** Sistem Manajemen Pansiyon (Penginapan)
**Namespace:** `Pansiyon_kayıt1` (Pansiyon Registration System)

**Form/Modul Terdeteksi:**

| Form Name | Fungsi | Komponen Utama |
|-----------|--------|----------------|
| **FrmYeniMüsteri** | Form Customer Baru | Input data tamu baru |
| **FrmMüsteriler** | List Customer | Daftar semua tamu |
| **FrmAnaForm** | Form Utama | Dashboard/main menu |
| **FrmOdalar** | Manajemen Kamar | BtnOda101-109 (9 kamar) |
| **FrmMesajlar** | Pesan/Messages | Sistem messaging |
| **FrmStoklar** | Inventory/Stok | TxtGıdalar, Txtıcecekler, Txtatıştırmalıklar |
| **FrmGelirGider** | Income/Expense | Laporan keuangan |
| **FrmGazeteler** | Koran/Berita | WebBrowser untuk baca koran |
| **FrmMüzik** | Musik Player | axWindowsMediaPlayer1 |
| **FrmAdminGiris** | Login Admin | TxtKullanıcıAdı, TxtSifre, BtnGiriş |

### String Database Connection

**⚠️ TEMUAN KRITIS - Hardcoded Connection String:**

```sql
Data Source=AKTAS;Initial Catalog=AyCicegiPansiyon;Integrated Security=True;
```

**Detail:**
- **Server Name:** AKTAS
- **Database Name:** AyCicegiPansiyon (Pansiyon Bunga Matahari)
- **Authentication:** Windows Integrated Security
- **Protocol:** Tidak dispesifikasi (default TCP)

### SQL Query Terdeteksi

**Query 1 - Admin Login Authentication:**
```sql
select * from AdminGiris where Kullanici =@KullaniciAdi AND Sifre=@Sifresi
```
- Tabel: `AdminGiris`
- Parameter: `@KullaniciAdi`, `@Sifresi`
- ⚠️ **Potensi kerentanan:** SQL Injection jika tidak diparameterize dengan benar

### Komponen .NET Framework

**Namespace Utama:**
- `System.Data` - Database operations
- `System.Data.SqlClient` - SQL Server connectivity
- `System.Windows.Forms` - Windows Forms UI
- `System.IO` - File operations
- `System.Linq` - LINQ queries
- `System.Collections.Generic` - Collections
- `System.Security.Cryptography` - Crypto operations (RNGCryptoServiceProvider)
- `AxInterop.WMPLib` - Windows Media Player
- `System.Text.RegularExpressions` - Regex

### UI Components (Hungarian Notation)

| Prefix | Tipe Control | Contoh |
|--------|--------------|--------|
| **Txt** | TextBox | TxtTc, TxtOdano, TxtUcret, TxtSifre |
| **Btn** | Button | BtnKaydet, BtnGüncelle, BtnTemizle, BtnAra, BtnDolu, BtnBoş |
| **Lbl** | Label | Lblalınan1-3, LblFaturalar1-3, Lblmaas, Lblsonuc |
| **Dt** | DateTimePicker | DtGiriş, DtÇıkış |
| **Cmb** | ComboBox | comboBox1 |

### Fitur Aplikasi Terdeteksi

**1. Manajemen Kamar:**
- 9 kamar tersedia (Oda 101-109)
- Status kamar: Dolu (Full), Boş (Empty)
- Button untuk setiap kamar

**2. Customer Management:**
- Input TC (Turkish ID number)
- Check-in/check-out dates
- Biaya (Ucret)
- Customer search (BtnAra)

**3. Financial Module:**
- Income tracking (Gelir)
- Expense tracking (Gider)
- Invoice management (Faturalar)

**4. Inventory:**
- Food items (Gıdalar)
- Beverages (İcecekler)
- Snacks (Atıştırmalıklar)

**5. Additional Features:**
- Message system
- News reader (Gazeteler)
- Music player
- Admin authentication

### Keamanan & Kerentanan

**✅ Temuan Positif:**
- Menggunakan `System.Security.Cryptography.RNGCryptoServiceProvider` (random number generator yang aman)
- Parameterized SQL queries (`@KullaniciAdi`, `@Sifresi`)
- Password field dengan mask (`UseSystemPasswordChar`)

**⚠️ Temuan Negatif:**
1. **Hardcoded Connection String** - Credentials di dalam binary
2. **Integrated Security** - Bergantung pada Windows authentication
3. **Tidak ada enkripsi password** - Password validation di database
4. **Debug strings** - Banyak string debug masih ada

### String Mencurigakan

**Tidak ditemukan:**
- ❌ URL C2 (Command & Control)
- ❌ Hardcoded credentials (selain connection string)
- ❌ Shell commands
- ❌ Registry manipulation strings
- ❌ Network exploitation strings
- ❌ Encryption/obfuscation indicators

**Catatan:**
String-string ini konsisten dengan aplikasi legitimate hotel/penginapan management system berbahasa Turki.


## 6. File Hashes - Fingerprint & Verification
**Deskripsi:** Hash kriptografis untuk identifikasi dan verifikasi file.

### Hash Values

| Algorithm | Hash Value |
|-----------|------------|
| **MD5** | `5c22381ff243c8b3fc6984842168f2c7` |
| **SHA-256** | `c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027` |

### Kegunaan Hash

**1. Verifikasi Integritas:**
- Memastikan file tidak dimodifikasi
- Deteksi perubahan/korupsi file
- Validasi autentisitas

**2. Threat Intelligence Lookup:**

Gunakan hash untuk pencarian di:

| Service | URL | Fungsi |
|---------|-----|--------|
| **VirusTotal** | virustotal.com/gui/file/[SHA256] | Multi-antivirus scan |
| **Hybrid Analysis** | hybrid-analysis.com | Sandbox analysis |
| **Any.Run** | app.any.run | Interactive malware analysis |
| **MalwareBazaar** | bazaar.abuse.ch | Malware database |
| **AlienVault OTX** | otx.alienvault.com | Threat intelligence |

**3. Digital Forensics:**
- Timeline reconstruction
- Chain of custody
- Evidence preservation

### Cara Pengecekan

**VirusTotal (Recommended):**
```bash
# Via Web
https://www.virustotal.com/gui/file/c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027

# Via CLI (jika ada API key)
vt file c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027
```

**PowerShell Hash Verification:**
```powershell
# Verifikasi MD5
Get-FileHash -Algorithm MD5 HnaZtD.exe

# Verifikasi SHA256
Get-FileHash -Algorithm SHA256 HnaZtD.exe
```

### Interpretasi Hasil

**Jika hash ditemukan di database:**
- ✅ File dikenal dan sudah dianalisis
- ⚠️ Cek detection ratio dan vendor reports
- ❌ Jika flagged sebagai malware → High risk

**Jika hash tidak ditemukan:**
- 📝 File baru atau custom-made
- 🔍 Perlu analisis manual lebih lanjut
- ⚠️ Tidak berarti file aman

**Rekomendasi:**
1. Upload file ke VirusTotal untuk multi-engine scanning
2. Cek reputation score dan vendor detections
3. Review behavior analysis results
4. Cross-reference dengan Hybrid Analysis untuk sandbox report


## 7. strings.txt - Complete String Dump
**Deskripsi:** Dump lengkap seluruh string ASCII/Unicode dari executable.

### Statistik String

| Metric | Value |
|--------|-------|
| **Total Strings** | 12,517+ strings |
| **Format** | ASCII & UTF-16LE (Unicode) |
| **Kategori** | UI, .NET classes, SQL, resources |
| **Bahasa** | English (framework), Turkish (UI) |

### Analisis Konten

File strings.txt berisi dump lengkap dari rabin2_strings.txt dengan detail tambahan. Konten sama seperti analisis sebelumnya pada rabin2_strings.txt.

**Temuan Identik:**
- UI components dan form names
- Database connection strings
- SQL queries
- .NET framework classes
- Turkish language UI strings

### String Pattern Analysis

**1. .NET Metadata:**
```
System, System.Data, System.Windows.Forms, System.Linq
mscorlib, System.Core, System.Reflection
CompilerGeneratedAttribute, DebuggerNonUserCodeAttribute
```

**2. Form Resources:**
```
Pansiyon_kayıt1.FrmYeniMüsteri.resources
Pansiyon_kayıt1.FrmMüzik.resources
Pansiyon_kayıt1.FrmAnaForm.resources
```

**3. UI Controls (Turkish):**
```
BtnGiriş (Login Button)
BtnGüncelle (Update Button)
BtnTemizle (Clear Button)
Lblalınan (Label Received)
```

**4. Database Operations:**
```
SqlConnection, SqlCommand, SqlDataReader
ExecuteReader, ExecuteNonQuery
DbConnection, DbCommand, DbDataReader
```

### Tidak Ditemukan

**String Mencurigakan yang TIDAK ada:**
- ❌ Command & Control (C2) URLs
- ❌ Hard-coded IP addresses (selain localhost)
- ❌ Shell commands atau script execution
- ❌ Registry key manipulation
- ❌ Process injection strings
- ❌ Keylogger indicators
- ❌ Network scanning tools
- ❌ Backdoor command strings
- ❌ Encryption key exchange
- ❌ Stealth/hiding techniques

### Kesimpulan String Analysis

**Karakteristik:**
- String konsisten dengan aplikasi hotel management legitimate
- Bahasa pemrograman dan framework standar (.NET)
- Tidak ada indikator malicious behavior
- UI berbahasa Turki menunjukkan target audience

**Catatan Penting:**
⚠️ Karena file menggunakan UPX packer, beberapa string mungkin tersembunyi dan akan muncul setelah runtime unpacking. Analisis dinamis diperlukan untuk melihat string yang muncul saat runtime.

---

## 8. metadata.txt - ExifTool Metadata Analysis
**Deskripsi:** Metadata file yang diekstrak menggunakan ExifTool.

### File Information

| Parameter | Nilai | Keterangan |
|-----------|-------|------------|
| **File Name** | c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027.exe | Hash sebagai nama |
| **File Size** | 725 kB | 724,992 bytes |
| **File Type** | Win32 EXE | Windows Executable |
| **MIME Type** | application/octet-stream | Binary executable |

### Version Information

| Parameter | Nilai | Status |
|-----------|-------|--------|
| **Internal Name** | HnaZtD.exe | ⚠️ Random name |
| **Original File Name** | HnaZtD.exe | - |
| **File Version** | 0.0.0.0 | ⚠️ Not versioned |
| **Product Version** | 0.0.0.0 | ⚠️ Not versioned |
| **Assembly Version** | 0.0.0.0 | ⚠️ Not versioned |
| **File Description** | (empty) | ⚠️ No description |
| **Legal Copyright** | (empty) | ⚠️ No copyright |

### Timestamps

| Type | Timestamp | Status |
|------|-----------|--------|
| **Compilation** | 2061:08:25 07:20:50 | ⚠️ ANOMALI - Future date! |
| **File Modification** | 2025:11:19 03:24:54 | Normal |
| **File Access** | 2025:11:18 23:24:18 | Normal |

### Red Flags

**1. Timestamp Manipulation:**
- Compilation: **2061** (38 tahun di masa depan!)
- Anti-forensic technique
- Reproducible build atau fake timestamp

**2. Missing Version Info:**
- All versions: 0.0.0.0
- No description, no copyright
- Not production-ready metadata

**3. Random Internal Name:**
- `HnaZtD.exe` (random characters)
- Tidak deskriptif
- Tidak match dengan tujuan aplikasi

---

## 9. filetype.txt - File Type Detection

```
PE32 executable (GUI) Intel 80386 Mono/.Net assembly, for MS Windows, 3 sections
```

**Konfirmasi:**
- ✅ PE32 executable
- ✅ Windows GUI application
- ✅ .NET/Mono assembly
- ✅ 3 sections (.text, .rsrc, .reloc)

---

## Ringkasan & Kesimpulan Analisis

### Identifikasi Aplikasi

**Nama:** Sistem Manajemen Pansiyon (Penginapan/Hotel)  
**Framework:** .NET Framework  
**Bahasa:** C# (CIL bytecode)  
**Target:** Windows (Vista+)  
**Database:** SQL Server (AyCicegiPansiyon)  

### Fungsionalitas Aplikasi

| Modul | Fungsi |
|-------|--------|
| **Customer Management** | Registration, check-in/out, customer list |
| **Room Management** | 9 rooms (Oda 101-109), status tracking |
| **Financial** | Income/expense tracking, invoicing |
| **Inventory** | Food, beverages, snacks tracking |
| **Messaging** | Internal messaging system |
| **Media** | News reader, music player |
| **Authentication** | Admin login system |

### Temuan Keamanan

#### ✅ Aspek Positif

1. **Security Features Aktif:**
   - Stack Canary (buffer overflow protection)
   - NX/DEP (data execution prevention)
   - ASLR support (address randomization)

2. **Coding Practices:**
   - Parameterized SQL queries
   - Cryptographically secure RNG
   - Password masking di UI

3. **No Malicious Indicators:**
   - Tidak ada C2 URLs
   - Tidak ada shell commands
   - Tidak ada backdoor strings
   - Tidak ada keylogger indicators

#### ⚠️ Red Flags & Kerentanan

1. **UPX Packer:**
   - File terkompresi
   - Mempersulit analisis statis
   - Sering digunakan malware
   - Perlu unpacking untuk analisis penuh

2. **Timestamp Anomali:**
   - Compilation date: 2061 (impossible)
   - Anti-forensic technique
   - Menunjukkan manipulasi metadata

3. **Hardcoded Credentials:**
   - Database connection string di binary
   - Server: AKTAS
   - Database: AyCicegiPansiyon
   - Integrated Security (Windows auth)

4. **No Digital Signature:**
   - File tidak ditandatangani
   - Publisher tidak terverifikasi
   - Mudah dipalsukan

5. **Debug Build:**
   - Debug symbols present
   - PDB path exposed
   - Memudahkan reverse engineering

6. **Version Information Kosong:**
   - All versions: 0.0.0.0
   - No copyright
   - Not production-ready

### Risk Assessment

| Kategori | Level | Keterangan |
|----------|-------|------------|
| **Malware Indicators** | 🟢 Low | No clear malicious patterns |
| **Code Obfuscation** | 🟡 Medium | UPX packer present |
| **Security Practices** | 🟡 Medium | Some vulnerabilities |
| **Metadata Integrity** | 🔴 High | Timestamp manipulation |
| **Overall Risk** | 🟡 **Medium** | Needs further analysis |

### Rekomendasi Tindakan

#### 1. Immediate Actions

**A. Hash Verification:**
```bash
# Check VirusTotal
https://www.virustotal.com/gui/file/c91267225764229b8a282e938b02a1408997d0d1e5558ca841a009bade568027
```

**B. Unpack File:**
```bash
# Using UPX
upx -d HnaZtD.exe -o HnaZtD_unpacked.exe
```

**C. .NET Decompilation:**
```bash
# Using dnSpy or ILSpy on unpacked file
dnspy HnaZtD_unpacked.exe
```

#### 2. Dynamic Analysis

**A. Sandbox Analysis:**
- Upload ke ANY.RUN
- Upload ke Hybrid Analysis
- Monitor behavior di isolated VM

**B. Network Monitoring:**
```powershell
# Monitor network connections
netstat -ano | Select-String "ESTABLISHED"
```

**C. Process Monitoring:**
```powershell
# Monitor created processes
Get-Process | Where-Object {$_.StartTime -gt (Get-Date).AddMinutes(-5)}
```

#### 3. Code Review (After Unpacking)

**Focus Areas:**
1. Authentication mechanism
2. SQL query construction
3. Data encryption methods
4. Network communication
5. File system operations
6. Registry access

#### 4. Security Hardening

**If Legitimate Application:**
1. Request signed version from developer
2. Implement network isolation
3. Use prepared statements for all SQL
4. Encrypt connection strings
5. Enable audit logging
6. Regular security updates

#### 5. Forensic Investigation

**If Suspicious:**
1. Memory dump analysis
2. String extraction from runtime
3. API call monitoring
4. Registry change tracking
5. File system monitoring

### Kesimpulan Akhir

**Aplikasi ini adalah:**
- ✅ Aplikasi legitimate hotel management system (berdasarkan string dan functionality)
- ⚠️ Dikemas dengan UPX packer (perlu unpacking)
- ⚠️ Memiliki timestamp anomali (red flag)
- ⚠️ Tidak memiliki digital signature
- ⚠️ Menggunakan debug build (not production-ready)

**Rekomendasi:**
1. **TIDAK RUN** tanpa analisis lebih lanjut
2. **Unpack** menggunakan UPX terlebih dahulu
3. **Upload** ke VirusTotal untuk multi-engine scan
4. **Decompile** .NET code untuk review source
5. **Run** di sandbox/VM terisolasi untuk behavior analysis
6. **Monitor** network dan system activities

**Risk Level: MEDIUM** - Perlu investigasi lebih lanjut sebelum deployment atau execution.

---

## Lampiran: Cara Analisis Lanjutan

### A. Unpacking UPX

```bash
# Download UPX
https://upx.github.io/

# Unpack executable
upx -d HnaZtD.exe

# Verify unpacked file
file HnaZtD.exe
```

### B. .NET Decompilation

**Tools:**
- dnSpy (recommended)
- ILSpy
- dotPeek
- JustDecompile

**Steps:**
1. Open unpacked file di dnSpy
2. Browse namespaces dan classes
3. Review authentication logic
4. Check SQL queries implementation
5. Analyze network operations

### C. Sandbox Analysis

**Online Sandboxes:**
- ANY.RUN (interactive)
- Hybrid Analysis (automated)
- Joe Sandbox
- Cuckoo Sandbox (self-hosted)

**What to Monitor:**
- Network connections
- File operations
- Registry modifications
- Process creation
- API calls

### D. Network Traffic Analysis

```powershell
# Capture traffic with Wireshark
# Filter: ip.addr == [target IP]

# Check DNS queries
# Check HTTP/HTTPS connections
# Look for suspicious protocols
```

---

**📝 Laporan dibuat:** 25 November 2025  
**🔍 Tools digunakan:** objdump, rabin2, ExifTool, strings, UPX detector  
**📊 Total analisis:** 9 files  
**⏱️ Metode:** Static Analysis

