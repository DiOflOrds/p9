# Software Requirements — P9 "Org-Cockpit" (extension of platform baseline)

*Extends SWR-001–065. Language: English (D011). Status `reviewed` per DoD. Verification = tests + acceptance checklist; coverage lands with sprint 1. v1.0 Sprint 0, T-0001 — G1 pending (T-0002).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-066 | Each repo may carry a versioned profile file (`steckbrief.yaml`: description, status aktiv/abgeschlossen/pausiert); the cockpit API shall serve description and status per repo — status falling back to "abgeschlossen" when a `<repo>-v1.0` closure baseline tag exists and to "aktiv" otherwise; team repos derive their kind from `team.yaml`/registry (aspice/pm = fixed team, projekt = project team). | STK-019 | Unit tests (profile parsing, fallback logic, kind detection) + checklist | high | reviewed |
| SWR-067 | The cockpit view shall group cards into fixed teams / project teams / active projects / closed projects, the closed group collapsed by default with a clear "abgeschlossen" marking, usable on desktop and phone. | STK-019 | UI acceptance checklist (browser + phone) | high | reviewed |
| SWR-068 | Each cockpit card shall show the short description, a status pill, and the open (including recurring) tasks of that repo (count plus the open ticket titles, linked to the board). | STK-019 | API test (cockpit contains description/status/tasks) + UI checklist | high | reviewed |
| SWR-069 | Profile files shall be added for ALL existing repos (p0–p9, pm, team-mail, platform-as-catalog-entry excluded) with accurate one-line descriptions, committed per repo. | STK-019 | Acceptance checklist (every card shows a real description) | medium | reviewed |

## Traceability

STK-019 ← SWR-066–070, SWR-074, SWR-082, SWR-086, SWR-087, SWR-088, SWR-089, SWR-091, SWR-102, SWR-103, SWR-104, SWR-105, SWR-106, SWR-107 (complete; no orphans). DoD applied 2026-08-16 (RM). G1 pending (T-0002). v1.2: +SWR-074 (Betriebs-CR T-0006 aus pm/N-0012, PM-Beschluss B014). v1.3: +SWR-082 (Betriebs-CR pm/T-0012 aus pm/N-0015, PM-Beschluss B021). v1.4: +SWR-086/087 (Betriebs-CRs pm/T-0020 aus pm/N-0020 und pm/T-0021 aus platform/N-0003, PM-Beschlüsse B029/B030). v1.5: +SWR-088 (Betriebs-CR pm/T-0022 Teil 1 „Anlegen", Routine-Session 2026-08-16). v1.6: +SWR-089 (Betriebs-CR pm/T-0022 Teil 2 „Starten", Routine-Session 2026-08-16). v1.7: +SWR-091 (Betriebs-CR pm/T-0030 aus Brief pm/N-0025, PM-Beschluss B044, Routine-Session 2026-08-16). v1.8: +SWR-102 (Betriebs-CR pm/T-0040 aus den Briefen pm/N-0032/N-0033, Routine-Session 2026-08-16 21:06). v1.9: +SWR-103 (Betriebs-CR pm/T-0016 nach pm/D006 — Sprint-Workflow-Sicht, Routine-Session 2026-08-16 22:19). v1.10: +SWR-104 (Betriebs-CR pm/T-0032 Teil 2 aus Brief pm/N-0025 — Uhrzeit-Takt, Routine-Session 2026-08-16 23:06). v1.11: +SWR-105 (Betriebs-CR platform/T-0003 aus der Auftraggeberfrage vom 2026-08-17 — CI-Status ohne Zugangsdaten prüfen). v1.12: +SWR-106 (Betriebs-CR pm/T-0041 — Terminierung auf Sprints statt auf Kalenderdaten). v1.13: +SWR-107 (platform/T-0004 — ein rotes CI-Ergebnis nennt den fehlgeschlagenen Schritt; Anlass: der erste Hostlauf von SWR-105 fand drei rote Repos und konnte für zwei die Ursache nicht nennen).

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

## Nachtrag v1.7 (Betriebs-CR pm/T-0030 aus Brief pm/N-0025, PM-Beschluss B044)

