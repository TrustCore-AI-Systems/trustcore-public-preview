# Admissibility Gate

The **admissibility gate** is the heart of TrustCore’s pre‑execution control layer.  Its purpose is to determine whether a proposed action is allowed to proceed under the owner’s policies and risk posture.  This document explains the problem it solves, how it works, and what properties it must exhibit.

## Motivation

Modern AI systems no longer simply answer questions; they **execute actions**.  Agents may query databases, trigger workflows, modify records, send communications, or move money.  Guardrails that operate at the conversational layer are not sufficient when the risk lies in what the system does, not just what it says【93636198385022†L140-L163】.

Organizations need a decision layer **between agent reasoning and tool invocation** to evaluate:

* Which tools are accessible.
* Which operations are permitted.
* What parameter ranges are allowed.
* Under what runtime conditions execution is authorized【93636198385022†L140-L160】.

Without this layer, conversational approval becomes a proxy for operational safety, which does not scale【93636198385022†L162-L163】.

## Core Pattern

An **admissibility gate** sits between applications, workflows, automations, AI tools, and high‑risk actions【412371766996528†L141-L144】.  When an agent intends to perform an action, it sends a request to the gate containing only metadata—not raw content or model internals:

* **Who** is acting (identity, role, group).
* **Where** they are acting (matter, account, jurisdiction, environment).
* **What** they want to do (action type, operation).
* **How fast** it must happen (urgency or turnaround).
* **Consent & constraints** (client instructions, supervision requirements, risk posture)【412371766996528†L154-L161】.

The gate applies declarative policies and returns one of three outcomes【412371766996528†L146-L153】:

| Outcome | Meaning |
| --- | --- |
| ✅ **Approve** | The action may proceed under current authority. |
| ❌ **Refuse** | The action is blocked because policy, identity, or context does not authorize it. |
| 🧑‍⚖️ **Supervised Override** | The action may proceed only if a named human decision‑maker explicitly approves it.  The override is scope‑bounded (action + context + time) and produces an enhanced audit record【412371766996528†L245-L247】. |

For every governed attempt, the gate produces a **sealed artifact**—a tamper‑evident record containing identifiers, timestamps, decision metadata, and refusal or override codes【412371766996528†L163-L170】.  These artifacts live in tenant‑controlled storage and support audit and evidentiary review【412371766996528†L163-L170】.

## Design Principles

To be effective, an admissibility gate should exhibit the following properties (adapted from [Thinking OS control objectives](https://www.thinkingoperatingsystem.com/pre-execution-action-governance-runtime)):

1. **Fail closed by default.** If policy, identity, or required context is missing or ambiguous, the gate must refuse or require supervised override【412371766996528†L218-L223】.
2. **Run before irreversible actions.** The gate evaluates requests *before* a filing is submitted, funds are transferred, or records are modified【412371766996528†L224-L226】.
3. **Model‑agnostic.** Decisions rely on metadata and policies, not on prompt inspection or model internals【412371766996528†L227-L229】.
4. **Tenant‑controlled policies and identity.** Rules and identity data come from the customer’s systems, not from the vendor【412371766996528†L230-L233】.
5. **No training on decision data by default.** The system must not use runtime decision data to train models without explicit opt‑in【412371766996528†L234-L236】.
6. **Integrity‑verifiable artifacts.** Each decision produces an append‑only record that can be independently verified【412371766996528†L237-L239】.
7. **Transparent refusal and override codes.** Governance outcomes are not generic errors; they include codes and reasons【412371766996528†L242-L246】.
8. **Supervised override accountability.** Overrides require an authenticated human and generate enhanced artifacts recording who accepted the risk【412371766996528†L245-L247】.
9. **Privacy‑preserving.** Where possible, the gate relies on labels and metadata rather than inspecting full content【412371766996528†L248-L249】.
10. **Integration with existing systems.** The gate consumes policy and identity from existing governance, risk, and compliance systems【412371766996528†L252-L253】.
11. **Non‑bypassable.** For workflows wired through the runtime, there must be no alternate path that bypasses the gate【412371766996528†L263-L265】.

## Relationship to Guardrails

Guardrails filter input and output at the conversational layer; they prevent harmful or inappropriate language.  Governance, on the other hand, protects execution【93636198385022†L165-L170】.  Both are necessary.  Guardrails stop malicious prompts and unsafe responses.  The admissibility gate stops unauthorized actions and produces an audit trail.  Together they form a layered defence for AI systems.

## Future Work

TrustCore’s admissibility gate is evolving.  Upcoming work includes:

* **Policy composition and conflict resolution.** Simplifying the authoring and management of complex policies.
* **Formal verification.** Proving that policies are well‑formed and free of conflicts or unintended consequences.
* **Context enrichment.** Integrating additional context sources (risk scores, external signals) to improve decisions.
* **Continuity governance.** Extending admissibility to ensure that an action remains valid over time and across hand‑offs (see [`controlled-context-continuity.md`](controlled-context-continuity.md)).

We invite feedback and collaboration to refine these concepts and build a robust open ecosystem around **pre‑execution AI governance**.
