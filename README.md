# 🖨️ Bambu Lab – Kammerlicht Steuerung

[![Open your Home Assistant instance and import this blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/Elemirus1996/ha-blueprint_BambuLab-P2S-Kammer-Licht/main/blueprints/bambu_lab_kammerlicht.yaml)

Home-Assistant-Blueprint für die **ha-bambulab** / **Bambu Lab Integration**.

## Funktionen
- Kammerlicht **AN**, wenn ein Druck startet
- Kammerlicht **AUS**, wenn Druck beendet ist und Tür geschlossen ist
- Kammerlicht **AN**, wenn die Tür geöffnet wird
- Wenn der Druck bereits **fertig** ist und die Tür geöffnet wird:
  - **Statusleuchte AUS**
  - **Kammerlicht AUS**, damit der Workflow wieder sauber im Idle-Zustand endet
- Kammerlicht **AUS**, wenn die Tür geschlossen wird und **kein aktiver Druck** läuft
- Optional: Fehlererkennung bevorzugt über **Diagnose-Sensoren**
- Optional: **Kammerlicht blinkt bei Fehler**
- Optional: **separate externe Statusleuchte**
  - **Aus** = Drucker inaktiv
  - **Grün pulsierend** = Druck fertig (nur bis Tür geöffnet wird)
  - **Blau pulsierend** = Druck läuft
  - **Blau mit Helligkeit nach Fortschritt** = optional beim Drucken
  - **Orange** = Warnung
  - **Rot** = Fehler
- Optional: **mehrere externe Fehlerleuchten** mit Farbe und Blinkintervall
- Optional: **ursprünglichen Zustand externer Fehlerleuchten nach Fehlerende wiederherstellen**
- Optional: **manueller Override** über `input_boolean`
- Konfigurierbare **aktive Druckzustände**

## Wiederherstellung der Fehlerleuchten
Wenn **Fehlerleuchten nach Fehlerende wiederherstellen** aktiviert ist, speichert das Blueprint beim Fehlerbeginn
über `scene.create` den aktuellen Zustand der externen Fehlerleuchten und stellt ihn nach Fehlerende wieder her.

Wenn du mehrere Instanzen des Blueprints verwendest, solltest du pro Instanz eine eigene **Szenen-ID für Wiederherstellung** setzen.

## Wichtige Änderung
Die grüne Fertig-Anzeige bleibt jetzt nur aktiv, solange der Druck fertig ist **und die Tür geschlossen bleibt**.
Wird die Tür nach einem fertigen Druck geöffnet, endet dieser Zustand und die Statusleuchte geht aus.

## Empfohlene Fehler-Sensoren
Nutze wenn möglich die Diagnose-Entities der Integration, zum Beispiel:

- `binary_sensor.<drucker>_print_error`
- `binary_sensor.<drucker>_hms_errors`

Diese kannst du gemeinsam im Feld **Diagnose Fehler-Sensoren** auswählen.

## Fortschrittssensor
Wenn deine Integration einen Druckfortschritt in Prozent bereitstellt, kannst du diesen beim Feld
**Druckfortschritt Sensor (%)** auswählen. Dann kann die externe blaue Statusleuchte beim Drucken
optional über die Helligkeit den Fortschritt anzeigen.

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

## Externe Leuchten
- **Externe Statusleuchte** = zeigt Druckstatus per Farbe/Pulsieren
- **Externe Fehlerleuchten** = blinken bei Fehler zusätzlich und können danach wiederhergestellt werden

## Hinweise
Die Bambu-Lab-Statuswerte können je nach Modell und Integration leicht variieren. Deshalb sind die **aktiven Druckzustände** im Blueprint anpassbar.
