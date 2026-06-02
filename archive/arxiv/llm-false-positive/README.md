# Sifting the Noise: A Comparative Study of LLM Agents in Vulnerability False Positive Filtering

- **arXiv:** [2601.22952v1](https://arxiv.org/abs/2601.22952)
- **PDF:** [2601.22952v1-LLM-False-Positive.pdf](./2601.22952v1-LLM-False-Positive.pdf)

## Related papers

This paper **cites** the following works from the local collection (see bibliography [15] and [29]):

- [IRIS: LLM-Assisted Static Analysis](../iris/README.md) — neuro-symbolic LLM + static analysis for vulnerability detection and FP reduction
- [LLM vs. Static Code Analysis (IEEE Access)](../../ieee/llm-vs-sca/README.md) — systematic benchmark of LLMs vs SonarQube, CodeQL, and SnykCode

## Summary

This paper compares three LLM-based agent frameworks—Aider, OpenHands, and SWE-agent—for filtering false positives from SAST
tools, using backbone models including Claude Sonnet 4, DeepSeek Chat, and GPT-5. Evaluated on the OWASP Benchmark and
real-world Java projects (Vul4J with CodeQL alerts), agentic approaches can dramatically reduce SAST noise: initial
false-positive rates above 92% on OWASP drop to as low as 6.3% in the best configuration, and up to 93.3% of false positives
are identified on a real-world sample. However, gains depend heavily on the agent framework, backbone model, and CWE
category—stronger models benefit from agentic reasoning while weaker ones may not—and aggressive filtering can suppress true
vulnerabilities at significant computational cost, so practical deployment requires careful trade-offs between precision,
recall, and operational overhead.
