# Projektplan: P9 „Org-Cockpit" — heute: Requirements-Heimat der Plattform (v1.0, T-0009)

*2026-08-21, PL@p9. Der Plan erfindet keine Aktivität: das ursprüngliche Projekt (Org-Cockpit) ist fertig (7/7 Tickets done); das Repo lebt als **Anforderungs-Heimat der Plattform** weiter — Entscheidung des Auftraggebers p9/D003 (Option A: nichts zieht um), Anzeigename per SWR-175.*

## 1. Ziele (heutiger Dauerauftrag)

| # | Ziel | Erfolgskriterium |
|---|---|---|
| Z1 | `p9/requirements/` ist die eine, gepflegte Heimat der Plattform-SWRs (Stand: SWR-001–184) | RM pflegt hier; Matrix (`trace_matrix.py`) läuft gegen diesen Bestand |
| Z2 | Kein Leser wundert sich mehr, warum hier Betrieb ist | Anzeigename gesetzt (SWR-175); dieser Plan erklärt die 78 Commits/Woche ohne offene Tickets |

## 2. Phasen

Keine — Dauerzustand. Neue SWRs entstehen durch Plattform-Arbeit (zuletzt v1.70: SWR-177–184, draft).

## 3. Workflows

Requirements-Regeln der Organisation (englisch, IDs, Verifikationskriterien, Changelog-Zeile je Version). Änderungen an Baseline-SWRs nur per CR.

## 4. Team und Rollen

Core Team implizit; die tragende Rolle ist **RM** (roles/rm.md). Keine projektspezifischen Rollen.

## 5. Infrastruktur

Repo `p9` (intern). ⚠ Identität bleibt `p9` — jede Referenz `p9/requirements/...` im Bestand hängt daran (D003).

## 6. Timeline

Folgt der Plattform-Arbeit; eigener Sprint-Plan existiert nicht.

## 7. Risiken

| Risiko | Wirkung | Maßnahme | Eigentümer |
|---|---|---|---|
| Niemand prüft, ob der Name über einem Ordner noch stimmt | Zweck-Drift unbemerkt (der Auftraggeber fand es, kein Preflight) | SWR-175 gebaut; Chronikzeile bei Zweckänderung Pflicht | PL |

## 8. Berichtsweg

Kein eigener Sprint-Report; Auffälligkeiten laufen über den Plattform-Report. Chronik: `docs/historie.md`.
