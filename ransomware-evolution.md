# Ransomware Evolution: From PC Cyborg to RaaS

> **Research note:** This report is a historical and defensive analysis of ransomware evolution, attack patterns, indicators of compromise (IoCs), threat-intelligence observations, and defensive controls.

Ransomware has changed a lot over time. It started as simple experimental malware created mainly for research. Over the years, it grew into a large global cybercrime industry that now earns billions of dollars every year. This report explains that evolution in three main stages: the early experimental ransomware, the rise of crypto-ransomware that used strong encryption, and the modern Ransomware-as-a-Service (RaaS) model where attackers sell ransomware tools to others. It also looks at how different ransomware groups operate, the techniques and tools they use, and the real-world damage they have caused.

## Ransomware Era Timeline

| **Period** | **Era** | **Key Families** | **Defining Feature** |
|---|---|---|---|
| 1989–2005 | Primitive Ransomware | PC Cyborg (AIDS) | Symmetric key, floppy disk |
| 2006–2012 | Scareware & Lockers | Reveton, WinLock | Fake law enforcement alerts |
| 2013–2016 | Crypto-Ransomware | CryptoLocker, CTB-Locker | Strong asymmetric encryption |
| 2017 | Worm-Propagated | WannaCry, NotPetya | Self-spreading via exploits |
| 2018–2020 | Big-Game Hunting | Ryuk, Maze | Targeted enterprises + double extortion |
| 2021–Present | RaaS Ecosystem | LockBit, ALPHV/BlackCat | Affiliate model, triple extortion |

## **1. EARLY RANSOMWARE ERA (1989–2012)**

## 1.1 PC Cyborg Trojan (AIDS Trojan) — 1989

### Overview

The PC Cyborg Trojan, authored by evolutionary biologist Joseph Popp, is widely regarded as the world's first ransomware. Distributed via floppy disks at the 1989 WHO AIDS conference, it was a primitive but historically pivotal attack that established the extortion model still in use today.

Target Industries: Healthcare researchers, WHO conference attendees, academic institutions.

### Attack Methodology

- Initial Access: Physical floppy disk distribution labelled 'AIDS Information Introductory Diskette'
- Infection: Replaced AUTOEXEC.BAT; activated after 90 boot cycles
- Encryption: Symmetric XOR-based encryption of directory names and the FAT table (not file contents)
- Lateral Movement: Manual floppy disk sharing — no network propagation capability

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .cyborg (renamed directories) |
| **Modified File** | AUTOEXEC.BAT (boot-time trigger) |
| **Registry** | N/A — pre-Windows era (DOS-based) |
| **Ransom Note** | Printed text demanding $189 to 'PC Cyborg Corp.' in Panama |
| **Payload File** | AIDS.EXE on infected floppy disk |

### Special Features

- World's first documented ransomware — established the extortion blueprint
- Symmetric encryption made decryption trivial for researchers (decryption keys were hardcoded)
- Physical distribution model — no internet required

### Real-World Impact

In 1989, approximately 20,000 floppy disks were mailed to attendees of the WHO AIDS conference. Victims across Europe, Africa, and the US received demands for $189. Joseph Popp was arrested but deemed unfit for trial. The attack exposed the concept of digital extortion to the world.

## 1.2 Reveton (Police Ransomware) — 2012

### Overview

Reveton, also known as 'Police Ransomware' or 'Locker ransomware', emerged around 2012 and represented a major evolution in social engineering. Rather than encrypting files, it locked the victim's entire desktop and displayed a fake law enforcement notice accusing the user of illegal activity.

Target Industries: General consumers, home users across Europe and North America.

### Attack Methodology

