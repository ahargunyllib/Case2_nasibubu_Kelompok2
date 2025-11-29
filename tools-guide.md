# Malware Analysis Tools & Resources

## 🛠️ Essential Tools Installation

### Windows Analysis VM (FlareVM)

FlareVM is a fully configured Windows-based malware analysis environment.

```powershell
# Install FlareVM (Run in PowerShell as Administrator)
# WARNING: This will modify your Windows installation significantly
# Only run on a dedicated VM!

Set-ExecutionPolicy Unrestricted -Force
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/mandiant/flare-vm/main/install.ps1') | iex
```

### Linux Analysis VM (REMnux)

REMnux is a Linux toolkit for reverse engineering malware.

```bash
# Install REMnux
wget https://REMnux.org/remnux-cli
chmod +x remnux-cli
sudo ./remnux-cli install
```

### Manual Tool Installation

#### Python Analysis Tools
```bash
# Core analysis libraries
pip install pefile
pip install yara-python
pip install oletools
pip install pycryptodome
pip install capstone  # Disassembly
pip install unicorn   # CPU emulator

# Optional but useful
pip install virustotal-api
pip install requests
pip install colorama
```

#### Static Analysis Tools

1. **Detect It Easy (DiE)**
   ```
   Platform: Windows, Linux, macOS
   Download: https://github.com/horsicq/Detect-It-Easy/releases
   Purpose: File type detection, packer identification
   ```

2. **pestudio**
   ```
   Platform: Windows
   Download: https://www.winitor.com/download
   Purpose: Comprehensive PE analysis
   ```

3. **PE-bear**
   ```
   Platform: Windows
   Download: https://github.com/hasherezade/pe-bear/releases
   Purpose: PE file viewer and editor
   ```

4. **IDA Free**
   ```
   Platform: Windows, Linux, macOS
   Download: https://hex-rays.com/ida-free/
   Purpose: Disassembler and debugger
   ```

5. **Ghidra**
   ```
   Platform: Windows, Linux, macOS
   Download: https://ghidra-sre.org/
   Purpose: NSA's reverse engineering tool
   ```

#### Dynamic Analysis Tools

1. **Sysinternals Suite**
   ```
   Platform: Windows
   Download: https://docs.microsoft.com/en-us/sysinternals/
   
   Key tools:
   - Process Monitor (procmon.exe)
   - Process Explorer (procexp.exe)
   - TCPView (tcpview.exe)
   - Autoruns (autoruns.exe)
   ```

2. **Regshot**
   ```
   Platform: Windows
   Download: https://sourceforge.net/projects/regshot/
   Purpose: Registry snapshot comparison
   ```

3. **FakeNet-NG**
   ```
   Platform: Windows
   Installation: pip install fakenet-ng
   Purpose: Network simulation for malware analysis
   ```

4. **INetSim**
   ```
   Platform: Linux
   Installation: apt-get install inetsim
   Purpose: Simulate internet services
   ```

## 📊 Online Analysis Platforms

### Sandbox Services

1. **ANY.RUN**
   - URL: https://app.any.run/
   - Free tier available
   - Interactive sandbox
   - Real-time analysis

2. **Hybrid Analysis**
   - URL: https://www.hybrid-analysis.com/
   - Free
   - Automated reports
   - API access

3. **Joe Sandbox**
   - URL: https://www.joesandbox.com/
   - Limited free analysis
   - Detailed reports

4. **Cuckoo Sandbox**
   - Self-hosted
   - Open source
   - Highly customizable
   - Setup: https://cuckoosandbox.org/

### Threat Intelligence

1. **VirusTotal**
   - URL: https://www.virustotal.com/
   - Multi-AV scanning
   - Behavior analysis
   - API available

2. **MalwareBazaar**
   - URL: https://bazaar.abuse.ch/
   - Malware sample repository
   - Free download
   - API access

3. **URLhaus**
   - URL: https://urlhaus.abuse.ch/
   - Malicious URL database

4. **ThreatFox**
   - URL: https://threatfox.abuse.ch/
   - IoC database

## 🔍 Analysis Techniques

### Static Analysis Workflow

```bash
# 1. Calculate hashes
md5sum sample.exe
sha1sum sample.exe
sha256sum sample.exe

# 2. File type identification
file sample.exe

# 3. Check VirusTotal
# Upload hash at virustotal.com

# 4. String extraction
strings sample.exe > strings.txt
strings -el sample.exe > strings_unicode.txt

# 5. PE analysis (if PE file)
python static_analyzer.py sample.exe

# 6. Disassembly
# Use IDA Free or Ghidra
```

### Dynamic Analysis Workflow

```powershell
# Windows Analysis VM

# 1. Take VM snapshot
# Name: "Clean State - Before Analysis"

# 2. Start monitoring tools
# - Process Monitor (with appropriate filters)
# - Process Explorer
# - Wireshark
# - Regshot (take "1st shot")

# 3. Execute malware
.\sample.exe

# 4. Observe for 5-10 minutes
# Watch for:
# - New processes
# - File modifications
# - Network connections
# - Registry changes

# 5. Stop monitoring and collect data
# - Save ProcMon logs
# - Stop Wireshark capture
# - Take Regshot "2nd shot" and compare

# 6. Revert to clean snapshot
```

