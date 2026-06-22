# Checkpoint 2

---

## Surveys and taxonomies

### 1) A Systematic Literature Review on Detecting Software Vulnerabilities with Large Language Models

- Local PDF: [2507.22659v2-kaniewski-slr.pdf](./2507.22659v2-kaniewski-slr.pdf)
- Web: [arXiv 2507.22659](https://arxiv.org/abs/2507.22659) / [DOI 10.1145/3815425](https://doi.org/10.1145/3815425)
- Living repo: [Awesome-LLM4SVD](https://github.com/hs-esslingen-it-security/Awesome-LLM4SVD)

**Summary:** The most comprehensive SLR on LLM-based vulnerability detection (**263 studies**, arXiv v2). It defines taxonomies for task formulation, input representation, system architecture, adaptation techniques, and **datasets**. Key LLM families covered: GPT, Claude, Gemini, LLaMA, CodeLlama, DeepSeek, CodeBERT-family. Useful as the primary map for Related Work and for choosing comparable evaluation setups.

**SAST tools (surveyed studies):** CodeQL, Semgrep, SonarQube, SpotBugs, and others depending on the primary study cited.

**LLMs (taxonomy-level):** general-purpose (GPT-4, Claude, Gemini), code-specialized (CodeLlama, DeepSeek-Coder, StarCoder), encoder/hybrid (CodeBERT + GNN).

**Benchmarks cited:** Juliet, OWASP Benchmark, Big-Vul, DiverseVul, CWE-Bench-Java, CASTLE, and others — see [dataset links](#benchmark-and-dataset-links) below.

---

### 2) LLMs in Software Security: A Survey of Vulnerability Detection Techniques and Insights

- Local PDF: [2502.07049v2-sheng-survey.pdf](./2502.07049v2-sheng-survey.pdf)
- Web: [arXiv 2502.07049](https://arxiv.org/abs/2502.07049)

**Summary:** Focused survey on LLM applications in vulnerability detection: model selection, prompt engineering, semantic processing, multi-agent setups. Reports that GPT-4/GPT-3.5 dominate empirical studies; CodeLlama is common in fine-tuning experiments. Highlights gaps: repository-level coverage, dataset leakage, neuro-symbolic hybrids (CodeQL + LLM).

**SAST tools (in reviewed papers):** CodeQL and classical static analyzers referenced as baselines; neuro-symbolic hybrids (e.g. CodeQL + LLM) discussed as an emerging direction.

**LLMs:** GPT-4, GPT-3.5, CodeLlama, CodeBERT-family, StarCoder, others.

**Benchmarks:** Juliet C/C++ and Java, Big-Vul, FFmpeg/QEMU subsets, function-level datasets — [Juliet](https://samate.nist.gov/SARD/test-suites/111), [Big-Vul](https://huggingface.co/datasets/bstee615/bigvul).

---

### 3) Large Language Model for Vulnerability Detection and Repair: Literature Review and the Road Ahead

- Local PDF: [2404.02525v1-llm-vuln-road-ahead.pdf](./2404.02525v1-llm-vuln-road-ahead.pdf)
- Web: [arXiv 2404.02525](https://arxiv.org/abs/2404.02525)

**Summary:** Early structured review (58 papers) on LLM adaptation for vulnerability **detection and repair**. Categorizes fine-tuning, prompting, and hybrid approaches; documents limitations (hallucination, scalability) and a roadmap for future work. Good bridge between classic static analysis background and modern LLM methods.

**SAST tools:** discussed as traditional baselines (rule-based and taint tools).

**LLMs:** GPT-family, CodeLlama, security-oriented fine-tuned models (especially Solidity).

**Benchmarks:** Juliet, Devign, Big-Vul, DiverseVul (survey-level references).

---

### 4) Modern Approaches to Software Vulnerability Detection: A Survey of Machine Learning, Deep Learning, and Large Language Models

- Local PDF: [electronics14224449-ml-dl-llm-survey.pdf](./electronics14224449-ml-dl-llm-survey.pdf)
- Web: [DOI 10.3390/electronics14224449](https://doi.org/10.3390/electronics14224449) / [MDPI full text](https://www.mdpi.com/2079-9292/14/22/4449)

**Summary:** Broader evolution from ML/DL to LLMs for vulnerability detection. Positions neuro-symbolic hybrid methods as a promising direction. Useful for one-paragraph background on why LLM-only detection is insufficient and why SAST+LLM pipelines are emerging.

**SAST tools:** traditional static and rule-based analyzers as the pre-LLM baseline class.

**LLMs:** frontier and code-specialized models in comparative studies.

**Benchmarks:** Juliet, OWASP, real-world CVE datasets (survey-level).

> **Link note:** NIST SARD (`samate.nist.gov`) and some publisher DOIs (ACM, MDPI) may block automated requests or be intermittently unavailable; local PDFs and arXiv/GitHub mirrors are provided where applicable.

---

## SAST background and benchmarks

### 5) Comparison and Evaluation on Static Application Security Testing (SAST) Tools for Java

- Local PDF: [fse2023-sast-java-comparison.pdf](./fse2023-sast-java-comparison.pdf)
- Web: [FSE 2023 PDF](https://sen-chen.github.io/pdf/C38-FSE2023-Comparison%20and%20Evaluation%20on%20Static%20Application%20Security%20Test%20(SAST)%20Tools%20for%20Java.pdf)

**Summary:** Foundational SAST evaluation on Java CVEs. Defines **pattern/rule-based** vs **semantic/taint** analysis; compares mainstream tools and CWE mapping practices. Key baselines: **CodeQL, Semgrep, SpotBugs, SonarQube**. Essential for explaining what “SAST” means in the diploma and how to evaluate tools fairly.

**SAST tools:** broad Java SAST set; primary baselines CodeQL, Semgrep, SpotBugs, SonarQube.

**LLMs:** not evaluated (pure SAST paper).

**Benchmarks:** Java CVE benchmark constructed by authors; methodology transferable to pipeline YAML evaluation.

---

### 6) CASTLE: Benchmarking Dataset for Static Code Analyzers and LLMs towards CWE Detection

- Local PDF: [2503.09433v1-castle.pdf](./2503.09433v1-castle.pdf)
- Web: [arXiv 2503.09433](https://arxiv.org/abs/2503.09433)
- Dataset: [CASTLE-Benchmark](https://github.com/CASTLE-Benchmark/CASTLE-Benchmark)

**Summary:** Hand-crafted **250 C micro-programs**, **25 CWEs**; compares **13 static analyzers**, **10 LLMs**, and formal tools (e.g. ESBMC). Introduces CASTLE Score. Documents limitations of Juliet/SARD (leakage, size). Strong source for SAST-vs-LLM benchmark design.

**SAST tools:** 13 static analyzers (see [CASTLE repo](https://github.com/CASTLE-Benchmark/CASTLE-Benchmark) for full list).

**LLMs:** 10 LLMs benchmarked (see CASTLE repo).

**Benchmarks:** [CASTLE-C250](https://github.com/CASTLE-Benchmark/CASTLE-Benchmark), Juliet (comparison baseline).

---

### 7) RealVuln: Benchmarking Rule-Based, General-Purpose LLM, and Security-Specialized Scanners on Real-World Code

- Local PDF: [2604.13764v1-realvuln.pdf](./2604.13764v1-realvuln.pdf)
- Web: [arXiv 2604.13764](https://arxiv.org/abs/2604.13764)

**Summary:** Compares rule-based SAST, general LLMs, and security-specialized scanners on **26 intentionally vulnerable Python repositories** (educational/CTF-style). Provides a landscape table of benchmarks (OWASP, Juliet, CASTLE, CWE-Bench, etc.) and argues synthetic suites overstate SAST performance. Useful for justifying evaluation beyond synthetic suites, with the caveat that RealVuln repos are not production codebases.

**SAST tools:** multiple rule-based and security-specialized scanners (paper compares scanner categories).

**LLMs:** general-purpose and security-specialized LLM scanners.

**Benchmarks:** RealVuln (26 repos); compares against OWASP Benchmark, Juliet, CASTLE, CWE-Bench-Java.

---

## CI/CD and pipeline security

### 8) Characterizing the Security of Github CI Workflows

- Local PDF: [sec22-koishybayev-github-ci.pdf](./sec22-koishybayev-github-ci.pdf)
- Web: [USENIX SEC'22 PDF](https://www.usenix.org/system/files/sec22-koishybayev.pdf)

**Summary:** Large-scale empirical study of **447,238 workflows** across **213,854 repositories**. Defines CI/CD security properties (admittance, execution, code control, secrets access) and shows systemic risks: overprivileged workflows, untrusted third-party Actions, missing updates. Foundational **threat model** for pipeline-configuration security.

**SAST tools:** GWChecker (authors' GitHub Action for bad-practice warnings); not a full vulnerability scanner.

**LLMs:** not used.

**Benchmarks / corpus:** 447k workflows (empirical statistics; not per-alert labeled benchmark).

---

### 9) Argus: A Framework for Staged Static Taint Analysis of GitHub Workflows and Actions

- Local PDF: [usenixsecurity23-argus.pdf](./usenixsecurity23-argus.pdf)
- Web: [USENIX SEC'23 PDF](https://www.usenix.org/system/files/usenixsecurity23-muralee.pdf)

**Summary:** **Semantic/taint SAST** for GitHub Actions: Workflow IR (WIR), offline taint summaries for third-party Actions, staged propagation. Evaluated on **~2.7M workflows**; **5,298 confirmed code-injection** vulnerabilities in manual subset. Best academic reference for why pipeline YAML needs taint analysis, not only regex rules.

**SAST tools:** ARGUS (staged static taint analyzer for workflows/actions).

**LLMs:** not used.

**Benchmarks / corpus:** ~2.7M workflows; manual validation subset with confirmed injections.

---

### 10) GHAST: GitHub Actions Security Tester

- Local PDF: [2208.03837v2-ghast.pdf](./2208.03837v2-ghast.pdf)
- Web: [arXiv 2208.03837](https://arxiv.org/abs/2208.03837)

**Summary:** Methodology and tool for assessing GHA workflow security: parses YAML, applies checklists for command injection, confidential data disclosure, misconfigurations. In-the-wild campaign on **50 open-source projects**, analyzing **131,168 workflows** and identifying **20 previously unknown** security issues. Early reference for **domain-specific workflow scanners** and security-check design.

**SAST tools:** GHAST (workflow static checks).

**LLMs:** not used.

**Benchmarks:** 50-project in-the-wild campaign (rule-based ground truth).

---

### 11) Unpacking Security Scanners for GitHub Actions Workflows

- Local PDF: [2601.14455v2-unpacking-gha-scanners.pdf](./2601.14455v2-unpacking-gha-scanners.pdf)
- Web: [arXiv 2601.14455](https://arxiv.org/abs/2601.14455)
- Dataset: [github-actions-security](https://github.com/sparkrew/github-actions-security)

**Summary:** First systematic comparison of **9 GHA security scanners** on **2,722 workflows** from **388 repos**. Defines **10 weakness classes** (injection, excessive permissions, unpinned actions, secrets exposure, etc.). Tiered recommendations: **poutine + actionlint** (fundamental), **+ frizbee** (essential), **+ semgrep** (advanced); **zizmor** achieves the broadest general-purpose weakness coverage (RQ1). Primary source for choosing SAST tools in pipeline experiments.

**SAST tools:** actionlint, poutine, zizmor, scorecard, semgrep, ggshield, frizbee, pinny, scharf.

**LLMs:** not evaluated.

**Benchmarks:** [Unpacking GHA corpus](https://github.com/sparkrew/github-actions-security) (2,722 workflows).

---

## Hybrid LLM + SAST (extensions)

### 12) LLM-Driven Adaptive Source–Sink Identification and False Positive Mitigation for Static Analysis (AdaTaint)

- Local PDF: [2511.04023v1-adataint.pdf](./2511.04023v1-adataint.pdf)
- Web: [arXiv 2511.04023](https://arxiv.org/abs/2511.04023)

**Summary:** Neuro-symbolic framework: LLM infers source/sink specs, static taint engine validates paths with constraint checks to reduce hallucinations. Evaluated on Juliet 1.3, SV-COMP-style C tasks, and real projects. Relevant as a **specification-inference + FP reduction** pattern for hybrid pipelines.

**SAST tools:** static taint engine (AdaTaint core) + symbolic validation.

**LLMs:** LLM-driven source/sink identification and FP filtering.

**Benchmarks:** [Juliet Java 1.3](https://samate.nist.gov/SARD/test-suites/111) ([mirror](https://github.com/UnitTestBot/juliet-java-test-suite)), SV-COMP-style C tasks, real-world projects.

---

## Checkpoint 1 references (LLM + SAST methods)

These papers were reviewed in [Checkpoint 1](../checkpoint-1/report.md); PDFs are in `docs/checkpoint-1/`.

### 13) IRIS: LLM-Assisted Static Analysis for Detecting Security Vulnerabilities

- Local PDF: [2405.17238v3-IRIS.pdf](../checkpoint-1/2405.17238v3-IRIS.pdf)
- Web: [arXiv 2405.17238](https://arxiv.org/abs/2405.17238)

**Summary:** Neuro-symbolic system: GPT-4 infers CWE-specific taint specs and filters CodeQL FPs. On CWE-Bench-Java (120 CVEs), CodeQL finds 27 vulnerabilities vs IRIS+GPT-4 finding 55 (+28), with ~5 pp lower false discovery rate.

**SAST:** CodeQL | **LLM:** GPT-4 | **Benchmark:** [CWE-Bench-Java](https://github.com/iris-sast/cwe-bench-java)

---

### 14) Sifting the Noise: LLM Agents in Vulnerability False Positive Filtering

- Local PDF: [2601.22952v1-LLM-False-Positive.pdf](../checkpoint-1/2601.22952v1-LLM-False-Positive.pdf)
- Web: [arXiv 2601.22952](https://arxiv.org/abs/2601.22952)

**Summary:** Compares agent frameworks (Aider, OpenHands, SWE-agent) with Claude Sonnet 4, DeepSeek Chat, and GPT-5 for triaging CodeQL alerts; on OWASP Benchmark, FP rates drop from >92% to as low as 6.3% in the best setup; on Vul4J + CodeQL, up to 93.3% of FPs identified, with precision/recall/cost trade-offs.

**SAST:** CodeQL alerts | **LLM:** Claude Sonnet 4, DeepSeek Chat, GPT-5; agents: Aider, OpenHands, SWE-agent | **Benchmarks:** [OWASP Benchmark](https://owasp.org/www-project-benchmark/), [Vul4J](https://github.com/tuhh-softsec/vul4j)

---

### 15) LLM vs. SAST: GPT-4 Advanced Data Analysis

- Local PDF: [2506.15212v1-LLM-vs-SAST.pdf](../checkpoint-1/2506.15212v1-LLM-vs-SAST.pdf)
- Web: [arXiv 2506.15212](https://arxiv.org/abs/2506.15212)

**Summary:** Controlled comparison of GPT-4 Advanced Data Analysis vs combined SAST baseline (SonarQube + Cloud Defence) on 32 MITRE ATT&CK–aligned vulnerability scenarios; GPT-4 reaches ~94% accuracy; McNemar’s test used for significance.

**SAST:** SonarQube + Cloud Defence | **LLM:** GPT-4 (ADA mode) | **Benchmark:** 32 custom vulnerability scenarios

---

### 16) Large Language Models Versus Static Code Analysis Tools (IEEE Access)

- Local PDF: [llm-vs-sca.pdf](../checkpoint-1/llm-vs-sca.pdf)
- Web: [DOI 10.1109/ACCESS.2025.3635168](https://doi.org/10.1109/ACCESS.2025.3635168)

**Summary:** Head-to-head benchmark of SonarQube, CodeQL, SnykCode vs GPT-4.1, Mistral Large, DeepSeek V3 on 10 C# projects (63 labeled vulns); LLMs achieve higher mean F1 (0.75–0.80) than SAST (0.26–0.55) via better recall, but with more FPs and weaker line-level localization.

**SAST:** SonarQube, CodeQL, SnykCode | **LLM:** GPT-4.1, Mistral Large, DeepSeek V3 | **Benchmark:** 10 C# projects, 63 vulnerabilities

---

### 17) Harnessing LLMs for Software Vulnerability Detection (IEEE Access)

- Local PDF: [harnessing-llm-for-vuln-detection.pdf](../checkpoint-1/harnessing-llm-for-vuln-detection.pdf)
- Web: [DOI 10.1109/ACCESS.2025.3541146](https://doi.org/10.1109/ACCESS.2025.3541146)

**Summary:** Black-box LLM vulnerability detection on pre-processed Juliet Java 1.3 (textual leakage cues removed); GPT-4 Turbo, GPT-4, Claude 3 Opus with CoT/ToT/self-consistency outperform CodeQL and SpotBugs in recall/F1 but produce more FPs.

**SAST:** CodeQL, SpotBugs | **LLM:** GPT-4 Turbo, GPT-4, Claude 3 Opus (CoT/ToT/self-consistency) | **Benchmark:** [Juliet Java 1.3](https://samate.nist.gov/SARD/test-suites/111) ([mirror](https://github.com/UnitTestBot/juliet-java-test-suite))

---

### 18) How Can ChatGPT Support Human Security Testers to Mitigate Supply Chain Attacks?

- Local PDF: [2310.00710v3-Supply-Chain-Attacks.pdf](../checkpoint-1/2310.00710v3-Supply-Chain-Attacks.pdf)
- Web: [arXiv 2310.00710](https://arxiv.org/abs/2310.00710)

**Summary:** ChatGPT generates security tests demonstrating supply-chain vulnerability propagation; 49 apps depending on 25 vulnerable libraries — tests generated for all cases, 24 demonstrated PoV, 6 reports filed and 4 CVEs assigned; library PoV tests are the critical prompt ingredient.

**SAST:** not primary | **LLM:** ChatGPT (PoV test generation) | **Benchmark:** 25 vulnerable libraries, 49 dependent apps

---

## Reference tables

### SAST taxonomy

| Type | Examples | Role | Papers |
|------|----------|------|--------|
| Pattern / rule-based | Semgrep, SonarQube, SpotBugs | Stable baseline | [5](#5-comparison-and-evaluation-on-static-application-security-testing-sast-tools-for-java), [15](#15-llm-vs-sast-gpt-4-advanced-data-analysis), [16](#16-large-language-models-versus-static-code-analysis-tools-ieee-access) |
| Semantic / taint | CodeQL, Argus | Real vulnerability analysis | [5](#5-comparison-and-evaluation-on-static-application-security-testing-sast-tools-for-java), [9](#9-argus-a-framework-for-staged-static-taint-analysis-of-github-workflows-and-actions) |
| Neuro-symbolic hybrid | IRIS+CodeQL, AdaTaint | LLM spec inference + static validation | [13](#13-iris-llm-assisted-static-analysis-for-detecting-security-vulnerabilities), [12](#12-llm-driven-adaptive-sourcesink-identification-and-false-positive-mitigation-for-static-analysis-adataint) |
| Domain-specific workflow | zizmor, poutine, actionlint, GHAST | **Pipeline configs** | [10](#10-ghast-github-actions-security-tester), [11](#11-unpacking-security-scanners-for-github-actions-workflows) |
| Linter + security hybrid | actionlint, Scorecard | Misconfigurations | [11](#11-unpacking-security-scanners-for-github-actions-workflows) |

### SAST tools per study

| Study | SAST / static tools |
|-------|---------------------|
| [IRIS](#13-iris-llm-assisted-static-analysis-for-detecting-security-vulnerabilities) | CodeQL |
| [Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering) | CodeQL |
| [LLM vs SAST](#15-llm-vs-sast-gpt-4-advanced-data-analysis) | SonarQube, Cloud Defence |
| [LLM vs SCA](#16-large-language-models-versus-static-code-analysis-tools-ieee-access) | SonarQube, CodeQL, SnykCode |
| [Harnessing LLM](#17-harnessing-llms-for-software-vulnerability-detection-ieee-access) | CodeQL, SpotBugs |
| [Argus](#9-argus-a-framework-for-staged-static-taint-analysis-of-github-workflows-and-actions) | ARGUS |
| [GHAST](#10-ghast-github-actions-security-tester) | GHAST |
| [Unpacking GHA](#11-unpacking-security-scanners-for-github-actions-workflows) | actionlint, poutine, zizmor, scorecard, semgrep, ggshield, frizbee, pinny, scharf |
| [Chen FSE](#5-comparison-and-evaluation-on-static-application-security-testing-sast-tools-for-java) | CodeQL, Semgrep, SpotBugs, SonarQube (+ broader set) |
| [CASTLE](#6-castle-benchmarking-dataset-for-static-code-analyzers-and-llms-towards-cwe-detection) | 13 static analyzers + ESBMC |
| [AdaTaint](#12-llm-driven-adaptive-sourcesink-identification-and-false-positive-mitigation-for-static-analysis-adataint) | static taint engine + symbolic validation |

### LLMs per study

| Study | LLM(s) |
|-------|--------|
| [IRIS](#13-iris-llm-assisted-static-analysis-for-detecting-security-vulnerabilities) | GPT-4 |
| [Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering) | Claude Sonnet 4, DeepSeek Chat, GPT-5 |
| [LLM vs SAST](#15-llm-vs-sast-gpt-4-advanced-data-analysis) | GPT-4 |
| [LLM vs SCA](#16-large-language-models-versus-static-code-analysis-tools-ieee-access) | GPT-4.1, Mistral Large, DeepSeek V3 |
| [Harnessing LLM](#17-harnessing-llms-for-software-vulnerability-detection-ieee-access) | GPT-4 Turbo, GPT-4, Claude 3 Opus |
| [Supply chain](#18-how-can-chatgpt-support-human-security-testers-to-mitigate-supply-chain-attacks) | ChatGPT |
| [CASTLE](#6-castle-benchmarking-dataset-for-static-code-analyzers-and-llms-towards-cwe-detection) | 10 LLMs (see repo) |
| [AdaTaint](#12-llm-driven-adaptive-sourcesink-identification-and-false-positive-mitigation-for-static-analysis-adataint) | LLM for source/sink + FP filtering |
| [Kaniewski SLR](#1-a-systematic-literature-review-on-detecting-software-vulnerabilities-with-large-language-models) | GPT, Claude, Gemini, CodeLlama, DeepSeek, … |
| [Sheng survey](#2-llms-in-software-security-a-survey-of-vulnerability-detection-techniques-and-insights) | GPT-4/3.5, CodeLlama, CodeBERT-family |

### Benchmark and dataset links

| Benchmark | Dataset link | Used in |
|-----------|--------------|---------|
| Juliet C/C++ 1.3 | [SARD #112](https://samate.nist.gov/SARD/test-suites/112) ([mirror](https://github.com/arichardson/juliet-test-suite-c)) | [CASTLE](#6-castle-benchmarking-dataset-for-static-code-analyzers-and-llms-towards-cwe-detection) |
| Juliet Java 1.3 | [SARD #111](https://samate.nist.gov/SARD/test-suites/111) ([mirror](https://github.com/UnitTestBot/juliet-java-test-suite)) | [Harnessing LLM](#17-harnessing-llms-for-software-vulnerability-detection-ieee-access), [AdaTaint](#12-llm-driven-adaptive-sourcesink-identification-and-false-positive-mitigation-for-static-analysis-adataint) |
| OWASP Benchmark | [owasp.org/www-project-benchmark](https://owasp.org/www-project-benchmark/) | [Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering) |
| CWE-Bench-Java | [GitHub](https://github.com/iris-sast/cwe-bench-java) / [HF](https://huggingface.co/datasets/iris-sast/CWE-Bench-Java) | [IRIS](#13-iris-llm-assisted-static-analysis-for-detecting-security-vulnerabilities) |
| CASTLE-C250 | [CASTLE-Benchmark](https://github.com/CASTLE-Benchmark/CASTLE-Benchmark) | [CASTLE](#6-castle-benchmarking-dataset-for-static-code-analyzers-and-llms-towards-cwe-detection) |
| RealVuln | [arXiv 2604.13764](https://arxiv.org/abs/2604.13764) | [RealVuln](#7-realvuln-benchmarking-rule-based-general-purpose-llm-and-security-specialized-scanners-on-real-world-code) |
| Vul4J | [tuhh-softsec/vul4j](https://github.com/tuhh-softsec/vul4j) | [Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering) |
| Big-Vul | [Hugging Face](https://huggingface.co/datasets/bstee615/bigvul) | [Kaniewski SLR](#1-a-systematic-literature-review-on-detecting-software-vulnerabilities-with-large-language-models) |
| DiverseVul | [wagner-group/diversevul](https://github.com/wagner-group/diversevul) | [Kaniewski SLR](#1-a-systematic-literature-review-on-detecting-software-vulnerabilities-with-large-language-models) |
| Unpacking GHA workflows | [sparkrew/github-actions-security](https://github.com/sparkrew/github-actions-security) | [Unpacking GHA](#11-unpacking-security-scanners-for-github-actions-workflows) |
| Argus workflow corpus | [Argus paper PDF](./usenixsecurity23-argus.pdf) | [Argus](#9-argus-a-framework-for-staged-static-taint-analysis-of-github-workflows-and-actions) |
| Koishybayev GHA corpus | [SEC'22 PDF](./sec22-koishybayev-github-ci.pdf) | [Koishybayev](#8-characterizing-the-security-of-github-ci-workflows) |

---

## Results

For pipeline-configuration security, the literature supports a **hybrid workflow**:

1. **Threat model and domain SAST** — [Koishybayev](#8-characterizing-the-security-of-github-ci-workflows), [Argus](#9-argus-a-framework-for-staged-static-taint-analysis-of-github-workflows-and-actions), [Unpacking GHA](#11-unpacking-security-scanners-for-github-actions-workflows): tiered scanner setup per Unpacking — **poutine + actionlint** (fundamental), **+ frizbee** (essential), **+ semgrep** (advanced); **zizmor** for broadest general-purpose coverage; Argus for taint-analysis background on workflow YAML.
2. **LLM role** — not a SAST replacement; best as **amplifier**: spec inference ([IRIS](#13-iris-llm-assisted-static-analysis-for-detecting-security-vulnerabilities), [AdaTaint](#12-llm-driven-adaptive-sourcesink-identification-and-false-positive-mitigation-for-static-analysis-adataint)), FP triage ([Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering)), contextual classification ([LLM vs SAST](#15-llm-vs-sast-gpt-4-advanced-data-analysis), [LLM vs SCA](#16-large-language-models-versus-static-code-analysis-tools-ieee-access)), prompting strategies ([Harnessing LLM](#17-harnessing-llms-for-software-vulnerability-detection-ieee-access)).
3. **Evaluation** — no standard LLM-vs-SAST benchmark for pipeline YAML with CVE labels; start from [Unpacking corpus](https://github.com/sparkrew/github-actions-security) + manual labeling (template: [CWE-Bench-Java](https://github.com/iris-sast/cwe-bench-java)); borrow metrics design from [Juliet](https://github.com/UnitTestBot/juliet-java-test-suite), [OWASP Benchmark](https://owasp.org/www-project-benchmark/), [CASTLE](#6-castle-benchmarking-dataset-for-static-code-analyzers-and-llms-towards-cwe-detection).
4. **Model families (from surveyed studies)** — frontier general-purpose models dominate benchmarks ([Kaniewski SLR](#1-a-systematic-literature-review-on-detecting-software-vulnerabilities-with-large-language-models), [Sheng survey](#2-llms-in-software-security-a-survey-of-vulnerability-detection-techniques-and-insights)): GPT-4/4.1, Claude 3 Opus/Sonnet, DeepSeek; code-specialized models (CodeLlama, DeepSeek-Coder) for fine-tuning; optional agentic triage ([Sifting the Noise](#14-sifting-the-noise-llm-agents-in-vulnerability-false-positive-filtering)).
