# LLM vs. SAST: A Technical Analysis on Detecting Coding Bugs of GPT-4 Advanced Data Analysis

- **arXiv:** [2506.15212v1](https://arxiv.org/abs/2506.15212) 
- **PDF:** [2506.15212v1-LLM-vs-SAST.pdf](./2506.15212v1-LLM-vs-SAST.pdf)

## Summary

The authors conduct a controlled empirical comparison between GPT-4 Advanced Data Analysis (formerly Code Interpreter) and
traditional SAST, combining SonarQube and Cloud Defence into a single SAST baseline. Using 32 representative coding security
mistakes drawn from MITRE ATT&CK–aligned vulnerability classes and code samples from GitHub and Snyk, they measure binary
detection outcomes and apply statistical tests (chi-squared and McNemar’s) to assess whether GPT-4 outperforms SAST. Results
indicate that GPT-4 achieves roughly 94% accuracy on these exploitable vulnerability types and detects issues that SAST
misses, while the study also discusses limitations of LLMs (e.g., lack of DAST/runtime analysis, hallucination risk) and
stresses security-by-design concerns for AI-assisted vulnerability scanning in production workflows.
