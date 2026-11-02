# 🤖 AI in Daily Work — Real Interview Questions

> Asked in almost every 2025–2026 interview, from service companies to big tech. They want: concrete examples + responsible-use judgment, not hype. Definitions: [`../../Definitions/11-AI-definitions.md`](../../Definitions/11-AI-definitions.md)
> 🟢 basic · 🟡 mid · 🔴 advanced · 🔥 very common · Tags = company that asked.

---

## How you use AI daily 🔥🔥
1. 🟢🔥 `[GEN]` How do you use AI tools in your day-to-day work?

    Ans: I use AI tools to automate repetitive tasks, generate code snippets, assist with debugging, and improve documentation. For example, I might use Copilot to quickly scaffold a new function or use ChatGPT to summarize complex logs.

2. 🟢🔥 `[TCS][INFY]` Which AI tools have you used? (Copilot, Amazon Q, ChatGPT, Claude)

    Ans: I have experience with GitHub Copilot for code generation, Amazon Q Developer for AWS-specific queries, ChatGPT for general problem-solving and explanations, and Claude for advanced reasoning tasks.

3. 🟡🔥 `[WMT][CTS]` Give a specific example where AI saved you time this week.

    Ans: This week, I used ChatGPT to quickly generate a script for parsing and analyzing log files, which would have taken me several hours to write manually. The AI-generated script was accurate and required minimal adjustments, saving significant time.
    
4. 🟡 `[ACN]` How has AI changed your workflow as a DevOps engineer?

    Ans: AI has streamlined my workflow by automating routine tasks, such as generating boilerplate code and configuration files. It allows me to focus more on complex problem-solving and strategic planning, improving overall efficiency.

5. 🟡🔥 `[PP]` What do you use Copilot for specifically? (IaC, tests, boilerplate)

    Ans: I primarily use Copilot for generating Infrastructure as Code (IaC) templates, writing unit and integration tests, and creating boilerplate code for new services. It helps me maintain consistency and speed up development.

6. 🟡 `[AMZN]` How do you use Amazon Q Developer in AWS work?

    Ans: I use Amazon Q Developer to quickly find solutions to AWS-specific issues, such as IAM policy configurations, service limits, and best practices. It helps me troubleshoot problems more efficiently and ensures that I follow AWS guidelines.

7. 🟡 `[CMCST]` Do you use AI to debug? Walk me through an example.

    Ans: Yes, I use AI to assist with debugging. For instance, when I encountered a complex error in a Kubernetes deployment, I used ChatGPT to analyze the error message and suggest potential causes. It provided insights into misconfigurations and helped me identify the root cause faster than traditional methods.

8. 🟢 `[CAPG]` How do you use AI for documentation / runbooks?

    Ans: I use AI to generate initial drafts of documentation and runbooks. For example, I can input a description of a process or system, and the AI will produce a structured document that I can then refine. This speeds up the documentation process and ensures clarity.

9. 🟡 `[HEXA]` Has AI made you more productive? How do you measure it?

    Ans: Yes, AI has significantly increased my productivity by reducing the time spent on repetitive tasks and allowing me to focus on higher-level problem-solving. I measure productivity improvements by tracking the time saved on specific tasks and the number of successful deployments or bug fixes completed in a given timeframe.

10. 🟡 `[DLT]` Where does AI NOT help you / where do you avoid it?

    Ans: AI does not help in areas that require deep domain expertise or critical decision-making, such as architectural design or security assessments. I avoid using AI for tasks that involve sensitive data or proprietary code, as it may pose risks to confidentiality and compliance.

## Responsible & safe use ⭐🔥 (they probe hard here)
11. 🟡🔥 `[WMT][PP]` What are the risks of using AI-generated code?

    Ans: The risks of using AI-generated code include potential security vulnerabilities, incorrect logic, and the introduction of bugs. AI may also produce code that does not adhere to best practices or organizational standards. To mitigate these risks, I always review and test AI-generated code thoroughly before deployment.

