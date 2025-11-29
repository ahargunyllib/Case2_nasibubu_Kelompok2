# Individual Contribution Report

- **Name:** Scorpian Erickda
- **Student ID:** 225150200111061  
- **Group:** 2  
- **Case:** Malware Analysis – Linux Static Analysis Script  
- **Date:** 29 November 2025  

---

## 1. My Role in the Team

**Primary Role:** Static Malware Analyst (Linux)

**Responsibilities:**
- Developing a Linux static analysis script to analyze Windows malware (.exe)
- Integrating tools: `file`, `strings`, `exiftool`, `objdump`, `rabin2`, hashing modules
- Preparing automated folder structure for evidence collection
- Providing Linux environment guidance to other team members
- Contributing analysis results to the team report

---

## 2. Tasks Completed

### **Week 1: Setup & Initial Analysis**

**Task 1: Environment setup & folder structure**  
**Time spent:** 2 hours  
**Output:**
- Automated folder structure generated in the script:
  - `analysis_<filename>/strings.txt`
  - `analysis_<filename>/metadata.txt`
  - etc.
- Script fully runnable on Kali Linux

**Task 2: Installing & testing tools (radare2, exiftool, objdump)**  
**Time spent:** 2 hours  
**Output:**  
- All tools functional and compatible with the script

---

### **Week 2: Deep Analysis**

**Task 3: Implement core static analysis code**  
**Time spent:** 3 hours  
**Output:**
- `filetype.txt`  
- `md5.txt` + `sha256.txt`  
- `strings.txt`  
- `metadata.txt`

**Task 4: Add objdump + radare2 analysis**  
**Time spent:** 2.5 hours  
**Output:**
- `objdump_headers.txt` → PE headers  
- `objdump_disasm.txt` → disassembly  
- `rabin2_info.txt` → PE details  
- `rabin2_strings.txt` → additional strings  

---

### **Week 3: Report & Presentation**

**Task 5: Implement packer detection (UPX, MPRESS, Themida)**  
**Time spent:** 1.5 hours  
**Output:**  
- `packer_detection.txt` (regex-based detection)

**Task 6: Final script testing & documentation**  
**Time spent:** 1 hour  
**Output:**  
- Full script functional  
- Evidence folder generated consistently  

---

### **Total Time Invested:** 12 hours

---

## 3. Tools & Techniques Used

### **Tools**

**radare2 / rabin2**  
Purpose: Deep PE structure analysis  
Usage:
- `rabin2 -I file.exe`
- `rabin2 -zz file.exe`  
Output:
- Section info  
- Import table  
- Hidden strings  

**exiftool**  
Purpose: Extracting PE metadata  
Output:
- Compilation timestamp  
- Original filename  
- File version metadata  

**objdump**  
Purpose: Header and disassembly analysis  
Usage:
- `objdump -x file.exe`
- `objdump -d file.exe`  
Output:
- Import table  
- Section sizes  
- Disassembled functions  

**strings**  
Purpose: Extract readable strings  
Output:
- API calls  
- URLs/domains  
- Packer signatures  

---

### **Analysis Techniques**
- Static PE analysis  
- Header inspection  
- Metadata extraction  
- Section mapping  
- Packer signature matching  

---

## 4. My Key Findings

### **Finding 1: Suspicious Metadata**
- **Description:** Metadata shows inconsistent timestamp  
- **Evidence:** `metadata.txt`  
- **Significance:** Possible compiler timestamp spoofing  
- **Contribution:** Automating metadata extraction

### **Finding 2: Suspicious API Imports**
- **Description:** Presence of VirtualAllocEx, WriteProcessMemory, CreateRemoteThread  
- **Evidence:** `objdump_headers.txt`  
- **Significance:** Indicates code injection behavior  
- **Contribution:** Extracting import list using objdump + rabin2

### **Finding 3: Packer Detection**
- **Description:** Detection of UPX/Aspack-like signatures  
- **Evidence:** `packer_detection.txt`  
- **Significance:** Malware likely packed  
- **Contribution:** Implemented regex-based packer signature module  

---

## 5. Report Sections I Contributed To

| Section | Contribution | Percentage |
|--------|-------------|------------|
| Executive Summary | Static analysis summary | 20% |
| Technical Analysis | Full Linux static analysis | 50% |
| Evidence Collection | All script-generated output | 100% |
| Timeline | Dev → analysis → testing | 30% |
| IoC List | Based on extracted strings | 40% |
| Recommendations | Packer & import analysis | 25% |
| Presentation Slides | - | - |

---

## 6. Collaboration Activities

### **Team Meetings Attended**
- Meeting 1: Tool requirements for Linux  
- Meeting 2: Integrating script evidence into report  
- Meeting 3: Finalization of evidence and technical explanation  

### **Communication**
- Primary channel: WhatsApp  
- Fast response and regular progress updates  

### **Helping Team Members**
- Assisting with malware sample testing  
- Sharing evidence folders  
- Explaining tool outputs  

---

## 7. Challenges & Solutions

### **Challenge 1:** Rabin2 error on corrupted PE  
**Solution:** Fallback to objdump  
**Outcome:** Analysis still completed successfully  

### **Challenge 2:** Strings output too large  
**Solution:** Separate strings file and use grep filtering  
**Outcome:** Faster IoC extraction  

### **Challenge 3:** Tools missing on default Kali installation  
**Solution:** Manual installation via `apt install`  
**Outcome:** All modules operational  

---

## 8. Skills Developed

### **Technical Skills**
- Bash scripting  
- radare2 competency  
- PE structure understanding  
- Packer signature recognition  

### **Soft Skills**
- Documentation  
- Cross-platform collaboration  
- Debugging  

---

## 9. What I Learned

### **Technical Knowledge**
- Deep PE structure  
- Objdump vs rabin2 differences  
- Regex-based packer detection  

### **Forensic Methodology**
- Static-based evidence collection  
- Systematic output logging  
- Importance of hashing  

### **Team Collaboration**
- Importance of fast communication  
- Clear role distribution improves analysis speed  

---

## 10. Self-Evaluation

### **Strengths**
- Developing the entire static analysis script  
- Clean and organized output  
- Strong technical depth  

### **Areas for Improvement**  
- Add import anomaly detection  

### **Overall Self-Assessment**
- **Contribution Level:** High  
- **Effort Level:** 9/10  
- **Quality of Work:** 9/10  

---

## 11. Peer Evaluation
(Optional)

---

## 12. Evidence of Work

Folder: `analysis_<filename>`  
- `filetype.txt`
- `md5.txt`
- `sha256.txt`
- `strings.txt`  
- `metadata.txt`  
- `objdump_headers.txt`  
- `objdump_disasm.txt`  
- `rabin2_info.txt` 
- `rabin2_strings.txt`
- `packer_detection.txt`


---

## 13. Presentation Contribution
- Slides on Linux static analysis  
- Explained script workflow  
- Explained functions of r2, objdump, exiftool  

---

## 14. Additional Comments
This project significantly improved my skills in:
- Bash scripting  
- Static malware analysis  
- Tool integration  

---

## Declaration
I declare that the information provided in this contribution report is accurate and reflects my individual work and contribution.

**Signature:** Scorpian Erickda  
**Date:** 29-11-2025
