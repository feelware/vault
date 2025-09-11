---
status: done
deadline: 2025-07-07T16:30
class: general
---
# Gestión de riesgos: examen final

## Frameworks de gestión de riesgo

### NIST SP 800-30

([diapositivas](../../source-material/lectures/pdf/riesgos-nist-sp-800-30.pdf), [documento oficial](../../source-material/misc/pdf/NIST%20SP800-30.pdf))

- NIST: 4 letras, 4 fases:
	- **P**reparación
	- **I**dentificación
	- **E**valuación
	- **R**espuesta
(Risk IT introduce Comunicación)

### ISO 31000

([diapositivas](../../source-material/lectures/pdf/riesgos-iso-31000.pdf), [documento oficial](../../source-material/misc/pdf/ISO_31000_2018(es).PDF))

### Risk IT

([diapositivas](../../source-material/lectures/pdf/riesgos-risk-it.pdf), [documento oficial](../../source-material/misc/pdf/Risk-IT-Framework-2nd-Edition_fmk_Eng_0620-1.pdf))

### ISO 27005

([diapositivas](../../source-material/lectures/pdf/riesgos-iso-27005.pdf), [documento oficial](../../source-material/misc/pdf/ISO%20IEC%2027005-2018.pdf))

### OCTAVE

([diapositivas](../../source-material/lectures/pdf/riesgos-octave.pdf))

#### OCTAVE Allegro

([documento oficial](../../source-material/misc/pdf/Octave%20Allegro.pdf))

#### OCTAVE-S

([documento oficial](../../source-material/misc/pdf/OCTAVE-S.pdf))

### MAGERIT

([diapositivas](../../source-material/lectures/pdf/riesgos-magerit.pdf), [documento oficial](../../source-material/misc/pdf/Magerit_v3_libro1_metodo.pdf))

## Riesgos en ciberseguridad

### CIS & PCI DSS

([diapositivas](../../source-material/lectures/pdf/riesgos-ciberseguridad.pdf))

#### CIS

([documento oficial](../../source-material/misc/pdf/CIS-Controls-Version-7-1.pdf))

#### PCI DSS

([documento oficial](../../source-material/misc/pdf/PCI-DSS-v4_0-LA.pdf))

---

# Risk Management Frameworks: Overview and Comparison

This report compares seven prominent risk management frameworks: **NIST SP 800‑30**, **ISO 31000**, **Risk IT**, **ISO 27005**, **OCTAVE Allegro**, **OCTAVE‑S**, and **MAGERIT**. Each framework’s focus, applicability, integration, level of detail, analysis style, and unique concepts are summarized below, followed by a comparative table highlighting key differentiators.

## NIST SP 800‑30 (Risk Assessment Guide)

NIST SP 800‑30 (2012) is a detailed U.S. guidance on conducting information security risk assessments for IT systems. It defines risk as the net negative impact of threats exploiting vulnerabilities (combining likelihood and impact) and provides a **structured risk assessment process**. The guide offers extensive procedures for identifying assets, threats, vulnerabilities and analyzing risk for senior decision-makers. Although written for federal agencies, it is widely adopted by large enterprises and government contractors. NIST 800‑30 is deeply integrated with the NIST Risk Management Framework and Cybersecurity Framework (CSF), often underpinning “Identify – Risk Assessment” activities. It can also align with ISO/IEC 27001’s risk requirements. The level of detail is high: the publication discusses both qualitative and quantitative methods, weighing trade-offs (e.g. qualitative impact ratings versus quantitative cost‑benefit analysis). Thus, NIST 800‑30 supports both qualitative and quantitative analyses. It does not introduce proprietary terminology; it uses standard risk concepts (threats, vulnerabilities, impact, likelihood) in line with other NIST guidance.

## ISO 31000 (Risk Management Principles and Guidelines)

