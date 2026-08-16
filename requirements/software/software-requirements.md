# Software Requirements — P9 "Org-Cockpit" (extension of platform baseline)

*Extends SWR-001–065. Language: English (D011). Status `reviewed` per DoD. Verification = tests + acceptance checklist; coverage lands with sprint 1. v1.0 Sprint 0, T-0001 — G1 pending (T-0002).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-066 | Each repo may carry a versioned profile file (`steckbrief.yaml`: description, status aktiv/abgeschlossen/pausiert); the cockpit API shall serve description and status per repo — status falling back to "abgeschlossen" when a `<repo>-v1.0` closure baseline tag exists and to "aktiv" otherwise; team repos derive their kind from `team.yaml`/registry (aspice/pm = fixed team, projekt = project team). | STK-019 | Unit tests (profile parsing, fallback logic, kind detection) + checklist | high | reviewed |
| SWR-067 | The cockpit view shall group cards into fixed teams / project teams / active projects / closed projects, the closed group collapsed by default with a clear "abgeschlossen" marking, usable on desktop and phone. | STK-019 | UI acceptance checklist (browser + phone) | high | reviewed |
| SWR-068 | Each cockpit card shall show the short description, a status pill, and the open (including recurring) tasks of that repo (count plus the open ticket titles, linked to the board). | STK-019 | API test (cockpit contains description/status/tasks) + UI checklist | high | reviewed |
| SWR-069 | Profile files shall be added for ALL existing repos (p0–p9, pm, team-mail, platform-as-catalog-entry excluded) with accurate one-line descriptions, committed per repo. | STK-019 | Acceptance checklist (every card shows a real description) | medium | reviewed |

## Traceability

STK-019 ← SWR-066–070, SWR-074, SWR-082, SWR-086, SWR-087, SWR-088, SWR-089 (complete; no orphans). DoD applied 2026-08-16 (RM). G1 pending (T-0002). v1.2: +SWR-074 (Betriebs-CR T-0006 aus pm/N-0012, PM-Beschluss B014). v1.3: +SWR-082 (Betriebs-CR pm/T-0012 aus pm/N-0015, PM-Beschluss B021). v1.4: +SWR-086/087 (Betriebs-CRs pm/T-0020 aus pm/N-0020 und pm/T-0021 aus platform/N-0003, PM-Beschlüsse B029/B030). v1.5: +SWR-088 (Betriebs-CR pm/T-0022 Teil 1 „Anlegen", Routine-Session 2026-08-16). v1.6: +SWR-089 (Betriebs-CR pm/T-0022 Teil 2 „Starten", Routine-Session 2026-08-16).

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

## Nachtrag v1.4 (pm/N-0020 + platform/N-0003, pm/T-0020 + pm/T-0021, PM-Beschlüsse B029/B030)

*Zwei Betriebs-CRs aus dem Briefkasten: der Projekt-Pool war nur eine Datei im Repo und im HMI nirgends zu sehen; und Ticketnummern wiederholen sich über die Repos hinweg (`T-0002` gibt es in `pm`, `p2` und `p10`), was jede projektübergreifende Ansicht mehrdeutig machte. Keine neue Projekt-Baseline — `p9-v1.0` bleibt Abnahmereferenz.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-086 | The project pool maintained by the PM team (`pm/management/projekt-pool.md`, pm/D005) shall be served read-only as its own backlog resource, split into the candidate categories of the source document (heading plus its table, parsed with the existing table parser rather than a second copy of that logic), and rendered as an own HMI tab next to the cockpit. A missing pool file shall be reported as such instead of raising, and sections without a table shall not produce empty cards. Creating and starting candidates from the HMI is explicitly **not** part of this requirement (it needs the P10 write path) and the view shall say so. | STK-019 | Unit tests (categories preserved with their tables, missing file handled, text-only section skipped) + UI checklist (tab shows the candidates on desktop and phone) | high | reviewed |
| SWR-087 | Ticket numbers are unique per repository only. Every API that exposes a ticket shall therefore also carry its unambiguous organisation-wide reference `<projekt>/T-xxxx`, derived in exactly **one** place on the server and reused by board, ticket detail, cockpit tasks, cockpit decision requests, inbox and decision history, so that the same number in two repositories can never be confused. The HMI shall display that reference wherever a ticket identifier is shown. Existing deep-links, ticket files and board tooling stay unchanged. | STK-019 | Unit tests (single derivation function, same number in two projects yields distinct references, board/detail/cockpit/inbox/history all carry it) + UI checklist | high | reviewed |

## Nachtrag v1.5 (pm/T-0022 Teil 1 „Anlegen", Routine-Session 2026-08-16)

