# Controlled Context Continuity

**Controlled context continuity** refers to maintaining the validity of an authorized state over time as the environment, actors, and responsibilities change.  Traditional admissibility checks answer “Is this action allowed right now?” but they do not ensure that the underlying context remains valid during long‑running workflows.  Continuity governance asks: **Does this interaction remain authorized to continue?**

## Why Continuity Matters

In many real‑world processes, actions are not instantaneous.  An AI agent may initiate a workflow that spans minutes, hours, or days.  During that time, context can shift—ownership may change, data may be updated, supervisory authority may expire, or risk posture may evolve.  A state that was valid at the moment of authorization can become stale or invalid.

A post on LinkedIn describing the evolution of AI governance notes that **valid‑state continuity** questions whether a previously valid state remains valid as context, responsibility, authority, users, hand‑offs, and consequences change【591104296555679†L43-L50】.  Admissibility should not live as a single‑point status; once context shifts, yesterday’s “valid” may already be stale【591104296555679†L43-L49】.  Continuity governance binds admissibility with evidence, responsibility, authority, degradation, and restoration signals【591104296555679†L49-L52】.

## Signals for Continuity

Maintaining controlled context continuity requires continuously or periodically checking signals that might invalidate the previously approved state.  Examples include:

* **Authority expiry:** Approver’s delegation expires or is revoked.
* **Ownership change:** The resource (account, record, matter) is transferred to a different owner or jurisdiction.
* **Policy drift:** Policies are updated, introducing new constraints or prohibitions.
* **Context degradation:** Critical data becomes outdated, incomplete, or inconsistent.
* **User hand‑off:** A different agent or human takes over the workflow, potentially changing the risk profile.
* **Operational anomalies:** Hesitation, overload, repeated uncertainty, or unsafe pressure can be human signals that the workflow should pause【591104296555679†L52-L56】.

These signals prompt the runtime to re‑evaluate admissibility.  If continuity checks fail, the system should refuse to continue or require supervised override.

## Design Considerations

1. **Anchors:** Each decision anchor (who, where, what, how fast, consent) must be monitored for change.  When an anchor drifts, the gate re‑runs admissibility.
2. **Granular state representation:** Represent workflows as sequences of stages with explicitly scoped authority.  Each stage may have its own expiry or hand‑off conditions.
3. **Audit updates:** Continuity checks and their outcomes should be appended to the same sealed artifact, ensuring a complete record of context evolution.
4. **Graceful degradation:** If continuity fails, the system should provide clear reasons and a path to resolution (e.g., re‑approval, updated policies).
5. **Human factors:** Recognize that human hesitation, overload, fear of mistakes, or pressure to continue are not just emotions; they can be signals for the system to pause【591104296555679†L52-L56】.

## Relationship to Admissibility

The **admissibility gate** decides whether an action is allowed at a point in time.  **Controlled context continuity** ensures that the decision remains valid as the workflow progresses.  Both are required for robust governance:

* **Admissibility without continuity** may allow workflows to run long after their context has degraded or authority has lapsed.
* **Continuity without initial admissibility** cannot provide a safe starting point.  The two mechanisms work together to ensure that actions are authorized **and** remain authorized throughout their lifecycle.

## Future Directions

TrustCore plans to integrate continuity governance into its runtime by:

* Adding **expiry horizons** to decision artifacts, requiring re‑authorization after a configured time or upon detected changes.
* Implementing **context monitors** that listen for policy updates, identity changes, or hand‑offs and trigger re‑evaluation.
* Providing **developer APIs** to query continuity status and to register custom signals.
* Surfacing **continuity dashboards** for human operators to review long‑running workflows and intervene when necessary.

By addressing continuity, we aim to ensure that **YES is not SEND** at any point in time—approval remains conditional on context staying valid.