ISO 31000:2018 is a generic **enterprise risk management** standard, providing high-level principles and a framework for managing risk across any organization. It is _not specific to cybersecurity_ but covers all types of risk (strategic, financial, operational, etc.). The standard is explicitly designed to be applied by organizations of **any size or sector**, so it is equally relevant for small businesses or large corporations. ISO 31000 is non‑certifiable guidance (principles and processes, not requirements) and does not prescribe technical procedures. It emphasizes integrating risk management into governance and decision-making (embedding risk awareness into culture). Its detail level is **conceptual rather than technical**: it outlines steps like establishing context, risk identification/analysis, treatment, and monitoring, but leaves methods open. ISO 31000 is flexible about analysis methods; organizations may use qualitative, quantitative, or mixed approaches as appropriate (the standard does not mandate one). It introduces broad risk concepts (risk appetite, risk criteria, context, etc.) consistent with general ISO risk terminology, but no unique model beyond standard risk management process.

## ISACA Risk IT Framework

The Risk IT Framework (2nd ed., 2009) by ISACA is an **IT‑risk management** framework that bridges business and technology risk. It provides an end-to-end view of IT-related risks — from boardroom strategy to operational execution. Risk IT is aimed at enterprises with mature governance (large organizations), especially those using COBIT for IT governance. It **complements COBIT**: where COBIT prescribes controls (the “means” of governance), Risk IT prescribes how to identify, govern and manage IT risk (the “ends”). It also builds on enterprise risk management (ERM) standards (COSO, ISO 31000, AS/NZS 4360) by applying them to IT risk. The framework is quite comprehensive: it defines three domains (Risk Governance, Risk Evaluation, Risk Response) with specific processes (e.g. RG1, RE2, RR1) and roles. It integrates deeply with COBIT and Val IT processes for IT governance and investment. Risk IT is suitable mostly for medium-to-large organizations with formal IT governance. It allows both qualitative and quantitative approaches: for example, it encourages use of key risk indicators and quantitative feedback to decision-makers while also emphasizing scenario analysis and business impact. Unique to Risk IT are its governance-centric concepts (risk appetite/tolerance metrics, portfolio-level risk profiles, IT-specific risk scenarios) and its vocabulary of “IT risk” (business risk arising from IT) and the RG/RE/RR process model.

## ISO/IEC 27005 (Information Security Risk Management)

ISO/IEC 27005:2018 (updated 2022) is the ISO standard for **information security risk management**, designed to complement ISO/IEC 27001. It provides guidelines for managing cybersecurity risks (confidentiality, integrity, availability) but _does not prescribe certification_ requirements. ISO 27005 covers any organization seeking an ISO 27001 ISMS: it is _technology-neutral_ and useful to both small and large firms. It aligns directly with ISO 27001: it details the risk assessment and treatment processes that ISO 27001 mandates, but leaves choices of exact methods to the organization. The standard outlines a seven-stage continuous process (establish context, risk assessment, risk treatment, etc.), with inputs/actions/outputs for each phase, but **does not lock in a single methodology**. In practice, organizations using ISO 27005 can choose qualitative scales or quantitative measures (e.g. financial impact), or mixed approaches. It emphasizes risk criteria definition (e.g. asset values, impact categories) and in 2022 explicitly introduced semi-quantitative options. ISO 27005 therefore supports both qualitative and quantitative analysis (the text notes advantages/disadvantages of each). Its terminology is that of the ISO 27000 series (assets, threats, vulnerabilities, risk owner, likelihood, impact, etc.) and it uses no new proprietary models beyond the standard risk assessment vocabulary.

## OCTAVE Allegro (CERT)