*Der Auftraggeber: „offene aufgaben müssen erledigt werden, beim PM gibts welche, die offen
sind, werden aber nicht gemacht, diese müssen auch terminiert werden." Belegt an `pm/T-0025`
(sechs Sessions offen, Agenda nannte es die ganze Zeit — als Randnotiz). Ursache: Nur
Decision-Requests hatten ein Zeitkonzept (`frist`/`default`); ein CR mit `prio: mittel` konnte
beliebig lange liegen, ohne dass ein Werkzeug das gemeldet hätte. Die Frist-Ampel existierte
bereits — als Inline-Kopie in `aggregation.cockpit`, nur für DRs. Diese Anforderung führt sie
zusammen, statt sie ein zweites Mal zu schreiben (Lesson B033). Kein neuer Takt und keine
Änderung am BOARD.md-Format: Formatänderungen am Board haben am 16.08. schon einmal alle
Prüf-Workflows rot gemacht und gehören gebündelt zu `pm/T-0013`.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-091 | Backlog tickets of every type shall be allowed to carry an optional `frist` (deadline), and that deadline shall be validated for every type — not only for decision-requests, where a typo previously fell back silently to "no deadline". Validation shall reject dates that merely look right but are not real calendar days (`2026-13-01`), for `frist` and `erstellt` alike, through one shared check. The deadline-to-traffic-light rule (red = passed, yellow = due within two days, green = later, grey = none or unreadable) shall exist exactly once (`board.frist_ampel`) and shall be used both by the open decision-requests and by the backlog deadlines; a ticket counts as overdue only while it is still open (`board.ist_ueberfaellig`) — a passed deadline on a closed ticket is history, not an accusation. Each cockpit card shall show its overdue tickets in full and ahead of the status counts (never folded into the three-item task list), each with deadline and days over, plus a count of open, non-recurring backlog tickets that carry no deadline at all ("ohne Frist") so that an untimed ticket is named as untimed instead of passing as merely open. | STK-019 | Unit tests (`test_board.py::FristTest`: traffic-light steps incl. day-by-day equivalence with the removed inline copy, overdue only while open, no deadline = never overdue, deadline validated for change-request/problem/task, decision-request regression, impossible dates; `test_org_cockpit.py::UeberfaelligTest`: overdue list with days-over, closed tickets excluded, untimed counter excludes recurring tickets, DR traffic light comes from `board.frist_ampel`) + UI checklist (cockpit card shows the overdue block above the status pills, on desktop and phone) | high | reviewed |

