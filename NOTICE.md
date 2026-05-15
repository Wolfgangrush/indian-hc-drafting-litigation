# NOTICE — Provenance and Privilege Statement

This document is part of the public release of the `indian-hc-drafting` plugin (v0.1.0 and onwards). It declares the provenance of the plugin's content, in order to address any question about advocate-client privilege, client confidentiality, professional ethics, and personal-data protection that may be raised by any reader, complainant, regulator, or Bar Council disciplinary authority.

The plugin is bench-config-aware: the universal structural skeleton is the same across all Indian High Courts, and bench-specific elements (Court header, Appellate-Side / Original-Side Rules reference, annexure-marker convention, paper-size and font preference) are supplied by the user via a `bench-config.md` file in the user's case folder. At the v0.1.0-alpha milestone, the plugin is most-deeply-validated for Bombay High Court (Nagpur Bench); other Indian High Courts are supported via bench-config and deep per-bench validation will come from community contribution.

This NOTICE is published in plain language so that any reader — practising advocate, judge, Bar Council officer, regulator, member of the public, fellow developer — can understand the position without ambiguity.

---

## 1. What this plugin contains

This plugin contains the following categories of content, and **only** the following categories of content:

(a) **Procedural skeletons** — the structural shape of pleadings prescribed by Indian procedural law (cause title, party block, statutory opening, prelude, facts section header, grounds section header, prayer, verification, counsel block, index, synopsis, list of annexures, accompanying applications).

(b) **Formatting conventions** — Registry-compliant text-formatting conventions of Indian High Courts — heading style, parties separator, salutation phrasing, annexure marker conventions, prayer-opening conventions, counsel block layout, paper size and font conventions, page numbering conventions for annexures. The default values shipped in the plugin reflect Bombay HC Nagpur conventions (the most-deeply-validated bench at this milestone); bench-specific values for other High Courts are supplied by the user via the `bench-config.md` file in the user's case folder.

(c) **Statutory references** — citations to public statutes (Constitution of India, Code of Civil Procedure 1908, Code of Criminal Procedure 1973, Bharatiya Nagarik Suraksha Sanhita 2023, Indian Evidence Act 1872, Bharatiya Sakshya Adhiniyam 2023, Motor Vehicles Act 1988, Hindu Marriage Act 1955, Special Marriage Act 1954, Family Courts Act 1984, Contempt of Courts Act 1971, Limitation Act 1963, and other public enactments).

(d) **Procedural rule references** — citations to public rules of court (Bombay High Court Appellate Side Rules 1960, Bombay High Court Original Side Rules, and the corresponding Appellate-Side / Original-Side Rules of any other Indian High Court as supplied by the user via bench-config; Bar Council of India Standards of Professional Conduct and Etiquette under Section 49(1)(c) of the Advocates Act 1961; State Civil and Criminal Manuals; Bombay High Court Practice Notes and Circulars and the corresponding Practice Notes of other High Courts as supplied by the user).

(e) **Generic placeholders** — every variable in every template is marked with a placeholder such as `[Petitioner]`, `[Respondent]`, `[Date]`, `[FIR No.]`, `[Annexure-A]`, `<DD.MM.YYYY>`, `<Case No./Year>`. No placeholder is filled with any specific person's name, any specific date, any specific case number, or any specific identifying information.

(f) **Anti-hallucination workflow** — six agents (Reader, Format, Drafter, Verifier, Refiner, Overseer) that operate on a case folder supplied by the user. The plugin itself contains no case folder.

---

## 2. What this plugin does NOT contain

This plugin does **not** contain any of the following, and has never contained any of the following at any point in any committed version:

(a) **No specific client matter.** No client of the author appears in the plugin, by name, by initials, by case number, by FIR number, by docket number, by court hall, by date pattern, by relief pattern, or by any other identifying signature.

(b) **No client communications.** No oral or written communication made to the author by or on behalf of any client appears in the plugin in any form, in whole, in summary, in paraphrase, or in pattern.

(c) **No client documents.** No document or instrument with which the author has become acquainted in the course of professional employment as an advocate appears in the plugin, in original, in redacted, in summary, in extract, or in pattern.

(d) **No personal data of any data principal.** The plugin processes no personal data, collects no personal data, stores no personal data. It contains no name, no contact information, no date of birth, no address, no biometric data, no financial data, no health data, no caste or community data, no political affiliation data, no other category of personal data as defined under the Digital Personal Data Protection Act 2023 of any identifiable natural person other than the author of this plugin himself (named publicly as the author and publisher).

(e) **No witness testimony, no deposition, no statement, no FIR content, no chargesheet content, no judgment content** of any specific matter handled by the author or any other advocate.

