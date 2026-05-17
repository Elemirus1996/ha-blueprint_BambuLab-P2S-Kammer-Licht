# 🖨️ Bambu Lab – Kammerlicht Steuerung (Home Assistant Blueprint)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FElemirus1996%2Fha-blueprint_BambuLab-P2S-Kammer-Licht%2Fblob%2Fmain%2Fblueprints%2Fbambu_lab_kammerlicht.yaml)

Ein Home Assistant Blueprint zur automatischen Steuerung des Kammerlichts eines Bambu Lab 3D-Druckers über die [Bambu Lab Integration](https://www.home-assistant.io/integrations/bambu_lab/).

---

## ✨ Funktionen

| Ereignis | Bedingung | Aktion |
|---|---|---|
| Druckauftrag startet (`printing`) | — | Licht **AN** |
| Druckauftrag endet (`idle` / `finish` / `failed`) | Tür ist **geschlossen** | Licht **AUS** |
| Kammertür wird **geöffnet** | — | Licht **AN** |
| Kammertür wird **geschlossen** | Kein Druck läuft | Licht **AUS** |

---

## 📦 Installation

### Option 1 – Ein-Klick Import (empfohlen)

Auf den Badge oben klicken oder diesen Link verwenden:

```
https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/blob/main/blueprints/bambu_lab_kammerlicht.yaml
```

### Option 2 – Manuell

1. Datei [`blueprints/bambu_lab_kammerlicht.yaml`](blueprints/bambu_lab_kammerlicht.yaml) herunterladen
2. In Home Assistant ablegen unter:
   ```
   config/blueprints/automation/bambu_lab_kammerlicht.yaml
   ```
3. In HA: **Einstellungen → Automationen → Blueprints** → Blueprint erscheint automatisch

---

## ⚙️ Konfiguration

Nach dem Import eine neue Automation aus dem Blueprint erstellen und folgende Entitäten auswählen:

| Feld | Beispiel-Entity |
|---|---|
| 🔵 Druckstatus Sensor | `sensor.bambu_p1s_print_status` |
| 🚪 Kammertür Sensor | `binary_sensor.bambu_p1s_door_open` |
| 💡 Kammerlicht | `light.bambu_p1s_chamber_light` |

> **Hinweis:** Die genauen Entity-Namen hängen von deinem Drucker-Modell (P1S, P2S, X1C, A1 etc.) und dem in HA vergebenen Namen ab. Du findest sie unter **Einstellungen → Geräte & Dienste → Bambu Lab**.

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
