# Harnessing Large Language Models for Software Vulnerability Detection: A Comprehensive Benchmarking Study

- **DOI:** [10.1109/ACCESS.2025.3541146](https://doi.org/10.1109/ACCESS.2025.3541146) 
- **PDF:** [harnessing-llm-for-vuln-detection.pdf](./harnessing-llm-for-vuln-detection.pdf)

## Summary

This paper benchmarks off-the-shelf large language models as black-box static analyzers for Java vulnerability detection,
comparing multiple prompting strategies—including chain-of-thought, tree-of-thoughts, and self-consistency—against
traditional tools CodeQL and SpotBugs on a rigorously pre-processed Juliet Java 1.3 dataset where textual cues about
vulnerability presence were removed. Experiments span GPT-4 Turbo, GPT-4, and Claude 3 Opus, using a multi-class
classification task that asks models to identify vulnerability types rather than simple binary presence checks. LLMs
outperform static analyzers in recall and F1, detecting more issues overall, but produce substantially more false positives;
the authors introduce a detailed security-review prompt that beats prior strategies in most settings, analyze cost and
practical trade-offs, and offer guidance for developers and security analysts on when and how to integrate LLM-based
detection alongside conventional SAST in the development pipeline.
