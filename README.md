# 🖨️ Bambu Lab – Kammerlicht Steuerung (Home Assistant Blueprint)

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz)
[![HA Blueprint](https://img.shields.io/badge/Home%20Assistant-Blueprint-blue.svg)](https://www.home-assistant.io/docs/automation/using_blueprints/)
[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](LICENSE)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FElemirus1996%2Fha-blueprint_BambuLab-P2S-Kammer-Licht%2Fblob%2Fmain%2Fblueprints%2Fbambu_lab_kammerlicht.yaml)

Ein Home Assistant Blueprint zur automatischen Steuerung des Kammerlichts eines Bambu Lab 3D-Druckers über die [Bambu Lab Integration](https://www.home-assistant.io/integrations/bambu_lab/).

---

## ✨ Funktionen

### 🔵 Normalbetrieb

| Ereignis | Bedingung | Aktion |
|---|---|---|
| Druckauftrag startet (`printing`) | — | Kammerlicht **AN** |
| Druckauftrag endet (`idle` / `finish`) | Tür ist **geschlossen** | Kammerlicht **AUS** |
| Kammertür wird **geöffnet** | — | Kammerlicht **AN** |
| Kammertür wird **geschlossen** | Kein Druck & kein Fehler | Kammerlicht **AUS** |

### 🚨 Fehler-Modus (optional)

| Ereignis | Option | Aktion |
|---|---|---|
| Druckfehler (`failed`) | Kammerlicht blinken | Kammerlicht blinkt **alle 2 Sekunden** |
| Druckfehler (`failed`) | Warnleuchte aktivieren | Warnleuchte blinkt in **einstellbarer Farbe & Takt** |
| Fehler behoben | — | Alle Lichter zurück in Normalzustand |

---

## 📦 Installation

### ⭐ Option 1 – HACS (empfohlen, automatische Updates)

1. HACS öffnen → **Blueprints** → **⋮ Menü** → **Custom Repositories**
2. URL eingeben: `https://github.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht`
3. Kategorie: **Automation** wählen → **Hinzufügen**
4. Blueprint in HACS installieren → fertig!

> ✅ Mit HACS erhältst du automatisch Benachrichtigungen bei neuen Updates!

### 🔗 Option 2 – Ein-Klick Import

Auf den blauen Badge oben klicken oder diesen Link im Browser öffnen (HA muss erreichbar sein):

```
https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/blob/main/blueprints/bambu_lab_kammerlicht.yaml
```

### 📂 Option 3 – Manuell

1. Datei [`blueprints/bambu_lab_kammerlicht.yaml`](blueprints/bambu_lab_kammerlicht.yaml) herunterladen
2. In Home Assistant ablegen unter:
   ```
   config/blueprints/automation/bambu_lab_kammerlicht.yaml
   ```
3. HA neu laden → **Einstellungen → Automationen → Blueprints**

---

## ⚙️ Konfiguration

Nach dem Import eine neue Automation aus dem Blueprint erstellen und die Felder ausfüllen:

### 🔵 Basis-Einstellungen

| Feld | Beispiel-Entity | Beschreibung |
|---|---|---|
| Druckstatus Sensor | `sensor.bambu_p1s_print_status` | Aktueller Druckstatus |
| Kammertür Sensor | `binary_sensor.bambu_p1s_door_open` | Tür offen/geschlossen |
| Kammerlicht | `light.bambu_p1s_chamber_light` | Licht in der Kammer |

### 🚨 Fehler-Einstellungen (optional)

| Feld | Standard | Beschreibung |
|---|---|---|
| Kammerlicht blinken bei Fehler | `Aus` | Kammerlicht blinkt alle 2 Sek. bei Fehler |
| Zusätzliche Warnleuchte | `Aus` | Zweite Lampe bei Fehler aktivieren |
| Warnleuchte Entity | — | Z. B. eine Hue oder WLED Lampe |
| Warnleuchte Farbe | Rot `[255, 0, 0]` | RGB-Farbe der Warnleuchte |
| Blink-Takt Warnleuchte | `2 Sekunden` | 1–30 Sekunden einstellbar |

> **Hinweis:** Die genauen Entity-Namen hängen von deinem Drucker-Modell und dem in HA vergebenen Namen ab. Du findest sie unter **Einstellungen → Geräte & Dienste → Bambu Lab**.

---

## 🔧 Kompatibilität

- ✅ Bambu Lab P2S
- ✅ Bambu Lab P1S
- ✅ Bambu Lab X1C
- ✅ Bambu Lab A1 (sofern Kammerlicht vorhanden)
- Home Assistant 2024.1+
- Bambu Lab Integration erforderlich

---

## 📄 Lizenz

Dieses Projekt steht unter der [Apache License 2.0](LICENSE).

---

## 👤 Autor

**Elemirus1996** – [GitHub Profil](https://github.com/Elemirus1996)
