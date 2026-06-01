# IRIS: LLM-Assisted Static Analysis for Detecting Security Vulnerabilities

- **arXiv:** [2405.17238v3](https://arxiv.org/abs/2405.17238v3) 
- **Venue:** ICLR 2025 
- **PDF:** [2405.17238v3-IRIS.pdf](./2405.17238v3-IRIS.pdf)

## Related papers

This paper is **cited by**:

- [Sifting the Noise: LLM Agents in FP Filtering](../llm-false-positive/README.md) — compares agent frameworks for triaging SAST false positives; references IRIS as prior work on LLM-assisted static analysis

## Summary

IRIS is a neuro-symbolic system that combines large language models with static taint analysis to detect security
vulnerabilities across entire repositories. The approach uses LLMs to infer CWE-specific taint specifications for third-party
libraries (reducing reliance on manual human-written rules) and to perform contextual analysis that filters false positives
from static analyzer alerts. The authors introduce CWE-Bench-Java, a benchmark of 120 manually validated vulnerabilities in
real-world Java projects averaging over 300K lines of code. On this benchmark, CodeQL detects 27 vulnerabilities while IRIS
with GPT-4 detects 55 (+28) and lowers the average false discovery rate by about 5 percentage points compared to CodeQL
alone; the system also uncovered four previously unknown vulnerabilities in recent project versions.
