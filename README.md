# 🖨️ Bambu Lab – Kammerlicht Steuerung

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml)

Home-Assistant-Blueprint für die **ha-bambulab** / **Bambu Lab Integration**.

## Funktionen
- Kammerlicht **AN**, wenn ein Druck startet
- Kammerlicht **AUS**, wenn Druck beendet ist und Tür geschlossen ist
- Kammerlicht **AN**, wenn die Tür geöffnet wird
- Kammerlicht **AUS**, wenn die Tür geschlossen wird und **kein aktiver Druck** läuft
- Fehlererkennung bevorzugt über **Diagnose-Sensoren** der Integration
- Optional: **Fehler-Blinken** des Kammerlichts
- Optional: **mehrere externe Warnleuchten** mit Farbe und Blinkintervall
- Optional: **manueller Override** über `input_boolean`
- Konfigurierbare **aktive Druckzustände**

## Wichtige Änderung
Die Fehler-Sensoren werden jetzt als **Liste mehrerer Diagnose-Sensoren** konfiguriert. Dadurch werden keine leeren optionalen Entity-IDs mehr als Trigger verwendet.

## Empfohlene Fehler-Sensoren
Nutze wenn möglich die Diagnose-Entities der Integration, zum Beispiel:

- `binary_sensor.<drucker>_print_error`
- `binary_sensor.<drucker>_hms_errors`

Diese kannst du jetzt gemeinsam im Feld **Diagnose Fehler-Sensoren** auswählen.

Wenn keine Diagnose-Sensoren gesetzt sind, nutzt das Blueprint optional den Fallback über den Druckstatus `failed`.

## Import
Nutze den Badge oben oder diesen Link:

```text
https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml
```

## Optionaler manueller Override
Wenn du verhindern möchtest, dass die Automation dein Kammerlicht automatisch ausschaltet, lege in Home Assistant einen Helper an:

- **Typ:** Input Boolean
- Beispiel: `input_boolean.bambu_kammerlicht_override`

Wenn dieser Helper auf **Ein** steht, schaltet die Automation das Licht nicht automatisch aus.

## Externe Warnleuchten
Du kannst jetzt **mehrere externe Lampen** auswählen, die bei Fehler gemeinsam blinken.

## Hinweise
Die Bambu-Lab-Statuswerte können je nach Modell und Integration leicht variieren. Deshalb sind die **aktiven Druckzustände** im Blueprint anpassbar.
