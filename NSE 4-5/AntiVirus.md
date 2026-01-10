#NSE4 

### Overview
FortiGate uses many techniques to detect viruses. These detection techniques include:
- **Antivirus** - This scan is the first, fastest and simplest way to detect malware. Detects for an exact match for a signature in the antivirus database.
- **Greyware** - Detects unsolicited programs which could be installed without the users knowledge.
- **AI** - Used to potentially detected Zero Day malware. Integrates with the Antivirus scan.

### AntiVirus Security Profile Feature Sets

![[Pasted image 20260110144512.png]]

#### Flow Based
FortiGate buffers but also transmits simultaneously. The anti-virus engine starts scanning after the whole file is buffered.

**Supported Features**
- Signature-based detection
- Virus outbreak prevention
- External malware block list
- FortiClient EMS threat feed

**Stream based** - Scans HTMl and JS files with antivirus engine 7.0, which eliminates the need to cache the entire file. This will not be used if any of the following antivirus scanning configurations or features are enabled.
- ML-based malware detection
- Extreme antivirus database
- Greyware scan
- Mobile malware database
- External block list
- EMS threat feed
- FortiGuard outbreak prevention
- DLP
- File filter

#### Proxy-Based

The Fortigate will buffer all data sent from the server and starts the antivirus can once the entire file is buffered. It then forwards the file to the client if a threat is not detected.

**Supported Features**
- Content disarm and reconstruction (CDR)
- Behaviour-based detection
- Common Internet File System (CIFS) scanning
- AI/ML, behavioural and human analysis
- MAPI and SSH protocol inspection
- FortiNDR inspection

### Common AntiVirus Issue Troubleshooting

1. Verify FortiGuard antivirus license
2. Force Fortigate to check for new antivirus updates
	- `execute update-av`
3. Debug application
	- `diagnose debug application update -1`
	- `diagnose debug enable`
	- `execute update-av`
4. Verify antivirus profile configuration