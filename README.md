# 🖨️ Bambu Lab – Kammerlicht Steuerung

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml)

Home-Assistant-Blueprint für die **ha-bambulab** / **Bambu Lab Integration**.

## Unterstützte Entities
- `sensor.drucker_p2s_druckstatus`
- `sensor.drucker_p2s_aktueller_arbeitsschritt`
- `sensor.drucker_p2s_druckfortschritt`
- `binary_sensor.drucker_p2s_gehausetur`
- `light.drucker_p2s_druckraumbeleuchtung`
- `binary_sensor.drucker_p2s_druckfehler`
- `binary_sensor.drucker_p2s_hms_fehler`

## Fehlerverhalten
- Fehler wird aktiv, wenn einer der gewählten Fehler-Sensoren auf `on` steht oder der Druckstatus `failed` ist.
- Fehler endet automatisch, sobald **alle** Fehler-Sensoren wieder `off` sind und der Druckstatus **nicht mehr** `failed` ist.
- Die Snapshot-Szene für externe Fehlerleuchten wird nur beim **Übergang in den Fehlerzustand** gespeichert.
- Nach Fehlerende werden externe Fehlerleuchten korrekt ausgeschaltet oder auf den Zustand **vor dem Fehler** zurückgesetzt.

## Enum-Werte
Das Blueprint arbeitet mit den technischen Statuswerten der Integration.

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