**Nachweis:** 11 neue Unit-Tests (Gesamtsuite 329, vorher 318), jeder mit SWR-091-Bezug im
Docstring. **Gegenprobe geführt:** gegen den Altstand (Frist-Prüfung nur im
decision-request-Zweig, reine Formprüfung des Datums, Ampel inline im Cockpit) scheitern
`test_frist_wird_auch_bei_change_request_geprueft`,
`test_unmoegliches_datum_faellt_nicht_auf_grau_zurueck` und
`test_ueberfaelliges_backlog_ticket_steht_in_der_kachel` nachweislich.
**Zusammengeführt statt kopiert:** `aggregation.cockpit` rechnet die DR-Ampel nicht mehr
selbst, sondern fragt `board.frist_ampel` — dieselbe Funktion, die die Backlog-Fristen
bewertet; ein Test vergleicht beide über einen ganzen Monat Tag für Tag.
**Bewusst nicht enthalten:** der Uhrzeit-Takt („jeden Tag um 14 Uhr") aus demselben Brief —
er berührt F14 (Session-Takt, p0/D027) und ist als `pm/T-0032` mit eigener Frist getrennt
eingeplant, damit keine dritte Taktlogik neben Session- und team-mail-Takt entsteht.

## Nachtrag v1.8 (pm/N-0032 + pm/N-0033, pm/T-0040, Routine-Session 2026-08-16 21:06)

*Betriebs-CR: Der Auftraggeber will nach jedem geplanten Lauf in Mission Control lesen, was
passiert ist, statt es in Cowork nachzuschlagen. Die Zusammenfassung existiert bereits — jede
Routine-Session schreibt sie in `pm/management/session-agenda.md`. Es wird **kein zweiter Text**
erzeugt, sondern der vorhandene ausgeliefert (B033). Kein neuer Takt, keine Änderung am
`BOARD.md`-Format (`pm/T-0036`/`T-0038` bleiben davon unberührt).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-102 | Mission Control shall serve, and show on the cockpit page above every project card, what the last routine session did: the "Das Wichtigste" block taken verbatim from `pm/management/session-agenda.md`, the commit timestamp of that file, and the number of times the file was written on the current day. The timestamp and the daily count shall be derived from the **git history** and never from the text of the file — a stale file left behind by a missed run would otherwise present its own old "Stand:" line as current (B038); the block's heading line, which carries that text timestamp, shall therefore not be part of the payload. The block heading shall be recognised by its beginning, not by its exact wording (lesson L-2026-08-16h/B054). When the last commit is older than two cadences (2 × 30 min) or unreadable, the tile shall say so in plain German ("seit HH:MM keine Session") instead of showing the old state as fresh; an unreadable timestamp counts as stale, never as fresh. No second copy of the summary shall be written anywhere. Additionally, the letterbox send button shall stay disabled until the conversation has been redrawn, so that a second click in the reload window cannot create a duplicate letter — the click is prevented, no letter is ever silently filtered (B050). | STK-019 | Unit tests (`test_session_kachel.py`: block cut at the next divider, heading with "Stand" excluded, heading recognised by prefix in three wordings, missing block yields empty instead of a substitute text, staleness at the two-cadence boundary day-by-day, unreadable timestamp counts as stale, naive/aware datetime comparison, daily count only for the current day, commit timestamp wins over the text timestamp, missing file and missing git repo do not raise, `GET /api/session` end-to-end) + UI checklist (tile is the first thing on the cockpit page on desktop and phone; double-click on send produces one letter) | high | reviewed |

**Nachweis:** 17 neue Unit-Tests (Gesamtsuite **353**, vorher 336), jeder mit SWR-102-Bezug im
Docstring. **Gegenprobe geführt — und die erste war wertlos:** gegen den Altstand scheitert die
Testdatei mit `ImportError: cannot import name 'session'`. Das belegt nur, dass ein Modul fehlt,
nichts über den Schaden — wörtlich die Lehre **L-2026-08-16h** aus derselben Session. Die zweite
Gegenprobe läuft deshalb über den **echten Abrufweg**: der Server aus `git archive HEAD`,
gegen dieselbe Agenda-Datei gestartet, beantwortet `GET /api/session` mit
**HTTP 404 „unbekannter Endpunkt"** — die Zusammenfassung war über die HMI nicht abrufbar, und
genau das ist die Beschwerde aus `pm/N-0032`/`N-0033`.

**Bewusst abweichend von der DoD des Tickets (Befund B056):** `pm/T-0040` DoD 1 verlangt „die Zahl
der **Sessions** des Tages". Geliefert wird `fortschreibungen_heute` — die Zahl der **Commits** auf
die Agenda. Grund: eine Session schreibt die Datei mehrfach (am 16.08.: **42 Commits** auf rund 30
Läufe), und Commits über eine Zeitlücke zu Sessions zu bündeln unterschätzt nachweislich — zwischen
`16:35:24` und `16:51:41` liegen 16 Minuten und **zwei verschiedene** Sessions. Eine Zahl, die sich
wie eine Messung liest und eine Heuristik ist, wäre B027/B038. Gezählt wird, was belegbar ist, und
das Feld heißt auch so.

## Nachtrag v1.9 (pm/D006, pm/T-0016, Routine-Session 2026-08-16 22:19)

*Betriebs-CR: Mit `pm/D006` ist jeder Routine-Lauf ein vollwertiger Genesis-Gesamtsprint; der PM
plant alle offenen Aufgaben aller Repos in `pm/management/sprint-aktuell.md`. Diese Workflow-Sicht
existierte nur als Datei — kein HMI-Endpunkt hat sie ausgeliefert. Es wird **kein zweiter Text**
erzeugt (B033). Kein neuer Takt, keine Änderung am `BOARD.md`-Format (`pm/T-0036`/`T-0038` bleiben
unberührt).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-103 | Mission Control shall serve, and show on the cockpit page directly below the "Letzte Session" tile, the current Genesis sprint plan taken from `pm/management/sprint-aktuell.md`: the rows of the plan table (task, role, due, status, reason) and the "Das Wichtigste" block of that same file. The plan table shall be located by a heading recognised **by its beginning** ("## Sprint-Plan…"), not by its exact wording (lesson L-2026-08-16h/B054), and the first table following that heading shall be used. Its timestamp shall come from the **git commit** of the file and never from its text; after two silent cadences (2 × 30 min) or an unreadable timestamp the view shall say the plan is stale rather than present it as current (B038). Each row shall carry a traffic light derived from the existing rule (`board.frist_ampel`): overdue red, ≤ 2 days yellow, later green, no date grey; the named states "dieser Sprint" and "wartet-auf-Mensch" are **not** dates and shall never be rendered green. **The view shall cross-check the plan against the actual backlog:** every ticket that is open (status not `done`/`rejected`) in any discovered repo and appears in **no** plan row shall be reported as `nicht_geplant` with ref and title, and counted. No second copy of the plan shall be written anywhere; the file the session already writes is the only source. | STK-019 | Unit tests (`test_sprint_sicht.py`: heading recognised by prefix in three wordings, first table after the heading wins, table before the heading ignored, missing heading yields an empty plan instead of a substitute, named states not green, date states use the shared `frist_ampel` rule, counters per state, `nicht_geplant` finds a ticket missing from the plan, a fully planned backlog yields an empty `nicht_geplant`, refs written in either `repo/T-xxxx` or bare form both match, staleness reuses the SWR-102 rule, missing file and missing git repo do not raise, `GET /api/sprint` end-to-end) + UI checklist (tile sits under "Letzte Session" on desktop and phone; a ticket left out of the plan is visible without opening anything) | high | reviewed |

## Nachtrag v1.10 (pm/N-0025 Teil 2, pm/T-0032, Routine-Session 2026-08-16 23:06)

*Betriebs-CR: „wiederkehrende aufgaben müssen auch terminiert werden, dann diese erledigt werden
(z.b. jeden tag, woche um 14 Uhr..)". Teil 1 des Briefs ist SWR-091; dieser Nachtrag trägt den
Rest. Die Abgrenzung stand vorher schriftlich (`pm/T-0032` Teil 1): **was ohne laufende Session
feuern muss, gehört zum Host-Scheduler; was nur bemerkt werden muss, ans Ticket.** Der Uhrzeit-Takt
ist deshalb **keine dritte Taktlogik** neben F14 (`p0/D027`) und den team-mail-Takten
(SWR-063/064), sondern eine Fälligkeitsfrage — er startet nichts, er meldet nur. Keine Änderung am
`BOARD.md`-Format (`pm/T-0036`/`T-0038` bleiben unberührt).*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-104 | The `takt` field shall additionally accept a time of day (`taeglich@HH:MM`, `woechentlich@<Mo–So>-HH:MM`), validated by the board generator; a time shall be accepted **only** for the daily and weekly cadence, because for monthly and longer cadences no rule exists for which day is meant and inventing one would be guessing. Tickets without a time shall behave exactly as before. Tickets shall carry an optional `zuletzt_erledigt` (date, or date and time) recording the progress of a recurring task — a field that is meaningless without `takt` and shall therefore be rejected without it. A recurring ticket shall count as **due** when its cadence time has passed since that last completion; **a missing, unreadable or time-less completion counts as never/earliest done, never as fresh** (a date without a time proves only the start of that day), mirroring the "stale unless proven otherwise" rule of `session.stille`. The derived deadline shall be routed through the **existing** traffic-light rule (`board.frist_ampel`) — one rule, two sources; a second computation would be B033. For that, the traffic light shall compare at **moment** precision instead of day precision, because "today 14:00" is past at 15:00 while the day is not; the statement for pure date deadlines shall stay identical day by day (a date deadline expires at the end of its day), and where only a day is known the deadline counts as passed rather than fresh. Cadence due-ness and traffic light are two facts and shall not be folded into one (B057): the cockpit shall list by due-ness, not by colour. **Widening the shared rule shall carry its neighbours with it:** every consumer of a deadline value shall read it through the same shared parser, and the ticket editor shall offer a ticket's own cadence value in its vocabulary, so that a deadline with a time neither breaks the cockpit nor gets silently dropped when an unrelated field is saved. Each cockpit card shall show its due recurring tickets in full alongside the overdue deadlines, naming the **skipped** cadence moment ("überfällig seit HH:MM") rather than claiming completion — if no session runs, nothing fires, and the display shall say so (B038). | STK-019 | Unit tests (`test_board.py::TaktUhrzeitTest`: existing cadences unchanged, syntax split, invalid times and cadences rejected incl. `monatlich@…`, validation of `takt` and `zuletzt_erledigt`, `zuletzt_erledigt` without `takt` rejected, missing completion counts as due, completion before/after the moment, missed session yields the skipped moment and red, date-only completion counts from the start of day, weekly cadence picks the right weekday and steps by 7 days, closed tickets never due, traffic light taken from `frist_ampel`, day-by-day equivalence with the pre-SWR-104 date rule over a full month × month, same-day time deadline red in the afternoon, day-as-reference counts as passed, board column carries the time without changing the column count; `test_org_cockpit.py::TaktFaelligTest`: due cadence in the card with skipped moment and plain-text cadence, cadences without a time excluded, same day/two moments yields two different answers, missing proof counts as due, **a deadline carrying a time does not break the card**; `test_p10_editor.py`: the editor offers the ticket's own time cadence so that saving another field cannot silently drop it) + UI checklist (the card names the skipped moment on desktop and phone) | medium | reviewed |

