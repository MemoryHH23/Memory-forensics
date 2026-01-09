# Memory Forensics & Malware Analysis
A student project focusing on memory forensics analysis using Volatility and PEStudio.

**Project Description**

This project performs a memory forensics investigation on a captured RAM image to identify suspicious processes and potential malware. The analysis focuses on detecting anomalous behavior in memory, extracting suspicious binaries, and performing static malware analysis to identify indicators of compromise.

The project was conducted as part of the Ethical Hacking course and emphasizes transparency, documentation, and forensic methodology.

**Objectives**

The objectives of this project are to:\
Analyze a memory dump using memory forensics tools.\
Identify suspicious or anomalous running processes.\
Extract potentially malicious binaries from memory.\
Perform static malware analysis on extracted files.\
Develop YARA rules for detecting similar malware.\
Document findings clearly and reproducibly.\
Ensure transparency when using AI-assisted tools.

**Scope of the Project**

The scope of this project is limited to:\
Memory analysis of a provided RAM image.\
Static malware analysis only (no execution of malware).\
Educational and controlled lab environment.

The project does not include live incident response, dynamic malware execution, or analysis of real-world production systems.

**Tools Used**

Volatility Framework – memory analysis and process enumeration.\
PEStudio – static analysis of extracted executables.\
YARA – creation of malware detection rules.\
LM Studio (google/gemma-3-12b) – AI assistance for drafting YARA rules and summarizing findings.\
GitHub – version control and documentation.

All AI-assisted results were manually reviewed and validated.

**Repository Structure**

├── README.md\
├── analysis/\
│   └── pestudio_analysis.md\
├── logs/\
│   └── volatility_results.txt\
├── prompts/\
│   └── AI_prompts.md\
├── rules/\
│   └── malware_detection.yar\
├── screenshots/\
│   ├── Screenshot 2025-12-16 102406.png\
│   ├── Screenshot 2025-12-16 103140.png\
│   ├── Screenshot 2025-12-16 103342.png\
│   ├── Screenshot 2025-12-16 103906.png\
│   ├── Screenshot 2025-12-16 104204.png\
│   ├── Screenshot 2025-12-16 105319.png\
│   ├── Screenshot 2025-12-18 125403.png\
│   ├── Screenshot 2025-12-18 125445.png\
│   ├── Screenshot 2025-12-18 140630.png\
│   ├── Screenshot 2025-12-18 141153.png\
│   ├── Screenshot 2025-12-18 141434.png\
│   └── Screenshot 2025-12-18 141614.png

**Installation & Environment**

1. System Requirements

Linux VM (tested on Kali Linux)

Windows VM (for PEStudio)

Python 3.9+ on Linux

Internet access for installation only

Internet disabled during analysis

RAM dump file: jo-2009-12-05.winddramimage

2. Linux VM – Tool Installation
2.1 Update System
sudo apt update && sudo apt upgrade -y

2.2 Install System Dependencies
sudo apt install -y \
  python3 python3-pip python3-venv \
  build-essential git libssl-dev \
  yara libyara-dev yara-doc

2.3 Create Forensic Working Directory
mkdir -p ~/forensics-env/tools
cd ~/forensics-env

2.4 Create and Activate Python Virtual Environment
python3 -m venv venv
source venv/bin/activate


Confirm activation:

(venv) user@linux:~/forensics-env $

2.5 Install Volatility 3
pip install volatility3


Verify installation:

vol -h

2.6 Install YARA Python Bindings
pip install yara-python


Verify:

python3 - << 'EOF'
import yara
print("YARA Python OK")
EOF

3. Windows VM – Tool Installation
3.1 Install PEStudio

Download PEStudio (portable ZIP)

Extract to C:\Tools\PEStudio\

No installation required

3.2 Windows Safety Configuration

Disable Windows Defender real-time protection

Disable SmartScreen

Disable internet connection

These steps prevent interference with malware samples during static analysis.

4. Workspace Setup (Linux VM)
mkdir -p ~/forensics-env/workspace/{memory,logs,extracted}
cd ~/forensics-env/workspace


Place the RAM dump in the memory directory:

mv jo-2009-12-05.winddramimage memory/

5. Memory Analysis (Volatility 3)
5.1 Identify System Information
vol -f memory/jo-2009-12-05.winddramimage windows.info

5.2 Enumerate Processes
vol -f memory/jo-2009-12-05.winddramimage windows.pslist
vol -f memory/jo-2009-12-05.winddramimage windows.psscan
vol -f memory/jo-2009-12-05.winddramimage windows.pstree


Save output:

vol -f memory/jo-2009-12-05.winddramimage windows.pslist > logs/pslist.txt
vol -f memory/jo-2009-12-05.winddramimage windows.psscan > logs/psscan.txt

