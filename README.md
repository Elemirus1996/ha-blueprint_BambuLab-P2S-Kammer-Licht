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

## Verwendete echte Enum-Werte
Das Blueprint arbeitet mit den technischen Statuswerten der Integration, nicht mit den übersetzten Anzeigenamen.

### Druckstatus
- `prepare`
- `running`
- `pause`
- `finish`
- `failed`
- `idle`
- `offline`

### Aktueller Arbeitsschritt
Beispiele:
- `idle`
- `printing`
- `cooling_chamber`
- `moving_toolhead_to_center_of_heatbed`
- `identifying_build_plate_type`
- `changing_filament`
- `calibrating_extrusion`
- `sweeping_xy_mech_mode`
- `waiting_for_heatbed_temperature`
- `auto_bed_leveling`
- `print_calibration_lines`

## Flow

### Leerlauf
- Arbeitsschritt = `idle`
- Tür auf → **Kammerlicht an**
- Tür zu → **Kammerlicht aus**
- Status-LED **aus**

### Vorbereitung
Folgende Arbeitsschritte werden als Vorbereitung behandelt:

- `cooling_chamber`
- `moving_toolhead_to_center_of_heatbed`
- `identifying_build_plate_type`
- `changing_filament`
- `calibrating_extrusion`
- `sweeping_xy_mech_mode`
- `waiting_for_heatbed_temperature`
- `auto_bed_leveling`
- `print_calibration_lines`
- `cleaning_nozzle_plate`
- `cleaning_nozzle_tip`
- `heatbed_preheating`
- `heating_hotend`
- `checking_extruder_temperature`
- `purifying_chamber_air`
- `checking_print_surface`

Verhalten:
- Status-LED **orange mit 50 % Helligkeit**
- Tür auf → **Kammerlicht an**
- Tür zu → **Kammerlicht aus**

### Druck läuft / Pause
Wenn Druckstatus = `running` oder `pause` oder Arbeitsschritt = `printing`:
- Kammerlicht **an**, auch wenn Tür geöffnet/geschlossen wird
- Status-LED **blau pulsierend**
- Helligkeit beginnt bei **5 %** und steigt anhand von **Druckfortschritt** in **5-%-Schritten**

### Fehler
Wenn Fehler erkannt wird über:
- `Druckstatus = failed`
- oder Fehler-Sensoren wie `Druckfehler` / `HMS-Fehler`

Dann:
- Kammerlicht **blinkt**
- Status-LED **rot pulsierend**
- zusätzliche Fehlerlampen **rot pulsierend**
- nach Fehlerende werden externe Fehlerlampen optional in den vorherigen Zustand zurückgesetzt

### Druck fertig
Wenn Druckstatus = `finish`:
- Status-LED **grün pulsierend**, solange die Tür geschlossen ist und der Arbeitsschritt noch **nicht `idle`** ist

Sobald die Tür geöffnet wird und der Ablauf in `idle` übergeht:
- Status-LED **aus**
- Kammerlicht **an**

Wenn danach wieder geschlossen wird und kein Druck läuft:
- Kammerlicht **aus**
- Workflow beginnt wieder von vorne
