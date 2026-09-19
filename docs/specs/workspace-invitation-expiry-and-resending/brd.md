---
type: BRD
title: Workspace Invitation Expiry and Resending
description: 'Business requirements drafted from the cited sources: 4 requirements,
  each citing the material it came from.'
tags:
- brd
- requirements
status: stable
generated:
  by: ichnos/gemini-3.8-flash
  at: '2026-09-19T21:07:54Z'
sources:
- id: s1
  resource: /meetings/2026-09-15-workspace-onboarding.md
  title: Workspace onboarding sync
- id: c1
  resource: https://github.com/MohamedAliZouariEng/quire-demo/issues/1
  title: 'Issue #1: Invitation lifecycle hardening'
- id: c2
  resource: /adr/0001-invitation-tokens.md
  title: 'ADR-0001: Invitation links carry single-use opaque tokens'
verified:
  by: human:MohamedAliZouariEng
  at: '2026-09-19T22:59:33Z'
ichnos:
  artifact_id: af9cf0d2-6a76-4342-94fc-76c67da8dca9
  run_id: dd733332-7a17-4a01-8180-817671d7e998
  requirement_ids:
  - R-01
  - R-02
  - R-03
  - R-04
---

# Summary

Reviewed by the end-to-end check.

A former contractor joined an enterprise customer's workspace using an invitation link forwarded months earlier, and users opening dead links currently receive a generic 'Page not found' error without understanding why.

# Goals

- Ensure invitations stop working after a set time period, defaulting to 7 days.[^s1][^c1]
- Provide clear feedback and next steps to users who access expired invitation links instead of showing 'Page not found'.[^s1][^c1]
- Allow administrators to resend invitations while invalidating any previously issued links.[^s1][^c2]

# Requirements

## R-01

**Must.** The product must expire invitation links automatically after a default period of 7 days.[^s1][^c1]

Rationale: Invitations must stop working after a while to prevent unauthorized access via old forwarded links.

Acceptance criteria:

- **AC-01**: Given an invitation sent 7 days ago by default, when a user accesses the invitation link after the 7-day period, then the invitation link is not accepted.

## R-02

**Must.** The product must allow admins to resend an invitation, which invalidates the previous link and issues a new token.[^s1][^c2]

Rationale: Resending replaces the old link; the old one must stop working, and the original token cannot be recovered from its hash.

Acceptance criteria:

- **AC-02**: Given an existing invitation, when an admin resends the invitation, then a new invitation link is created and the previous invitation link stops working.

## R-03

**Must.** The product must display a clear message stating that the invitation expired, along with a way to ask for a new one, when an expired link is opened.[^s1][^c1]

Rationale: Users currently see a generic 'Page not found' error and need clear feedback and a path forward.

## R-04

**Should.** The product should allow workspace owners to configure the invitation expiry period within a range of 1–30 days.[^s1]

Rationale: Workspace owners may need custom expiry policies tailored to their workspace.

# Assumptions

- Expiry checking will be handled via a new timestamp check during invitation acceptance.[^s1][^c2]
- Target release is before the enterprise trial ends in early November, though no firm date was agreed.[^s1]

# Open questions

- Do invitations that already exist get an expiry date at rollout, or keep working until used?[^s1]
- Is the expiry period set per workspace or once for the whole product?[^s1]
- Should the expired-link page show who sent the invitation?[^s1]
- How does invitation lookup by token hash behave when an invitation is resent?[^s1]

# Risks

- The admin settings screen may not be able to accommodate another configuration field in this cycle.[^s1]

# Out of scope

- Changing the email provider or email templates beyond the link itself.[^s1]
- SSO and SCIM provisioning.[^s1]

[^s1]: [Workspace onboarding sync](/meetings/2026-09-15-workspace-onboarding.md)
[^c1]: [Issue #1: Invitation lifecycle hardening](https://github.com/MohamedAliZouariEng/quire-demo/issues/1)
[^c2]: [ADR-0001: Invitation links carry single-use opaque tokens](/adr/0001-invitation-tokens.md)
