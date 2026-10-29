<div align="center">

# PentAGI Skill

### A safety-first agent skill for autonomous AI penetration testing

**Hard legal scope rules · Lab-first workflow · Gated runs · Honest cost reality**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Type: Agent Skill](https://img.shields.io/badge/Type-Agent%20Skill-purple.svg)](SKILL.md)
[![For: PentAGI](https://img.shields.io/badge/For-PentAGI%20by%20VXControl-red.svg)](https://github.com/vxcontrol/pentagi)
[![Rules: 6 Hard Rules](https://img.shields.io/badge/Safety-6%20Hard%20Rules-brightgreen.svg)](#the-hard-rules)

</div>

---

[PentAGI](https://github.com/vxcontrol/pentagi) puts a team of autonomous AI
agents — an Orchestrator, a Researcher, a Developer, and an Executor running
20+ real tools (nmap, Metasploit, sqlmap, Nuclei…) — on a target you name in
plain language. That is enormous power with almost no friction.

This repository is a **skill** (a structured instruction file) that any
Claude-compatible or agent-skills-compatible assistant can load. It teaches
the assistant how to plan, scope, and run PentAGI **responsibly**: written
authorisation before any run, lab targets first, isolated environments only,
and a hard budget cap — every time, no exceptions.

> **PentAGI itself is not included here and is not my project.** It is built
> by [VXControl](https://github.com/vxcontrol). This repo contains only the
> skill/playbook for using it safely. Full credit below.

## Why this exists

Autonomous pentesting agents are one bad prompt away from scanning a system
nobody authorised. The tools don't check permission — **the operator has to**.
Existing guides focus on installation and capability; almost none encode the
legal and operational discipline as rules an AI assistant must refuse to
break. This skill does:

- It **refuses** third-party and client production targets without a signed
  pentest agreement.
- It makes **lab-first** the default, not an afterthought.
- It puts **scope and spend caps** in writing before any run starts.
- It is honest about **what PentAGI can't do**, what it costs, and what
  hardware it actually needs.

## What's inside

| File | What it is |
| --- | --- |
| [`SKILL.md`](SKILL.md) | The skill itself — hard rules, architecture briefing, install prerequisites, gated run workflow |
| [`README.md`](README.md) | This page |
| [`LICENSE`](LICENSE) | MIT licence for the skill content |

**The skill covers:**

- **6 non-negotiable hard rules** that outrank any task instruction
- A plain-language briefing on PentAGI's agent architecture and memory design
- **Install prerequisites** — VM/VPS sizing, Docker, LLM provider choices, and why the local-model route needs ~20 GB VRAM
- **Cost reality** — roughly 500k–1M tokens per moderate run: ~$1–5 on budget models, $10–50+ on frontier models
- A **five-gate workflow** for every run: authorisation → environment → budget → guided run → report-to-fix-list
- Legitimate use cases: auditing your own builds before delivery, learning agent-orchestrated security, honest "we security-test what we build" positioning

## The hard rules

| # | Rule |
| --- | --- |
| 1 | **Owned or explicitly authorised targets only.** Written permission that specifically authorises pentesting. A normal website-build or maintenance contract does **not** count — exploit testing needs its own signed pentest agreement. |
| 2 | **Lab targets first.** Intentionally vulnerable labs (DVWA, Metasploitable) and local copies of your own sites, on a host-only network. Live owned systems only after lab runs are understood. |
| 3 | **Never point it at third-party production sites.** No client live sites, no "free audit" lead generation. Unauthorised testing can be a criminal offence (IT Act §§43/66, CFAA, Computer Misuse Act…), and "the AI did it" is not a defence. |
| 4 | **Scope and spend cap before every run.** Written scope note (target, permission basis, in/out, no-DoS rule, duration) plus a hard LLM budget and deliberate tool-call limits. |
| 5 | **Isolated environment only.** PentAGI holds Docker-socket (root-equivalent) power over its host. Dedicated Linux VM or VPS only — never a daily-driver host. |
| 6 | **The operator verifies permission — every time.** PentAGI never checks authorisation. Reachable, public, or "just a demo" is not permission. |

## Quick start

1. **Get the skill.** Copy [`SKILL.md`](SKILL.md) into your agent's skills
   folder — for example `~/.claude/skills/pentagi/SKILL.md`, or your
   assistant's custom-skills directory — keeping the file name `SKILL.md`.
2. **Ask your assistant about PentAGI.** With the skill loaded, questions
   like *"plan a PentAGI lab for my own test site"* or *"what do I need
   before installing PentAGI?"* will trigger the playbook: concepts first,
   scope checklist second, install plan for your approval third.
3. **Install PentAGI itself** from the upstream project when — and only
   when — the prerequisites are met:
   [github.com/vxcontrol/pentagi](https://github.com/vxcontrol/pentagi)

The skill never installs software, pulls images, or spends money on its own.
Installing and spending always need your explicit go-ahead.

## PentAGI at a glance

| Aspect | Summary |
| --- | --- |
| **What it is** | Fully autonomous multi-agent penetration-testing system |
| **Agents** | Orchestrator (plans, delegates, re-plans) · Researcher (recon/OSINT, vuln sources) · Developer (attack strategy, exploit code) · Executor (20+ tools in sandboxed Kali containers) |
| **Tools** | nmap, Metasploit, sqlmap, Nuclei, Gobuster, and more |
| **Memory** | PostgreSQL + pgvector (long-term / working / episodic); optional Graphiti/Neo4j knowledge graph |
| **Interfaces** | Web UI (HTTPS :8443), REST & GraphQL APIs, flow templates, Assistant steering, optional Langfuse observability |
| **Built-in guardrails** | Always-on tool-call limits, Reflector, execution monitoring — these cap runaway usage; they do **not** check authorisation |
| **Minimum hardware** | 4 GB RAM documented floor; **≥16 GB RAM Linux VM/VPS recommended** in practice; local LLMs need 32B-class models (~20 GB VRAM) |
| **Cost per run** | ~500k–1M tokens → ~$1–5 (budget models) to $10–50+ (frontier models) |
| **Honest capability** | An energetic junior pentester with superhuman patience: strong at recon and known vulnerabilities, weak on business-logic flaws and deep chaining. Not a replacement for expert judgement. |
| **Upstream licence** | Source MIT; official Docker images & web UI under a separate EULA (lawful, authorised pentesting only) |

## Legal & ethical disclaimer

This skill is for **lawful, authorised security testing and education
only** — on systems you own, in labs you control, or under a signed
penetration-testing agreement. Penetration testing without authorisation is
illegal in most jurisdictions and can cause real damage to systems and data.
The author of this skill accepts no liability for misuse. If you are unsure
whether you have authorisation for a target, the answer is that you do not.

## Credits

- **PentAGI** — created and maintained by
  [VXControl](https://github.com/vxcontrol):
  [github.com/vxcontrol/pentagi](https://github.com/vxcontrol/pentagi).
  All credit for the system belongs to them. This repository is an
  independent, unofficial playbook and is not affiliated with or endorsed
  by VXControl.
- **This skill** — written and maintained by
  [Ahmad Raza](https://github.com/Ahmadraza970) (Ahmad Digital Studio).
  Contributions and corrections are welcome via issues and pull requests.

---

<div align="center">

*Test what you own. Get permission in writing. Cap the spend. Fix what you find.*

</div>
