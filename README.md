# Local LLM MoM Evaluation — Qwen3:4B vs. Phi-4 Mini

![Inference Engine](https://img.shields.io/badge/Inference%20Engine-Ollama%20%28Local%29-blue)
![Hardware](https://img.shields.io/badge/Hardware-Intel%20i5--8th%20Gen%20%7C%2016%20GB%20RAM-orange)
![Environment](https://img.shields.io/badge/Environment-CPU--Only-red)

[cite_start]A formal, in-depth evaluation of locally-hosted small language models (SLMs) optimized for automated **Minutes of Meeting (MoM) generation** directly from meeting transcripts on standard consumer CPU hardware[cite: 435].

---

## 📋 Executive Summary

[cite_start]This report evaluates the performance, speed, accuracy, and compliance of two prominent open-weight models (**Qwen3:4B** and **Phi-4 Mini**) across various formal and informal transcripts[cite: 436, 438, 439].

### Key Findings
* [cite_start]**Total Transcripts Processed:** 4 (Mixed formal and informal content)[cite: 436, 437, 438].
* [cite_start]**Qwen3:4B Cumulative Inference Time:** **3,266 seconds** (~54.4 min) across 3 main transcripts[cite: 439].
* [cite_start]**Phi-4 Mini Cumulative Inference Time:** **690 seconds** (~11.5 min) across 3 main transcripts[cite: 440].
* [cite_start]**Performance Velocity:** Phi-4 Mini delivers a massive **4.7× throughput advantage** overall[cite: 441].

### 🏆 Overall Recommendation
[cite_start]**Phi-4 Mini is recommended as the default production model** for operational deployment on this hardware profile[cite: 441]. [cite_start]It is significantly faster while outputting well-structured, hallucination-controlled segments[cite: 441]. 

[cite_start]*Note: **Qwen3:4B** produces slightly richer details and superior contextual parsing on long, highly complex legislative proceedings (e.g., `transcript_3.txt`)[cite: 442]. [cite_start]However, its active thinking mode inflates generation times to over 25 minutes for a single shorter file, rendering it impractical for real-time applications unless allocated to overnight batch jobs[cite: 442].*

---

## 💻 Test Environment Specifications

[cite_start]All benchmarks were conducted via pure CPU inference without hardware acceleration[cite: 449, 453].

| Component | Specification | Notes |
| :--- | :--- | :--- |
| **CPU** | Intel Core i5 — 8th Generation | [cite_start]Pure CPU execution throughout evaluation [cite: 449, 453] |
| **RAM** | 16 GB | [cite_start]Shared between Host OS, Ollama server, and active weights [cite: 450] |
| **Storage** | 512 GB SSD | [cite_start]Local repository for model configurations and text dumps [cite: 451] |
| **Operating System**| Windows | [cite_start]Standard platform distribution [cite: 452] |
| **Inference Engine**| Ollama (Local) | [cite_start]Local localized instance runner [cite: 452] |
| **GPU** | None / Not utilized | [cite_start]No hardware acceleration available [cite: 449, 453] |
| **Qwen3:4B Quant** | `Q4_K_M` | [cite_start]4-bit standard quantization pulled directly via Ollama [cite: 454] |
| **Phi-4 Mini Quant**| GGUF (Imported) | [cite_start]Downloaded from Hugging Face and imported via custom Modelfile [cite: 455] |

---

## 📄 Source Transcripts Profile

[cite_start]The models were tested against 3 distinct core contextual transcripts under `MODE B` (Formal Proceedings) configuration rules[cite: 458, 461, 464]:

1. **Transcript 1: Scheduling & Email Policy Meeting**
   * [cite_start]**File Source:** `transcript_1.txt` [cite: 457]
   * [cite_start]**Size / Word Count:** 5,456 bytes (~790 words) [cite: 457]
   * [cite_start]**Duration Range:** 00:00 – 07:15 [cite: 457]
   * [cite_start]**Type:** Internal operations (informal dynamic) [cite: 457, 458]
   * [cite_start]**Context:** Small-team conflicts on scheduling tools (Outlook vs. web tracker), email subject lines, prioritization labelling rules, and office holiday party layout[cite: 458]. [cite_start]No specific participants named except for "Ellen"[cite: 459].

2. **Transcript 2: Pakistan Cabinet Meeting Address**
   * [cite_start]**File Source:** `transcript_2.txt` [cite: 459]
   * [cite_start]**Size / Word Count:** 2,101 bytes (~310 words) [cite: 460]
   * [cite_start]**Duration Range:** 00:00 – 03:01 [cite: 460]
   * [cite_start]**Type:** Government Executive / Cabinet Address [cite: 460]
   * [cite_start]**Context:** Translated official speech detailing a major transparent government transaction, recognition of a national award recipient, and a formal state invitation to the PTI for political dialogue[cite: 460, 461]. [cite_start]Participants are not individually identified by name[cite: 462].

3. **Transcript 3: Pakistan Senate Committee Proceedings**
   * [cite_start]**File Source:** `transcript_3.txt` [cite: 462]
   * [cite_start]**Size / Word Count:** 18,185 bytes (~2,600 words) [cite: 462]
   * [cite_start]**Duration Range:** Not specified inside the transcript text [cite: 463]
   * [cite_start]**Type:** Legislative / Senate Parliamentary Committee session [cite: 463]
   * [cite_start]**Context:** Multi-topic complex Senate debate reviewing judicial boundary interactions under Article 69, domestic violence legislation frameworks, the Bounty Rape Bill, CBDR-RC parameters, gender equality issues, Balochistan regional unrest, and Khyber Pakhtunkhwa emergency structural updates[cite: 464]. [cite_start]Features multiple explicit named lawmakers/participants[cite: 464, 465].

---

## 📊 Comprehensive Performance Benchmark

| Transcript Target | Model Variant | Generation Time | Relative Execution Speed | Completion Status | Core Quality Observations |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [cite_start]**transcript_1.txt**<br>`~790 words` [cite: 467, 468] | [cite_start]**Qwen3:4B** [cite: 468] | [cite_start]**1,567.4 s** (~26.1 min) [cite: 468] | [cite_start]6.7× Slower [cite: 468] | [cite_start]<kbd>Complete</kbd> [cite: 469] | Thinking mode was active. [cite_start]Produced an outstanding structured MoM, but truncated the final office party segment and standard action items[cite: 469, 470]. |
| | [cite_start]**Phi-4 Mini** [cite: 470] | [cite_start]**232.4 s** (~3.9 min) [cite: 470] | [cite_start]**Baseline** [cite: 471] | [cite_start]<kbd>Complete</kbd> [cite: 471] | [cite_start]Populated all structural headings[cite: 472]. [cite_start]Successfully captured the office party item, but appended unsolicited meta-commentary[cite: 473]. |
| [cite_start]**transcript_2.txt**<br>`~310 words` [cite: 473, 474] | [cite_start]**Qwen3:4B** [cite: 474] | [cite_start]**1,461.1 s** (~24.4 min) [cite: 474] | [cite_start]7.9× Slower [cite: 474] | [cite_start]<kbd>Complete</kbd> [cite: 475] | [cite_start]Excellent structural layout[cite: 475]. [cite_start]Adhered strictly to constraints by documenting "no clear decisions" where matching data was absent[cite: 476]. |
| | [cite_start]**Phi-4 Mini** [cite: 476] | [cite_start]**185.4 s** (~3.1 min) [cite: 476] | [cite_start]**Baseline** [cite: 477] | [cite_start]<kbd>Complete</kbd> [cite: 478] | [cite_start]Rapid operational delivery[cite: 478]. [cite_start]However, introduced context bleeding by referencing an external "Marala transaction" not in the file[cite: 479]. |
| [cite_start]**transcript_3.txt**<br>`~2,600 words` [cite: 480] | [cite_start]**Qwen3:4B** [cite: 480] | [cite_start]**237.5 s** (~4.0 min) [cite: 481] | [cite_start]**0.87× (Faster Here)** [cite: 481] | [cite_start]<kbd>Complete</kbd> [cite: 482] | [cite_start]**Best overall output in the evaluation suite.** Extracted named officials flawlessly with deep logical structure[cite: 482, 483]. |
| | [cite_start]**Phi-4 Mini** [cite: 484] | [cite_start]**272.4 s** (~4.5 min) [cite: 484] | [cite_start]1.15× Slower Here [cite: 485] | [cite_start]<kbd>Partial</kbd> [cite: 485] | [cite_start]Failed to build a full formal MoM structure[cite: 485]. [cite_start]Emitted a highly condensed key-points summary instead[cite: 485]. |
| [cite_start]**AGGREGATED TOTALS** [cite: 486] | [cite_start]**Qwen3:4B** [cite: 486] | [cite_start]**3,266.0 s** (~54.4 min) [cite: 486] | [cite_start]*High Latency Profile* [cite: 486] | *High Quality* | [cite_start]**Phi-4 Mini is 4.7× faster across low-to-mid length files.** [cite: 486] |
| | [cite_start]**Phi-4 Mini** [cite: 486] | [cite_start]**690.2 s** (~11.5 min) [cite: 486] | [cite_start]**High Throughput Standard** [cite: 486] | *Structural Weakness on Long Files* | [cite_start]**Recommended for standard automated pipelines.** [cite: 441] |

---

## 🔍 Granular Output & Quality Analysis

### [cite_start]Transcript 1: Scheduling & Email Policy Meeting [cite: 301, 302]
* **Qwen3:4B Assessment:**
  * [cite_start]*Strengths:* Correctly isolated core operational issues (Outlook vs. web tracker scheduling overlaps) and recorded the two binding policy decisions[cite: 303, 304, 305]. [cite_start]Avoided name hallucinations[cite: 306].
  * [cite_start]*Weaknesses:* Dropped the final social agenda item (holiday party layout) entirely and cut off before generating action item tables due to token exhaustion from long thinking tokens[cite: 306, 307, 308].
* **Phi-4 Mini Assessment:**
  * [cite_start]*Strengths:* Generated all template divisions smoothly within 4 minutes, tracking "Ellen" and the Chair with specific action tasks[cite: 310, 312, 313].
  * [cite_start]*Weaknesses:* Leaked unprofessional first-person prose ("myself") and included meta-notes advising users on real-world management best practices[cite: 313, 314].

### [cite_start]Transcript 2: Pakistan Cabinet Meeting Address [cite: 316]
* **Qwen3:4B Assessment:**
  * [cite_start]*Strengths:* Captured the complex political balance of the speech[cite: 316]. [cite_start]Correctly registered the political dialogue initiation with the PTI as a "Deferred / Pending Matter"[cite: 318]. 
  * [cite_start]*Weaknesses:* Latency profile of 24 minutes for processing a 3-minute speech transcript represents an operational bottleneck[cite: 318].
* **Phi-4 Mini Assessment:**
  * [cite_start]*Strengths:* Processed and completed processing in ~3 minutes[cite: 320].
  * [cite_start]*Weaknesses:* Suffered from explicit hallucination/context bleed—labeling the file as the "Marala transaction" when the word "Marala" never appeared anywhere in the source document[cite: 321].

### [cite_start]Transcript 3: Pakistan Senate Committee Proceedings [cite: 324]
* **Qwen3:4B Assessment:**
  * [cite_start]*Strengths:* Flawless parsing of a complex, mixed Urdu-English legislative session[cite: 326]. [cite_start]Accurately extracted all key political figures including *Senator Aisha Raza, Senator Salim Madhubwala, Mr. Tony Jal, Mr. Kamran Murtaza*, and the *Attorney General*[cite: 325]. [cite_start]Derived 5 logical, text-supported actions without hallucination[cite: 325, 327].
  * *Weaknesses:* Slight deviation from the requested MoM template format and minor utilization of verbatim quote snippets[cite: 328, 329].
* **Phi-4 Mini Assessment:**
  * *Strengths:* Isolated the primary constitutional tension around legislative autonomy under Article 69[cite: 331, 332].
  * [cite_start]*Weaknesses:* Struggled significantly with data length and contextual density[cite: 336]. [cite_start]Instead of building a structured MoM, it collapsed the output into a standard 4-topic key-points summary, omitting mandatory participant logs, open questions, risks, and next steps[cite: 332, 333, 334].

---

## 🛠 Model Selection Quick-Reference Matrix

Depending on the operational constraints of your CPU environment, select your inference target using this strategy:

| Operational Requirement | Recommended Local Model | Execution Configuration |
| :--- | :--- | :--- |
| **High-Throughput Pipelines** | `Phi-4 Mini` | [cite_start]Use shorter system instructions with strict token limits via Ollama[cite: 215]. |
| **Multilingual/Complex Transcripts** | `Qwen3:4B` | [cite_start]`Q4_K_M` via Ollama[cite: 214]. [cite_start]Run as an isolated batch task to accommodate active thinking overhead[cite: 213, 215]. |
| **Next Evaluated Benchmark** | `Gemma 3 4B` | [cite_start]To be tested next for potentially superior instruction adherence[cite: 216]. |

---
[cite_start]*Internal Distribution Only · Self-contained performance assessment report generated on June 5, 2026[cite: 211, 212].*
