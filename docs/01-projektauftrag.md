# Projektauftrag P9 — „Org-Cockpit" (v1.0, G0 übernommen)

*2026-08-16, PL. **G0-Äquivalent: pm/T-0008, Option P9a (pm/D002 → p9/D000)** — kein Doppel-G0 (bewährtes P7-Muster). Quelle: Brief pm/N-0003: „welches Team hat gerade welche Aufgaben … zwei feste Teams … Status … abgeschlossen markiert … kurze Beschreibung, allein aus P1-8 kann man das nicht sehen."*

## Was und Warum

Das Cockpit listet heute 13 Repos gleichförmig — wer was ist, was läuft und was fertig ist, erschließt sich nicht. P9 macht daraus die **Organisations-Übersicht**: je Repo ein versionierter **Steckbrief** (Kurzbeschreibung + Status), Gruppierung in **Feste Teams (ASPICE, PM) / Projekt-Teams / aktive Projekte / abgeschlossene Projekte** (eingeklappt), je Karte Status-Pille, Beschreibung und die laufenden (auch wiederkehrenden) Aufgaben. Abgeschlossen wird automatisch erkannt (Abschluss-Baseline `<repo>-v1.0`), von Hand übersteuerbar.

## Abnahmekriterien

1. Cockpit zeigt die vier Gruppen mit korrekten Zuordnungen; Abgeschlossenes eingeklappt und markiert (Stichprobe Browser + Handy).
2. Jede Karte: Kurzbeschreibung + Status-Pille + offene Aufgaben inkl. Takt-Tickets (Stichprobe).
3. Steckbriefe für ALLE Bestandsrepos nachgetragen (nie wieder raten, was „p3" war).
4. Requirements-first (SWR-066–069, Matrix 0 Lücken), Gates Inbox, Schätzung, 0 €.

## Rahmen

2 Sprints (S0 heute: Anforderungen + G1; S1: Umsetzung + Abnahme, Baseline p9-v1.0). Kein ADR nötig (bestehende Muster: Discovery ADR-004, Steckbrief analog team.yaml).
