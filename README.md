# Via Romana

Interaktive Lernplattform mit vier statischen Seiten:
- Startseite (`/`)
- Magister-Portal (`/magister/`)
- Spielfeld (`/play/`)
- Regeln (`/rules/`)

Die App nutzt Firebase Authentication + Firestore (keine kostenpflichtigen Tools notwendig).

Aktueller Funktionsstand:
- `/magister/` ist ein Dashboard für Unterrichtsmaterialien
- `/play/` ist direkt spielbar (kein Zugangscode erforderlich)
- Das System ist in Deutsch und Englisch nutzbar (DE/EN Umschalter)

## Inhalte im Projekt

- `index.html`
- `magister/index.html`
- `play/index.html`
- `rules/index.html`
- `assets/logo.svg` (Logo)
- `assets/favicon.svg` (Tab-Icon / Favicon)
- `firebase/firestore.rules`
- `firebase/README.md` (Firebase Setup)

## 1) Firebase konfigurieren

1. Firebase Projekt erstellen.
2. In Authentication aktivieren:
   - E-Mail/Passwort (nur für Magister-Login)
3. Firestore aktivieren.
4. Firestore-Regeln aus `firebase/firestore.rules` einspielen.
5. In dieser Datei Firebase Config eintragen:
   - `magister/index.html`

## 2) Lokal testen

Einfacher lokaler Start mit Python:

```bash
cd /workspaces/viaromana
python3 -m http.server 8080
```

Dann im Browser öffnen:

```text
http://localhost:8080
```

## 3) Deploy auf GitHub Pages (empfohlen)

Das Repo ist statisch aufgebaut und direkt GitHub-Pages-fähig.

1. Änderungen committen und pushen:

```bash
git add .
git commit -m "Add deploy docs, logo and favicon"
git push origin main
```

2. In GitHub öffnen:
   - Repository Settings -> Pages
   - Source: Deploy from a branch
   - Branch: `main` + `/ (root)`

3. Speichern und kurz warten, dann ist die Seite live.

Hinweis:
- Datei `CNAME` ist bereits vorhanden. Damit bleibt eure Custom Domain aktiv.

## 4) Deploy auf Firebase Hosting

Das Projekt ist bereits vorkonfiguriert über `firebase.json`.
Die Standard-Projektbindung ist über `.firebaserc` auf `viaromanaeducation` gesetzt.

Einmalig:

```bash
npm install -g firebase-tools
firebase login
```

Projekt deployen (ohne `firebase init`):

```bash
cd /workspaces/viaromana
firebase deploy
```

Alternativ mit expliziter Projekt-ID:

```bash
firebase deploy --project viaromanaeducation
```

Optional nur Hosting deployen:

```bash
firebase deploy --only hosting --project DEIN_FIREBASE_PROJECT_ID
```

Optional Firestore Rules deployen:

```bash
firebase deploy --only firestore:rules --project DEIN_FIREBASE_PROJECT_ID
```

Hinweis:
- Falls du den Projektnamen dauerhaft speichern willst, kannst du lokal ausführen:

```bash
firebase use --add
```

## 6) Letzter Produktions-Schritt (einmalig in der Console)

Falls bei Login der Fehler `CONFIGURATION_NOT_FOUND` erscheint, ist Firebase Authentication im Projekt noch nicht initial aktiviert.

Einmal in der Firebase Console ausführen:
- Authentication -> Get started
- Sign-in method -> Email/Password aktivieren

Danach funktionieren Magister-Registrierung, Login und Materialverwaltung vollständig.

## 5) Logo und Favicon

- Logo: `assets/logo.svg`
- Tab-Icon: `assets/favicon.svg`

Das Favicon ist bereits in allen Seiten eingebunden:
- Startseite
- Magister
- Spielfeld
- Regeln
