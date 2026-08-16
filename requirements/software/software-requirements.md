# Software Requirements — P9 "Org-Cockpit" (extension of platform baseline)

*Extends SWR-001–065. Language: English (D011). Status `reviewed` per DoD. Verification = tests + acceptance checklist; coverage lands with sprint 1. v1.0 Sprint 0, T-0001 — G1 pending (T-0002).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-066 | Each repo may carry a versioned profile file (`steckbrief.yaml`: description, status aktiv/abgeschlossen/pausiert); the cockpit API shall serve description and status per repo — status falling back to "abgeschlossen" when a `<repo>-v1.0` closure baseline tag exists and to "aktiv" otherwise; team repos derive their kind from `team.yaml`/registry (aspice/pm = fixed team, projekt = project team). | STK-019 | Unit tests (profile parsing, fallback logic, kind detection) + checklist | high | reviewed |
| SWR-067 | The cockpit view shall group cards into fixed teams / project teams / active projects / closed projects, the closed group collapsed by default with a clear "abgeschlossen" marking, usable on desktop and phone. | STK-019 | UI acceptance checklist (browser + phone) | high | reviewed |
| SWR-068 | Each cockpit card shall show the short description, a status pill, and the open (including recurring) tasks of that repo (count plus the open ticket titles, linked to the board). | STK-019 | API test (cockpit contains description/status/tasks) + UI checklist | high | reviewed |
| SWR-069 | Profile files shall be added for ALL existing repos (p0–p9, pm, team-mail, platform-as-catalog-entry excluded) with accurate one-line descriptions, committed per repo. | STK-019 | Acceptance checklist (every card shows a real description) | medium | reviewed |

## Traceability

STK-019 ← SWR-066–070, SWR-074, SWR-082 (complete; no orphans). DoD applied 2026-08-16 (RM). G1 pending (T-0002). v1.2: +SWR-074 (Betriebs-CR T-0006 aus pm/N-0012, PM-Beschluss B014). v1.3: +SWR-082 (Betriebs-CR pm/T-0012 aus pm/N-0015, PM-Beschluss B021).

## Nachtrag v1.1 (pm/D003, N-0008)

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-070 | Discovery, board tooling, cockpit and baselines shall support project folders nested inside the `projects` collection repo (a project = folder with `tickets/` whose enclosing git root is `projects`); board status transitions, commits and closure tags (`p10-v1.0`) operate on the enclosing repo; existing top-level repos keep working unchanged. | STK-019 | Unit tests (nested discovery, board ops on enclosing repo) + checklist | high | reviewed |

## Nachtrag v1.2 (pm/N-0012, PM-Beschluss B014)

*Betriebs-CR nach der P9-Abnahme: wiederkehrende von einmaligen Aufgaben unterscheidbar machen. Keine neue Projekt-Baseline — `p9-v1.0` bleibt Abnahmereferenz.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-074 | Tickets shall carry an optional `takt:` field from a fixed vocabulary (per-session, daily, weekly, monthly, quarterly, yearly); the board generator shall validate it, show it as its own column (one-off tickets read "einmalig") and count the recurring ones in the board header. Board cards, ticket detail and the cockpit task list shall mark recurring tickets in plain German, so a permanently open ticket is recognisable as an intentional standing duty rather than a stalled one-off. Tickets without the field behave exactly as before. | STK-019 | Unit tests (valid/invalid cadence, board column and header count, one-off unchanged, aggregation passes the field through) + UI checklist | medium | reviewed |

## Nachtrag v1.3 (pm/N-0015, pm/T-0012, PM-Beschluss B021)

*Betriebs-CR nach der P9-Abnahme: der Kopfbereich listete alle entdeckten Repos in einem Dropdown, das Cockpit dagegen nur die relevanten Gruppen. Keine neue Projekt-Baseline — `p9-v1.0` bleibt Abnahmereferenz.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-082 | The navigation groups (fixed teams / project teams / active projects / closed projects) shall be derived **once** on the server from the same profile-and-baseline classification the cockpit uses, and be served as an ordered navigation resource; the HMI header shall render the active groups as directly clickable entries with the current one highlighted, keep closed projects reachable behind a collapsed "weitere (n)" toggle (auto-expanded when the current project sits in it), and leave hash deep-links (`#/board/p3`, including links to closed projects) working unchanged. Empty groups shall not be rendered. | STK-019 | Unit tests (classification shared with cockpit, ordering, closed projects separated, empty groups omitted, nested projects included) + UI checklist (header shows only active entries, click navigates, deep-link to a closed project still resolves) | high | reviewed |