**Nachweis:** 20 neue Unit-Tests (Gesamtsuite **400**, vorher 380), jeder mit SWR-104-Bezug im
Docstring. **Gegenprobe über den echten Abrufweg geführt, nicht über einen Import** (L-2026-08-16h):
dieselbe Testwelt, dasselbe Ticket (`takt: taeglich@14:00`, `zuletzt_erledigt: 2026-08-15 14:30`),
beide Server antworten auf `GET /api/cockpit` mit **HTTP 200** — der Server aus `git archive HEAD`
meldet `ueberfaellig: []`, `unterminiert: 0` und **kein Feld** `takt_faellig`. Das Ticket sah über
die HMI **kerngesund** aus, während sein 14:00-Termin seit Stunden versäumt war; der Neustand
meldet an derselben Stelle `seit: 2026-08-16 14:00`, `ampel: rot`. Zweite Gegenprobe über die
**Skript-Route**, die auch die CI fährt: `board.py --check` beendet sich im Altstand mit **exit 1**
(*„ungültiger takt: taeglich@14:00"*) und im Neustand mit **exit 0** — der Wunsch aus dem Brief war
vorher nicht nur unbeantwortet, er war **nicht aufschreibbar**.

**Der Befund dieses Laufs (B058), in eigener Sache.** Die Umstellung von der Tages- auf die
Momentregel war nicht geplant und ist beim Schreiben des ersten Tests aufgefallen: der abgeleitete
Termin „heute 14:00" hätte um 15:00 die Farbe **gelb** („heute fällig") bekommen, weil
`frist_ampel` Tage vergleicht. Damit hätte ausgerechnet der versäumte Takt so ausgesehen wie ein
noch offener — dieselbe Faltung zweier Fakten wie in **B057**. Die Regel liegt jetzt auf Momenten,
und ein Test vergleicht beide Fassungen für reine Datumsfristen **Tag für Tag über einen ganzen
Monat gegen jeden Bezugstag desselben Monats** (961 Vergleiche), damit die Erweiterung die
Bedeutung von SWR-091 nicht verschiebt.