- Initial Access: Drive-by downloads via exploit kits (Blackhole, Neutrino), malvertising
- Payload: Dropped via the stronghold banking trojan as a secondary payload
- Lock Mechanism: Replaced the Windows shell; prevented access to the desktop entirely
- Geolocation: Used the victim's IP address to display localized law enforcement branding (FBI, PCEU, BKA)
- Payment: Demanded payment via prepaid vouchers (Ukash, Paysafecard, MoneyPak)

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **C2 Infrastructure** | Dynamic IPs via fast-flux DNS; rotated daily |
| **Registry Key** | HKCU\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Winlogon\\Shell |
| **File Dropped** | %APPDATA%\\[random].exe |
| **File Hash (MD5)** | e4b5d5f5e8c0a891b45d3f12a7c8a2b1 (sample variant) |
| **Network** | HTTP beacons to attacker C2 for geo-targeting payload selection |

### Special Features

- Identified geo-targeted social engineering — displayed local police logos
- No file encryption — pure screen-locker, making removal possible without key
- First widespread use of prepaid cards as anonymous payment method

### Real-World Impact

By mid-2012, Reveton had infected hundreds of thousands of systems across Europe and the US. The FBI issued a public warning in 2012. Europol's EC3 and FBI jointly disrupted associated infrastructure in 2013, arresting the alleged ringleader in Spain. Estimated earnings exceeded $400,000/month at peak.

## **2. CRYPTO-RANSOMWARE ERA (2013–2016)**

## 2.1 CryptoLocker — 2013

### Overview

CryptoLocker marked the dawn of true crypto-ransomware, using military-grade RSA-2048 encryption for the first time against victims. Operated by a Russian cybercriminal group led by Evgeniy Bogachev (also responsible for the GameOver Zeus botnet), it was the template for nearly every modern ransomware operation.

Target Industries: SMBs, legal firms, financial services, healthcare, general consumers.

### Attack Methodology

- Initial Access: Malicious email attachments (ZIP files posing as FedEx/UPS delivery notices), GameOver Zeus botnet
- Encryption: AES-256 for files; RSA-2048 for key exchange with C2 server
- File Targeting: Scanned all drives and network shares for 70+ file extensions (.doc, .xls, .jpg, .pdf, etc.)
- C2 Communication: Used a domain generation algorithm (DGA) to evade takedowns
- Time Pressure: 72-hour countdown timer to increase victim panic and payment urgency

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | No extension change; files encrypted in place |
| **Ransom Note** | DECRYPT_INSTRUCTION.txt / .html dropped in each folder |
| **Registry** | HKCU\\Software\\CryptoLocker\\Files (encrypted file list) |
| **C2 Domains** | DGA-based; sinkholed by Operation Tovar (2014) |
| **File Hash** | Variant: 1f49b33d3d5c3e54f7e6ca4b62b4f5bc |
| **Network** | TCP 443/80 to C2; unique victim ID in HTTP header |

### Special Features

- First ransomware to use RSA public-key cryptography for secure key exchange
- Bitcoin payment introduced as primary ransom channel
- Domain Generation Algorithm (DGA) — generated 1,000+ domains/day for C2 resilience
- Countdown timer and ransom escalation mechanism

### Real-World Impact

Operation Tovar (2014) — a coalition of law enforcement agencies including the FBI, Europol, and NCA, together with cybersecurity firms, seized CryptoLocker's C2 infrastructure. Estimates suggest over $3 million was extorted before shutdown. Bogachev remains on the FBI's most-wanted list with a $3M bounty.

## 2.2 CTB-Locker (Curve-Tor-Bitcoin Locker) — 2014

### Overview

CTB-Locker introduced two major innovations to crypto-ransomware: elliptic curve cryptography (ECC) for faster and smaller key operations, and Tor for anonymous C2 communication. It was one of the first ransomware families sold as a kit to affiliates — a precursor to modern RaaS.

Target Industries: Consumers, SMBs, healthcare, government agencies.

### Attack Methodology

