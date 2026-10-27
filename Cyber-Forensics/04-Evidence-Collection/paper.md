# Plan Computer Crime Evidence Collection

**Author:** Rifat Abuelenin  
**Course:** TIM-8310 — Cyber Forensics  
**Type:** Doctoral coursework / academic technical review  
**Original submission:** 2025

> This is an edited-format transcription of coursework, not a peer-reviewed publication or an empirical validation. References and technical claims require independent verification.

In the rapidly evolving landscape of cybercrime, the ability to plan and execute a forensic evidence collection strategy is vital for both legal integrity and the preservation of digital evidence. This paper presents a comprehensive forensic response to a hypothetical yet realistic cybercrime scenario involving an active computer connected to the internet, running multiple sessions, and containing an external drive. The scenario underscores the importance of preserving volatile data, preventing unauthorized remote tampering, and maintaining the chain of custody in line with digital forensic best practices. The paper outlines each step in the response process from securing the crime scene and documenting system status to live data acquisition, network isolation, imaging, evidence preservation, and analysis all framed within legally admissible forensic procedures and guided by internationally recognized frameworks such as NIST SP 800-86 and ISO/IEC 27037. Through detailed examination and logical sequencing of forensic actions, the discussion emphasizes not only the technical and procedural considerations but also the ethical and legal implications of digital evidence handling. The goal is to highlight a practical, smart, and secure methodology for digital crime scene management, capable of withstanding both legal scrutiny and real-world cybercriminal sophistication.

## Planning the Actions and Considerations for Investigating a Live Computer Crime Scene

Investigating a digital crime scene involving active processes and internet-connected devices requires a meticulous, well-coordinated approach that preserves volatile data, ensures legal admissibility, and maintains forensic integrity. The steps below outline a structured response plan aligned with best practices in digital forensics, cybersecurity frameworks, and criminal procedure.

## Securing the Scene and Establishing Legal Authority

The very first step involves physically securing the location and ensuring no one tampers with any digital or physical evidence. Investigators must confirm that proper legal authority such as a search warrant is in place before any action is taken. The Fourth Amendment in the U.S. Constitution mandates this, and failure to comply can render all collected evidence inadmissible in court (Casey, 2011). This includes preventing remote access by unplugging external network connections only if volatile data has been captured or if deemed necessary to avoid immediate data loss.

## Initial Scene Survey and Documentation

Before touching any devices, investigators must document the scene. This includes photographing screens, visible hardware configurations, power lights, network cabling, peripheral connections, and timestamps. The goal is to establish a visual baseline of the device's operational status at the time of discovery. Documentation must be thorough to support the chain of custody and validate findings during legal proceedings (National Institute of Standards and Technology [NIST], 2006).

3. Volatile Data Acquisition (Live Data Collection)

When a device is powered on and connected to the internet, volatile data such as RAM, network sessions, active processes, and open ports can be lost immediately upon shutdown. Therefore, live data acquisition is prioritized. Tools such as FTK Imager, Belkasoft Live RAM Capturer, or Volatility can extract memory dumps, running processes, user sessions, clipboard contents, and encryption keys (Altheide & Carvey, 2011). This information is critical in identifying malware activity, remote access attempts, or active VPN tunneling.

Network Isolation (Not Shutdown)

Instead of unplugging the device abruptly, investigators should isolate it from the network in a controlled manner. This can involve adding a hardware-based isolation device, using a network tap, or changing firewall rules to cut outbound communication. This prevents remote destruction of evidence while preserving system state. Abrupt disconnection without capturing volatile data may result in data destruction by command and control (C2) servers (Jones, Bejtlich, & Rose, 2006).

## Identification and Prioritization of Digital Evidence Sources

Once the system is stabilized, investigators must identify all potential sources of evidence. This includes the main internal drive, connected external storage, USB devices, memory cards, network logs, and cloud storage credentials found on the system. Investigators should create a forensic triage list to prioritize devices based on volatility and relevance (Carrier, 2005). For example, live logs of system activity may take precedence over archived documents during this stage.

## Forensic Imaging and Preservation

After live data is collected, investigators proceed to create a bit-by-bit forensic image of the internal and external storage media using write-blocking tools and certified imaging software such as EnCase or dd. This step is critical for preserving the original evidence while allowing for safe analysis on copies. Imaging must include hashing (MD5/SHA256) to verify integrity before and after imaging. Every action must be logged for the chain of custody (Nelson, Phillips, & Steuart, 2018).

## Analysis of Acquired Data

The next step is forensic analysis, which includes examining registry keys, login times, USB history, browser caches, encryption artifacts, malware traces, deleted file recovery, and keyword searches. Specialized forensic suites like Autopsy or X-Ways allow layered analysis through timelines, hash sets, and indexed search. During this phase, the evidence must be correlated with the timeline of the suspected crime (Luttgens, Pepe, & Mandia, 2014).

## Documentation and Reporting

all findings must be compiled into a formal forensic report. The report should include a case summary, methodologies used, tools employed, timeline reconstruction, findings, and expert opinions. Reports should remain neutral, factual, and written with court admissibility in mind. Visuals like timelines and hash verification logs enhance credibility (Pollitt & Shenoi, 2006).

## Maintaining Chain of Custody Throughout

Throughout all stages, maintaining the chain of custody is non-negotiable. This means logging every individual who handles the evidence, the time and reason for access, and storage conditions. The chain ensures legal validity and is often challenged in court if broken or incomplete (Casey, 2011).

## Conclusion

Investigating a live cybercrime scene demands a methodical and legally sound approach, where every decision can determine the admissibility and integrity of digital evidence. This paper outlined a comprehensive forensic plan for managing a crime scene involving active processes and internet-connected devices beginning with legal authorization and scene security, followed by volatile data capture, controlled network isolation, forensic imaging, and deep forensic analysis. Each step is grounded in established standards such as NIST SP 800-86 and industry-leading tools and practices. The importance of preserving volatile data, maintaining the chain of custody, and ensuring the integrity of evidence cannot be overstated. In digital forensics, there is no room for error or assumptions. By adhering to strict procedural guidelines and technical precision, forensic professionals not only uphold justice but also safeguard the digital truth in an era where cybercrime leaves no physical trace, only data trails. As cybercriminals grow more sophisticated, so must our methodologies grounded in science, driven by procedure, and protected by law.

## References

Rogers, M. K. (2006). A two-dimensional circumplex approach to digital forensic examinations. Digital Investigation, 3(Supplement), 137–147. https://doi.org/10.1016/j.diin.2006.06.012

James, J. I., & Gladyshev, P. (2010). A survey of digital forensic investigators’ current practices. Digital Investigation, 7(3–4), 116–123. https://doi.org/10.1016/j.diin.2010.05.002

Quick, D., & Choo, K. K. R. (2014). Digital forensic intelligence: Data subsets and Open Source Intelligence (DFINT+OSINT): An exploratory study. Computers & Electrical Engineering, 42, 107–123. https://doi.org/10.1016/j.compeleceng.2014.01.008