12. 🟡🔥 `[AMZN]` How do you make sure AI output is correct and safe before shipping?

    Ans: I validate AI output by conducting code reviews, running automated tests, and performing security scans. I also cross-reference AI suggestions with official documentation and best practices to ensure accuracy and safety before shipping.

13. 🟡🔥 `[CTS]` Would you paste company code or secrets into ChatGPT? Why not?

    Ans: No, I would never paste company code or secrets into ChatGPT or any external AI tool. Doing so could lead to data leakage and compromise sensitive information. I always ensure that any code or data shared with AI tools is sanitized and does not contain proprietary or confidential information.

14. 🟡 `[ACN]` How do you handle AI suggesting insecure config (open SG, public S3)?

    Ans: If AI suggests an insecure configuration, I immediately review the suggestion and assess its implications. I would reject any insecure recommendations and instead implement secure configurations based on best practices and organizational policies. Additionally, I would document the incident and provide feedback to improve the AI tool's suggestions.

15. 🟡 `[DLT][EY]` What's your company's AI usage policy? How do you follow it?

    Ans: My company's AI usage policy emphasizes responsible use, data privacy, and security. I follow it by ensuring that I do not share sensitive information with AI tools, reviewing AI-generated output for accuracy and security, and adhering to guidelines for acceptable use. I also participate in training sessions to stay updated on best practices for AI usage.

16. 🔴 `[PP]` Who is accountable when AI-generated code causes an incident?

    Ans: Accountability for AI-generated code incidents typically lies with the organization and the individuals responsible for reviewing and deploying the code. While AI can assist in code generation, it is ultimately the responsibility of human developers and managers to ensure the code is safe, secure, and compliant with organizational standards.

17. 🟡 `[INFY]` How do you avoid over-relying on AI and losing fundamentals?

    Ans: To avoid over-relying on AI, I maintain a strong foundation in core programming and DevOps principles. I regularly practice coding without AI assistance, participate in code reviews, and stay updated on industry best practices. Additionally, I critically evaluate AI suggestions and ensure that I understand the underlying logic before implementing them.

18. 🟡 `[CMCST]` What are data-privacy concerns with AI coding tools?

    Ans: Data-privacy concerns with AI coding tools include the potential for sensitive information to be inadvertently shared or exposed. AI tools may store or process code snippets, which could lead to data leakage if proprietary or confidential information is included. To mitigate these concerns, I avoid sharing sensitive data with AI tools and ensure that any code used is sanitized and free of confidential information.

19. 🔴 `[AMZN]` How do you validate an AI-suggested IAM policy?

    Ans: To validate an AI-suggested IAM policy, I review the policy for adherence to the principle of least privilege, ensuring that it grants only the necessary permissions. I also test the policy in a controlled environment to verify its functionality and check for any potential security risks. Additionally, I cross-reference the policy with AWS best practices and documentation to ensure compliance.

20. 🟡 `[WMT]` Have you ever caught AI giving you wrong/hallucinated output?

    Ans: Yes, I have encountered instances where AI provided incorrect or hallucinated output. In such cases, I cross-checked the information with official documentation and consulted with colleagues to verify its accuracy. I also reported the issue to the AI tool's support team to help improve its performance.


## GenAI literacy 🔥 (basics they expect you to know)
21. 🟢🔥 `[GEN]` What is an LLM? What is a token / context window?

    Ans: An LLM (Large Language Model) is a type of AI model designed to understand and generate human-like text based on vast amounts of data. A token is a unit of text, such as a word or subword, that the model processes. The context window refers to the maximum number of tokens the model can consider at once when generating or understanding text.

22. 🟡🔥 `[WMT][PP]` What is a hallucination? How do you deal with it?

    Ans: A hallucination in AI refers to when the model generates information that is false or not grounded in reality. To deal with hallucinations, I cross-verify the output with reliable sources, use multiple AI tools for confirmation, and apply critical thinking to assess the plausibility of the information provided.

23. 🟡🔥 `[AMZN]` What is RAG and why does it reduce hallucination?

    Ans: RAG (Retrieval-Augmented Generation) is a technique that combines retrieval of relevant information from external sources with the generative capabilities of an LLM. By grounding the model's responses in factual data retrieved from trusted sources, RAG helps reduce hallucinations and improves the accuracy of the generated output.