5.3 Inspect Suspicious Process (PID 3708)
vol -f memory/jo-2009-12-05.winddramimage windows.dlllist --pid 3708 > logs/dll_3708.txt
vol -f memory/jo-2009-12-05.winddramimage windows.cmdline --pid 3708
vol -f memory/jo-2009-12-05.winddramimage windows.envars --pid 3708

5.4 Analyze Process Memory Layout
vol -f memory/jo-2009-12-05.winddramimage windows.memmap --pid 3708 > logs/memmap_3708.txt

5.5 Extract Executable Artifacts
vol -f memory/jo-2009-12-05.winddramimage windows.dumpfiles --pid 3708 -D extracted/
vol -f memory/jo-2009-12-05.winddramimage windows.memdump --pid 3708 -D extracted/

6. Identify Extracted Files (Linux VM)
file extracted/*
strings extracted/* | less


Identify valid Portable Executable (PE) files for further analysis.

7. Transfer Files to Windows VM

Transfer identified executables to the Windows VM using a shared folder or isolated disk.

8. Static Analysis (PEStudio – Windows VM)

Launch PEStudio

Open the extracted executable

Review:

Indicators and severity

Imports and suspicious API usage

Embedded strings

Section headers and permissions

Resources and embedded payloads

Document findings.

9. Correlation and Documentation

Correlate Volatility findings with PEStudio indicators and document all results, logs, and extracted artifacts.

10. Completion

Following these steps fully replicates the memory forensics and static malware analysis exercise using
jo-2009-12-05.winddramimage.

**Methodology**

The analysis followed a structured forensic workflow:

1. Identification of the correct memory profile
2. Enumeration of running processes and system artifacts
3. Detection of anomalies such as:\
Unusual process names\
Suspicious parent-child relationships\
Hidden or terminated processes
4. Extraction of suspicious binaries from memory
5. Static malware analysis using PEStudio
6. Identification of indicators of compromise
7. Creation of YARA rules based on verified indicators
8. Documentation of findings and analysis steps

**Analysis & Findings**

The memory analysis revealed one or more suspicious processes exhibiting abnormal characteristics. Indicators observed during analysis included:\
Unexpected process behavior\
Suspicious memory regions\
Abnormal imports and strings within extracted binaries

Static analysis of extracted files indicated characteristics commonly associated with malicious software. Detailed logs and artifacts are available in the repository.

**Indicators of Compromise (IoCs)**

The following types of IoCs were identified during the investigation:\
Suspicious process names\
Unique strings found within extracted binaries\
Abnormal imported functions\
Indicators of packing or obfuscation

These indicators were used as the basis for YARA rule development.

**YARA Rules**

Custom YARA rules were created to detect malware samples exhibiting similar characteristics to those identified during the analysis.\
Location: rules/malware_detection.yar

Rule logic based on:

Unique strings\
PE file characteristics\
Verified forensic indicators

The rules are intended for educational and detection purposes in controlled environments.
The final YARA rules are modified to match the syntax of a .yar file.

**AI / LLM Usage Transparency**

An LLM (google/gemma-3-12b via LM Studio) was used to assist with:\
Drafting YARA rule structures\
Summarizing malware behavior

Transparency measures taken:\
All AI-generated output was treated as untrusted\
Manual verification was performed for all findings

Prompts and outputs are documented in:\
prompts/AI_prompts.txt

This ensures reproducibility and compliance with course requirements.

**Challenges & Limitations**

Several challenges and limitations were encountered:\
Limited context depending on memory dump quality\
Risk of false positives when identifying suspicious processes\
Static analysis limitations without dynamic execution\
AI-generated suggestions required careful validation

**Ethical & Legal Considerations**

This project was conducted strictly for educational purposes.\
All analysis was performed on pre-provided lab material in a controlled environment.\
No real-world systems or personal data were involved.

**Conclusion**

This project demonstrates a complete memory forensics workflow, from process analysis to malware detection rule creation. It highlights the importance of structured methodology, careful validation, and transparency when using AI-assisted tools in security-related investigations.

**References**

Digital Corpora. (2009). 2009 M57 Patents – RAM images. 
https://digitalcorpora.s3.amazonaws.com/s3_browser.html#corpora/scenarios/2009-m57-patents/ram/

Digital Corpora. (u.å.). Digital Corpora. 
https://digitalcorpora.org/

LMStudio.ai. (u.å.). LM Studio. 
https://lmstudio.ai/

Volatility Foundation. (u.å.). Volatility Framework documentation. 
https://volatilityfoundation.org/

Winitor. (u.å.). PEStudio documentation. 
https://www.winitor.com/
