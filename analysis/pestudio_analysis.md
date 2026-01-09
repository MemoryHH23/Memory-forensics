This report presents a static analysis of a Windows executable using PEStudio. The purpose of the analysis was to identify structural properties, imported functions, and readable strings in order to assess potential security risks. Due to limitations in the free version of PEStudio, screenshots were used to document the findings. The analysis focuses on file properties, VirusTotal results, sections, imports, and strings. Overall, the file does not show clear signs of malware, but some elements reduce its trustworthiness and justify further investigation.

<img width="1223" height="546" alt="image" src="https://github.com/user-attachments/assets/3b56dd0c-dee0-4920-9298-a38198a4bd6c" />

In PEStudio, the file is identified as a 32-bit Windows console executable compiled with Visual Studio 2008. The compilation date is from 2009, which means the file is quite old. The file does not contain any version or description information, which makes it harder to identify its origin. PEStudio also shows that the digital certificate is invalid and that an unknown overlay is present. These are not direct signs of malware, but they reduce trust in the file.
<img width="1033" height="447" alt="image" src="https://github.com/user-attachments/assets/f5f51abc-ed00-4a59-a1b9-d49f203897bb" />
PEStudio shows a VirusTotal score of 2 out of 70 detection engines. This means that most antivirus tools do not classify the file as malicious. However, two engines flag the file as suspicious, which means it cannot be considered completely safe. The low detection rate suggests that the file is not widely known as malware, but it still deserves further analysis.
<img width="1147" height="563" alt="image" src="https://github.com/user-attachments/assets/7ec87974-8b85-443a-b6c5-443ef75cf8ee" />
The file contains three standard sections: .text, .rdata, and .data. All sections have expected sizes and permissions, and no unusual or suspicious section names are present. The entropy values are moderate, which suggests that the file is not packed or encrypted. Overall, the section layout looks normal and does not indicate attempts to hide code.
<img width="1281" height="758" alt="image" src="https://github.com/user-attachments/assets/310a26b8-8771-49ba-86f4-005e063aaa91" />
The import table shows that the program uses many Windows API functions related to memory management, process handling, service control, and networking. Functions such as AdjustTokenPrivileges, CreateServiceW, and StartServiceW indicate that the program can change system privileges and manage Windows services. The presence of networking functions from WS2_32.dll shows that the program is capable of network communication. These functions are legitimate, but together they give the program broad control over the system, which should be treated with caution.

<img width="835" height="757" alt="image" src="https://github.com/user-attachments/assets/501b4128-a711-48e9-a0d2-ff290bf46a7b" />


This view shows additional imported Windows API functions related to memory allocation, file handling, environment variables, and system information. The program also imports functions from WS2_32.dll and ADVAPI32.dll, which means it can perform network communication and interact with system settings. All imported functions are legitimate, but the large number of low-level system calls indicates that the program has extensive access to the operating system, which should be handled carefully.

<img width="848" height="855" alt="image" src="https://github.com/user-attachments/assets/37306f56-484e-49bc-a0ed-028f21ae66d6" />

This screenshot shows many imported functions from KERNEL32.dll, which are used for basic program operations such as memory handling, file access, process control, and console input/output. These functions are common in Windows applications and do not indicate malicious behavior by themselves. However, the large number of system-level functions shows that the program interacts closely with the operating system, which increases its potential impact if misused.

<img width="1215" height="468" alt="image" src="https://github.com/user-attachments/assets/c1d6a2cd-43cb-4920-a73f-e02c622f91d3" />

The indicators summary in PEStudio shows general information about the file, including its hash values, compiler details, and VirusTotal results. The file has a low VirusTotal score (2/70), which means most antivirus engines do not detect it as malicious. However, PEStudio also reports an invalid certificate and an unknown overlay, which are not ideal and slightly reduce trust in the file. Overall, the indicators suggest that the file is not clearly malicious, but it contains some elements that require attention.

<img width="506" height="860" alt="image" src="https://github.com/user-attachments/assets/2ac9456f-267f-4d8c-86e6-852f69947a6a" />

This screenshot shows additional readable strings containing DLL names and common Windows API functions such as file handling, registry access, and console operations. All of these strings are standard for Windows applications and do not directly indicate malicious behavior. However, the presence of many low-level system and registry-related strings shows that the program has wide access to system resources, which should be noted.
<img width="510" height="863" alt="image" src="https://github.com/user-attachments/assets/71e97b0b-11e2-4aac-924d-2dbe0931f8b6" />


This screenshot shows strings related to debugging checks, process control, and system information, such as IsDebuggerPresent and TerminateProcess. These functions are legitimate and can be used for normal error handling and stability checks. However, the presence of debugging-related strings indicates that the program is aware of analysis or debugging environments, which is something to note.

<img width="595" height="861" alt="image" src="https://github.com/user-attachments/assets/c54f38e4-f4b6-4295-ac83-4084a93cc829" />

This screenshot shows strings related to digital certificates, exception handling, and general system functions. References to GlobalSign and Microsoft Corporation suggest the use of standard certificate and trust components. However, the presence of <program name unknown> indicates missing metadata, which makes the file harder to identify. Overall, the strings appear normal, but the missing program name slightly reduces transparency.

<img width="1223" height="857" alt="image" src="https://github.com/user-attachments/assets/e00c1b2a-eebd-4513-b008-a3a3992beded" />

This screenshot shows many strings related to Microsoft Visual C++ runtime errors and exception handling. These messages are automatically included when programs are compiled with Visual Studio and are used for error reporting. They do not indicate malicious behavior by themselves. However, the large number of runtime error strings suggests that the binary was compiled without removing default runtime messages, which is common in older or poorly maintained software.

<img width="1022" height="706" alt="image" src="https://github.com/user-attachments/assets/9ad5ee21-b081-4f72-b025-d209c259a215" />

The strings view shows many readable text strings related to Windows API functions, privilege handling, and service management. These strings match the imported functions seen earlier and confirm that the program interacts closely with the operating system. No obviously malicious commands or hidden strings are visible. However, the presence of strings related to privileges and services indicates that the program is capable of performing sensitive system actions.

Conclusion

The PEStudio analysis shows that the file is an older Windows executable compiled with Visual Studio 2008. It has a low VirusTotal detection rate (2/70) and a normal section structure, which suggests that it is not packed or heavily obfuscated. However, the presence of an invalid digital certificate, an unknown overlay, and extensive system-level imports lowers confidence in the file. Based on this static analysis, the file cannot be classified as clearly malicious, but it should also not be considered fully trustworthy. A dynamic analysis would be recommended for a more complete assessment.

AI

AI tools were used to help structure the report and improve the clarity of the written explanations (Qwen2.5-VL). 
Prompt 
”I performed a static malware analysis using PEStudio and provided screenshots of the results. Explain what each screenshot shows in simple terms, focus on noteworthy or problematic findings, and then write an abstract and a conclusion suitable for a student report”
(Then we sended each picture) To support the textstructure we also used ChatGPT 5.2 and wrote some of it of our own.



