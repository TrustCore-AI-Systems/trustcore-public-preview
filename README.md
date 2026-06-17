# TrustCore Public Preview

Welcome to the **TrustCore Public Preview** repository.  This repository provides non‑confidential materials for developers, partners, and researchers interested in **runtime governance** and **pre‑execution control** for AI systems.

## Contents

* **`index.html`** – A simple landing page demonstrating our brand aesthetic.  It explains the vision and principles of the TrustCore control layer.
* **`logo.svg`** – The TrustCore logo in SVG format.  It uses a dark theme with cyan and teal accents to reflect our premium enterprise style.
* **`SECURITY.md`** – Guidelines for responsible disclosure of vulnerabilities.  Please read this before reporting any security issues.
* **`ROADMAP.md`** – An outline of upcoming milestones, including SDK releases, integrations, and governance enhancements.
* **`FOUNDING-PILOT.md`** – Information about our early pilot program for partners.  Interested organizations can request access through this program.
* **`docs/`** – Detailed concept papers:
  * **`admissibility-gate.md`** – Describes how the TrustCore pre‑execution gate works and why it matters.
  * **`controlled-context-continuity.md`** – Introduces continuity governance and explains why admissibility must remain valid over time.
  * **`github-money-path.md`** – Provides guidance for developers interacting with financial systems via GitHub and outlines how TrustCore can help protect monetary workflows.

## Purpose

This repository is **not** the full TrustCore codebase.  We are preparing open source components and SDKs, but core control plane code remains proprietary and audited.  The public preview allows us to gather feedback on our documentation, governance model, and ecosystem integrations without exposing sensitive internals.

By sharing high‑level design documents and a minimal landing page, we invite **community discussion** on runtime governance problems such as:

* How to prevent AI agents from executing unauthorized actions.
* How to manage supervision boundaries between humans and machines.
* How to create tamper‑evident audit trails for each governed action.
* How to maintain valid context over long‑running agent workflows.

We welcome pull requests that improve the clarity, accessibility, and accuracy of our public materials.  However, please **do not** submit actual control plane code or proprietary implementation details here.

## Get Involved

* **Read the docs.** Start with [`docs/admissibility-gate.md`](docs/admissibility-gate.md) to understand the core problem TrustCore solves.
* **Share feedback.** Open issues or discussions to suggest improvements.  For sensitive topics or vulnerabilities, follow [SECURITY.md](SECURITY.md).
* **Join the pilot.** Interested in trialing TrustCore within your organization?  See [`FOUNDING-PILOT.md`](FOUNDING-PILOT.md) for eligibility and contact information.

Thank you for your interest in **runtime governance** and **control before consequence**.
