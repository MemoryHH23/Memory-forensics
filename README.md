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
├── logs/\
│   └── volatility_results.txt\
├── rules/\
│   └── malware_detection.yar\
├── prompts/\
│   └── llm_yara_prompts.txt\
└── extracted/\
    └── suspicious_binary.exe

**Installation & Environment**


**Methodology**

The analysis followed a structured forensic workflow:

1. Identification of the correct memory profile
2. Enumeration of running processes and system artifacts
3. Detection of anomalies such as:
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

**AI / LLM Usage Transparency**

An LLM (google/gemma-3-12b via LM Studio) was used to assist with:\
Drafting YARA rule structures\
Summarizing malware behavior

Transparency measures taken:\
All AI-generated output was treated as untrusted\
Manual verification was performed for all findings

Prompts and outputs are documented in:\
prompts/llm_yara_prompts.txt

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
