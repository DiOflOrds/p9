# Organigramm: Org-Cockpit

*Generiert aus den Registries (`process/teams/registry.yaml`, `process/roles/besetzungen.yaml`) durch `platform/scripts/organigramm.py` — **nicht von Hand pflegen**, Änderungen gehören in die Registry (Konzept `process/docs/03-rollenmodell-v2-orga-rework.md` Kap. 8).*

**Auftrag:** Org-Cockpit: Teams/Projekte gruppiert mit Status, Beschreibung und Aufgaben; projects-Discovery

```mermaid
graph TB
  MENSCH["Mensch<br/>Auftraggeber / Gates"]
  PM["PM-Team<br/>koordiniert alle PL"]
  MENSCH --> PM
  p9["Org-Cockpit<br/>entwicklung · aktiv"]
  PM --> p9
  p9_CORE["Core Team<br/>10 Rollen · Cowork/Session · sprint"]
  p9 --> p9_CORE
```

## Beteiligte

| Instanz | Rolle | Motor | Takt | Status | Quelle | Hinweis |
|---|---|---|---|---|---|---|
| ARCH@p9 | Architekt | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| CHG@p9 | Change-Manager | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| CM@p9 | Konfigurationsmanager | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| COACH@p9 | Prozess-Coach | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| DEV@p9 | Entwickler | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| PL@p9 | Projektleiter | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| PROB@p9 | Problemmanager | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| QM@p9 | Qualitätsmanager | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| RM@p9 | Requirements-Manager | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |
| TEST@p9 | Verifikationsingenieur | Cowork/Session | sprint | aktiv | Core Team (implizit) | — |

Rollen-Bauplan: `process/roles/<rolle>.md` · projektspezifischer Teil: `roles/<rolle>.md` in diesem Repo · Historie: `docs/historie.md`
