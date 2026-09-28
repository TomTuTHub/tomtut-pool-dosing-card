# TomTuT Pool Dosing Card

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/hacs/integration)
[![GitHub Release](https://img.shields.io/github/v/release/TomTuTHub/tomtut-pool-dosing-card)](https://github.com/TomTuTHub/tomtut-pool-dosing-card/releases/latest)
[![HA Version](https://img.shields.io/badge/Home%20Assistant-2024.1.0%2B-blue)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Custom Lovelace Dashboard Card fuer die **[TomTuT Pool Dosing Integration](https://github.com/TomTuTHub/tomtut-pool-dosing)** (Beniferro Gen2 Dosieranlage). Zeigt pH-Wert, Redox-Wert, Pumpenstatus, Firmware-Version und Wasserfluss mit Animationen an.

> **Disclaimer:** Dieses Projekt ist nicht affiliiert mit Beniferro, Poolsana oder deren Tochtergesellschaften. Nutzung auf eigene Verantwortung.

---

![TomTuT Pool Dosing Card](screenshots/card-preview.png)

---

## Features

- **pH- und Redox-Werte** — Live-Anzeige der aktuellen Messwerte direkt auf der Card
- **Animierter Wasserfluss** — Animierte Wellendarstellung mit konfigurierbarer Geschwindigkeit und Richtung
- **Animierte Pumpen** — Drei Pumpen-Stile: Pfeil, Ventilator, Punkte-Rad — drehen wenn die Pumpe laeuft
- **Firmware-Anzeige / Freitextfeld** — Zeigt die Firmware-Version oder einen eigenen Text an
- **Smarte Steckdose** — Optionales Ein/Aus-Icon fuer eine verknuepfte Steckdose direkt in der Card
- **Zwei Anlagentypen** — Vordefinierte Layouts fuer Typ 1 und Typ 2 (Beniferro Gen2)
- **Drei Bildvarianten** — wirklich transparent (das Dashboard-Theme scheint durch), grau oder weiss
- **Theme-tauglich** — die Karte malt ihre Flaeche nicht selbst; `--ha-card-background`, `--ha-card-backdrop-filter` und `--ha-card-box-shadow` aus deinem Theme greifen (Glas-Themes inklusive)
- **Visueller Editor** — Kompletter GUI-Editor mit Live-Vorschau, keine YAML-Kenntnisse noetig
- **Vollstaendig anpassbar** — Positionen, Groessen und Farben aller Elemente individuell einstellbar

---

## Voraussetzungen

- Home Assistant **2024.1.0** oder neuer
- [HACS](https://hacs.xyz/) installiert
- **[TomTuT Pool Dosing Integration](https://github.com/TomTuTHub/tomtut-pool-dosing)** installiert und konfiguriert — fuer die transparente Bildvariante **v1.9.7 oder neuer**

> **Wichtig:** Die Integration muss **zuerst** installiert sein — sie stellt die Sensoren bereit, die diese Card anzeigt. Sie liefert auch die Anlagen-Grafiken aus; ist sie noch aelter als v1.9.7, faellt die Card automatisch auf die graue Variante zurueck.

---

## Installation

### Via HACS (empfohlen)

1. HACS in Home Assistant oeffnen
2. **Frontend** → Drei-Punkte-Menue → **Benutzerdefinierte Repositories**
3. Repository hinzufuegen: `https://github.com/TomTuTHub/tomtut-pool-dosing-card` — Kategorie: **Dashboard**
4. Nach **TomTuT Pool Dosing Card** suchen und **Herunterladen**
5. Browser neu laden

### Manuelle Installation

1. `tomtut-pool-dosing-card.js` vom [neuesten Release](https://github.com/TomTuTHub/tomtut-pool-dosing-card/releases/latest) herunterladen
2. Nach `config/www/community/tomtut-pool-dosing-card/` in der Home Assistant Instanz kopieren
3. In HA: **Einstellungen → Dashboards → Ressourcen** → Ressource hinzufuegen:
   - URL: `/local/community/tomtut-pool-dosing-card/tomtut-pool-dosing-card.js`
   - Ressourcentyp: **JavaScript-Modul**
4. Browser neu laden

---

## Konfiguration

Die Card im Dashboard-Editor hinzufuegen: **Karte hinzufuegen** → **TomTuT Pool Dosing** auswaehlen. Der visuelle Editor oeffnet sich automatisch.

### Grundeinstellungen

| Option | Pflicht | Beschreibung |
|---|---|---|
| `entity_prefix` | Ja | Entity-Praefix deiner Dosieranlage |
| `model` | Nein | Anlagentyp: `type1` (Standard) oder `type2` |
| `image_variant` | Nein | Bildvariante: `transparent` (Standard), `grey` (grauer Kasten) oder `light` (weiss). Der alte Wert `dark` gilt weiterhin und bedeutet `transparent` |
| `plug_entity` | Nein | Entity-ID einer smarten Steckdose (z.B. `switch.dosieranlage`) |

### Entity-Praefix ermitteln

Der Praefix ist `sensor.` gefolgt vom Namen deiner Dosieranlage in Home Assistant. Leerzeichen werden zu Unterstrichen, alles klein.

Beispiel: Heisst deine Anlage *Meine Pool Dosieranlage*, dann ist der Praefix: `sensor.meine_pool_dosieranlage`

### YAML-Beispiel (manuelle Konfiguration)

```yaml
type: custom:tomtut-pool-dosing-card
entity_prefix: sensor.tomtut_pool_dosieranlage
model: type1
image_variant: transparent
plug_entity: switch.dosieranlage
```

### Erweiterte Einstellungen

Im visuellen Editor unter **Erweiterte Einstellungen** koennen alle Positionen, Groessen und Farben der einzelnen Elemente angepasst werden:

- **Wasserfluss** — Geschwindigkeit, Richtung, Position, Hoehe, Breite
- **Pumpen** — Position, Groesse, Drehgeschwindigkeit, Symbol-Stil
- **Firmware/Freitext** — Position, Groesse, Farbe, Hintergrund-Box
- **Messwerte** — Position, Groesse, Farbe, Labels, Hintergrund-Box
- **Steckdose** — Position

---

## Themes und eigene Farben

Die Card malt ihre Flaeche **nicht** selbst: die Kartenflaeche gehoert dem Theme. Damit greifen
`--ha-card-background`, `--ha-card-backdrop-filter`, `--ha-card-box-shadow`, `--ha-card-border-color`
und `--ha-card-border-radius` genauso wie bei den eingebauten Karten — mit der Bildvariante
**Transparent** schlaegt also auch ein Glas-/Blur-Theme durch.

Die Elemente **auf** der Grafik (Messwert-Kaesten, Firmware-Kasten, Steckdose, Wellen, Pumpen) behalten
ihre eigenen Farben, weil sie auf dem Bild liegen und nicht auf der Kartenflaeche — die HA-Textfarben
waeren dort je nach Theme unlesbar. Wer sie trotzdem anpassen will, setzt im Theme diese Variablen:

| Variable | Standard | Wirkung |
|---|---|---|
| `--tomtut-pool-dosing-value-background` | `rgba(0,0,0,0.75)` | Hintergrund der Messwert-Kaesten |
| `--tomtut-pool-dosing-value-border-color` | `rgba(255,255,255,0.15)` | Rahmen der Messwert-Kaesten |
| `--tomtut-pool-dosing-value-color` | `#fff` | Schrift der Messwerte (die Editor-Option „Farbe" hat Vorrang) |
| `--tomtut-pool-dosing-badge-background` | `rgba(0,0,0,0.6)` | Hintergrund des Firmware-/Freitextfelds |
| `--tomtut-pool-dosing-plug-background` | `rgba(0,0,0,0.4)` | Hintergrund des Steckdosen-Knopfs |
| `--tomtut-pool-dosing-plug-on-color` | `#4caf50` | Steckdose an |
| `--tomtut-pool-dosing-plug-off-color` | `#f44336` | Steckdose aus |
| `--tomtut-pool-dosing-wave-1-color` … `-3-` | Blautoene | die drei Wellenlinien |
| `--tomtut-pool-dosing-pump-idle-color` | `rgba(0,0,0,0.25)` | Pumpensymbol, Pumpe steht |
| `--tomtut-pool-dosing-pump-active-color` | `rgba(0,0,0,0.9)` | Pumpensymbol, Pumpe laeuft |

Beispiel im Theme:

```yaml
mein_theme:
  tomtut-pool-dosing-value-background: "rgba(255,255,255,0.18)"
  tomtut-pool-dosing-value-color: "#fff"
```

---

## Verwendete Entities

Die Card nutzt folgende Entities der Integration:

| Entity | Beschreibung |
|---|---|
| `sensor.*_ph` | pH-Wert |
| `sensor.*_redox` | Redox-Wert (mV) |
| `sensor.*_firmware_version` | Firmware-Version der Anlage |
| `sensor.*_flow` | Wasserdurchfluss-Status |
| `binary_sensor.*_ph_pumpe` | pH-Dosierpumpe aktiv |
| `binary_sensor.*_redox_pumpe` | Redox-Dosierpumpe aktiv |

---

## Support & Issues

Bugs und Feature-Requests bitte hier melden:
[https://github.com/TomTuTHub/tomtut-pool-dosing-card/issues](https://github.com/TomTuTHub/tomtut-pool-dosing-card/issues)

---

## Lizenz

MIT License — siehe [LICENSE](LICENSE) fuer Details.

---

## Ueber den Autor

Ich bin ausgebildeter Fachinformatiker fuer Systemintegration mit langjaeehriger IT-Erfahrung. Frueher war es der MCSE — heute ist es Vibe Coding. Diese Card wurde mit Hilfe von Claude gebaut. Ohne KI-Unterstuetzung haette ich das nebenbei nie in dieser Form hinbekommen. Der Code wurde von mir getestet und laeuft in meinem eigenen Produktiv-Setup.

Mehr auf [thomasbase.de](https://thomasbase.de) und [YouTube @TomTuT](https://www.youtube.com/@TomTuT).

---

Das war TomTuT, bleib hart am Gas.
