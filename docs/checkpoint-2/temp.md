# Checkpoint 2 — Literature Background (draft)

Topic: applying LLMs to security testing with comparative evaluation against SAST, focused on **vulnerability detection in CI/CD pipeline configurations** (primarily GitHub Actions YAML).

---

## 1. Which SAST methods to use

### 1.1 SAST taxonomy (conceptual)

| Type | Idea | Examples | Role in diploma |
|------|------|----------|-----------------|
| **Pattern / rule-based** | Template rules on YAML or code | Semgrep, SonarQube, SpotBugs | Stable, reproducible baseline |
| **Semantic / taint analysis** | Track untrusted data from sources to sinks | CodeQL, Argus, IRIS+CodeQL | Closer to real vulnerability analysis |
| **Domain-specific workflow scanners** | Built for `.github/workflows/` | zizmor, poutine, actionlint, GHAST | **Direct fit for pipeline configs** |
| **Linter + security hybrid** | Syntax checks plus partial security | actionlint, OpenSSF Scorecard | Misconfigurations, not only CVE classes |

### 1.2 General SAST background (source code, transferable methodology)

| Paper | Link | Use for background |
|-------|------|--------------------|
| Chen et al., FSE 2023 — *Comparison and Evaluation on SAST Tools for Java* | [PDF](https://sen-chen.github.io/pdf/C38-FSE2023-Comparison%20and%20Evaluation%20on%20Static%20Application%20Security%20Test%20(SAST)%20Tools%20for%20Java.pdf) | CWE mapping, taint vs rules, CodeQL / Semgrep / SpotBugs, evaluation pitfalls |
| CASTLE, TASE 2025 | [arXiv 2503.09433](https://arxiv.org/abs/2503.09433) | 13 SAST + 10 LLM on 250 C micro-benchmarks; Juliet/SARD limitations; CASTLE Score |
| RealVuln, 2026 | [arXiv 2604.13764](https://arxiv.org/abs/2604.13764) | Benchmark landscape table (OWASP, Juliet, CASTLE, CWE-Bench, etc.) |

### 1.3 SAST for pipeline / GitHub Actions (primary domain)

Literature defines **10 common weakness classes** for GitHub Actions workflows (injection, excessive permissions, unpinned actions, secrets exposure, etc.).

| Tool | Strategy | Role in hybrid pipeline |
|------|----------|-------------------------|
| **poutine** | Conservative, few high-severity findings | Strict SAST baseline |
| **zizmor** | Broad coverage, more noise | Maximum SAST recall |
| **actionlint** | Syntax and runner compatibility | Structural workflow errors |
| **Semgrep** | YAML rules, easy to extend | Custom rule baseline |
| **CodeQL (`language: actions`)** | GitHub semantic rules | Industry standard (CLI/extractor limitations in local experiments) |
| **Argus** (USENIX SEC'23) | Staged static taint on workflows + actions | Best academic reference for taint on GHA |
| **GHAST** | Checklist of misconfigurations in YAML | Early GHA security methodology |

**Recommended SAST stack for experiments:**

- **Pipeline baseline:** `poutine + zizmor` (as in Unpacking paper) ± Semgrep for custom rules.
- **Background reference architecture:** Argus (WIR + taint summaries for third-party actions).
- **Cross-paper comparison baseline:** CodeQL + Semgrep + SonarQube (as in checkpoint-1 papers 3, 5, 6).

---

## 2. Which LLM types and subtypes to use

### 2.1 Model families

| Category | Models | When to use |
|----------|--------|-------------|
| **General-purpose frontier** | GPT-4 / GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 | Zero-shot, CoT, triage, agents — **main choice without fine-tuning** |
| **Code-specialized** | CodeLlama, DeepSeek-Coder, CodeQwen, StarCoder | Compare code-tuned vs general models |
| **Encoder / hybrid DL** | CodeBERT + CNN/GNN | Pre-LLM era background; secondary for this topic |
| **Security fine-tuned** | Rare, mostly Solidity/smart contracts | Not standard for pipeline YAML |

**Practical minimum for diploma (2–3 models):**

1. GPT-4o or Claude 3.5 — primary (IRIS, FP-filtering, comparative benchmarks).
2. One open-weight code model (DeepSeek-Coder / CodeLlama) — cost and reproducibility.
3. Optional: agentic framework (OpenHands / SWE-agent) if LLM = post-SAST triage layer.

### 2.2 Usage modes (more important than model choice)

| Mode | Description | Key papers |
|------|-------------|------------|
| **Zero- / few-shot classification** | “Is this YAML vulnerable?” | [LLM vs SAST 2506.15212](https://arxiv.org/abs/2506.15212); IEEE ACCESS 3635168 |
| **Prompt engineering** | CoT, ToT, self-consistency | [Harnessing LLM, IEEE 3541146](https://doi.org/10.1109/ACCESS.2025.3541146) |
| **Neuro-symbolic hybrid** | LLM infers specs / filters + SAST engine | [IRIS 2405.17238](https://arxiv.org/abs/2405.17238); AdaTaint; CPGHunter |
| **Agentic triage** | Multi-step analysis with tools | [Sifting the Noise 2601.22952](https://arxiv.org/abs/2601.22952) |
| **PoV / test generation** | Demonstrate exploitability, not just labels | [Supply chain 2310.00710](https://arxiv.org/abs/2310.00710) |

For pipeline security, **hybrid** and **triage** are better justified than “LLM replaces SAST”.

---

## 3. Datasets

### 3.1 CI/CD and GitHub Actions (best fit)

| Dataset | Scale | Ground truth | Source |
|---------|-------|--------------|--------|
| **Unpacking workflow corpus** | 2,722 workflows, 388 repos | Scanner alerts mapped to 10 weakness classes | [arXiv 2601.14455](https://arxiv.org/abs/2601.14455); [github.com/sparkrew/github-actions-security](https://github.com/sparkrew/github-actions-security) |
| **Argus evaluation** | ~2.7M workflows; 5,298 confirmed injections (manual subset) | Manual validation | [USENIX SEC'23 Argus](https://www.usenix.org/system/files/usenixsecurity23-muralee.pdf) |
| **Koishybayev SEC'22** | 447,238 workflows, 213,854 repos | Empirical statistics, not full per-alert labels | [Characterizing Security of GitHub CI](https://www.usenix.org/system/files/sec22-koishybayev.pdf) |
| **GHAST campaign** | 50 projects, 131 workflows | Rule-based checks SC-1..SC-N | [arXiv 2208.03837](https://arxiv.org/abs/2208.03837) |

**Gap:** there is no standard benchmark “LLM vs SAST on pipeline YAML with CVE-level labels”. Likely approach:

- Start from open corpus (Unpacking / Argus subset),
- Manually label a subset (template: IRIS → CWE-Bench-Java),
- Or synthesize vulnerable / fixed YAML pairs.

### 3.2 Transferable benchmarks (methodology, not domain)

| Dataset | Type | Pros | Cons for pipeline |
|---------|------|------|---------------------|
| **Juliet Java/C++ 1.3** | Synthetic | Clean labels, CoT experiments | Not YAML; possible LLM training leakage |
| **OWASP Benchmark** | Synthetic Java | FP triage, statistical tests | Not CI/CD |
| **CWE-Bench-Java** | 120 real CVEs | Whole-repo, IRIS baseline | Java code, not workflows |
| **CASTLE-C250** | 250 C programs, 25 CWEs | SAST + LLM side-by-side | Micro-benchmark |
| **RealVuln** | 26 real vulnerable repos | Real-world scanners | Not pipeline-specific |
| **Vul4J** | Reproducible Java CVEs | FP filtering paper (CodeQL alerts) | Java, not YAML |
| **Big-Vul / DiverseVul** | Large function-level | ML scale | Noisy labels |

**Strategy:**

- **Background + metrics design:** Juliet, OWASP, CASTLE (from surveys).
- **Main experiment:** curated **pipeline YAML dataset** (Unpacking corpus + manual labels).
- **Benchmark construction reference:** CWE-Bench-Java + IRIS paper.

---

## 4. Role of LLM

Consensus from checkpoint-1 papers and recent SLRs:

```
SAST (deterministic)              LLM (contextual)
─────────────────────             ─────────────────────────────
Rules / taint engine        ←──→  Infer sources/sinks/specs
Reproducible alerts         ←──→  Filter false positives
CWE mapping                 ←──→  Explain why alert matters
Misses cross-step context   ←──→  Reason over full workflow YAML
High FP on edge cases       ←──→  Triage in CI/CD pipeline
```

### Five documented LLM roles

1. **Specification inference** — infer taint sources/sinks for unknown actions (IRIS, SemTaint, AdaTaint).
2. **Alert triage / FP filtering** — post-processing after SAST (Sifting the Noise, IRIS FilterPath).
3. **Contextual classification** — direct vulnerable / not on config snippets (comparative benchmarks).
4. **Reasoning strategies** — CoT / ToT / self-consistency for ambiguous cases (Harnessing LLM).
5. **Actionable output** — PoV tests, patch hints, severity (supply chain paper).

**Not a primary role:** replacing the taint engine or acting as the sole merge gate without SAST (hallucination risk, non-determinism).

**Working thesis conclusion:** LLMs are most effective as an **intelligent amplifier** of security testing: SAST gives stable baseline coverage; LLMs add contextual reasoning, noise reduction, and triage support.

---

## 5. Background papers (priority for Related Work)

### Tier 1 — Surveys and taxonomies (foundation)

| # | Paper | Link | Background contribution |
|---|-------|------|-------------------------|
| 1 | Kaniewski et al., SLR (ACM TOSEM) | [arXiv 2507.22659](https://arxiv.org/abs/2507.22659) / [DOI 10.1145/3815425](https://doi.org/10.1145/3815425) | Task formulation, architectures, adaptation, **dataset table**; [Awesome-LLM4SVD](https://github.com/hs-esslingen-it-security/Awesome-LLM4SVD) |
| 2 | Sheng et al., 2025 | [arXiv 2502.07049](https://arxiv.org/abs/2502.07049) | LLM families, benchmarks, prompts, gaps (repo-level, leakage) |
| 3 | MDPI Electronics 2025 | [DOI 10.3390/electronics14224449](https://doi.org/10.3390/electronics14224449) | Static → ML → LLM evolution; neuro-symbolic direction |
| 4 | Fu et al., 2024 | [arXiv 2404.02525](https://arxiv.org/abs/2404.02525) | LLM adaptation for detection and repair; limitations |

### Tier 2 — SAST background

| # | Paper | Link | Background contribution |
|---|-------|------|-------------------------|
| 5 | Chen, FSE 2023 | [PDF](https://sen-chen.github.io/pdf/C38-FSE2023-Comparison%20and%20Evaluation%20on%20Static%20Application%20Security%20Test%20(SAST)%20Tools%20for%20Java.pdf) | SAST types, taint vs rules, tool evaluation |
| 6 | CASTLE | [arXiv 2503.09433](https://arxiv.org/abs/2503.09433) | SAST vs LLM benchmark design |
| 7 | RealVuln | [arXiv 2604.13764](https://arxiv.org/abs/2604.13764) | Benchmark comparison landscape |

### Tier 3 — CI/CD and pipeline security (domain)

| # | Paper | Link | Background contribution |
|---|-------|------|-------------------------|
| 8 | Koishybayev, USENIX SEC'22 | [PDF](https://www.usenix.org/system/files/sec22-koishybayev.pdf) | CI/CD threat model: overprivileged workflows, untrusted actions |
| 9 | Muralee, USENIX SEC'23 — Argus | [PDF](https://www.usenix.org/system/files/usenixsecurity23-muralee.pdf) | Taint analysis on workflows, WIR, large-scale study |
| 10 | GHAST | [arXiv 2208.03837](https://arxiv.org/abs/2208.03837) | GHA security check methodology |
| 11 | Unpacking GHA Scanners | [arXiv 2601.14455](https://arxiv.org/abs/2601.14455) | Systematic comparison of zizmor / poutine / actionlint / Semgrep; 2,722 workflows |

### Tier 4 — LLM + SAST methods (checkpoint-1 + extensions)

| # | Paper | Link | Use |
|---|-------|------|-----|
| 12 | IRIS | [arXiv 2405.17238](https://arxiv.org/abs/2405.17238) | Neuro-symbolic architecture; CWE-Bench-Java |
| 13 | Sifting the Noise | [arXiv 2601.22952](https://arxiv.org/abs/2601.22952) | Agentic FP filtering (OWASP + Vul4J) |
| 14 | AdaTaint | [arXiv 2511.04023](https://arxiv.org/abs/2511.04023) | LLM source/sink + symbolic validation |
| 15 | CPGHunter | [DOI 10.1007/s10664-026-10842-2](https://doi.org/10.1007/s10664-026-10842-2) | LLM + taint; Juliet + CWE-Bench-Java |
| 16 | LLM vs SAST (GPT-4) | [arXiv 2506.15212](https://arxiv.org/abs/2506.15212) | Evaluation template: scenarios, McNemar |
| 17 | LLM vs SCA (IEEE) | [DOI 10.1109/ACCESS.2025.3635168](https://doi.org/10.1109/ACCESS.2025.3635168) | Multi-tool / multi-model real-project benchmark |
| 18 | Harnessing LLM (IEEE) | [DOI 10.1109/ACCESS.2025.3541146](https://doi.org/10.1109/ACCESS.2025.3541146) | CoT / ToT / self-consistency protocol |
| 19 | Supply chain / ChatGPT | [arXiv 2310.00710](https://arxiv.org/abs/2310.00710) | PoV test generation for CI/CD context |

---

## 6. Suggested Related Work structure

```mermaid
flowchart TB
    subgraph bg1 [Block 1: Threats]
        A[Koishybayev SEC22 CI/CD threats]
        B[Unpacking 10 weakness classes]
    end
    subgraph bg2 [Block 2: SAST]
        C[Chen FSE23 SAST taxonomy]
        D[Argus taint on workflows]
        E[zizmor / poutine / Semgrep]
    end
    subgraph bg3 [Block 3: LLM in security]
        F[Kaniewski SLR taxonomy]
        G[Sheng survey models and datasets]
    end
    subgraph bg4 [Block 4: Hybrid LLM plus SAST]
        H[IRIS neuro-symbolic]
        I[FP filtering agents]
        J[Comparative benchmarks from checkpoint-1]
    end
    bg1 --> bg2 --> bg3 --> bg4
```

---

## 7. Summary — what to adopt in the diploma

| Component | Recommendation |
|-----------|----------------|
| **SAST** | poutine + zizmor (+ Semgrep); Argus for background; CodeQL actions if available |
| **LLM** | GPT-4o / Claude 3.5 (primary) + one code-LLM; modes: CoT + agentic triage |
| **LLM role** | Amplifier after SAST: triage, contextual reasoning, spec hints — not replacement |
| **Dataset** | Unpacking corpus + manual labeled subset; metrics from Juliet / OWASP / CWE-Bench |
| **Background cites** | Kaniewski SLR + Sheng + Koishybayev + Argus + Unpacking + Chen FSE SAST |
