# Historie: P9 „Org-Cockpit" / Requirements-Heimat — Chronik und Lessons Learned

*Projektgedächtnis (Konzept 03 Kap. 5). Geseedet 2026-08-21 (T-0009).*

## Steckbrief

- **Auftrag (historisch):** Org-Cockpit — Teams/Projekte gruppiert mit Status im HMI; **erreicht** (7/7 Tickets done)
- **Auftrag (heute):** Requirements-Heimat der Plattform (p9/D003, Option A — nichts zieht um)
- **Profil / Datenklasse:** entwicklung / intern
- **Status:** aktiv (als Heimat; das Bau-Projekt ist fertig)

## Chronik

| Datum | Ereignis | Beleg |
|---|---|---|
| 2026-08-17 | Org-Cockpit gebaut (Discovery projects/, Gruppierung) | T-0001–T-0007 |
| 2026-08-20 | Auftraggeber-Brief: „kann dieses Projekt geschlossen werden? warum gibts das noch?" — Messung: 7/7 done, 78 Commits/Woche, 81 SWRs im Ordner | N-0001, T-0008 |
| 2026-08-20 22:25 | Entscheid D003: Option A + Anzeigename „Org-Cockpit"; SWR-175 gebaut | D003, SWR-175 |
| 2026-08-21 | v1.70: SWR-177–184 (Orga-Rework-Nachtrag + neue Sichten, draft) | platform/T-0042 |
| 2026-08-21 | **Sprint 28:** SWR-189 (Instanzschlüssel = `rolle@einheit`, strukturell **neben** dem Literal), SWR-190 (Goldset-Abdeckung als stehende Prüfung), SWR-135 v1.74 (Frontend-Rückschneidung). Matrix **190 SWRs / 0 Lücken** | v1.73–v1.75 |

## Lessons Learned

| # | Lehre | Quelle | Übernommen nach |
|---|---|---|---|
| 1 | Keine Prüfung fragt, ob der Name über einem Ordner noch stimmt — der Auftraggeber fand es | N-0001/SWR-175 | SWR-175, Risikoliste im Projektplan |
| 2 | Identität ≠ Beschriftung: Ordner bleiben, Anzeigenamen ändern sich | D003 | Konzept 04 Kap. 7 (Migrationsprinzip) |

## Offene Fäden

- Review SWR-177–184 (platform/T-0042).
