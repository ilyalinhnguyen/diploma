# How Can ChatGPT Support Human Security Testers to Help Mitigate Supply Chain Attacks?

- **arXiv:** [2310.00710v3](https://arxiv.org/abs/2310.00710) 
- **PDF:** [2310.00710v3-Supply-Chain-Attacks.pdf](./2310.00710v3-Supply-Chain-Attacks.pdf)

## Summary

This work explores whether LLMs can help developers understand and mitigate software supply chain attacks by automatically
generating security tests that demonstrate how vulnerabilities in third-party libraries propagate into client applications.
The authors design prompt templates that feed ChatGPT vulnerability metadata, application call context, and
proof-of-vulnerability (PoV) tests from affected libraries, then ask the model to produce analogous tests for 49 applications
depending on 25 vulnerable libraries. ChatGPT generated tests for all cases, with 24 successfully demonstrating PoV; six new
vulnerability reports were filed and four CVEs assigned. The study compares ChatGPT with prior tools
([TRANSFER](https://github.com/soarsmu/transfer) and [SIEGE](https://github.com/emaiannone/siege)) and several other LLMs,
finding that LLM-generated tests outperform existing automated generators and that library PoV tests are the most critical
prompt ingredient—without them, no generated test successfully demonstrated exploitation in the application context.