**Bewusst nicht enthalten:** ein Scheduler. Läuft keine Session, feuert nichts — die Anzeige sagt
dann „überfällig seit HH:MM". Das ist die ehrliche Grenze dieser Umsetzung (T-0032 Teil 1,
Entscheidung 4) und keine stille Falschaussage (B038). Eine Aufgabe, die **ohne** Session laufen
muss, gehört in die Windows-Aufgabenplanung neben den Mail-Autopiloten — nicht in das `takt`-Feld.

**Nachtrag zum Nachweis — B059, gefunden von der Gegenprüfung, nicht von der Suite.** Eine
unabhängige Prüfung des Commits fand **zwei** Stellen, an denen die Erweiterung der geteilten
Regel ihre Nachbarn zurückgelassen hatte, und **alle 400 Tests waren dabei grün**:

1. `aggregation.cockpit` filterte über `board.ist_ueberfaellig` (liest die Frist seit SWR-104 über
   `als_moment`, akzeptiert also eine Uhrzeit), berechnete die Tage-über daneben aber weiter mit
   `date.fromisoformat`. Ein Ticket mit `frist: 2026-08-15 14:00` kam durch den Filter und ließ die
   Berechnung mit `ValueError` platzen — **erst nach Ablauf des Termins**, und weil `cockpit_alle`
   über alle Projekte läuft, riss es die **gesamte** Cockpit-Seite mit (nach außen als irreführendes
   **HTTP 404 „unbekanntes Projekt"**). Vor SWR-104 fiel derselbe Wert harmlos auf „grau".
2. Der Ticket-Editor (P10-Schreibpfad) baut sein `<select>` aus `vokabular.takte`. Ein
   Uhrzeit-Takt stand dort nicht — der Browser hätte auf „einmalig" zurückgesetzt und das Speichern
   eines **beliebigen anderen Feldes** hätte den Takt stillschweigend gelöscht (B051/B038).

Beides ist behoben und mit je einem Regressionstest belegt (Suite **402**). Die Gegenprobe läuft
gegen den Commit, der den Fehler trug: `test_frist_mit_uhrzeit_laesst_die_kachel_nicht_platzen`
scheitert dort nachweislich.

## Nachtrag v1.11 (Auftraggeberfrage 2026-08-17, platform/T-0003)

*Betriebs-CR: „Was muss ich tun, damit der Configmanager GitHub-Commits selbst überprüft?" Antwort
auf die Rechtefrage: **nichts** — die Repos unter `DiOflOrds` sind öffentlich, die Actions-API
antwortet ohne Anmeldung. Damit entfällt der Klasse-A-Vorgang (Zugänge, Playbook Kap. 16)
vollständig; es bleibt reine Werkzeugarbeit. Der Abruf läuft **auf dem Host**, nicht in der
Cowork-Sandbox: die hat keinen GitHub-Zugang, und ein Geheimnis gäbe es hier ohnehin nicht zu
verwahren. Schließt die Mensch-Aufgabe aus `pm/T-0010`, `pm/T-0013` und `pm/T-0026`
(„ein Blick auf die Actions-Seite").*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-105 | The organisation shall be able to verify from the host, **without any GitHub credentials**, whether the CI runs for the commits it has just pushed finished successfully. A check script shall derive the repositories to inspect from the existing discovery — a repository qualifies only if it has both an `origin` remote and at least one workflow file — and shall report per repository exactly one state: green **for the pushed commit**, red, still running, or no run yet for that commit. **A run that is green for a different commit shall never count as green for the current one:** the run's head SHA shall be matched against the local commit, and "no run yet" shall be reported as such and never folded into green — the same "stale unless proven fresh" rule as `session.stille` and `zuletzt_erledigt`. A repository carrying a workflow file but **no remote** shall be reported as "no CI expected" instead of being silently skipped, so that a gate which exists only as a file is visible as one. Because the repositories are public the check shall use the **unauthenticated** Actions API and shall therefore hold a request budget across its polling rounds; an exhausted rate limit shall be reported in its own words as an error and never as "no run". The result shall be written **outside** the git repositories — so that checking never dirties a working copy — in both machine-readable and plain-German form, and the script shall exit non-zero unless every inspected repository is green for the pushed commit. It shall replace the five browser tabs of `abschluss.cmd` step [5/5]. | STK-019 | Unit tests (`test_ci_status.py`, all with an injected fetch function — see the note on the network below: discovery requires remote **and** workflow, workflow without remote reported separately, remote slug parsed from HTTPS and SSH form, green only when the head SHA matches, a green run for another commit yields "no run yet", red carries conclusion and run URL, queued/in-progress yields "running", rate limit 403 yields an error distinct from "no run", request budget stops the polling and says so, polling only re-queries non-final repositories, exit code non-zero unless everything is green, report written outside the repositories) + host acceptance (one real run after a push: the file names the pushed SHA and matches the Actions page) | high | reviewed |

**Ehrlich zur Verifikation: der Netzweg ist hier nicht bewiesen.** Die Cowork-Sandbox hat keinen
GitHub-Zugang (Guardrail 2); **jeder** Test injiziert die Abruffunktion. Damit ist die
**Auswertung** belegt — SHA-Vergleich, Zustandslogik, Budget, Exit-Code — und die **Abfrage**
nicht. Das ist der Unterschied zwischen „getestet" und „läuft", und er steht hier, statt in einer
grünen Zahl zu verschwinden (B027/B038). Der Nachweis für den Netzweg ist der **erste Lauf am
Host**; bis dahin gilt die Anforderung als umgesetzt, aber nicht als abgenommen.

**Bewusst nicht enthalten:** eine Kachel im Cockpit. Die Prüfung entsteht auf dem Host nach dem
Push, das Cockpit läuft in der Session — eine Anzeige dafür ist eine eigene Fläche und wäre neben
diesem Skript B025. Ebenso nicht enthalten: ein Token. Sollten Repos später privat werden, genügt
eine Fine-grained PAT mit **Actions: Read** und **Metadata: Read** — nichts sonst; das Skript
nimmt sie über `GITHUB_TOKEN` entgegen, ohne sie je zu speichern.

## Nachtrag v1.12 (Auftraggeber 2026-08-17, pm/T-0041)

*Betriebs-CR: „terminierung bitte nicht auf datum, sondern auf sprint. Aktuell wird ASPICE Routine
session jede stunde ausgeführt. Das ist ein Sprint. Alle Aufgaben müssen auf die Sprint's
aufgeplant werden". `pm/D006` erklärt jeden Routine-Lauf zum Sprint; geplant wurde bis hierher
trotzdem auf Kalenderdaten. Bei **stündlichem** Takt sind das rund **24 Sprints am Tag** — „23.08."
wäre etwa Sprint 150, ein Abstand, den niemand umrechnet.*

*Drei Entscheidungen des Auftraggebers: **(1)** `frist` und `geplant_sprint` laufen **parallel**;
**(2)** die nächsten Sprints tragen feste Nummern, alles dahinter ist eine geordnete
**Warteschlange**; **(3)** Feld, Zähler, Plandatei und Kachel in **einem** Zug — vier Flächen, was
das Playbook B025 nennt. Zu (1) hat das Team die bekannte Schwäche benannt (zwei Angaben zu „wann
ist es dran" driften, B033); sie wird deshalb **geprüft statt vorausgesetzt**. Zu (3) ist die
Gegenmaßnahme, dass keine der vier Flächen eine **neue** Regel erfindet.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-106 | Planning shall use **sprints** as its unit instead of calendar dates, one sprint being one routine run. The organisation shall keep a single append-only register (`pm/management/sprints.jsonl`, one line per sprint with number, run identifier, start and cadence in minutes) as the **only** place that knows which run is current; the number shall **not** be derived from git history, because one session writes many commits and commits are therefore not runs (B056, evidenced by 42 commits over roughly 30 runs). Opening a sprint shall be **idempotent through a caller-supplied run identifier** — the same run starting twice shall not advance the counter, and the identity of a run shall be a fact the run states rather than one inferred from a time window. An unreadable register line shall be skipped without stopping the counter and without resetting it to zero. Tickets shall carry an optional `geplant_sprint` (a plain number or `Sprint 42`), validated; vague values such as "soon" or "next sprint" shall be rejected, since an intention is not a plan. Recurring tickets (`takt`) shall carry **no** sprint number — they run in every sprint, and a number beside the cadence field would be a second statement about the same thing (B033). Each planned row shall be marked **fixed** within the next `HORIZONT` sprints and **queue** beyond it: the same number, with its bindingness spoken rather than implied, because at 24 sprints a day a number 150 runs out would be false precision. A sprint number shall never receive a date traffic light. Since `frist` and `geplant_sprint` are kept in parallel by decision of the client, they shall answer **two different questions** — the deadline promised outside the team, and the run in which the team touches it — and every ticket whose planned sprint would fall after its own deadline **even at an uninterrupted cadence** shall be reported as a contradiction, above the plan table, not below it. | STK-019 | Unit tests (`test_sprint_planung.py`: empty register is sprint 0 not 1, counter increments, same run identifier does not advance it, missing identifier rejected, broken line neither stops nor resets the counter, cadence read from the last entry, time estimate arithmetic incl. a past sprint; field parsed in both spellings, vague values rejected, validation reports them; contradiction reported when the sprint falls after the deadline, not when it falls before, only the most favourable case counts, closed tickets and empty fields exempt; sprint number is not a date and never green, a sprint number beats a date in the same cell, cadence wording does not look unplanned, horizon splits fixed from queue, counters keep both apart, date rows keep working) + UI checklist (tile shows the current sprint number and cadence, marks queue rows, shows contradictions above the table) | high | reviewed |

**Nachweis:** 20 neue Unit-Tests (Gesamtsuite **444**, vorher 424). **Gegenprobe über den echten
Bestand geführt** (Regel 1 aus L-2026-08-16h): die Sicht gegen die 16 Repos gestartet meldet
`Sprint 1`, **17 Planzeilen**, `dieser_sprint: 6`, `fest_geplant: 5`, `warteschlange: 6`,
`nicht_geplant: []` und `widersprueche: []` — und beim Zwischenstand hat derselbe Lauf
`pm/T-0041` als **nicht geplant** gemeldet, weil das Ticket vor seiner Planzeile existierte. Der
Bestandsabgleich aus SWR-103 hat also die Umstellung überwacht, die ihn erweitert.

**Ehrlich zur Schätzung.** `sprint_register.geschaetzte_zeit` rechnet Takt × Abstand und ist eine
**Schätzung**, keine Zusage: steht die Cowork-App still, kommt der Sprint später. Sie existiert
ausschließlich für die Widerspruchsprüfung und wird nirgends als Termin angezeigt — genau deshalb
bleibt `frist` das Feld für Zusagen.

**Sprint 1 ist der erste Lauf nach der Umstellung.** Rückwirkend wird nicht nummeriert; die Läufe
davor ließen sich nur aus Commits schätzen, und das wäre B056 ein zweites Mal.

## Nachtrag v1.13 (platform/T-0004, Sprint 2 2026-08-17)

*Der **erste Hostlauf** von SWR-105 hat drei rote Repos gemeldet — `p3`, `p5`, `platform` — und
damit genau das geleistet, wofür er gebaut wurde. Er hat aber auch seine Grenze gezeigt: er sagt
`ROT` und nicht **warum**. Für `platform` ließ sich die Ursache lokal nachstellen (`pm/T-0042`);
für `p3` und `p5` nicht, und die naheliegende Erklärung — Board-Format und Push-Reihenfolge —
wurde durch `p7` **widerlegt** (derselbe Commit-Zeitpunkt auf die Sekunde, dieselbe Workflow-Datei,
grün). Was bleibt, steht in der Lauf-Ausgabe: eine Abfrage entfernt, öffentlich, unangemeldet.*

*Ein `ROT` ohne Schritt ist eine Farbe, kein Befund — es lässt genau die Lücke offen, die SWR-105
schließen sollte: dass ein Mensch eine Seite öffnen muss.*

| ID | Requirement | Trace | Verification | Prio | Status |
|---|---|---|---|---|---|
| SWR-107 | For every repository reported **red**, the CI status check shall additionally name the **job** and the **step** that failed, obtained from the unauthenticated jobs endpoint of the run it has just judged (`GET /repos/{slug}/actions/runs/{id}/jobs`). The lookup shall use the run id **of the red run**, not of the first run in the list. It shall be made **once per red repository and only after** the polling loop has ended, because red is a final state and a repeated lookup would spend the hourly quota for nothing; green, running and unrun repositories shall trigger **no** lookup at all. The lookup shall count against the **same** request budget and appear in the **same** `abfragen` figure — a second, silent counter would be the duplicate-source fault B033. If the lookup fails for any reason — exhausted budget, network error, unexpected payload, a failed job whose steps all report success — the repository shall **remain red** and the report shall say *"step unknown"*; a diagnosis that swallows a finding is worse than no diagnosis (B038). Where no failing step can be identified but a failing job can, the **job name** shall be reported instead of nothing. | STK-019 | Unit tests (`test_ci_status.py`, injected fetch: red repository names job and step; the run id of the red run is used and not that of the first listed run; a green repository triggers no jobs request; a failing jobs request leaves the state red and yields "step unknown"; a failed job without a failed step falls back to the job name; the lookups are counted in `abfragen`; an exhausted budget suppresses the lookups, is reported in the machine-readable field **and** in the text, and a sufficient budget leaves that field false; a payload of unexpected shape — list instead of object, non-object entries, non-list steps — yields "step unknown" and never an exception; `neutral` counts as no failure just like `skipped`; several failed jobs are counted rather than reduced to the first; a successful lookup that names no job says why) + host acceptance (one real run: the report names a step for a red repository) | high | reviewed |

**Ehrlich zur Verifikation — dieselbe Grenze wie bei SWR-105.** Jeder Test injiziert die
Abruffunktion; die Cowork-Sandbox hat keinen GitHub-Zugang (Guardrail 2, in diesem Sprint erneut
bestätigt). Belegt ist damit die **Auswertung**, nicht die **Abfrage**. Der Nachweis für den
Netzweg ist der erste Hostlauf, der einen Schritt benennt — bis dahin steht das hier und nicht in
einer grünen Zahl (B027/B038).

**Warum die Nachfrage nach der Warteschleife steht und nicht in ihr.** In der Schleife wird
gefragt, *ob* ein Repo fertig ist; die Diagnose gilt einem Zustand, der sich nicht mehr ändert.
Beides zu vermischen hieße, für jedes rote Repo in jeder Runde erneut zu fragen — bei 60 Abfragen
je Stunde die sicherste Art, das Budget an eine Antwort zu verlieren, die schon vorliegt.
