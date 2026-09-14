# Einsatzübersicht

Dashboard für die Auswertung von Technikereinsätzen (Dämmarbeiten, Außendienst) bei VARM.

## Was es zeigt

- **KPIs** — Anzahl Einsätze, aktive Techniker, Ø Einsatzdauer
- **Ø Dauer pro Techniker** — Balken mit Markierung des Gesamtdurchschnitts, plus Verlauf über die Zeit
- **Ø Dauer pro Dämmtyp** — Balken mit Soll-Markierung (Firmenrichtwert), plus Verlauf über die Zeit
- **Matrix Techniker × Dämmtyp** — welcher Techniker braucht für welchen Dämmtyp wie lange
- **Einsatztabelle** — Einzeleinsätze mit Kunde, Adresse, Start/Ende und Dauer

## Datenquelle

Die Live-Daten kommen aus einem Google Sheet, das per Make.com-Automation aus den
Techniker-Check-ins befüllt wird. Das Dashboard liest das Sheet alle 60 Sekunden neu.

Die Live-Anbindung läuft über die MCP-Capability der Claude-Artifacts-Umgebung
(`window.claude.use("mcp")` → Google Drive). Wird die Datei außerhalb davon geöffnet
(lokal im Browser, GitHub Pages o. ä.), fällt sie auf einen **anonymisierten
Beispiel-Snapshot** zurück — echte Kunden- und Technikerdaten sind bewusst nicht
im Repository enthalten.

## Konfiguration

Im `<script>`-Block in `index.html`:

| Konstante | Bedeutung |
| --- | --- |
| `FILE_ID` | ID des Google Sheets mit den Check-in-Daten |
| `COMPANY_RICHTWERTE` | Soll-Dauer je Dämmtyp in Minuten (Abweichungen von `DEFAULT_RICHTWERT`) |
| `DEFAULT_RICHTWERT` | Soll-Dauer für alle übrigen Dämmtypen (aktuell 60 min) |
| `OUTLIER_MIN_MINUTES` | Einsätze unter dieser Dauer gelten als Ausreißer (Check-out-Fehler) und fließen nicht in Durchschnitte ein |

## Nutzung

`index.html` ist eine einzelne, eigenständige Datei ohne Build-Schritt — einfach im
Browser öffnen oder als statische Seite ausliefern.

## Offene Punkte

- [ ] Distanz-Automation (Fahrtwege zwischen Einsätzen)
- [ ] Vollständigkeitsprüfung des Sheets (Zeilen ohne erfasste Dauer)