(f) **No client list, no chamber list, no associate list, no instructing-counsel list, no opposing-counsel list, no judge-specific intelligence** of any kind.

(g) **No tracking, no telemetry, no analytics, no opt-in error reporting, no login, no account, no cloud sync.** The plugin runs entirely on the user's machine. The plugin author receives no information about who installs the plugin, who uses it, on what cases, with what facts, with what outcomes.

---

## 3. The legal distinction

Indian law has long recognised a clear distinction between two categories:

(i) **Specific client communications and documents** — protected under Section 132 of the Bharatiya Sakshya Adhiniyam 2023 (formerly Section 126 of the Indian Evidence Act 1872) and under Rule 17 of the Bar Council of India Standards of Professional Conduct and Etiquette. This category is privileged and confidential. An advocate may not disclose it.

(ii) **General professional knowledge of procedural law** — an advocate's accumulated knowledge of how a writ petition is structured under Article 226 of the Constitution, what the prayer clause of a bail application looks like under Section 483 of the BNSS, what statutory opening a Criminal Revision Application requires under Section 442 of the BNSS, how the Bombay High Court Registry expects the parties separator to appear. This category is the advocate's own professional knowledge. It is not the property of any specific client. It is not privileged.

This plugin operates **entirely within category (ii)**.

Every Indian advocate accumulates this knowledge through years of practice, through study of the Code of Civil Procedure, through study of the Code of Criminal Procedure, through study of the Constitution, through study of the Bombay High Court Rules, through study of leading procedural textbooks (Mulla, Sarkar, Ratanlal and Dhirajlal), through observation of court practice, through senior-counsel mentorship, through Bar Association continuing education, and through reading the published judgments of the Supreme Court and the High Courts.

The plugin codifies that accumulated procedural knowledge into machine-readable form. It does not codify any client's confidential information.

The same distinction underlies why every Indian law school teaches drafting, why every Indian law library carries a Mulla on the CPC, why every legal-aid clinic distributes pleading templates, and why no court has ever held that an advocate is barred from sharing procedural knowledge with another advocate, with a law student, with a junior, or with the public.

The plugin is, in this respect, identical in legal character to a published drafting textbook, a continuing legal education handout, or a senior advocate's pleading-style lecture. The medium is software. The content is procedural knowledge.

---

## 4. The author's professional position

The author is **Rushikesh R. Mahajan**, Advocate, enrolled with the Bar Council of Maharashtra and Goa, practising before the Bombay High Court, Nagpur Bench. The plugin is published under the open-source brand **Wolfgang Rush**, which is the author's publishing handle for legal-technology infrastructure; the real-identity accountability declared in this section attaches to the author personally and is not displaced by the use of a publishing handle.

The author retains full enrollment, full responsibility, and full liability under the Advocates Act 1961, the Bar Council of India Rules, the Bombay High Court Rules, and the Standards of Professional Conduct and Etiquette.

The plugin is published as a personal contribution to the open-source legal-technology ecosystem. It is published without any commercial channel, without any solicitation of professional work, without any advertisement of professional services, and without any acceptance of work through this repository.

This NOTICE is filed of record in this open-source repository so that any person who reads, reviews, audits, or assesses this plugin has full transparency about its provenance and its scope from the moment of release.

---

## 5. Verification of clean provenance

The repository owner shall maintain, on a private offline record, a build log demonstrating that every line of every file in the plugin was either:

(a) authored from scratch as procedural skeleton, OR
(b) derived from public statute, public rule, public judgment, or public procedural textbook, OR
(c) derived from the author's own original procedural knowledge as a practitioner.

No line of any file was, at any stage, copied from, paraphrased from, summarised from, or pattern-matched against any specific client matter, client communication, or client document.

This NOTICE is the author's signed declaration of that position.

---

## 6. Reporting concerns

If any reader, regulator, fellow advocate, or member of the public believes any specific content in this plugin is derived from a specific client matter or specific confidential communication, the reader is requested to:

(a) identify the file and line at issue in the plugin,
(b) identify the specific client matter or communication believed to be the source,
(c) explain the basis of the belief,

and raise the concern via a GitHub Issue on this repository.

Concerns raised with these particulars will be investigated and the file or line will be removed or rewritten if the concern is well-founded. Concerns raised without these particulars cannot be acted upon.

---

## 7. Standing instruction to forks and derivatives

Any fork, derivative, downstream redistribution, or commercial integration of this plugin or its content shall preserve this NOTICE in unmodified form, and shall extend the same provenance discipline to any content added in the fork or derivative.

This NOTICE travels with the code under the same MIT licence that governs the source.

---

*Signed and dated by way of public commit history on the repository. The author stands by every line of this notice.*
