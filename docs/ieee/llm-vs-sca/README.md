# Large Language Models Versus Static Code Analysis Tools: A Systematic Benchmark for Vulnerability Detection

- **DOI:** [10.1109/ACCESS.2025.3635168](https://doi.org/10.1109/ACCESS.2025.3635168) 
- **PDF:** [llm-vs-sca.pdf](./llm-vs-sca.pdf)
- **Dataset:** [ProjectAnalyzer on GitHub](https://github.com/Damian0401/MasterThesis)

## Related papers

This paper is **cited by**:

- [Sifting the Noise: LLM Agents in FP Filtering](../../arxiv/llm-false-positive/README.md) — benchmarks LLM agents for SAST false-positive filtering; cites this IEEE Access study as a head-to-head LLM vs static analysis benchmark

## Summary

This study provides a head-to-head benchmark of three rule-based SAST analyzers (SonarQube, CodeQL, SnykCode) and three LLMs
on GitHub Models (GPT-4.1, Mistral Large, DeepSeek V3) over ten real-world C# projects containing 63 labeled vulnerabilities
spanning SQL injection, hard-coded secrets, outdated dependencies, and related categories. The LLMs achieve higher mean F1
scores (0.797, 0.753, and 0.750) than the static tools (0.260, 0.386, and 0.546), driven mainly by superior recall and
broader contextual reasoning, but at the cost of more false positives, imprecise line-level localization due to tokenization,
and unreliable CWE mapping. The authors conclude that LLMs are competitive for finding real flaws yet too noisy for
standalone use in safety-critical audits, and recommend a hybrid workflow: LLMs for early, context-aware triage during
development and deterministic SAST for high-assurance verification, supported by an open JSON-based evaluation harness
released with the paper.