- Initial Access: Spam email campaigns, exploit kits (Nuclear, Angler)
- Encryption: ECDH (Elliptic Curve Diffie-Hellman) — master public key embedded; session keys ephemeral
- Tor Anonymity: C2 hosted on .onion hidden services — made infrastructure takedown very difficult
- Affiliate Sales: Malware kit sold to criminal affiliates for ~$3,000

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .ctbl, .ctb2 (depending on variant) |
| **Ransom Note** | !Decrypt-All-Files-[random].bmp, .txt |
| **C2** | .onion Tor hidden service addresses (rotated per campaign) |
| **Processes** | net.exe, vssadmin.exe (shadow copy deletion) |
| **Registry** | HKCU\\Software\\[random GUID] |

### Special Features

- First ransomware to use ECC — faster key generation, smaller key sizes
- First major use of Tor for C2 — greatly enhanced operator anonymity
- Early affiliate/partner model — crime-as-a-service precursor

### Real-World Impact

In 2015, CTB-Locker pivoted to targeting web servers running WordPress, encrypting entire site contents. Thousands of websites were defaced with ransom demands. A Romanian national was arrested in 2016 in connection with the operation, but affiliate structure allowed others to continue.

## **3. WORM-PROPAGATED RANSOMWARE (2017)**

## 3.1 WannaCry — 2017

### Overview

WannaCry was a watershed moment in ransomware history. Leveraging the NSA-developed EternalBlue exploit, it spread autonomously across unpatched Windows systems worldwide in May 2017, infecting over 230,000 machines in 150 countries within 24 hours. Attributed to North Korea's Lazarus Group, it was as much a cyberweapon as ransomware.

Target Industries: Healthcare (NHS UK), telecommunications, manufacturing, government, transport.

### Attack Methodology

