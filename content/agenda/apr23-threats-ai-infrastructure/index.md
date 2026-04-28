---
title: "Hunting for Threats Against AI Infrastructure"
description: "AI is now both the weapon and the target. Mandiant's threat hunters show what nation-state actors are already doing — and what you need to log before you can even start defending."
date: 2026-04-23T08:15:00-07:00
image: "session-title.jpg"
categories: ["Agenda"]
tags: ["security", "ai", "mandiant", "threat-hunting", "google-cloud"]
series: ["Google Cloud Next 2026"]
session_date: "2026-04-23"
rating: 4
---

## What this session is about

Traditional detection is no longer enough. To stay ahead of attackers, you must proactively hunt for threats. Demystify how to build a threat-hunting program from scratch to minimise breach impact and reduce dwell time. We'll cover how to assemble a team from your security operations centre and incident response staff, establish clear processes, and choose the right tools. In addition, we'll explore several use cases for proactively finding attacks against AI infrastructure.

**Speakers:** Ryan Fried (Principal Security Consultant, Google Cloud) · John Palmisano (Manager, Mandiant, Google Cloud)

---

## 07:00am start on a Thursday

![Starbucks Nitro Cold Brew and two Quest Bars on the hotel room counter](early-morning-fuel.jpg)

This was the first session of Day 2. First session 08:15. Starbucks Nitro Cold Brew and two Quest Bars from the hotel lobby.

Breakfast of champions. I first tried Quest bars a long time ago when experimenting with Keto — delighted I was able to have them again! However discovered on this trip that Starbucks Nitro Cold Brew cans are not available in the UK, which is genuinely upsetting information to bring home.

