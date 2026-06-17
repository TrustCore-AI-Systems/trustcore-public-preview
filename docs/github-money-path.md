# GitHub Money Path Guidance

When developers build automations that touch financial systems, they often manage the workflow via GitHub: code repositories, CI/CD pipelines, configuration files, and secrets.  This document offers guidance on protecting the **money path**—any path that can trigger the movement of funds or other high‑value transactions—when working in GitHub.

## Why It Matters

Financial operations involve irreversible consequences.  Accidentally deploying a script that triggers a wire transfer or modifies billing rules could cause serious losses.  In the age of AI‑assisted development, it is critical to maintain a **human approval boundary** between code changes and execution.  As noted in discussions of pre‑execution governance, enterprises must apply control between reasoning and action【93636198385022†L140-L163】, and they must refuse or require supervised override when context is ambiguous【412371766996528†L218-L223】.

## Best Practices

1. **Separate code from secrets.** Use GitHub’s secret storage or an external vault to store API keys, credentials, and private keys.  Never commit these directly into version control.
2. **Use branch protection rules.** Require pull request reviews and status checks before merging code to branches that control financial workflows.
3. **Implement pre‑execution gates.** Integrate TrustCore’s pre‑execution control layer into automation steps that can move money or adjust financial records.  The gate will assess whether the action is authorized and, if necessary, require supervised override.
4. **Audit your CI/CD pipelines.** Ensure that deployment scripts cannot bypass the gate or call financial APIs directly.  Every invocation should flow through the admissibility gate.
5. **Version policies with code.** Store declarative policy files alongside code, review them like other changes, and ensure they are loaded into the gate before execution.
6. **Monitor for drift.** Changes in identity, environment, or policy can invalidate previously approved workflows.  Use continuity governance to detect when a money path is no longer valid (see [`controlled-context-continuity.md`](controlled-context-continuity.md)).
7. **Test in observe‑only mode.** Before enabling enforcement, run the gate in observation mode to see what would have been blocked.  This allows you to fine‑tune policies without interrupting operations【412371766996528†L258-L259】.

## Example Workflow

Imagine a repository containing scripts to process payroll.  A developer updates a script to change the salary calculation formula.  The following controls help secure the money path:

1. The developer creates a pull request.  Branch protection requires at least two approvals and successful unit tests.
2. A workflow file defines a CI job that, when triggered, packages the script and deploys it to a staging environment.
3. The deployment script calls TrustCore’s API to request permission to apply the new formula to the payroll system.  The gate sees that the action type is `updatePayroll`, the actor is the CI service account, the target environment is staging, and urgency is low.  Policy allows this, so the gate returns **Approve**.
4. Later, when promoting to production, the gate evaluates the same action but now the environment is production and the policy requires a human override.  The CI job pauses until an authorized finance officer approves.  Once approval is recorded, the deployment proceeds, and a sealed artifact logs the action and the approver【412371766996528†L146-L153】.
5. If at any point the finance officer’s delegation expires or policies change, continuity checks would cause subsequent deployment attempts to be refused until re‑authorization occurs【591104296555679†L43-L50】.

## Closing Thoughts

Protecting the money path is about more than secure coding; it requires **runtime governance**, **controlled context continuity**, and a culture of human oversight.  By integrating TrustCore’s admissibility gate into your GitHub workflows, you can ensure that AI agents and automation scripts do not move money without explicit permission and a complete audit trail.
