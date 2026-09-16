# 1. Security posture and scope

This guide is written for administrators evaluating or operating the MediaWiki Cargo extension in a production environment. It emphasizes controls that reduce confidentiality, integrity, availability, and credential-exposure risk.

It assumes Cargo may be used by editors who are not server administrators and may be reachable from an internet-facing MediaWiki deployment. If the wiki is private, the same controls still matter because authenticated users, compromised accounts, crawlers, automation, and accidental expensive queries can trigger the same classes of failure.

Recommendations labeled "enterprise baseline" are intentionally stricter than upstream defaults. They are compensating controls, not claims that Cargo is unsafe by design.

---

[← Back to README](../README.md) | [Next: Risk matrix →](02-risk-matrix.md)
