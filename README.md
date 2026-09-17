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

## Schritt 2: Mit GitHub Pages live schalten

**Update 17.09.2026:** Cloudflare hat sein Dashboard umgebaut – der frühere einfache "Pages"-Weg ("Dateien hochladen, fertig") ist verschwunden, alles läuft jetzt über "Workers" und bräuchte zusätzlich eine technische Konfigurationsdatei. Das ist für eine reine statische Seite unnötig kompliziert geworden. Stattdessen: **GitHub Pages** – direkt in GitHub eingebaut, kein zweiter Account, keine Konfigurationsdatei nötig, macht genau das, was Cloudflare Pages früher gemacht hat.

1. Im Repository (z. B. `DropRadar-V001`) oben auf **„Settings"** klicken (Zahnrad-Symbol in der Kopfzeile).
2. In der linken Seitenleiste ganz unten auf **„Pages"** klicken.
3. Unter „Build and deployment" → „Source": **„Deploy from a branch"** auswählen (meist schon voreingestellt).
4. Branch: **„main"**, Ordner: **„/ (root)"** → **„Save"** klicken.
5. Nach ca. 1 Minute steht oben auf dieser Seite die fertige Live-URL, z. B. `https://hack-guru.github.io/DropRadar-V001/`.

Jede spätere Änderung, die du auf GitHub hochlädst oder über das Stift-Symbol bearbeitest, wird automatisch neu deployed – genau wie vorher geplant, nur eben direkt über GitHub statt über Cloudflare.

## Schritt 3 (später): eigene Domain

1. Domain bei einem Registrar deiner Wahl kaufen (z. B. über Cloudflare Registrar, oder woanders) – das ist der einzige Punkt, an dem wirklich Geld fließt (~10–15 €/Jahr).
2. Im Repository unter Settings → Pages → „Custom domain" die gekaufte Domain eintragen.
3. Beim Domain-Anbieter (bzw. bei Cloudflare, falls die Domain dort verwaltet wird) einen CNAME-Eintrag auf `hack-guru.github.io` setzen – GitHub zeigt beim Eintragen der Domain genau an, welcher DNS-Eintrag nötig ist.

Cloudflare kann dabei trotzdem sinnvoll bleiben – einfach nur als DNS-Verwalter/CDN vor der GitHub-Pages-Seite, ganz ohne den komplizierten Workers-Weg von oben.

Die beiden angelegten Cloudflare-Worker-Projekte (`dropradar-website`, `designartlab-website`) brauchen wir nicht mehr – die kannst du einfach stehen lassen oder unter Compute → Workers löschen.

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
