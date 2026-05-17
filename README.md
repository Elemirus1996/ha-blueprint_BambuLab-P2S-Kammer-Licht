# 🖨️ Bambu Lab – Kammerlicht Steuerung

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml)

Home-Assistant-Blueprint für die **ha-bambulab** / **Bambu Lab Integration**.

## Unterstützte Entities
Getestet bzw. ausgelegt auf folgende Entitäten der Integration:

- `sensor.drucker_p2s_druckstatus`
- `sensor.drucker_p2s_aktueller_arbeitsschritt`
- `sensor.drucker_p2s_druckfortschritt`
- `binary_sensor.drucker_p2s_gehausetur`
- `light.drucker_p2s_druckraumbeleuchtung`
- `binary_sensor.drucker_p2s_druckfehler`
- `binary_sensor.drucker_p2s_hms_fehler`

## Flow

### Leerlauf
- Arbeitsschritt = **Leerlauf**
- Tür auf → **Kammerlicht an**
- Tür zu → **Kammerlicht aus**
- Status-LED **aus**

### Vorbereitung
Folgende Arbeitsschritte werden als Vorbereitung behandelt:

- `Kühlkammer`
- `Werkzeugkopf wird in die Mitte bewegt`
- `Identifizierung der Bauplatte`
- `Filament wechseln`
- `Kalibrierung der Extrusion`
- `Reinigung der Düsenspitze`
- `Fegen im XY-Mechanik-Modus`
- `Warten darauf, dass das Heizbett die Zieltemperatur erreicht`
- `Automatische Bettnivellierung`
- `Drucken von Kalibrierungslinien`

Verhalten:
- Status-LED **orange mit 50 % Helligkeit**
- Tür auf → **Kammerlicht an**

### Druck läuft
Wenn Druckstatus = **Läuft** oder Arbeitsschritt = **Drucken**:
- Kammerlicht **an**, auch wenn Tür geöffnet/geschlossen wird
- Status-LED **blau pulsierend**
- Helligkeit beginnt bei **5 %** und steigt anhand von **Druckfortschritt** in **5-%-Schritten**

### Fehler
Wenn Fehler erkannt wird über:
- `Druckstatus = Fehlgeschlagen`
- oder Fehler-Sensoren wie `Druckfehler` / `HMS-Fehler`

Dann:
- Kammerlicht **blinkt**
- Status-LED **rot pulsierend**
- zusätzliche Fehlerlampen **rot pulsierend**
- nach Fehlerende werden externe Fehlerlampen optional in den vorherigen Zustand zurückgesetzt

### Druck fertig
Wenn Druckstatus = **Fertig**:
- Status-LED **grün pulsierend**

Sobald die Tür geöffnet wird:
- Status-LED **aus**
- Kammerlicht **an**

Wenn danach wieder geschlossen wird und kein Druck läuft:
- Kammerlicht **aus**
- Workflow beginnt wieder von vorne

## Hinweise
- Die externe Statusleuchte sollte idealerweise **RGB** und **Helligkeit** unterstützen.
- Für mehrere Blueprint-Instanzen sollte eine eigene Wiederherstellungs-Szenen-ID für Fehlerleuchten gesetzt werden.