*Betriebs-CR, direkte Fortsetzung von SWR-086: Der Pool war seit T-0020 nur lesbar. Setzt auf dem
P10-Schreibpfad auf (Commit-mit-Rücknahme-Muster aus `tickets.py`), baut aber keinen zweiten
Schreibmechanismus — eigenes Modul `backend/pool.py`, weil die Zieldatei kein Ticket ist. Der
zweite Teil des Auftrags ("Starten": Projektordner + G0-Decision-Request) ist bewusst **nicht**
Teil dieser Anforderung — größerer, riskanterer Schreibvorgang (neuer Ordner, Requirements-
Grundgerüst, und laut frischem Befund desselben Tages, `pm/T-0026`, CI-/Matrix-Workflows mit
fester Repo-Liste, die ein neuer Projektordner sonst unsichtbar bricht); gehört in eine eigene
Session mit eigenem Nachweis. `pm/T-0022` bleibt dafür offen. Keine neue Projekt-Baseline —
`p9-v1.0`/`p10-v1.0` bleiben Abnahmereferenz.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-088 | The Projekt-Pool tab shall offer a PIN-protected form to add a new candidate to either category (team or technical). A team candidate requires a short kebab-case name, a short description and the table's own fields (Nutzen, Voraussetzung); a technical candidate requires a free-text title and its own field (Quelle). New rows are appended at the end of their own category's table, sharing a single running number across both categories; duplicate candidate names are rejected. Every accepted candidate is written to `pm/management/projekt-pool.md` and committed in a single commit with recognizable origin ("Mensch via HMI"); a failing commit leaves the file unchanged, reported in plain German. The candidate appears in the Pool tab on the next read — no server restart required. | STK-019 | Unit tests (`platform/tests/test_pool_kandidat.py`: validation per category, cross-category numbering, end-of-category insertion, duplicate rejection, commit + rollback on failure, HTTP wiring) + UI checklist (form works on desktop and phone, PIN required remotely) | medium | reviewed |

**Nachweis:** 17 neue Unit-Tests (Gesamtsuite 285, vorher 268), jeder mit SWR-088-Bezug im
Docstring. Wiederverwendet statt neu gebaut: `aggregation.pool_abschnitte`/`parse_md_tabellen` zum
Lesen (Duplikat-Prüfung gegen die vorhandene Tabelle statt einer zweiten Parser-Kopie), das
Commit-mit-Rücknahme-Muster aus `tickets.py` zum Schreiben (Lesson 2026-08-16: keine zweite
Tabellen- oder Commit-Logik).

## Nachtrag v1.6 (pm/T-0022 Teil 2 „Starten", Routine-Session 2026-08-16)

*Direkte Fortsetzung von SWR-088 — derselbe Ticketauftrag, der zweite, größere Schreibvorgang.
Nur Technik-Kandidaten: Team-Kandidaten brauchen die vollere Team-Gründung aus `intake.md`
(Steckbrief, Profil, Datenklasse, Zugänge) und sind laut Ticket bewusst nicht im Umfang.
**Variante A** aus dem Ticket gebaut (keine Antwort auf die A/B-Rückfrage im Briefkasten, Default
laut Ticket) — der Knopf entscheidet nichts, er bereitet einen G0-Antrag vor (Playbook Kap. 16,
Klasse A bleibt beim Menschen). Projekt-Nummerierung und BOARD.md-Erzeugung laufen über dieselbe
Discovery/Generierung wie Board, Matrix und Preflight (`board.projekt_pfade`,
`board.generiere_board`) — keine zweite Kopie (Lesson p9/T-0007, pm/T-0026). Keine neue
Projekt-Baseline — `p9-v1.0`/`p10-v1.0` bleiben Abnahmereferenz.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-089 | The Projekt-Pool tab shall offer a way to "start" a technical candidate: it creates a new project folder `projects/p<N>` (next free number, derived from the same discovery board/matrix/preflight use) containing a draft project order (`docs/01-projektauftrag.md`), an empty decision log, a `steckbrief.yaml`, and a G0 decision-request ticket (`T-0001`, options G0a/G0b/G0c, one-week deadline, default G0a) plus its BOARD.md — folder and G0 request land in exactly one commit to the `projects` repo with recognizable origin ("Mensch via HMI"); a failing commit leaves nothing on disk. Team candidates are rejected with a plain-German pointer to the full team-founding path instead. On success the candidate is removed from the pool in a second commit to `pm`; if only that second commit fails, the already-committed project is kept (not rolled back) and the response says so in plain German instead of only logging it (lesson from pm/T-0024/B038: a silent failure mode is worse than a loud one). The button itself decides nothing — the human still answers the G0 request. | STK-019 | Unit tests (`platform/tests/test_pool_starten.py`: technical-only, numbering across top-level and collection repo, ticket validity, BOARD.md, pool removal, two commits with recognizable origin, rollback on failed project commit, project kept + plain-German warning on failed pool-removal commit, rejection of unknown/team candidates and of characters that would break the ticket frontmatter or table, HTTP wiring incl. PIN) + UI checklist (form works on desktop and phone, PIN required remotely, message shows the created G0 reference) | medium | reviewed |

**Nachweis:** 20 neue Unit-Tests (Gesamtsuite 305, vorher 285), jeder mit SWR-089-Bezug im
Docstring. Wiederverwendet statt neu gebaut: `board.projekt_pfade` zur Projekt-Discovery/-
Nummerierung (dieselbe Quelle wie Preflight/Matrix), `board.lade_tickets`/`board.validiere_alle`/
`board.generiere_board` zum Prüfen und Rendern des neuen G0-Tickets (keine zweite Board-Logik).
