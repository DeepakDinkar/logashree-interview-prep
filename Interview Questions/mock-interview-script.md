# 🎭 Mock Interview Script — 45-Min DevOps Round

> A realistic timed round in the style of **TCS / Infosys / Accenture / Deloitte / EY**. Do this with a friend, or self-run with a timer. **Speak answers aloud.** Grade yourself after. Answers live in `../../Definitions/` and the other question files — don't peek until you've attempted.

**How to run:** set a 45-min timer. Stick to the time per section. If you freeze for >30s, say "let me think" and move forward — that's realistic.

---

## ⏱️ Section 1 — Intro & resume (0:00–0:07)
1. Tell me about yourself. *(90-sec pitch: DevOps, 4 yrs, AWS/Terraform/CI-CD, key wins)*
2. Walk me through your current project (QOMOI). *(use `project-walkthrough.md`)*
3. What's your day-to-day as a DevOps engineer?

✅ *Looking for:* clear structure, "I" statements, quantified results, calm delivery.

---

## ⏱️ Section 2 — Rapid-fire fundamentals (0:07–0:17)
Quick, one-line answers. Interviewer fires 12–15:
4. Region vs Availability Zone?
5. Security Group vs NACL?
6. ALB vs NLB?
7. ECS EC2 launch type vs Fargate?
8. What is Terraform state? Why a remote backend?
9. `terraform plan` vs `apply`?
10. Docker image vs container? What is a layer?
11. What is a multi-stage build?
12. Kubernetes: pod vs deployment vs service?
13. Liveness vs readiness probe?
14. git merge vs rebase?
15. git reset vs revert?
16. What is least privilege?
17. Logs vs metrics vs traces?
18. How do you use AI tools in your work?

✅ *Looking for:* fast recall, no rambling. Stumbling on >3 = revise `rapid-fire-200.md`.

---

## ⏱️ Section 3 — Deep dive (0:17–0:29)
Pick the candidate's strongest area and go deep:
19. Walk me through your CI/CD pipeline end to end — every stage and gate.
20. How does GitHub Actions authenticate to AWS securely? *(OIDC)*
21. How do you structure a Terraform project for 3 environments?
22. How do you handle secrets across dev/stage/prod?
23. How do you roll back a bad deployment?
24. How did you reduce cost by 35%? Be specific.

✅ *Looking for:* depth, real experience, trade-off awareness.

---

## ⏱️ Section 4 — Hands-on / whiteboard (0:29–0:39)
Candidate writes or talks through one:
25. Write a shell script that alerts if disk usage exceeds 80%.
26. Write a multi-stage Dockerfile for a Node app.
27. Write Terraform for an S3 bucket with versioning + encryption.
28. *(or)* Design a highly-available 3-tier web app on AWS — draw it.

✅ *Looking for:* can actually produce working code/design, talks while doing it.

---

## ⏱️ Section 5 — Scenario / troubleshooting (0:39–0:44)
29. A deployment went out and the site returns 5xx. What do you do right now?
30. A pod is in CrashLoopBackOff — how do you debug it?
31. Two engineers ran `terraform apply` at once — what happens / how prevented?

✅ *Looking for:* "mitigate first (rollback), then root-cause"; structured diagnosis.

---

## ⏱️ Section 6 — Behavioral + your questions (0:44–0:45+)
32. Tell me about a production incident you handled. *(STAR)*
33. A time you had a disagreement with a teammate.
34. Why are you looking to change? Why this company?
35. **Do you have any questions for us?** *(always say yes — have 2 ready)*

✅ *Looking for:* STAR structure, ownership, genuine curiosity.

---

## 📝 Self-scoring rubric (rate each /5)
| Area | Score | Notes |
|------|-------|-------|
| Intro & project clarity | /5 | |
| Fundamentals recall | /5 | |
| Technical depth | /5 | |
| Hands-on ability | /5 | |
| Troubleshooting approach | /5 | |
| Communication & calm | /5 | |
| Behavioral / STAR | /5 | |

**Total /35.**
- **28+** → interview-ready. Do 1–2 more mocks for polish.
- **21–27** → close. Target the sections you scored <3.
- **<21** → more prep + hands-on practice before applying.

## 🔁 Run this 3 times before a real interview
1. First run: rough, lots of gaps — note them.
2. Revise weak areas for a few days.
3. Second & third run: should feel smooth and timed.

---
💡 The real differentiator at service/consulting companies isn't obscure trivia — it's **clear communication, confident project stories, and a structured troubleshooting approach.** This mock trains exactly that.
