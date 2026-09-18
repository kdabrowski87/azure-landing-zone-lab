# Landing Zone Roadmap

This roadmap tracks the sequence of architecture decisions for the Contoso Retail Azure Landing Zone.

Order and scope are derived from [company.md](company.md) (see section 17 "Initial Platform Scope" and section 21 "Next Architecture Decision"). Each item is mapped to the relevant [Cloud Adoption Framework](https://learn.microsoft.com/azure/cloud-adoption-framework/) phase for learning purposes.

CAF phases used below: **Strategy**, **Plan**, **Ready** (build the landing zone), **Govern** (policy/RBAC/compliance), **Manage** (day-2 operations).

| # | Topic | CAF Phase | ADR | Status |
|---|-------|-----------|-----|--------|
| — | Business context & requirements | Strategy / Plan | [company.md](company.md) | Done |
| 1 | Management group hierarchy | Ready | [ADR-0001](decisions/ADR-0001-management-group-hierarchy.md) | Decided |
| 2 | Subscription organization / model | Ready | ADR-0002 | Not started |
| 3 | Azure Policy baseline | Govern | ADR-0003 | Not started |
| 4 | Platform RBAC model | Govern | ADR-0004 | Not started |
| 5 | Shared connectivity design (networking) | Ready | ADR-0005 | Not started |
| 6 | Central management & monitoring design | Manage | ADR-0006 | Not started |
| 7 | Infrastructure as Code deployment model | Ready | ADR-0007 | Not started |
| 8 | CI/CD pipeline structure | Ready | ADR-0008 | Not started |
| 9 | Application Landing Zone onboarding approach | Ready / Govern | ADR-0009 | Not started |

## How we work through each item

1. Explain the concept plainly (what/why/options) and relate it to the current CAF phase.
2. Ask clarifying questions specific to Contoso Retail's context — decisions aren't made without your input.
3. Record the agreed decision as an ADR in `docs/decisions/` (using a standard ADR template: Context, Decision, Consequences, Alternatives considered).
4. Update this roadmap's status column.
5. Only once an ADR is settled, optionally implement it as Bicep/pipeline code in the matching repo folder (`management/`, `platform/`, `connectivity/`, `pipelines/`, etc.).

## Status legend

- **Not started** – not yet discussed
- **In progress** – actively being designed
- **Decided** – ADR written and accepted
- **Implemented** – Bicep/pipeline code exists for this decision
