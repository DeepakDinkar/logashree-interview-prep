# 📖 AI-Assisted Engineering — Definitions & Examples

> Roadmap: [`../Roadmap/11-AI-Assisted-Engineering.md`](../Roadmap/11-AI-Assisted-Engineering.md) · Resume tools: Copilot, Amazon Q, ChatGPT, Claude.

### 📚 Reference docs
- [GitHub Copilot docs](https://docs.github.com/en/copilot) · [Amazon Q Developer](https://aws.amazon.com/q/developer/) · [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/)
- [OpenAI docs](https://platform.openai.com/docs) · [Anthropic Claude docs](https://docs.anthropic.com/) · [Prompt engineering guide](https://www.promptingguide.ai/)
- [Google — Prompting best practices](https://ai.google.dev/gemini-api/docs/prompting-intro) · [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)
- [OWASP Top 10 for LLM Apps](https://owasp.org/www-project-top-10-for-large-language-model-applications/) · [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

---

## Tools (know what each is for) 🔥
- **GitHub Copilot** — AI pair-programmer in your IDE; inline code/IaC completion, chat, test generation. Best for boilerplate, Terraform/YAML, unit tests.
- **Amazon Q Developer** — AWS-aware assistant; answers AWS questions, generates AWS code, explains errors, suggests fixes in CLI/IDE. Best for cloud-specific work.
- **ChatGPT / Claude** — general LLM assistants; explain code, refactor, draft scripts/runbooks, debug from logs/stack traces, rubber-duck design.
- **Amazon Bedrock** — AWS service to build GenAI apps on foundation models (if asked about building, not just using).

## Core GenAI concepts 🔥
- **LLM (Large Language Model)** — model trained on huge text that predicts the next **token** to generate human-like responses.
- **Token** — a chunk of text (~¾ of a word) the model reads/writes; billing + limits are per token.
- **Context window** — max tokens the model can consider at once (prompt + response). Big code = may exceed it.
- **Prompt vs completion** — your input vs the model's output.
- **Hallucination** 🔥 — the model confidently invents something false (a non-existent CLI flag, API, or AWS service). Why you must verify.
- **RAG (Retrieval-Augmented Generation)** — fetch relevant docs/data and feed them into the prompt so answers are grounded in your real content (reduces hallucination).
- **Embeddings / vector search** — turn text into numeric vectors to find semantically similar content (powers RAG).
- **Fine-tuning vs prompting** — retrain a model on your data vs just crafting good prompts/RAG (prompting is cheaper, usually enough).
- **Agent** — an LLM that can use tools/APIs to take actions in steps. **MCP** — a standard protocol for connecting AI to tools/data.
- **Temperature** — randomness knob (low = deterministic, high = creative).

## Prompting well 🔥
1. **Context** — stack, versions, constraints ("Terraform 1.8, AWS provider 5, must be least-privilege").
2. **Specific task** — "write", "refactor", "explain", "find the bug".
3. **Format** — "output only the HCL", "as a table", give an example.
4. **Iterate** — refine with feedback; ask for edge cases and trade-offs.

## Responsible use ⭐ (interviewers test this)
- **You own the output** — always review and understand it before shipping.
- **No secrets / proprietary code** in public AI tools — data leakage risk.
- **Validate security** — AI may suggest `0.0.0.0/0`, public S3, or `s3:*`; never accept blindly.
- **Test everything** — AI hallucinates APIs/flags; run `plan`, tests, scans.
- **Licensing** — be aware generated code may resemble training data.
- **Follow company AI policy** and data-governance rules.

## Risks of AI-generated code 🔥 (common question)
Hallucinated APIs/flags · insecure defaults (open security groups, public buckets) · outdated patterns · subtle logic bugs · license/IP concerns · over-reliance eroding fundamentals · leaking sensitive data into prompts.

---

## 🎯 Likely interview Qs (answers above)
- How do you use AI in your daily DevOps work? (give 2–3 concrete examples + review habit)
- What are the risks of AI-generated code and how do you mitigate them?
- How do you ensure AI output is secure and correct before shipping?
- What is a hallucination? What is RAG? Why does it help?
- Have you used Copilot / Amazon Q? What for?
- What's your company's policy on pasting code into AI tools?
