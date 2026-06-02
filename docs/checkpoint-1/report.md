# Checkpoint 1

### 1) IRIS: LLM-Assisted Static Analysis for Detecting Security Vulnerabilities

- Local PDF: [2405.17238v3-IRIS.pdf](./2405.17238v3-IRIS.pdf)
- Web: [arXiv 2405.17238](https://arxiv.org/abs/2405.17238)

**Summary:** IRIS proposes a neuro-symbolic design where LLMs augment static analysis rather than replace it: the model
infers taint specifications and performs contextual filtering to reduce SAST noise and missed detections. The method is
validated on `CWE-Bench-Java` (120 manually validated vulnerabilities) against CodeQL, where IRIS+GPT-4 reports substantially
better detection (55 vs 27), lower false discovery rate, and additional previously unknown findings. For my diploma topic,
this could be a good reference architecture for a hybrid LLM+SAST pipeline, including pipeline-configuration security checks.

### 2) Sifting the Noise: A Comparative Study of LLM Agents in Vulnerability False Positive Filtering

- Local PDF: [2601.22952v1-LLM-False-Positive.pdf](./2601.22952v1-LLM-False-Positive.pdf)
- Web: [arXiv 2601.22952](https://arxiv.org/abs/2601.22952)

**Summary:** This paper focuses on the operational SAST bottleneck—false-positive triage—and compares agentic frameworks
(Aider, OpenHands, SWE-agent) instead of one-shot prompting. Validation is done on OWASP Benchmark and real Java projects
(Vul4J + CodeQL alerts), showing very large FP reduction in the best setups, while also documenting the precision/recall/cost
trade-off and risk of suppressing true vulnerabilities. For my diploma topic, it directly supports adding an LLM-based
post-processing layer in CI/CD after SAST scanning.

### 3) LLM vs. SAST: A Technical Analysis on Detecting Coding Bugs of GPT-4 Advanced Data Analysis

- Local PDF: [2506.15212v1-LLM-vs-SAST.pdf](./2506.15212v1-LLM-vs-SAST.pdf)
- Web: [arXiv 2506.15212](https://arxiv.org/abs/2506.15212)

**Summary:** This is a direct GPT-4 vs SAST benchmark that evaluates 32 vulnerability scenarios and emphasizes statistical
rigor. The methodology uses a combined SAST baseline (SonarQube + Cloud Defence), binary per-case outcomes, and chi-squared
McNemar tests; reported results indicate strong GPT-4 performance and missed detections by SAST in selected classes. For my
diploma topic, it provides a reusable evaluation template for pipeline-configuration security: 
- build a fixed scenario set with ground-truth labels,
- run LLM and SAST on the same inputs with the same success criteria,
- record binary detection matrices and core metrics,
- apply significance testing (e.g., McNemar) to compare methods,
- separately document practical risks such as hallucinations, FP burden, and non-runtime limitations.

### 4) How Can ChatGPT Support Human Security Testers to Help Mitigate Supply Chain Attacks?

- Local PDF: [2310.00710v3-Supply-Chain-Attacks.pdf](./2310.00710v3-Supply-Chain-Attacks.pdf)
- Web: [arXiv 2310.00710](https://arxiv.org/abs/2310.00710)

**Summary:** The main contribution is moving beyond classification to automatic generation of PoV security tests that
demonstrate exploitability in application context. Here, PoV (Proof of Vulnerability) means an executable test that reliably
reproduces vulnerable behavior in the target app (e.g., crash, unsafe path, unexpected execution), making the security risk
concrete rather than hypothetical. The study validates this on 25 vulnerable libraries and 49 dependent apps, compares
against [TRANSFER](https://github.com/soarsmu/transfer) and [SIEGE](https://github.com/emaiannone/siege), and reports
practical external impact (security reports and assigned CVEs). For my diploma topc, this is highly relevant to CI/CD and
dependency risk: LLMs can be used not only to label issues, but to generate actionable security tests for pipeline workflows.

### 5) Large Language Models Versus Static Code Analysis Tools: A Systematic Benchmark for Vulnerability Detection

- Local PDF: [llm-vs-sca.pdf](./llm-vs-sca.pdf)
- Web: [DOI 10.1109/ACCESS.2025.3635168](https://doi.org/10.1109/ACCESS.2025.3635168)

**Summary:** This study provides a systematic real-project benchmark (10 C# projects, 63 vulnerabilities) comparing
rule-based SAST tools with modern LLMs. Its method combines quality metrics (precision/recall/F1) and operational metrics,
and the findings reinforce a common pattern: LLMs often improve recall/F1 but introduce more noise and weaker localization.
For my diploma topic, it is one of the strongest comparative sources because it uses a broad multi-tool/multi-model setup (3
SAST + 3 LLMs), evaluates on labeled real projects, reports both effectiveness and developer-facing cost, and provides a
practical hybrid recommendation that is directly transferable to pipeline-configuration scanning.

### 6) Harnessing Large Language Models for Software Vulnerability Detection: A Comprehensive Benchmarking Study

- Local PDF: [harnessing-llm-for-vuln-detection.pdf](./harnessing-llm-for-vuln-detection.pdf)
- Web: [DOI 10.1109/ACCESS.2025.3541146](https://doi.org/10.1109/ACCESS.2025.3541146)

**Summary:** This paper’s key focus is prompt engineering for vulnerability detection, showing that inference strategy (CoT,
ToT, self-consistency) can materially change results. **CoT (Chain-of-Thought)** prompts the model to reason step by step in
one chain (e.g., identify sources/sinks, check sanitization, then decide). **ToT (Tree-of-Thoughts)** generates and scores
several reasoning branches and keeps the best path, which helps on ambiguous code. **Self-consistency** repeats the prompt
multiple times and aggregates answers (e.g., majority vote) for a more stable label. The method uses Juliet Java 1.3 with
preprocessing to remove leakage clues and compares LLMs against CodeQL/SpotBugs, reporting improved recall/F1 but higher
false-positive rates and non-trivial cost trade-offs. For my diploma topic, it is crucial for designing robust prompting and
evaluation protocols in pipeline-configuration analysis.

## Results 
Based on these 6 papers, the strongest conclusion is that **LLMs are most effective as an intelligent amplifier of the
security testing process**, rather than a full replacement for traditional SAST. For vulnerability detection in pipeline
configurations, the most robust approach is a hybrid workflow: SAST provides stable and reproducible baseline coverage, while
LLMs add contextual reasoning, noise reduction, and decision support through triage and PoV-oriented checks.
