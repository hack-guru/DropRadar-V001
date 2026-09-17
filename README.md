# DropRadar – Website-Grundgerüst

Das ist die erste echte, deploybare Version des Prototyps: eine statische Website (kein Server, keine Datenbank nötig) mit zwei Datendateien, die du später direkt pflegst:

- `data/designs.json` – DesignArtLab-Motive mit Preisen je Plattform (Featured Shop im Design-Finder)
- `data/deals.json` – aktuelle Rabatte im Rabatte-Board (später auch andere Marken)

**Wichtig:** Die Seite lädt diese JSON-Dateien per `fetch`. Das funktioniert nur, wenn sie über einen echten Server ausgeliefert wird (z. B. Cloudflare Pages) – nicht, wenn du `index.html` einfach doppelklickst und lokal im Browser öffnest.

## Schritt 1: GitHub-Repository anlegen

1. Auf [github.com](https://github.com) einloggen → oben rechts auf **„+“ → „New repository“**.
2. Name z. B. `dropradar-website`, Sichtbarkeit „Public" ist okay (kein Geheimnis in diesen Dateien).
3. „Create repository" klicken (ohne README, .gitignore etc. anzuhaken – die Dateien bringst du gleich mit).
4. Auf der leeren Repo-Seite auf **„uploading an existing file"** klicken.
5. Alle Dateien aus diesem Ordner (inklusive des `data`-Unterordners) per Drag & Drop dort reinziehen.
6. Unten „Commit changes" klicken. Fertig – kein Git, kein Terminal nötig.

## Schritt 2: Mit Cloudflare Pages verbinden

1. In Cloudflare einloggen → im Menü **„Workers & Pages"** → **„Create"** → Tab **„Pages"** → **„Connect to Git"**.
2. Cloudflare fragt nach Zugriff auf GitHub → dort meldest du dich mit deinem eigenen GitHub-Account an und bestätigst per Klick (kein Passwort wird an mich weitergegeben, das läuft direkt zwischen dir, GitHub und Cloudflare).
3. Dein Repository `dropradar-website` auswählen.
4. Build-Einstellungen: **Framework preset = „None"**, **Build command = leer lassen**, **Build output directory = `/`** (bzw. „/" stehen lassen).
5. „Save and Deploy" klicken. Nach ca. 1 Minute ist die Seite unter einer `*.pages.dev`-Adresse live.

Jede spätere Änderung, die du auf GitHub hochlädst (z. B. eine bearbeitete `deals.json`), wird automatisch neu deployed.

## Schritt 3 (später): eigene Domain

1. In Cloudflare Pages beim Projekt → „Custom domains" → „Set up a custom domain".
2. Domain bei einem Registrar deiner Wahl kaufen (z. B. direkt über Cloudflare Registrar, oder woanders) – das ist der einzige Punkt, an dem wirklich Geld fließt (~10–15 €/Jahr).
3. DNS-Eintrag laut Cloudflare-Anleitung setzen – bei Domains, die schon über Cloudflare laufen, meist ein Klick.

## Inhalte pflegen (aktuell)

Auf GitHub eine der beiden JSON-Dateien öffnen → Stift-Symbol „Edit this file" → Eintrag anpassen/ergänzen → „Commit changes". Cloudflare deployed automatisch neu. Kein Code-Wissen nötig, nur auf die Kommas in der JSON-Struktur achten.

Für eine komfortablere Eingabemaske (statt JSON von Hand) kann später ein kostenloses Headless-CMS (z. B. Decap CMS) ergänzt werden – das ist Phase 2.

## Rechtliches (schon eingebaut, aber noch nicht startklar)

`impressum.html` und `datenschutz.html` liegen bereits im Ordner und sind im Footer von `index.html` verlinkt.

**Bevor die Seite live geht, unbedingt noch erledigen:**
1. In `impressum.html` steht bei der Adresse `[BITTE HAUSNUMMER ERGÄNZEN]` – die Hausnummer ist gesetzlich Pflichtangabe (ladungsfähige Anschrift), ohne sie ist das Impressum nicht rechtsgültig. Einfach den Platzhalter durch die echte Hausnummer ersetzen (auf GitHub direkt über das Stift-Symbol editierbar).
2. `datenschutz.html` an der gleichen Stelle (Abschnitt „1. Verantwortlicher") ebenfalls die Hausnummer ergänzen.

Die E-Mail-Adresse im Impressum ist bewusst nicht als Klartext im HTML hinterlegt, sondern wird erst per Klick auf „E-Mail-Adresse anzeigen" per JavaScript zusammengesetzt – das hält einfache Scraper/Bots ab, die nur den rohen Seitentext nach `@`-Adressen durchsuchen. Ein hundertprozentiger Schutz ist damit nicht möglich (ein Impressum muss die Adresse letztlich frei zugänglich machen, das schreibt das Gesetz so vor), aber die große Masse automatisierter Adress-Sammler geht damit leer aus.

Cookie-Banner: aktuell bewusst noch nicht eingebaut, weil die Seite noch keine Cookies/Tracking setzt (steht auch so in der Datenschutzerklärung). Sobald Werbung/Analytics dazukommt, muss vor dem Setzen der Cookies ein Consent-Banner davor.

## Android-„App" (schon eingebaut)

Die Seite ist bereits eine installierbare PWA (Progressive Web App): `manifest.json`, `sw.js` und die App-Icons (`icon-192.png`, `icon-512.png` – aktuell nur Platzhalter-Monogramm) sind schon drin. Sobald die Seite live ist, kann sie auf Android über Chrome-Menü → „Zum Startbildschirm hinzufügen" wie eine echte App installiert werden: eigenes Icon, kein Browser-Rahmen, läuft im eigenen Fenster. Kostet nichts, braucht keinen Play-Store-Eintrag und keine separate App-Pflege – jede Änderung an der Website erscheint automatisch auch in der „App".

Für einen echten Play-Store-Eintrag (falls gewünscht) gibt es zwei Wege, beide packen nur die bestehende Website in eine App-Hülle, keine doppelte Pflege:
- **Trusted Web Activity via Bubblewrap** (Googles offizielles, kostenloses Tool) – einmaliger Aufwand, danach nur noch der einmalige Google-Play-Entwicklerkonto-Betrag (aktuell ca. 25 $ einmalig).
- **Fertiger Wrapper-Dienst** (z. B. Median.co, GoNative) – schneller eingerichtet, aber mit monatlicher Gebühr.

Beides ist ein späterer Schritt, kein Blocker für den aktuellen Start.
