SIEM-Driven Digital Forensic Investigation: Log Correlation, Anti-Forensic Detection, and Evidence Integrity
Author: Rifat Abuelenin
Course: TIM-8310 — Cyber Forensics
Document type: Revised academic technical review (derived from 2025 doctoral coursework)
Status: Portfolio review draft; not peer-reviewed or experimentally validated
Scope and evidence statement: This paper analyzes established digital-forensic practices and proposes illustrative SIEM detection use cases. No original incident dataset, laboratory experiment, SIEM deployment, benchmark, or courtroom testimony is claimed. Illustrative examples are not findings from a real investigation.

Abstract
Security Information and Event Management (SIEM) systems can help investigators correlate security events across endpoints, identity services, applications, and networks. However, alerting and centralized logging are not substitutes for disciplined evidence acquisition, integrity verification, contextual interpretation, and documented custody. This technical review examines how SIEM-assisted log correlation can support incident reconstruction and identify possible anti-forensic activity, including audit-log deletion, disabled logging, and gaps in expected telemetry. It then considers forensic preservation, evidence presentation, the risks of delayed collection, and the limits of automated anomaly detection. The analysis draws on the author's original coursework and publicly documented NIST guidance. Proposed use cases are conceptual and require environment-specific testing before operational deployment.
1. Introduction and purpose
A digital investigation frequently involves evidence distributed across systems: authentication events, endpoint activity, network records, application logs, and cloud audit trails. A SIEM can bring some of these sources into a common search and correlation environment. This improves investigative visibility when collection coverage, timestamps, retention, access controls, and parsing are reliable. A SIEM cannot reconstruct events that were never logged, have already expired, or were collected without sufficient context.

The central question of this review is: How can SIEM-assisted correlation support defensible cyber investigations while reducing the risk that anti-forensic activity or evidence-handling weaknesses will distort the resulting timeline?

The review focuses on three related concerns: (1) collecting and correlating relevant telemetry; (2) identifying signs of evidence suppression or manipulation; and (3) preserving and explaining digital evidence in a defensible manner.
2. Review approach and limitations
This is a narrative technical review, not a systematic literature review. The original coursework supplied the topics and conceptual discussion. The revision distinguishes established guidance from proposed detection ideas and replaces unsupported certainty with qualified claims. NIST SP 800-86 is used as a primary, verifiable foundation for evidence identification, acquisition, processing, analysis, and reporting. NIST SP 800-61 Revision 3 supplies current incident-response context.

No reproducible database search, formal quality appraisal, or experimental evaluation was performed. Consequently, this document does not establish detection accuracy, comparative product superiority, or legal admissibility in a specific case.
3. SIEM and the investigative timeline
3.1 Relevant log sources
An investigation may correlate:
- Identity and authentication: sign-ins, failed logins, MFA events, privileged role changes, and session activity.
- Endpoints and servers: process creation, service changes, endpoint-security alerts, and audit-policy changes.
- Network and perimeter: firewall decisions, VPN activity, DNS queries, and proxy events.
- Applications and cloud platforms: administrative actions, access records, and service-specific audit events.
The evidentiary value of each source depends on its completeness, reliability, retention, and relationship to the incident hypothesis. SIEM ingestion should preserve original records or maintain an auditable link to them rather than treating normalized fields as the only evidence.
3.2 Correlation and timestamp quality
A defensible timeline should distinguish event time, collection time, and SIEM ingestion time. Time-zone conversion, clock drift, delayed forwarding, and inconsistent timestamp precision can change apparent event order. Network time synchronization can reduce discrepancies but cannot retroactively prove that every timestamp is correct. Analysts should document known offsets and corroborate significant events using independent sources where possible.
3.3 Example investigative sequence (illustrative, not observed)
A hypothetical account-compromise investigation might correlate repeated authentication failures, a successful privileged login, an administrative configuration change, and an unexpected gap in endpoint logs. Such a sequence would justify further examination; it would not, by itself, establish the identity of an attacker or prove malicious intent.
4. Detecting possible anti-forensic behavior
Anti-forensic activity seeks to conceal, degrade, or misdirect an investigation. SIEM detections can surface indicators of this activity, but analysts must distinguish malicious behavior from maintenance, outages, policy changes, and ordinary system operations.
Proposed detection use case	Illustrative signal	Required validation
Audit-log clearing	Log-clearing event or abrupt loss of historical records	Confirm host state, administrator activity, and retention settings
Logging service disabled	Service stop or audit-policy change followed by reduced telemetry	Check approved changes, agent health, and alternate logs
Unexpected telemetry gap	Host normally sends events but suddenly stops	Rule out network failure, ingestion backlog, and host shutdown
Suspicious privilege change	New elevated role followed by security-control modification	Correlate authorization records, change tickets, and user activity
Possible timestamp manipulation	Inconsistent event ordering or unexplained clock changes	Compare independent time sources and original record metadata