OCTAVE Allegro (2007, SEI/CMU) is an **asset-focused risk assessment method** developed by Carnegie Mellon’s CERT. It is a streamlined version of the original OCTAVE, tailored for speed and agility in small-to-medium organizations. Allegro’s process is simplified (about 8 steps) and focuses explicitly on **critical information assets and associated risks**, rather than exhaustively cataloging all organizational assets. It reduces complexity and resource requirements: only key assets are scoped, and the amount of data collection, training, and documentation is minimized. This makes Allegro more practical for organizations without extensive security staff. It is _especially relevant to cybersecurity_ because it centers on IT/information assets and vulnerabilities. Unlike some rigid frameworks, Allegro’s scope can adapt to organizational needs and can be repeated periodically. It is typically qualitative (gathering asset profiles, threat lists, risk scenarios) but organizations may attach scores to likelihood/impact if desired. No direct integration with other standards (it is standalone), but its concepts (asset valuation, threat modeling) can feed into any ISMS. Unique concepts in Allegro include **information asset profiles** and **threat profiles**, emphasizing business impact and mitigation strategies for the most important assets.

## OCTAVE‑S (OCTAVE Strategic)

OCTAVE‑S (2008, SEI/CMU) is a **variant of OCTAVE** aimed at **small or decentralized organizations**. It is even more simplified than Allegro. OCTAVE‑S focuses on strategic (mission-level) risks rather than granular technical detail. A small team (often just an internal IT/security group) defines threat profiles and high-level asset scope relative to business goals. This makes it suitable for flat organizations or small agencies where formal security programs may be limited. The methodology has only three phases and assumes the team has enough knowledge to proceed without extensive external data. OCTAVE‑S is primarily qualitative, emphasizing understanding of mission, objectives and critical assets rather than calculating precise numeric risk. Like Allegro, it is standalone (not part of ISO or COBIT), but it uses similar terms (threat profiles, impact, risk scenarios). Its unique model is its **flat, self-directed** approach: the organization’s own security team drives the assessment focusing on top-priority risks, with minimal overhead.

## MAGERIT (Spanish Government Methodology)

MAGERIT v3 (2012) is a Spanish government **risk analysis and management methodology** for information systems, developed by Spain’s Ministry of Finance/Administration. It follows ISO 31000’s process (risk context, analysis, evaluation, treatment) and uses the same terminology. It is freely available and widely used for public sector projects (especially those under Spain’s National Security Scheme). MAGERIT is quite detailed: it consists of three volumes (method, asset catalog, and technical guidelines) covering every step. It is meant for organizations heavily relying on IT services. Integration-wise, MAGERIT is aligned with ISO/IEC 27001 (both in structure and control considerations) and with ISO 31000 risk principles. It supports both qualitative (threat/vulnerability identification, impact categories) and quantitative elements (e.g. monetary valuation of asset impact). The methodology introduces some unique elements such as a comprehensive catalog of assets and threats, impact evaluation rules, and iterative risk treatment planning. Because it is Spanish-language and tailored for government, it has less global adoption, but its concepts (asset-at-risk analysis, risk matrices) are standard.

## Comparative Table

