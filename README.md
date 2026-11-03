# Haushaltsbuch – PWA fürs iPhone

Ein persönlicher Finanz-Tracker als installierbare Web-App: Einnahmen und Ausgaben eintragen, Monatssummen sehen, Verteilung nach Kategorie als Kuchendiagramm. Läuft nach der Installation im Vollbild und offline.

## Was in diesem Ordner liegt

| Datei | Zweck |
|---|---|
| `index.html` | Die komplette App (Oberfläche, Logik, Diagramm, CSV-Export/-Import) |
| `manifest.webmanifest` | Sagt dem iPhone: Name, Icon, Vollbild-Start |
| `sw.js` | Service Worker, hält die App offline verfügbar |
| `icons/` | App-Icons für Home-Bildschirm und Android |

## Schritt 1: Online stellen mit GitHub Pages (kostenlos)

Ein Service Worker funktioniert nur über **HTTPS**. GitHub Pages liefert das automatisch.

1. Auf [github.com](https://github.com) anmelden (oder kostenlos registrieren).
2. Oben rechts **+ → New repository**. Name z. B. `haushaltsbuch`. Sichtbarkeit **Public** (für GitHub Pages im kostenlosen Tarif nötig). Auf **Create repository** klicken.
3. Auf der leeren Repo-Seite den Link **uploading an existing file** anklicken.
4. Den **Inhalt** dieses Ordners hineinziehen: `index.html`, `manifest.webmanifest`, `sw.js` und den Ordner `icons`. Wichtig: `index.html` muss ganz oben im Repo liegen, nicht in einem Unterordner.
5. **Commit changes** klicken.
6. Im Repo auf **Settings → Pages**. Unter *Build and deployment*: Source **Deploy from a branch**, Branch **main**, Ordner **/ (root)**, **Save**.
7. Nach ein bis zwei Minuten steht oben die Adresse, z. B. `https://<dein-name>.github.io/haushaltsbuch/`.

**Datenschutz:** Der Code ist öffentlich, deine Einträge aber nicht. Sie werden nur auf deinem iPhone gespeichert und nie an GitHub oder einen Server geschickt.

## Schritt 2: Auf dem iPhone installieren

1. Die Adresse in **Safari** öffnen (andere Browser auf dem iPhone können das je nach iOS-Version nicht).
2. Unten auf **Teilen** (Quadrat mit Pfeil) tippen.
3. **Zum Home-Bildschirm** wählen, eventuell erst nach unten scrollen.
4. Name prüfen („Haushalt“) und **Hinzufügen** tippen.

Ab jetzt startet die App über das Icon im Vollbild, ohne Safari-Leiste, auch im Flugmodus.

## Wichtig: Datensicherung

Die Einträge liegen nur im Speicher dieser App auf dem iPhone.

- Sie überleben Neustarts und App-Updates.
- Sie gehen verloren, wenn du das Icon vom Home-Bildschirm löschst oder in den iOS-Einstellungen die Website-Daten löschst.
- Sie werden **nicht** zwischen Geräten synchronisiert.

Deshalb: In der App unter **Daten sichern → Als CSV exportieren** tippen und die Datei in der Dateien-App oder iCloud Drive speichern. Mit **CSV importieren** holst du sie zurück, auch auf ein neues Gerät. Doppelte Einträge werden beim Import übersprungen.

Die CSV nutzt Semikolons und Komma als Dezimaltrennzeichen und lässt sich direkt in Excel oder Numbers öffnen.

## Änderungen an der App veröffentlichen

1. Geänderte Dateien im Repo hochladen (gleicher Weg wie oben, vorhandene Dateien werden ersetzt).
2. In `sw.js` die Zeile `const VERSION = "haushaltsbuch-v1";` hochzählen, z. B. auf `v2`. Sonst kann das iPhone noch eine Weile die alte Fassung aus dem Cache zeigen.
3. Die App auf dem iPhone einmal komplett schließen und neu öffnen. Deine Daten bleiben erhalten.

## Lokal testen am Mac

Im Terminal in diesem Ordner:

```bash
python3 -m http.server 8000
```

Dann `http://localhost:8000` im Browser öffnen. Das iPhone erreicht diese Adresse nicht, dafür ist Schritt 1 da.

## Mögliche nächste Schritte

- Kategorien anpassen: in `index.html` die Liste `const CATS = { ... }` ändern.
- Einträge bearbeiten statt nur löschen.
- Monatsvergleich als Balkendiagramm über das Jahr.
- Sync zwischen Geräten mit einem Backend wie Supabase.