These are candidate use cases, not deployed rules or tested detection results. Before production use, a SOC team should define source requirements, exceptions, alert severity, triage procedures, and metrics such as false-positive rate and time to investigation.
5. Evidence acquisition, integrity, and custody
NIST SP 800-86 describes an investigative process encompassing identification and acquisition of relevant data, processing, analysis, and reporting. Acquisition priorities should consider both evidentiary value and volatility. Memory contents, running processes, and live network connections may disappear quickly, while stored logs can also be overwritten or rotated. The correct order of collection depends on the incident, authority, and risk of changing the system.

Integrity verification can include cryptographic hashes of acquired files or forensic images, preservation of originals, documented tool versions, controlled storage, and access logging. A matching hash helps demonstrate that two bitstreams are identical at the time of comparison; it does not independently prove who created the original record, that its contents are true, or that a court will admit it.

Chain-of-custody records should identify evidence items, handlers, transfers, dates, purposes, and storage conditions. A gap can create a credibility challenge, but its legal consequences depend on applicable rules and case-specific circumstances. Investigators should preserve potentially exculpatory or contradictory material rather than selecting only events that support an initial theory.
6. Tools and analytical boundaries
SIEM products and log-analysis platforms, including Splunk, Elastic-based deployments, and IBM QRadar, can support searching, normalization, and correlation. Their actual forensic usefulness depends on configuration, licensed features, source integrations, retention, and export controls. This paper does not benchmark or rank these products.

Other forensic tools serve different purposes. For example, a memory acquisition utility collects a memory image, while a framework such as Volatility primarily analyzes captured memory. Disk-imaging tools, artifact parsers, and packet-analysis utilities may provide corroboration outside the SIEM. Tool selection should follow the evidence question rather than the assumption that one platform can perform the entire investigation.

Machine-learning anomaly detection may help prioritize unusual behavior, but model outputs require explanation and independent corroboration. Training-data limitations, concept drift, false positives, and incomplete telemetry prevent an anomaly score from functioning as proof of compromise or proof of a previously unknown attack.
7. Reporting and courtroom communication
A forensic report should separate observations, analytical inferences, alternative explanations, and unresolved questions. A clear report can include:
1. The investigative question and legal or organizational authority.
2. Systems and evidence sources examined, including coverage limitations.
3. Acquisition procedures, timestamps, hashes, tool versions, and custody records.
4. A chronology with references to original artifacts.
5. Findings, confidence levels, alternative explanations, and limitations.
6. Recommendations for additional collection or validation.
U.S. evidentiary rules may raise questions of relevance, authentication, and expert testimony, but admissibility is a legal determination made in context. Neither blockchain-based storage, append-only logging, nor a hash automatically makes evidence admissible. Technical reports should avoid legal guarantees and be reviewed by qualified counsel when prepared for litigation.
8. Why investigative delay matters
Delays can allow volatile evidence to disappear, logs to rotate, accounts to change state, and witnesses' recollections to weaken. Conversely, hasty collection without authorization or documentation can also compromise an investigation. Teams should define escalation paths, retention policies, evidence-preservation triggers, and coordination with legal and privacy stakeholders in advance.

