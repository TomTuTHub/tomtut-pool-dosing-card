# TomTuT Pool Dosing Card

> Custom Lovelace Card fuer Home Assistant zur Anzeige und Steuerung einer Pool-Dosieranlage (pH, Redox, Pumpen).

## Shared-Base (nicht loeschen)

Die folgenden Dateien enthalten uebergreifende Infos. Lies sie bei Bedarf:

- `../../_shared-base/arbeitsweise.md` — Wie Thomas arbeitet und kommuniziert
- `../../_shared-base/geraete.md` — Geraete, Dropbox-Sync, Cloud-Accounts
- `../../_shared-base/1password-workflow.md` — Credential-Zugriff via 1Password CLI

> 1Password-Zugang ist ein dedizierter Claude-Account. Passwort jederzeit bei Thomas erfragen, 30 Min Session.

## Projekt-Kontext

Custom Lovelace Card (Web Component mit Lit Element) fuer die Darstellung einer Pool-Dosieranlage in Home Assistant. Zeigt pH-Wert, Redox-Wert, Pumpenstatus, Firmware und Wasserstatus an.

## Tech-Stack

- **Sprache:** JavaScript (gebundelt/minifiziert)
- **Framework:** Lit Element (Web Components)
- **Ziel:** Home Assistant Lovelace Dashboard
- **Konfiguration:** `entity_prefix` als Pflichtparameter

## Dateien

```
tomtut-pool-dosing-card-work/
├── tomtut-pool-dosing-card.js       # Aktuelle Version (v23)
├── tomtut-pool-dosing-card.v22.js   # Aeltere Version (v22)
├── tomtut-pool-dosing-card.v23.js   # Version 23
└── .git/                             # Git-Repo (noch keine Commits)
```

## NAS Mirror

- **Origin:** /volume1/Claude/tomtut-pool-dosing-card.git

## Master-Regel: STARTUP_PROMPT.md aktuell halten

Die `STARTUP_PROMPT.md` ist ein lebendes Dokument. Aktualisiere sie am Ende jeder Session oder bei wichtigen Zwischenschritten mit:
- Aktueller Projektstand
- Offene Aufgaben / naechste Schritte
- Getroffene Entscheidungen
- Kontext fuer die naechste Session