I picked this deliberately because the AI threats topic is huge. Everything is AI. Google (and their acquired company [Mandiant](https://www.mandiant.com)) deal with real-world incidents constantly. When they say they're seeing something in the wild, it means someone is already dealing with it in production.

It is something every Engineer needs to keep at the forefront of their mind.

---

## The two-front attack

The session opened with a clear framing.

![The Two-Front Attack — AI as Weapon & AI as Target, with threat actor categories and example techniques on each side](two-front-attack.jpg)

AI is simultaneously giving defenders an advantage (faster analysis, better signal processing, pattern recognition at scale) and creating a new attack surface.

The two fronts:

**AI as a Weapon** — adversaries using AI to accelerate their attack lifecycle. Phishing at scale, automated reconnaissance, credential stuffing. The time-consuming parts of the attack chain — the stuff that used to take weeks — now takes minutes — attacks at machine speed.

**AI as a Target** —  AI systems themselves as the attack surface. Prompt injection, model extraction, data poisoning, jailbreaking. If you deploy an AI agent with access to internal systems, that agent is now a vector. I was linked this earlier which details this better — [one example of how this plays out in the wild](https://blog.7ai.com/claude-fraud-malware-campaign-ai-developer-tools).

The uncomfortable part: most organisations are deploying AI fast enough that they're years ahead of their own security posture for it.

---

## What nation-state actors are already doing

The session got very concrete very quickly. Mandiant has visibility into active threat actor campaigns. Two nation-state examples.

![APT31 (PRC): AI-enabled vulnerability analysis with a real hexstrike MCP prompt — automated exploit development pipeline](apt31-mcp-injection.jpg)

**[APT31](https://en.wikipedia.org/wiki/APT31) (PRC)** — running AI-enabled vulnerability analysis. The slide showed an actual `hexstrike` MCP (Model Context Protocol) server prompt being used to automate parts of an exploit development pipeline. This is not a proof-of-concept. This is documented activity. The model is being fed technical data and asked to assess exploitability and generate working code.

**[APT28](https://en.wikipedia.org/wiki/APT28) (Russia)** — running PROMPTSTEAL, a data miner designed to extract information via carefully crafted prompt sequences. Feed an AI agent the right sequence and it will surface data it was never supposed to surface.

Cyber crime groups are moving at similar speed: QUIETVAULT (credential stealer) and PROMPTFLUX (a just-in-time self-modifying payload that rewrites itself to evade detection). PROMPTFLUX in particular represents a new class of threat — traditional signature-based detection is useless against a payload that changes itself on each execution.

---

## Prompt injection: what it actually looks like

![Fruitshell prompt injection — hidden instructions embedded in a document, triggering obfuscated PowerShell execution via the AI agent](fruitshell-prompt-injection.jpg)

The "Fruitshell" example. An attacker embeds hidden instructions inside what looks like a standard document — a PDF, a policy doc, anything the AI agent is likely to read. When the agent retrieves and processes that document, it executes the hidden commands. In the slide example, the result is obfuscated PowerShell running on the host.

The detection problem: the AI is behaving exactly as designed — it retrieved a document and acted on its contents. The malice is in the document, not in any behaviour the agent has been told to prohibit. Standard behavioural detection will not catch this.

---

## Shifting to defence

The second half of the session pivoted from threat landscape to how you actually respond to it.

![Defender's Advantage — three-stage framework: Assess your AI systems, build a Threat Model, then run structured Threat Hunts](defenders-advantage.jpg)

Three stages: **Assess → Threat Model → Threat Hunt**

1. **Assess** — understand what AI systems you have deployed, what data they have access to, what actions they can take. Most organisations cannot fully answer this question.

2. **Threat Model** — take each AI system and work through what an attacker would do with it. What can be injected? What can be extracted? What can be impersonated? What happens if the agent is over-privileged?

3. **Threat Hunt** — proactively search for evidence of those attacks in your telemetry. Not waiting for an alert. Going looking.

The session walked through all three stages using a reference application called Nexus — a RAG (Retrieval-Augmented Generation) chatbot with access to internal documents and external APIs.

---

## The Nexus application — a vulnerable data flow

![Nexus Application — vulnerable RAG pipeline data flow showing three threat scenarios: hidden instructions via prompt injection, over-privileged insider access, and unauthorised data retrieval](nexus-rag-pipeline.jpg)

The Nexus diagram shows why AI applications are a different class of security problem.

The chatbot has a RAG pipeline feeding it internal documents. It has access to external APIs (Calendar, ServiceDesk) and a Payroll database in BigQuery. Three threat scenarios:

- **Threat A** — hidden instructions embedded in organisation policy documents. When the RAG pipeline retrieves them, the instructions execute via the chatbot.
- **Threat B** — an over-privileged insider with Read/Write access to the database can use the chatbot to escalate actions that their actual role would not normally permit.
- **Threat C** — a low-level employee asks the chatbot about CEO salary. No ACL enforcement on the retrieval layer means the chatbot will surface it.

None of these are exotic attack scenarios. They are default behaviours of a naively deployed RAG application.

The three use cases from the session — Indirect Prompt Injection, Over-Privileged Agents, and Unauthorised Sensitive Data Access — map directly to these three threat scenarios. Each one had a clear telemetry requirement and a clear response.

---

## You can't hunt what you don't log

The sharpest line of the session:

> *You can't hunt what you don't log. You can't see what you can't visualise.*

Every single telemetry source in the use case slides carried the same warning:

⚠️ *NOT ENABLED BY DEFAULT*

Retrieval Context Logs. Agent Trace/Runtime Logs. Tool Input/Output Logs. Prompt/Response Logging. PII/DLP Scanning Logs. None of them on by default. All of them required to detect or investigate any of the three threat scenarios above.

The entire second half of the session was essentially: here is what you need to detect this attack — now go turn it on.

![High-Fidelity Alerts — SIEM alert rules to build now: Probing, Guardrail Evasion, Privilege Escalation, Fuzzing, Token Consumption Anomaly, Unexpected Internet Egress, Rapid Tool-Call Looping](high-fidelity-alerts.jpg)

The practical list of alerts to add to your [SIEM](https://en.wikipedia.org/wiki/Security_information_and_event_management):

- **Probing** — high volume of blocked/filtered prompts from a single user
- **Guardrail Evasion** — prompts flagged Safe generating Unsafe responses
- **Privilege Escalation** — agent accessing a sensitive data store for the first time
- **Fuzzing** — burst of 4xx/5xx API errors from the model endpoint
- **Token Consumption Anomaly** — sudden >300% spike in output token generation per minute from a specific API key
- **Unexpected Internet Egress** — training/inference containers making outbound connections to non-allowlisted IPs
- **Rapid Tool-Call Looping** — agent attempting the same tool execution more than 5 times in under 10 seconds

These are concrete. Buildable today. Most of them are just query logic on logs you may or may not already have enabled.

---

## Why I picked this

The framing of AI having no moral compass resonated — it's an accurate observation about how the technology behaves without structure. We have seen the news reports of what some models were able to do in the name of freedom. The agent is not making ethical choices. It does what the instructions say. If the instructions are malicious or can be manipulated, it follows them just as faithfully as the legitimate ones.

The logging gap is the thing I'm taking back. Companies are early in building out AI-powered tooling internally and the default logging configuration is not fit for purpose for security. That needs to be addressed before deployment, not after an incident.

My takeaway: build an internal agent bank in a Google Cloud project — Scheduling, Documentation, HR, Talent Acquisition, Code Standards. And then try to jailbreak it (with AI also). Running the threat model yourself before someone else does is the only way to know what you actually have.

---
