# Sitzplangenerator

Web-Tool zum automatischen Erstellen von Sitzplänen für den Unterricht — Teil der Lehrkraft-Werkzeuge auf [tinkeredu.de](https://tinkeredu.de/tools/Sitzplangenerator.html).

Eine einzelne HTML-Datei ohne Build-Schritt, ohne Server, ohne externe Abhängigkeiten: `Sitzplangenerator.html` im Browser öffnen und loslegen. Alle Daten bleiben lokal.

## Funktionen

- **Klassenliste:** Schüler:innen einzeln, per Mehrfachauswahl oder per .txt-/CSV-Import anlegen; doppelte Namen werden abgefangen
- **Raum & Tische:** Tische auf einem 6×5-Raster platzieren (2 Sitze pro Tisch, einzeln oder ganze Zeilen/Spalten)
- **Wünsche & Trennungen:** „soll neben" / „soll nicht neben" mit Priorität 1–3; doppelte Relationen werden dedupliziert
- **Gruppen:** Zwang-Gruppen, deren Mitglieder nah beieinander sitzen sollen (mit Teilpunkten bei geringer Distanz)
- **Platzieren:** Drag & Drop aus dem Schülerpool oder Tap-to-place (iPad/touch-tauglich); Plätze können gepinnt werden
- **Optimierer:** Simulated Annealing mit echter Abkühlung plus Hill-Climbing, chunked asynchron mit Fortschrittsbalken — die Seite friert nicht ein
- **Top-3-Lösungen:** die drei besten Sitzpläne zum Durchklicken und Übernehmen
- **Live-Score:** Bewertung des aktuellen Plans in Echtzeit
- **Export & Persistenz:** JSON-Export/Import, PNG-Export des Raumplans, Druckansicht, Autosave im Browser (localStorage)
- **Einführungsassistent:** geführter 6-Schritte-Rundgang beim ersten Besuch, jederzeit über den „?"-Button wieder aufrufbar
- **Undo:** Strg+Z macht die letzte Platzierung rückgängig

## Nutzung

`Sitzplangenerator.html` in einem aktuellen Browser öffnen — fertig. Für den lokalen Test z. B.:

```bash
python3 -m http.server 8000
# dann http://localhost:8000/Sitzplangenerator.html
```

## Technik

- Reines Vanilla HTML/CSS/JavaScript in einer Datei (~1200 Zeilen)
- Scoring: gewichtete Relationen (Priorität 1–3), Distanzklassen (Nebentisch / Tisch davor-dahinter / zwei Tische), Gruppen-Bonus, Pins als harte Constraints
- Optimierung: Multi-Restart SA (lange Abkühlphase) + lokale Verbesserung per Hill-Climbing
- Keine Cookies, kein Backend — Autosave und Wizard-Flag liegen in `localStorage`
