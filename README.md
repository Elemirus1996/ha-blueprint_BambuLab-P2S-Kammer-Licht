# 🖨️ Bambu Lab – Kammerlicht & Status LED (vereinfacht)

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml)

Vereinfachtes Home-Assistant-Blueprint für **ha-bambulab / Bambu Lab**.

## Verwendete Entities
- `sensor` Druckerstatus
- `binary_sensor` Gerätetür
- `light` Kammerlicht
- `light` Status-LED

## Ablauf
- Prüft den Druckstatus alle **10 Sekunden**.
- Zusätzliche Reaktion direkt bei Änderungen von Druckstatus und Tür.

### Leerlauf (`idle`)
- Status-LED **aus**.
- Kammerlicht **aus**.
- Wird die Tür geöffnet, ist das Kammerlicht an, bis die Tür wieder geschlossen wird.

### Druck / Pause (`running`, `pause`)
- Kammerlicht immer **an** (unabhängig von der Tür).
- Status-LED **blau**, wahlweise **statisch** oder **pulsierend**.

### Druck fertig (`finish`, `finished`)
- Status-LED **grün**, wahlweise **statisch** oder **pulsierend**.
- Kammerlicht bleibt zunächst an und geht nach **5 Minuten** (konfigurierbar) aus.
- Wenn die Tür in dieser Zeit geöffnet und danach wieder geschlossen wird, wechselt alles sofort in den Leerlauf-Modus.

### Druckfehler (`failed`, `error`, `print_error`)
- Kammerlicht **an**.
- Status-LED **rot pulsierend**.
