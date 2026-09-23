# Changelog

## 2026-09-23 – erste Version

- ESPHome-Konfiguration für einen iMSys-Zähler (SML, 9600 Baud 8N1) mit wispr WS-IR-UART/TTL
  und Waveshare ESP32-S3-Zero (ESP-IDF, 4 MB Flash).
- Sensoren: Bezug (1.8.0), Einspeisung (2.8.0), aktuelle Leistung (16.7.0), Zählernummer
  (96.1.0, lesbar nach DIN 43863-5), WLAN-Signal, Laufzeit.
- Datenbankschonend: Zählerstände höchstens 1× pro Minute und nur bei Änderung, Leistung nur bei Änderung.
- RGB-Status-LED: blau = Daten kommen, grün = gültig, gelb/lila/rot blinkend = Netzwerk-/Auslese-/beide Fehler.

### Erkenntnisse aus dem Aufbau

- **TX am Lesekopf mit VCC brücken.** Offen leuchtet die IR-Sendediode dauerhaft und blendet den
  Fototransistor – es kommen keine Daten an.
- RX am wispr-Kopf ist das Lesesignal und wird direkt (nicht gekreuzt) an den ESP-Eingang geführt.
- Ein zuerst verwendeter Wemos D1 mini (ESP8266, CH340) ließ sich per WebSerial nicht flashen
  („Failed to open serial port“). Der ESP32-S3 mit nativem USB macht diese Probleme nicht.
- `compile_process_limit: 1`, weil ein paralleler ESP-IDF-Build auf einem kleinen HA-Host
  den OOM-Killer ausgelöst hat.
