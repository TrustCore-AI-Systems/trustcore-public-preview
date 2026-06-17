# Security Policy

## Supported Versions

TrustCore’s control plane is currently in limited preview.  Only select pilot partners have access to the core system.  The materials in this repository are documentation and design assets; there is no runtime code to exploit here.  Nevertheless, we take security seriously and encourage responsible disclosure of any issue you discover in our documentation, website, or related systems.

| Version | Supported | Notes |
| --- | --- | --- |
| Public preview materials | ✅ | Updated regularly |
| Pilot API & SDK | ✅ | Private access only |
| Internal prototypes | ❌ | Not publicly available |

## Reporting a Vulnerability

If you believe you have found a security vulnerability or other sensitive issue related to TrustCore, **please do not open a public issue**.  Instead, contact us via email at:

```
security@trustcore.ai
```

Include as much detail as possible to help us understand and reproduce the issue.  We commit to acknowledging receipt within **three business days** and will work with you to verify and address the problem.  Once the issue is resolved, we will credit reporters who request recognition.

### PGP

For encrypted communication, our PGP public key is available on request via the same email address.  We recommend encrypting reports that contain sensitive information.

## Coordinated Disclosure

We follow a coordinated vulnerability disclosure process inspired by [GitHub’s private vulnerability reporting guidelines](https://docs.github.com/en/code-security/how-tos/report-and-fix-vulnerabilities/report-privately).  After verifying a report, we will prepare a fix or mitigation and, if appropriate, publish an advisory describing the issue and its resolution.  We ask that reporters refrain from publicly disclosing details until we have released a remediation or have mutually agreed on a disclosure timeline.

## Security Features in TrustCore

Although this repository does not contain runtime code, TrustCore’s products implement several security controls:

* **Fail‑closed gating:** If policy, identity, or context is missing or ambiguous, the pre‑execution gate refuses or escalates the action【412371766996528†L218-L223】.
* **Tenant‑owned policies and identities:** All authorization data comes from client systems【412371766996528†L230-L233】.
* **Tamper‑evident audit records:** Every decision yields an append‑only, integrity‑verifiable artifact【412371766996528†L163-L170】.
* **No training on decision data:** Runtime decision data is never used to train models without explicit opt‑in【412371766996528†L231-L236】.

We appreciate your help in keeping TrustCore safe and secure.