- Initial Access: Automated — no phishing required; exploited SMBv1 (EternalBlue/MS17-010) on exposed port 445
- Propagation: Self-replicating worm that scanned the internet for vulnerable SMBv1 hosts
- Lateral Movement: DoublePulsar kernel backdoor installed; spread within networks instantly
- Encryption: AES-128 per file; RSA-2048 key exchange with C2
- Kill Switch: Checked for an unregistered domain; registration by Marcus Hutchins halted global spread

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .WNCRY appended to encrypted files |
| **Ransom Note** | @Please_Read_Me@.txt, @WanaDecryptor@.exe |
| **Exploit** | MS17-010 (EternalBlue) — SMBv1 port 445 |
| **File Hash (SHA256)** | 24d004a104d4d54034dbcffc2a4b19a11f39008a575aa614ea04703480b1022c |
| **Kill Switch Domain** | [iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com](http://iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com) (sinkholed) |
| **C2** | .onion Tor hidden services for payment portal |
| **Mutex** | Global\\MsWinZonesCacheCounterMutexA |

### Special Features

- EternalBlue exploit weaponized — first major use of leaked NSA cyberweapons
- Fully autonomous worm propagation — no user interaction required
- Kill-switch mechanism (accidental) embedded in code — discovered by Marcus Hutchins
- DoublePulsar kernel rootkit for persistence and lateral movement

### Real-World Impact

WannaCry devastated the UK's National Health Service, forcing 80 NHS trusts offline. Over 19,000 appointments were cancelled. Emergency patients were turned away from A&E departments. Estimated damage to NHS alone exceeded £92 million. The US and UK governments officially attributed the attack to North Korea's Lazarus Group in December 2017.

## 3.2 NotPetya — 2017

### Overview

NotPetya (initially misidentified as Petya ransomware) was, in reality, a destructive cyberweapon disguised as ransomware. Attributed to Russia's Sandworm (GRU Unit 74455), it was designed for maximum destruction rather than profit. It remains the most costly cyberattack in history, causing over $10 billion in global damages.

Target Industries: Ukrainian government, global logistics, pharma, shipping, finance (Maersk, Merck, FedEx).

### Attack Methodology

- Initial Access: Trojanized update to Ukrainian tax software M.E.Doc — supply chain attack
- Propagation: Combined EternalBlue, Mimikatz credential harvesting, and PsExec/WMIC for lateral movement
- Encryption: Modified MBR to lock boot; AES-128 encrypted files; decryption key overwritten — permanently destructive
- Design Intent: No functional decryption mechanism — ransom email was quickly taken down

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .Petya / no extension (MBR overwrite) |
| **Ransom Note** | MBR-level text: 'Oops, your important files are encrypted' |
| **Exploit** | MS17-010 EternalBlue + Mimikatz + PsExec |
| **File Hash (SHA256)** | 027cc450ef5f8c5f653329641ec1fed91f694e0d229928963b30f6b0d7d3a745 |
| **C2** | No C2 required — destructive wiper |
| **Supply Chain Vector** | M.E.Doc software update server ([medoc.com.ua](http://medoc.com.ua)) |

### Special Features

- Supply chain attack vector — first major instance of software update poisoning
- Pseudo-ransomware: designed as a wiper; no functional recovery possible
- Hybrid propagation — combined exploit, credential theft, and admin tools
- Targeted Ukraine but escaped globally, highlighting collateral damage risks

### Real-World Impact

Maersk (shipping giant) lost $300M and had to reinstall 45,000 PCs and 4,000 servers in 10 days. Merck lost $870M. FedEx/TNT lost $400M. Ukraine's government, banks, and energy grid were severely disrupted. Total global damage: $10B+. NATO classified it as a state-sponsored cyberweapon.

## **4. BIG-GAME HUNTING ERA (2018–2020)**

## 4.1 Ryuk — 2018

### Overview

Ryuk emerged in August 2018 and pioneered 'big-game hunting' — deliberately targeting large enterprises and critical infrastructure for multi-million-dollar ransoms instead of indiscriminate mass infections. Attributed to Russian-speaking group WIZARD SPIDER (also behind TrickBot), Ryuk became the dominant enterprise ransomware of its era.

Target Industries: Hospitals, municipal governments, media companies, logistics, finance.

### Attack Methodology

- Initial Access: Phishing emails deploying Emotet, which delivered TrickBot; then Ryuk as final-stage payload
- Dwell Time: Operators spent weeks or months inside the network before deploying ransomware
- Reconnaissance: Active AD enumeration, data staging, and backup identification before encryption
- Encryption: RSA-4096 + AES-256; unique key per victim; shadow copies deleted via vssadmin
- Lateral Movement: Cobalt Strike beacons, WMI, PsExec, RDP

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .RYK appended to encrypted files |
| **Ransom Note** | RyukReadMe.html / RyukReadMe.txt |
| **Registry** | HKEY_CURRENT_USER\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run — persistence |
| **Shadow Delete** | vssadmin Delete Shadows /All /Quiet |
| **File Hash (SHA256)** | 8d3f68b16f0710f858d8c1d2c699260e6f43161a5510abb0e7ba567bdca0f5c9 |
| **C2** | Hard-coded IPs in binary; changed per campaign |
| **Beacon** | Cobalt Strike — custom malleable C2 profiles |

### Special Features

- Pioneered the 'big-game hunting' model — weeks-long dwell before detonation
- Three-tier delivery: Emotet → TrickBot → Ryuk
- Deliberately targeted backup systems and shadow copies before encryption
- Manual operator involvement — not automated spray-and-pray

### Real-World Impact

**Universal Health Services (2020)**

Ryuk struck UHS, one of the largest US hospital networks, in September 2020 — during the COVID-19 pandemic. 400 hospitals across the US and UK were affected. Staff reverted to paper records. Cost to UHS: ~$67 million. The attack is considered one of the most dangerous ransomware incidents given its life-threatening context.

## 4.2 Maze — 2019

### Overview

Maze ransomware, operated by an unidentified Russian-speaking group, fundamentally changed ransomware by introducing 'double extortion' in November 2019. Rather than just encrypting files, operators began exfiltrating data first — then threatening to publish it on a dedicated 'leak site' if victims refused to pay. This changed the entire economics of ransomware defense.

Target Industries: Healthcare, legal, manufacturing, government, financial services.

### Attack Methodology

- Initial Access: Phishing, RDP brute force, exploit kits (Fallout), purchased VPN credentials
- Data Exfiltration: Multi-gigabyte data theft before encryption — used Rclone, WinSCP, custom tools
- Encryption: ChaCha20 + RSA-2048; encrypted in 512KB blocks for speed
- Lateral Movement: Cobalt Strike, BloodHound for AD reconnaissance, Mimikatz
- Affiliate Network: First major operation to openly recruit affiliates with revenue sharing

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | Random 4–7 character extension appended |
| **Ransom Note** | DECRYPT-FILES.html in each folder |
| **Leak Site** | mazenews.top (Tor) — victim data published publicly |
| **File Hash (SHA256)** | 3f8a3aeacb0c4cba0ccaf4e8ea7f89c0db85c78e7f4a22e7cc5f91c96da0fc2e |
| **Exfil Tools** | Rclone.exe, WinSCP |
| **C2 Protocols** | HTTP(S) to attacker-controlled infrastructure; Tor fallback |

### Special Features

- Invented double extortion — encryption + threatened data leak
- Operated a public 'Maze News' dark web leak site
- Ran structured press releases and media outreach to increase reputational damage
- Announced formal shutdown in November 2020 — operators migrated to Egregor

### Real-World Impact

**Cognizant (2020)**

Maze attacked IT giant Cognizant in April 2020, stealing and encrypting data from the $16B company. Cognizant disclosed losses of $50–70 million from the attack. The breach affected Cognizant's clients indirectly, demonstrating supply chain ransomware risk.

## **5. MODERN RaaS ECOSYSTEM (2021–PRESENT)**

## 5.1 LockBit — 2019–2024

### Overview

LockBit became the world's most prolific ransomware operation, responsible for more confirmed attacks than any other group between 2022–2024. It operated a highly polished Ransomware-as-a-Service platform with formal affiliate recruitment, SLAs, bug bounties for its own malware, and automated victim management portals.

Target Industries: Healthcare, government, legal, manufacturing, education, finance — virtually all sectors.

### Attack Methodology

- Initial Access: Phishing, exploit of public-facing apps (Fortinet, Citrix, Exchange CVEs), purchased access from initial access brokers
- Encryption Speed: LockBit 3.0 — among fastest ransomware ever tested; encrypts only first 4KB of files for maximum speed
- Intermittent Encryption: Partial encryption defeats file-scanning AV solutions
- Lateral Movement: AnyDesk, Cobalt Strike, PsExec, Active Directory GPO abuse
- Data Exfil: StealBit custom exfiltration tool — automated terabyte-scale data theft

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .lockbit / .lock / .abcd (variant-dependent) |
| **Ransom Note** | Restore-My-Files.txt / LockBit_Ransomware.hta |
| **Leak Site** | lockbitapt[.]onion — 'LockBit 3.0 Blog' |
| **File Hash (SHA256)** | a56b41a6023f828cccaaef470874571b4b772b8941a75a8a8f7e058cba5f7e92 |
| **Exfil Tool** | StealBit.exe (custom — encrypted C2 comms) |
| **Wallpaper** | Desktop wallpaper replaced with ransom demand |
| **Registry** | HKLM\\SOFTWARE\\LockBit — configuration storage |
| **C2 Ports** | TCP 443, 80; Tor .onion fallback |

### Special Features

- Full RaaS platform — affiliates get 80% of ransom; operators take 20%
- Bug bounty program — paid researchers to find flaws in LockBit malware
- LockBit 3.0 incorporated Evasion from BlackMatter codebase
- Self-spreading capability (LockBit 2.0) via AD group policy
- Victim support chat portal — professional negotiation infrastructure

### Real-World Impact

**Royal Mail UK (2023)**

LockBit attacked Royal Mail in January 2023, disrupting international parcel and letter delivery for weeks. LockBit demanded £65.7 million. Royal Mail refused. LockBit published all stolen data. Operation Cronos (February 2024) — Europol/FBI takedown seized LockBit infrastructure, 34 servers, 1,000 decryption keys. LockBit relaunched within a week.

## 5.2 ALPHV / BlackCat — 2021

### Overview

ALPHV (branded BlackCat) made history as the first major ransomware written in Rust — enabling highly efficient cross-platform attacks against Windows, Linux, and VMware ESXi simultaneously. Operated by a sophisticated Russian-speaking group believed to include former REvil members, BlackCat introduced triple extortion and a public victim-shaming API.

Target Industries: Healthcare, energy, financial services, universities, critical infrastructure.

### Attack Methodology

- Initial Access: Compromised credentials, phishing, unpatched VPN/firewall vulnerabilities (Cisco ASA, Fortinet)
- ESXi Targeting: Dedicated Linux/ESXi encryptor — encrypted virtual machine datastores directly
- Encryption: AES-128 + RSA-2048; Rust enables near-native performance cross-platform
- Triple Extortion: Encryption + data leak threat + DDoS attacks on victims who refuse to pay
- API: Exposed a JSON API for affiliates to query victim status and ransom progress

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | Random 7-character extension (configured per campaign) |
| **Ransom Note** | RECOVER-[extension]-FILES.txt |
| **Leak Site** | alphvmmm27o3yd43kiocxnrk456kxmtxosmvsqa7dn34jl2m3zbf4yqd.onion |
| **File Hash (SHA256)** | 731adcf2d7fb61a8335e23dbee2436249e5d5753977ec465754c6b699e9bf161 |
| **Language** | Rust binary — detectable by Rust runtime artifacts |
| **ESXi Artifacts** | esxcli vm process kill — terminates VMs before encryption |
| **C2** | Tor .onion + clearnet fallback; victim-unique negotiation URLs |

### Special Features

- First major ransomware written in Rust — cross-platform, high performance, AV-evasive
- Triple extortion: encryption + data theft + DDoS campaigns
- Searchable victim data portal — allowed stolen data to be queried publicly
- Highly configurable JSON-based build system for affiliates

### Real-World Impact

**Change Healthcare (2024)**

ALPHV/BlackCat attacked Change Healthcare (UnitedHealth subsidiary) in February 2024 — the largest healthcare data breach in US history. 100M+ patient records were compromised. The attack disrupted prescription processing across the US for weeks. UnitedHealth paid a $22M ransom. ALPHV then 'exit-scammed' their own affiliate, disappearing with the payment.

## 5.3 Cl0p — 2019–Present

### Overview

Cl0p (TA505) distinguished itself through a series of zero-day mass-exploitation campaigns targeting widely used enterprise file transfer products — MOVEit, GoAnywhere MFT, and Accellion FTA — affecting thousands of organisations in a single campaign. Cl0p rarely deploys traditional encryption, instead relying almost entirely on data theft and extortion.

Target Industries: Finance, healthcare, government, legal, retail — primarily via software supply chain.

### Attack Methodology

- Initial Access: Zero-day exploits in enterprise file transfer software (MOVEit CVE-2023-34362, GoAnywhere CVE-2023-0669)
- Exfiltration-Only Model: In many campaigns, no encryption deployed — pure data exfiltration and extortion
- Mass Exploitation: Automated scanning and exploitation of thousands of targets simultaneously
- Cl0p Leak Site: Data published in installments to maximize pressure on victims

### Indicators of Compromise

| **IoC Type** | **Value / Description** |
|---|---|
| **File Extension** | .clop appended in traditional campaigns |
| **Ransom Note** | ClopReadMe.txt |
| **Leak Site** | clop[.]to (clearnet) + Tor .onion mirrors |
| **MOVEit Exploit** | CVE-2023-34362 — SQL injection → webshell 'human2.aspx' |
| **Webshell Hash** | 6cbf38f5f27e6a3eaf32e2ac73ed944417b69e87fdc73f63a7d8d3cb2ff81ed4 |
| **C2 Domains** | cloptorbrhsyggs6.onion (Tor), [clop.to](http://clop.to) (clearnet) |

### Special Features

- Mass zero-day exploitation — single vulnerability used to hit hundreds of enterprises simultaneously
- Data-only extortion model in many campaigns — no ransomware binary deployed
- Supply chain targeting — attacked software used by thousands of downstream organizations
- Operated clearnet (non-Tor) leak site for maximum visibility

### Real-World Impact

**MOVEit Campaign (2023)**

Cl0p's exploitation of MOVEit Transfer's zero-day affected 2,000+ organisations and 62M+ individuals including US federal agencies (DoE, USDA), British Airways, BBC, Shell, and hundreds of universities. Total estimated cost: $10B+. Cl0p used the data in installment releases — publishing new victim data weekly for months.

## **6. THREAT INTELLIGENCE SUMMARY**

## 6.1 Comparative Attack Profile Matrix

| **Group** | **Active** | **Encryption** | **Extortion Model** | **Avg Ransom** | **Estimated Revenue** |
|---|---|---|---|---|---|
| **PC Cyborg** | 1989 | Symmetric XOR | Single | $189 | ~$30K |
| **CryptoLocker** | 2013–14 | RSA-2048+AES | Single | $300–500 | $3M+ |
| **WannaCry** | 2017 | RSA+AES-128 | Single (worm) | $300 | $140K (actual) |
| **Ryuk** | 2018–21 | RSA-4096+AES | Single (targeted) | $500K–5M | $150M+ |
| **Maze** | 2019–20 | ChaCha20+RSA | Double | $1M+ | $100M+ |
| **LockBit** | 2019–24 | AES+RSA (fast) | Double+Supply | $2M avg | $1B+ |
| **BlackCat** | 2021–24 | AES-128+RSA | Triple | $5M+ | $300M+ |
| **Cl0p** | 2019–now | Data-only (often) | Double (data) | $10M+ | $500M+ |

## 6.2 MITRE ATT&CK Technique Mapping

| **Phase** | **ATT&CK ID** | **Technique & Common Ransomware Use** |
|---|---|---|
| Initial Access | **T1566.001** | Spearphishing Attachment — CryptoLocker, Ryuk, Maze, LockBit |
| Initial Access | **T1190** | Exploit Public-Facing Application — Cl0p (MOVEit), BlackCat (Fortinet) |
| Execution | **T1059.001** | PowerShell — used by nearly all modern ransomware for stage delivery |
| Persistence | **T1547.001** | Registry Run Keys — Ryuk, CryptoLocker, Reveton |
| Privilege Escalation | **T1068** | Exploitation for Privilege Escalation — WannaCry, NotPetya |
| Defense Evasion | **T1027** | Obfuscated Files — LockBit, BlackCat (Rust packing) |
| Credential Access | **T1003.001** | LSASS Memory Dumping — Ryuk via Mimikatz |
| Discovery | **T1018** | Remote System Discovery — Ryuk, LockBit AD enumeration |
| Lateral Movement | **T1021.001** | Remote Desktop Protocol — Ryuk, LockBit, BlackCat |
| Exfiltration | **T1048** | Exfil over Alt Protocol — Maze (Rclone), Cl0p, BlackCat (StealBit) |
| Impact | **T1486** | Data Encrypted for Impact — all crypto-ransomware families |
| Impact | **T1490** | Inhibit System Recovery — vssadmin delete (Ryuk, LockBit, WannaCry) |

## 6.3 Ransom Note Evolution

The following examples illustrate how ransomware operator communications evolved from crude to corporate-grade messaging:

| **Era / Family** | **Example / Characteristic** |
|---|---|
| **1989 PC Cyborg** | If you are reading this message, then your software lease from PC CYBORG CORPORATION has expired. Please renew your lease... Send $189 to PC Cyborg Corp., PO Box 7, Panama. |
| **2013 CryptoLocker** | Your personal files are encrypted! Your documents, photos, databases and other important files have been encrypted with strongest encryption and unique key. The private key is stored only on our server. To decrypt files you need to obtain the private key. Send Bitcoin 0.3 BTC to: [wallet address]. You have 72 hours to complete payment. |
| **2022 LockBit 3.0** | All your important files are stolen and encrypted. Victims are directed to a dedicated site for instructions, with publication threatened if payment is refused. |

## 6.4 Dark Web Infrastructure — Typical Leak Site Architecture

Modern ransomware groups operate sophisticated dark web portals. The standard leak site architecture for a top-tier group includes:

- Public victim listing page — countdown timers, company names, sector tags
- Sample data preview — small leaked file set to prove data possession
- Full data release section — published in installments to maximize media coverage
- Press section — official statements and negotiation updates
- Affiliate portal (private) — dashboard for affiliates to manage builds and victims
- Victim negotiation chat — encrypted, Tor-based, often with SLA guarantees

## **7. DEFENSIVE RECOMMENDATIONS & CONCLUSIONS**

## 7.1 Defensive Framework by Attack Phase

| **Kill Chain Phase** | **Ransomware Technique** | **Defensive Control** |
|---|---|---|
| Initial Access | Phishing, exploit, RDP brute force | MFA, email filtering, patch management, disable SMBv1 |
| Execution | PowerShell, scripts, macros | AppLocker, script block logging, disable macros |
| Persistence | Registry run keys, services | Privileged account monitoring, EDR behavioral rules |
| Lateral Movement | PsExec, WMI, RDP, AD abuse | Network segmentation, least privilege, LAPS |
| Exfiltration | Rclone, StealBit, FTP | DLP tools, egress filtering, proxy inspection |
| Encryption | File system traversal, VSS deletion | Immutable backups (3-2-1), honeypot files, EDR |
| Extortion | Leak site, DDoS, media contact | Incident response plan, legal counsel, cyber insurance |

## 7.2 Conclusions

The ransomware landscape has undergone a fundamental transformation over four decades. What began as a single researcher's experiment distributed on floppy disks has become a multi-billion-dollar criminal industry with geopolitical dimensions. Several key conclusions emerge from this analysis:

- Encryption alone is no longer sufficient leverage — modern groups combine encryption, data theft, DDoS, and reputational destruction into multi-vector extortion campaigns.
- RaaS democratized ransomware — sophisticated tooling is now accessible to any criminal affiliate willing to share revenue, dramatically lowering the barrier to entry.
- Nation-state and criminal lines are blurring — WannaCry and NotPetya demonstrated that state-sponsored actors can weaponize ransomware for destructive geopolitical goals.
- Supply chain is the new frontier — Cl0p's zero-day campaigns show that targeting shared infrastructure yields exponential victim counts from a single vulnerability.
- Defense requires a layered, behavioral approach — signature-based detection is consistently defeated by modern ransomware; behavioral EDR, immutable backups, and network segmentation are essential.

Ransomware will continue to evolve. The integration of AI for spearphishing personalization, quantum-resistant encryption, and deepfake-enhanced extortion are credible near-term threats. Organisations must treat ransomware resilience as a continuous programme — not a checkbox — encompassing technical controls, staff training, tested incident response plans, and executive awareness.

## 7.3 References & Intelligence Sources

- CISA Ransomware Guide — [cisa.gov/ransomware](http://cisa.gov/ransomware)
- [Group-IB Ransomware Notes](https://www.group-ib.com/resources/ransomware-notes/)
- Europol IOCTA Reports — Internet Organised Crime Threat Assessment
- MITRE ATT&CK Framework — [attack.mitre.org](http://attack.mitre.org)
- Mandiant / Google Threat Intelligence — M-Trends Annual Report
- CrowdStrike Global Threat Report 2024
- [Trend Micro — Ryuk Ransomware](https://www.trendmicro.com/en_us/what-is/ransomware/ryuk-ransomware.html)
- Chainalysis Crypto Crime Report 2024 — ransomware chapter
- Recorded Future Ransomware Tracker & Ransomwatch
- Conti/LockBit leaked chat logs — analysis by BleepingComputer, vx-underground
- US DOJ press releases — Operation Cronos, Tovar, Goldendust indictments