24. 🟡 `[CTS]` Prompting vs fine-tuning — when each?

    Ans: Prompting involves providing specific instructions or context to an LLM to guide its output without altering the model itself. Fine-tuning, on the other hand, involves training the model on a specialized dataset to adapt it for specific tasks or domains. Prompting is suitable for general use cases, while fine-tuning is preferred when consistent performance on a particular task is required.

25. 🟡 `[ACN]` What are embeddings / vector search used for?

    Ans: Embeddings are numerical representations of text or data that capture semantic meaning, allowing for efficient comparison and retrieval. Vector search uses these embeddings to find similar items in a high-dimensional space, enabling applications such as semantic search, recommendation systems, and clustering of related content.

26. 🟡 `[CMCST]` What is an AI agent? What is MCP?

    Ans: An AI agent is an autonomous entity that can perceive its environment, make decisions, and take actions to achieve specific goals. MCP (Multi-Context Processing) refers to the ability of an AI agent to handle multiple contexts or tasks simultaneously, allowing it to adapt its behavior based on different situations and requirements.

27. 🟢 `[HEXA]` What is prompt engineering? Give tips for a good prompt.

    Ans: Prompt engineering is the practice of designing effective prompts to elicit desired responses from an AI model. Tips for a good prompt include being clear and specific, providing context, using examples, and iteratively refining the prompt based on the model's output to achieve the best results.

28. 🟡 `[DLT]` What is Amazon Bedrock? (building vs using AI)

    Ans: Amazon Bedrock is a fully managed service that allows developers to build and deploy AI applications without managing the underlying infrastructure. It provides access to foundation models from various providers, enabling users to create custom AI solutions while focusing on application logic rather than model training and maintenance.

29. 🔴 `[PP]` What is the OWASP Top 10 for LLM apps? (prompt injection, data leakage)

    Ans: The OWASP Top 10 for LLM apps highlights the most critical security risks associated with applications that utilize large language models. Key risks include prompt injection, where malicious input can manipulate the model's output; data leakage, where sensitive information may be exposed; and other vulnerabilities such as model inversion attacks, adversarial inputs, and insufficient access controls. Developers should implement robust security measures, including input validation, access restrictions, and monitoring to mitigate these risks.

30. 🟡 `[EY]` What is temperature in an LLM?

    Ans: Temperature is a parameter that controls the randomness of an LLM's output. A lower temperature (e.g., 0.2) makes the model's responses more deterministic and focused, while a higher temperature (e.g., 0.8) allows for more diverse and creative outputs. Adjusting the temperature can help balance between accuracy and creativity in the generated text.


## AI in DevOps / ops (emerging) 🔥
31. 🟡 `[WMT]` How could AI help in CI/CD or incident response? (AIOps, log summaries)

    Ans: AI can assist in CI/CD and incident response by automating repetitive tasks, analyzing logs, and providing insights for faster decision-making. In CI/CD, AI can optimize build pipelines, predict failures, and suggest fixes. In incident response, AI can summarize logs, detect anomalies, and recommend remediation steps, enabling quicker resolution and reducing downtime.

32. 🟡 `[CMCST]` What is AIOps? How is AI used in observability?

    Ans: AIOps (Artificial Intelligence for IT Operations) leverages AI and machine learning to enhance IT operations by automating processes, analyzing large volumes of data, and providing actionable insights. In observability, AI can be used to monitor system performance, detect anomalies, correlate events across different sources, and predict potential issues before they impact users, improving overall system reliability and efficiency.

33. 🟡 `[AMZN]` Would you let AI auto-remediate production? Risks?

    Ans: I would be cautious about allowing AI to auto-remediate production issues. While AI can provide valuable insights and recommendations, there are risks associated with automated actions, such as unintended consequences, misconfigurations, or exacerbating the issue. I would prefer a human-in-the-loop approach where AI suggests remediation steps, but a qualified engineer reviews and approves the actions before implementation.

