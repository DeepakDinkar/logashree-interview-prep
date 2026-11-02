# 11. AI-ASSISTED ENGINEERING — Roadmap

> Resume lists **GitHub Copilot, Amazon Q Developer, ChatGPT, Claude**. Companies now ask *"how do you use AI day-to-day?"* in almost every round. Have concrete, responsible examples — not buzzwords.

```
AI-ASSISTED ENGINEERING (for DevOps)
│
├── 1. THE TOOLS YOU USE
│   ├── GitHub Copilot — inline code/IaC completion, tests, boilerplate
│   ├── Amazon Q Developer — AWS-aware code, CLI help, troubleshooting
│   ├── ChatGPT / Claude — explain, refactor, draft scripts, rubber-duck
│   └── CLI assistants / chat in IDE (VS Code)
│
├── 2. WHERE AI HELPS IN DEVOPS DAILY
│   ├── Write Terraform / Dockerfiles / K8s YAML faster
│   ├── Generate + explain shell scripts & regex
│   ├── Draft GitHub Actions workflows
│   ├── Debug errors (paste stack trace / kubectl describe)
│   ├── Summarize logs & incidents
│   ├── Write unit/integration tests
│   ├── Convert between clouds / translate configs
│   └── Documentation, runbooks, commit messages, PR descriptions
│
├── 3. PROMPTING WELL
│   ├── Give context (stack, constraints, versions)
│   ├── Specify output format + examples
│   ├── Iterate / refine
│   ├── Ask for trade-offs & edge cases
│   └── Chain-of-thought for complex design
│
├── 4. RESPONSIBLE USE ⭐ (interviewers probe this)
│   ├── ALWAYS review AI output — you own it
│   ├── Never paste secrets / proprietary code into public tools
│   ├── Validate security (AI can suggest insecure IAM / public S3)
│   ├── Test before merge (AI hallucinates APIs/flags)
│   ├── Understand the code — don't ship what you can't explain
│   └── Follow company AI policy & data governance
│
├── 5. GENAI CONCEPTS (good to know)
│   ├── LLM, token, context window
│   ├── Prompt vs completion
│   ├── Hallucination
│   ├── RAG (Retrieval-Augmented Generation)
│   ├── Fine-tuning vs prompting
│   ├── Embeddings / vector search
│   └── Agents / MCP (tool-using AI)
│
└── 6. AI IN THE PIPELINE / OPS (emerging)
    ├── AIOps — anomaly detection in metrics/logs
    ├── AI code review (Copilot/CodeRabbit)
    ├── AI-assisted incident summaries
    ├── Security: AI scanning + risk of AI-generated vulns
    └── Amazon Q / Bedrock in AWS workflows
```

## 🏗️ Your real examples (rehearse these)
- *"I use **Copilot** to scaffold Terraform modules and K8s manifests, then review every line and run `plan`/`validate` before applying."*
- *"I use **Amazon Q Developer** for AWS-specific questions and to debug CLI/permission errors faster."*
- *"I paste failing `kubectl describe` / stack traces into **ChatGPT/Claude** to speed up root-cause, then verify against docs."*
- *"AI drafts my runbooks, PR descriptions and commit messages — I edit for accuracy."*
- *"I never put secrets or proprietary config into external tools, and I always validate security suggestions."*

## 🎯 Interview focus
- "How do you use AI in your daily work?" → give 2–3 concrete DevOps examples + the review/validation habit.
- "What are the risks of AI-generated code?" → hallucinated APIs, insecure defaults, licensing, data leakage.
- "How do you make sure AI output is safe to ship?" → review, test, scan, understand it.
- Basic GenAI literacy: LLM, hallucination, RAG, context window.

→ Definitions: [`../Definitions/11-AI-definitions.md`](../Definitions/11-AI-definitions.md)