Regulatory reporting is a distinct obligation from forensic completion. For example, GDPR Article 33 generally requires notification of certain personal-data breaches to the competent supervisory authority without undue delay and, where feasible, within 72 hours after the controller becomes aware of the breach, subject to its risk-based exception. This is not a universal 72-hour deadline for finishing forensic analysis.
9. Discussion: research and operational gaps
Three practical gaps emerge from the conceptual analysis:
- Evidence provenance versus detection: An alert may identify suspicious activity without proving the authenticity or completeness of its underlying data.
- Telemetry continuity versus attacker activity: Missing logs may indicate tampering, but may equally reflect operational failure. Corroboration is essential.
- Analytical capability versus legal defensibility: Sophisticated correlation or anomaly detection does not replace reproducible acquisition and transparent reporting.
A future, separately labeled proposed study could test candidate anti-forensic alerts in an authorized laboratory using synthetic logs. It would need documented data generation, ground truth, explicit rule logic, false-positive measurement, and reproducible analysis. That study has not been performed as part of this paper.
10. Conclusion
SIEM-assisted log correlation can strengthen cyber investigations by organizing distributed telemetry and highlighting patterns that warrant scrutiny. Its contribution is strongest when paired with disciplined acquisition, integrity checks, independent corroboration, and transparent reporting. Anti-forensic detections should be treated as investigative leads rather than definitive proof, while automated models and tamper-resistant storage must not be mistaken for guarantees of accuracy or admissibility. A defensible investigation is defined not by the number of alerts produced but by the quality, traceability, and limitations of the evidence used to explain events.
Verified reference foundation
Kent, K., Chevalier, S., Grance, T., & Dang, H. (2006). Guide to integrating forensic techniques into incident response (NIST SP 800-86). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-86

National Institute of Standards and Technology. (2025). Incident response recommendations and considerations for cybersecurity risk management: A CSF 2.0 community profile (NIST SP 800-61 Rev. 3). https://csrc.nist.gov/projects/incident-response

European Parliament and Council of the European Union. (2016). Regulation (EU) 2016/679, Article 33. https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng/
Original coursework bibliography: verification pending
The five entries below were supplied in the original coursework. Their bibliographic metadata and alignment with individual claims have not been independently confirmed. They are retained for provenance, not cited as verified support in this revision.
- Ahmad Bhutta, H., Jahangir, M. T., & Ahmad Bhutta, A. (2025). Advancing Wi-Fi intrusion detection systems with machine learning techniques for enhanced classification of wireless attacks. ICACS. DOI supplied: 10.1109/ICACS64902.2025.10937819.
- Iqbal, R., Doctor, F., More, B., Mahmud, S., & Yousuf, U. (2022). Enabling cybersecurity defenses: Advanced endpoint detection, data breach identification, and anomaly resolution. Future Generation Computer Systems, 137, 74–85. DOI supplied: 10.1016/j.future.2022.07.005.
- Alenezi, A., & Basha, S. M. (2022). Detection of counter-forensic incidents using security information and incident management (SIEM) systems. IJACSA, 13(3), 34–41. DOI supplied: 10.14569/IJACSA.2022.0130306.
- Alneyadi, S., Sithirasenan, E., & Muthukkumarasamy, V. (2017). A log aggregation design criteria for robust SIEM: Security information and event management in enhancing threat detection. Computers & Security, 73, 1–15. DOI supplied: 10.1016/j.cose.2017.09.003.
- Casey, E. (2011). Digital evidence and computer crime: Forensic science, computers, and the Internet (3rd ed.). Academic Press.
Citation cleanup note: The original text also cited Fanuscu et al. (2022), Elvisianah et al. (2023), and Bhandari et al. (2023), without matching entries in the supplied bibliography. Those unsupported in-text citations were not carried into the revised narrative.