34. 🔴 `[PP]` How do you prevent AI-generated code from introducing vulnerabilities into the pipeline?

    Ans: To prevent AI-generated code from introducing vulnerabilities, I implement a multi-layered approach that includes thorough code reviews, automated security scans, and adherence to coding standards. I also use static and dynamic analysis tools to detect potential vulnerabilities and ensure that any AI-generated code is tested in a controlled environment before deployment. Additionally, I provide training for the team on secure coding practices and the responsible use of AI tools.

35. 🟡 `[ACN]` How do you use AI for code review? Can it replace human review?

    Ans: I use AI to assist with code reviews by providing suggestions for improvements, identifying potential bugs, and ensuring adherence to coding standards. However, AI cannot replace human review entirely, as it may miss context-specific issues or nuanced design considerations. Human reviewers are essential for evaluating the overall architecture, understanding business requirements, and making judgment calls that AI may not be capable of.

36. 🟡 `[DLT]` How might you use AI to write/maintain Terraform at scale?

    Ans: I could use AI to generate and maintain Terraform configurations by providing it with high-level infrastructure requirements. The AI can create modular and reusable Terraform code, suggest optimizations, and help with versioning and state management. However, I would ensure that all generated code is reviewed for correctness, security, and compliance with organizational standards before deployment.

## Scenario / behavioral 🔥
37. 🟡🔥 `[GEN]` Tell me about a time AI helped you solve a hard problem.

    Ans: Recently, I was troubleshooting a complex issue in a Kubernetes cluster where pods were failing to start due to an obscure configuration error. I used ChatGPT to analyze the error logs and suggested potential causes based on similar issues it had seen. It pointed me towards a misconfigured ConfigMap that I had overlooked. After correcting the ConfigMap, the pods started successfully. This experience highlighted how AI can accelerate problem-solving by providing insights that might not be immediately apparent.

38. 🟡 `[AMZN]` Tell me about a time AI gave wrong output and how you caught it.

    Ans: During a recent project, I used an AI tool to generate an IAM policy for a new service. The AI suggested permissions that were too broad, potentially violating the principle of least privilege. I caught this by reviewing the generated policy against our security guidelines and running a simulation in a test environment. I corrected the policy to ensure it only granted necessary permissions, preventing potential security risks.

39. 🟡 `[WMT]` A junior over-relies on Copilot and ships a bug. How do you coach them?

    Ans: I would first review the situation with the junior developer to understand how the bug occurred and the role Copilot played in it. I would explain the importance of critical thinking and code review, emphasizing that AI tools are aids, not replacements for judgment. I would provide guidance on best practices for using Copilot, such as reviewing generated code, running tests, and seeking peer feedback before shipping. Additionally, I would encourage them to learn from the experience and apply these lessons in future work.

40. 🔴 `[PP]` Your team wants to adopt an AI tool. How do you evaluate it for security/compliance?

    Ans: I would evaluate the AI tool by conducting a thorough security and compliance assessment. This includes reviewing the tool's data handling practices, encryption methods, access controls, and compliance with relevant regulations (e.g., GDPR, HIPAA). I would also assess the tool's ability to integrate with our existing security infrastructure and perform penetration testing to identify potential vulnerabilities. Additionally, I would consult with legal and compliance teams to ensure that adopting the tool aligns with organizational policies and industry standards.

---

## 💬 Model answer frame (for Q1 "how do you use AI daily")
> "I use AI as an accelerator, not a replacement for judgment. Day-to-day: **Copilot** scaffolds my Terraform modules, K8s manifests and unit tests; **Amazon Q** helps with AWS-specific debugging and IAM questions; **ChatGPT/Claude** help me root-cause by explaining stack traces and `kubectl describe` output, and draft runbooks/PR descriptions. The rule I never break: **I review and understand every line, run `plan`/tests/scans, and never paste secrets or proprietary code into external tools.** It's made me noticeably faster on boilerplate while I keep ownership of correctness and security."

## ⭐ Your resume tie-in
Resume literally lists *AI-Assisted Engineering: GitHub Copilot, Amazon Q Developer, ChatGPT, Claude* — so expect follow-ups. Have one crisp example per tool ready.
