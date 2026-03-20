# Firebase Setup (Auth + Firestore, kostenlos)

Dieses Projekt nutzt nur:
- Firebase Authentication
- Cloud Firestore

Damit bleibt alles im kostenlosen Spark-Plan moeglich (abhängig von eurem Traffic).

## 1) Firebase Projekt anlegen
1. Firebase Console -> Neues Projekt erstellen.
2. Web-App registrieren.
3. SDK-Config in `magister/index.html` eintragen.

## 2) Authentication aktivieren
1. Authentication -> Sign-in method.
2. Aktivieren:
  - E-Mail/Passwort (fuer Magister)

## 3) Firestore aktivieren
1. Firestore Database erstellen (Produktionsmodus).
2. Datei `firebase/firestore.rules` als Security Rules einspielen.

## 4) Datenschema
- `materials/{MATERIAL_ID}`
  - `ownerUid: string`
  - `ownerEmail: string`
  - `title: string`
  - `type: string`
  - `description: string`
  - `url: string`
  - `createdAt: timestamp`
  - `updatedAt: timestamp`

## 5) Ablauf
- Magister registriert sich oder loggt sich ein.
- Magister legt Unterrichtsmaterialien im Dashboard an.
- Materialien werden in Firestore gespeichert.
- Das Spielfeld ist direkt und ohne Login spielbar.