## 📝 YARA Rule Templates

### Basic Detection Rule
```yara
rule Malware_Sample_Generic {
    meta:
        description = "Generic malware detection"
        author = "Your Name"
        date = "2025-11-12"
        hash = "sha256_hash_here"
    
    strings:
        $s1 = "suspicious_string_1" ascii wide
        $s2 = "suspicious_string_2" ascii wide
        $hex1 = { 6A 40 68 00 30 00 00 }  // Example hex pattern
    
    condition:
        uint16(0) == 0x5A4D and  // MZ header
        (2 of ($s*) or $hex1)
}
```

### API-based Detection
```yara
rule Malware_Keylogger {
    meta:
        description = "Detects keylogger behavior"
        
    strings:
        $api1 = "GetAsyncKeyState" ascii
        $api2 = "GetKeyboardState" ascii
        $api3 = "SetWindowsHookEx" ascii
        $api4 = "GetForegroundWindow" ascii
        
    condition:
        uint16(0) == 0x5A4D and
        3 of ($api*)
}
```

### String-based Detection
```yara
rule Malware_C2_Communication {
    meta:
        description = "Detects C2 communication indicators"
        
    strings:
        $url1 = /https?:\/\/[a-z0-9]{8,16}\.[a-z]{2,6}/ ascii wide
        $cmd1 = "cmd.exe /c" ascii wide
        $cmd2 = "powershell.exe -enc" ascii wide
        
    condition:
        uint16(0) == 0x5A4D and
        any of them
}
```

## 🌐 Network Detection Rules

### Snort Rules

```bash
# Detect suspicious HTTP User-Agent
alert tcp any any -> any 80 (msg:"Suspicious User-Agent"; \
    content:"User-Agent|3a| MalwareBot"; \
    sid:1000001; rev:1;)

# Detect known C2 IP
alert tcp any any -> 192.0.2.1 any (msg:"Known C2 Server"; \
    sid:1000002; rev:1;)

# Detect large data exfiltration
alert tcp any any -> any any (msg:"Large Data Transfer"; \
    dsize:>100000; \
    sid:1000003; rev:1;)
```

### Suricata Rules

```bash
# Detect malware download
alert http any any -> $HOME_NET any (msg:"PE Download"; \
    filemagic:"PE32 executable"; \
    sid:1000004; rev:1;)

# Detect encoded PowerShell
alert tcp any any -> any any (msg:"Encoded PowerShell"; \
    content:"powershell"; nocase; \
    content:"-enc"; distance:0; \
    sid:1000005; rev:1;)
```

## 📚 Reference Materials

### Suspicious API Calls by Category

#### Network APIs
- `InternetOpenA/W` - Initialize WinINet
- `InternetOpenUrlA/W` - Open URL
- `InternetReadFile` - Read from internet
- `URLDownloadToFileA/W` - Download file
- `WSAStartup` - Initialize Winsock
- `socket`, `connect`, `send`, `recv` - Raw socket operations

#### Process Manipulation
- `CreateProcessA/W` - Create new process
- `CreateRemoteThread` - Code injection
- `VirtualAllocEx` - Allocate memory in another process
- `WriteProcessMemory` - Write to another process
- `OpenProcess` - Get handle to process

#### Registry Manipulation
- `RegCreateKeyExA/W` - Create registry key
- `RegSetValueExA/W` - Set registry value
- `RegOpenKeyExA/W` - Open registry key
- `RegDeleteKeyA/W` - Delete registry key

#### File Operations
- `CreateFileA/W` - Create/open file
- `WriteFile` - Write to file
- `DeleteFileA/W` - Delete file
- `MoveFileA/W` - Move/rename file

#### Cryptography
- `CryptAcquireContextA/W` - Get crypto context
- `CryptEncrypt` - Encrypt data
- `CryptDecrypt` - Decrypt data
- `CryptHashData` - Hash data

#### Anti-Analysis
- `IsDebuggerPresent` - Check for debugger
- `CheckRemoteDebuggerPresent` - Check for remote debugger
- `GetTickCount` - Timing checks
- `Sleep` - Delay execution

### Common Persistence Mechanisms

```
Registry Run Keys:
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

Startup Folders:
%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup
%PROGRAMDATA%\Microsoft\Windows\Start Menu\Programs\Startup

Scheduled Tasks:
C:\Windows\System32\Tasks\

Services:
HKLM\System\CurrentControlSet\Services\
```

## ⚠️ Safety Guidelines

### VM Configuration
1. **Snapshot before analysis**
2. **Disable shared folders**
3. **Use Host-Only networking** (or NAT with INetSim)
4. **Disable clipboard sharing**
5. **Never use personal/production networks**

### Data Handling
1. **Password protect malware archives** (use: `infected`)
2. **Label clearly as malware**
3. **Store in isolated location**
4. **Use encrypted storage**
5. **Delete when analysis complete**

### Legal Considerations
1. **Only analyze for educational purposes**
2. **Use public/authorized samples only**
3. **Follow institutional policies**
4. **Document chain of custody**
5. **Respect laws and regulations**

---

**Remember: Malware analysis is powerful but dangerous. Always prioritize safety!** 🔒
