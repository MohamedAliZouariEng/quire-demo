---
type: BRD
title: 'Workspace Invitation Lifecycle Hardening: Expiry, Resending, and Error Handling'
description: 'Business requirements drafted from the cited sources: 5 requirements,
  each citing the material it came from.'
tags:
- brd
- requirements
status: stable
generated:
  by: ichnos/gemini-3.8-flash
  at: '2026-09-19T22:28:17Z'
sources:
- id: s1
  resource: /meetings/2026-09-15-workspace-onboarding.md
  title: Workspace onboarding sync
- id: c4
  resource: https://github.com/MohamedAliZouariEng/quire-demo/issues/1
  title: 'Issue #1: Invitation lifecycle hardening'
- id: c2
  resource: /adr/0001-invitation-tokens.md
  title: 'ADR-0001: Invitation links carry single-use opaque tokens'
- id: c3
  resource: /project/product-overview.md
  title: Quire product overview
- id: c1
  resource: /project/glossary.md
  title: Onboarding glossary
verified:
  by: human:MohamedAliZouariEng
  at: '2026-09-19T22:54:45Z'
ichnos:
  artifact_id: 115f16f1-17f0-467c-9764-fbb70c3780eb
  run_id: 7a1550a1-1406-438f-9d51-6a3e5a66bc6a
  requirement_ids:
  - R-01
  - R-02
  - R-03
  - R-04
  - R-05
  epic:
    number: 6
    url: https://github.com/MohamedAliZouariEng/quire-demo/issues/6
  stories:
  - key: S-1
    number: 7
    url: https://github.com/MohamedAliZouariEng/quire-demo/issues/7
  - key: S-2
    number: 8
    url: https://github.com/MohamedAliZouariEng/quire-demo/issues/8
  - key: S-3
    number: 9
    url: https://github.com/MohamedAliZouariEng/quire-demo/issues/9
  - key: S-4
    number: 10
    url: https://github.com/MohamedAliZouariEng/quire-demo/issues/10
resource: https://github.com/MohamedAliZouariEng/quire-demo/issues/6
---

# Summary

Invitation links currently never expire, allowing unauthorized or unintended access via old links, and users attempting to access unusable or dead invitation links only see a generic 'Page not found' error.

# Goals

- Ensure invitations stop working after a defined period of time.[^s1][^c4]
- Provide clear feedback to users when an invitation link has expired, along with a way to ask for a new invitation.[^s1][^c4]
- Allow administrators to resend invitations, invalidating previous links.[^s1]

# Requirements

## R-01

**Must.** The product must expire invitation links after 7 days by default.[^s1][^c4]

Rationale: Invitations must stop working after a while so that old links cannot be used indefinitely to join workspaces.

Acceptance criteria:

- **AC-01**: Given an invitation link sent 7 or more days ago, when a user opens the link, then the link cannot be used to join the workspace.

## R-02

**Must.** The product must allow workspace owners and admins to resend an invitation, which invalidates the previous invitation link and issues a new one.[^s1][^c2][^c3]

Rationale: Admins need the ability to invite users again if a link was missed or expired, and replacing the link ensures the old token cannot be used.

Acceptance criteria:

- **AC-02**: Given an existing pending invitation, when an admin resends the invitation, then a new invitation link is issued and the previous invitation link stops working.

## R-03

**Must.** The product must display a clear error message stating that the invitation expired when an invitee opens an expired invitation link, instead of a generic 'Page not found' error.[^s1][^c3][^c4]

Rationale: Users who open dead links today receive an unhelpful generic error and do not understand why the link failed.

Acceptance criteria:

- **AC-03**: Given an invitation link that has expired, when an invitee navigates to the link, then the system displays a clear message stating the invitation has expired instead of a generic 'Page not found'.

## R-04

**Must.** The product must provide a way for an invitee on an expired invitation page to ask for a new invitation.[^s1]

Rationale: Users whose links have expired need a path to request a replacement invitation.

Acceptance criteria:

- **AC-04**: Given a user viewing an expired invitation error page, when reviewing the page, then the user is presented with a way to ask for a new invitation.

## R-05

**Should.** The product should allow workspace owners to configure the invitation expiry duration between 1 and 30 days.[^s1]

Rationale: Lina proposed that workspace owners be able to customize the expiry setting, while Omar suggested limiting the range to 1–30 days.

Acceptance criteria:

- **AC-05**: Given a workspace owner in settings, when changing the invitation expiry duration, then values between 1 and 30 days are accepted.

# Assumptions

- Invitation tokens remain single-use and hashed, requiring resend operations to generate entirely new tokens.[^s1][^c1][^c2]
- The target delivery for the feature is before the enterprise trial ends in early November.[^s1]

# Open questions

- Do invitations that already exist get an expiry date at rollout, or keep working until used?[^s1]
- Is the expiry period set per workspace or once for the whole product?[^s1]
- Should the expired-link page show who sent the invitation?[^s1]
- Can the admin settings screen accommodate another field this cycle?[^s1]
- How does invitation lookup by token hash behave when an invitation is resent?[^s1]

# Risks

- Engineering capacity constraints may prevent adding a new configuration field to the admin settings screen during this cycle.[^s1]

# Out of scope

- Changing the email provider or email templates beyond the link itself.[^s1]
- SSO and SCIM provisioning.[^s1]

[^s1]: [Workspace onboarding sync](/meetings/2026-09-15-workspace-onboarding.md)
[^c4]: [Issue #1: Invitation lifecycle hardening](https://github.com/MohamedAliZouariEng/quire-demo/issues/1)
[^c2]: [ADR-0001: Invitation links carry single-use opaque tokens](/adr/0001-invitation-tokens.md)
[^c3]: [Quire product overview](/project/product-overview.md)
[^c1]: [Onboarding glossary](/project/glossary.md)
...............................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................