|**Framework**|**Cybersecurity Relevance / Practical Use**|**Org Size Suitability**|**Integration with Other Standards**|**Level of Detail / Complexity**|**Risk Analysis Style**|**Unique Terms / Models**|
|---|---|---|---|---|---|---|
|**NIST SP 800‑30**|Rigorous IT security risk assessment guide (U.S. federal focus); highly relevant to cybersecurity assessments.|Medium–large (designed for federal agencies; heavy methodology).|Core to NIST RMF and CSF (Identify); can map to ISO/IEC 27001 risk steps.|**High detail** – multi-tiered, formal risk assessment process.|Supports both qualitative and quantitative analysis (discusses trade-offs).|Common risk terms (threat, vulnerability, impact); no new jargon.|
|**ISO 31000**|Broad enterprise risk management (ERM) – not specific to cyber; useful for embedding risk culture.|Any size (explicitly designed for any organization).|Generic; underpins many systems but not specific (often used alongside ISO 27001, COSO, etc.).|**High-level guidelines** – principles and process; little technical detail.|Method-agnostic (allows qualitative, quantitative or mixed, as needed).|Standard ERM concepts (risk context, appetite, criteria); no unique model.|
|**Risk IT (ISACA)**|Focused on IT/business risk (cyber and non-cyber IT threats); aligns risk to business value.|Large enterprises (COBIT adopters; best for well-governed IT organizations).|Closely linked with COBIT (IT governance) and Val IT; based on COSO/ISO 31000 ERM concepts.|**Moderate detail** – defined process model (Governance, Evaluation, Response) but not low-level technical steps.|Both quantitative (IT risk metrics/KRIs) and qualitative (risk scenarios) approaches.|Introduces IT-specific risk domains (e.g., _IT Risk Governance_ processes RG1–RG3) and IT‑centric risk vernacular.|
|**ISO/IEC 27005**|Directly addresses information security risk (supports ISO 27001 ISMS).|Any size; applies to all organizations implementing ISO 27001 (flexible scope).|Complements ISO 27001 controls; also conceptually aligns with NIST SP 800-30 risk steps.|**Moderate** – defines 7-step process (context, assessment, treatment, etc.), but techniques are up to user.|Both – explicitly allows qualitative, semi-quantitative or quantitative methods for risk estimation.|Uses standard info-security terms (asset, threat, vulnerability, CIA triad); no novel model.|
|**OCTAVE Allegro**|Cyber risk assessment focusing on information assets and threats.|Small to mid-sized orgs (developed for SMBs or teams with limited resources).|Standalone method (not part of ISO/IEC or COBIT); can inform an ISMS or security program.|**Moderate** – structured (8 workshops/steps) but streamlined; less bureaucratic than full OCTAVE.|Primarily qualitative (asset profiles, threat scenarios); can include basic quantitative scales if desired.|Asset-centric profiles and risk scenarios; emphasizes business impact on key _information assets_.|
|**OCTAVE‑S**|Strategic cyber risk method for small/flat organizations.|Small organizations or departments (minimal hierarchy).|Standalone; not integrated into larger frameworks.|**Low complexity** – only 3 phases; lightweight process.|Qualitative, focusing on mission/business objectives rather than detailed threats.|Emphasizes _strategic_ risk (mission, objectives) and uses minimal documentation (self-directed approach).|
|**MAGERIT**|Governmental IT risk analysis method (widely used in Spanish public sector).|Any size (especially public agencies and organizations with heavy ICT use).|Aligns with ISO 31000 risk process and ISO 27001 ISMS structure; used to implement Spain’s security policies.|**High detail** – three-volume methodology (conceptual rules, asset/threat catalogs, guidelines).|Supports both qualitative (threat/vulnerability matrices) and quantitative (impact valuations) approaches.|Uses standardized risk mgmt terms (per ISO), with Spanish-specific assets and controls catalogs; holistic governance focus.|

Each framework thus occupies a distinct niche. NIST 800‑30 is exhaustive and highly detailed, suited to rigorous cybersecurity programs in large organizations. ISO 31000 offers universal risk principles but little technical depth. Risk IT targets IT governance, emphasizing integration of IT risk into enterprise decision-making. ISO 27005 is tailored to information security management systems (ISM), aligning closely with ISO 27001. OCTAVE Allegro and OCTAVE‑S are flexible, workshop-based methods for smaller teams, focusing on asset-centric (Allegro) or mission-centric (OCTAVE-S) risks. MAGERIT provides a comprehensive Spanish-centered approach, blending ISO-style processes with public-sector requirements.

**Sources:** Authoritative publications and guidance for each framework were consulted. NIST SP 800‑30 and ISO documents provide core descriptions; the ISACA Risk IT framework is described by ISACA publications; ISO 27005 summaries and ESG resources detail its scope; OCTAVE materials and analyses describe Allegro and S’s features; and official MAGERIT documentation and reviews explain its structure and usage. All distinguishing characteristics above are drawn from these sources.
