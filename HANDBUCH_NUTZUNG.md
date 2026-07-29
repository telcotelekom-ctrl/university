# Gesamt-Handbuch für Finanziers01

## 1. Ziel des Systems

Dieses Projekt ist eine browserbasierte Unternehmens- und Bewerbungsplattform mit einem lokalen Runtime-Layer. Es verbindet:

- ein zentrales Portal im Root
- einen geführten Business-Workflow
- eine Bewerbungssuite
- einen lokalen Node.js-Server für API- und Datenfunktionen

Das System soll als Präsentationsplattform, Prototyp, Datenarchitektur-Blueprint und Grundlage für spätere Backend- oder Hosting-Integration dienen.

---

## 2. Übersicht der Projektstruktur

Die wichtigsten Ordner und Dateien sind:

- [index.html](index.html) – Hauptportal
- [bewerbung.html](bewerbung.html) – Bewerbungssuite
- [app/index.html](app/index.html) – Guided Business Suite
- [portal.js](portal.js) – Legacy-Referenz für alte Workflow-Logik
- [style.css](style.css) – gemeinsamer Stil-Helfer
- [server/server.js](server/server.js) – lokaler Runtime-Server
- [server/data](server/data) – lokale JSON-Daten
- [server/db/schema.sql](server/db/schema.sql) – Datenbank-Blueprint
- [legacy](legacy) – Archivierte Legacy-Versionen

---

## 3. Schnellstart

### Variante A: Ohne Server direkt im Browser starten

1. Öffne [index.html](index.html) in einem Browser.
2. Nutze die Navigation zum Business- oder Bewerbungsmodul.
3. Die Eingaben bleiben lokal gespeichert, solange der Browser-Cache bzw. der lokale Speicher erhalten bleibt.

### Variante B: Mit lokalem Server starten

1. Öffne ein Terminal im Projektordner.
2. Führe aus:

```bash
node server/server.js
```

3. Öffne anschließend:

- http://127.0.0.1:3000/
- http://127.0.0.1:3000/server/api/health

Die Health-Prüfung wurde erfolgreich verifiziert. Der Server antwortet mit Status 200 und dem JSON-Inhalt:

```json
{"ok":true,"runtime":"server-b","timestamp":"2026-07-28T16:03:51.603Z"}
```

---

## 4. Nutzung der Hauptmodule

### 4.1 Portal: [index.html](index.html)

Das Portal ist der Einstiegspunkt für Nutzer.

Es enthält:
- Überblick über die verschiedenen Module
- Business- und Bewerbungskonzepte
- Investor-Formulare
- eine eingebettete Shadow-Ansicht aus dem lokalen Runtime-Layer
- direkten Zugriff auf den Server-B-Bereich über das Portal

Portal-Zugang zu Server B:
- Vom Root-Portal aus wird im unteren Bereich eine Server-B-Shadow-Ansicht eingebunden.
- Der eigentliche Server-B-Zugriff läuft über die lokale Runtime-Adresse http://127.0.0.1:3000/.
- Zusätzlich sind die relevanten Server-B-Routen direkt erreichbar unter /legacy/index.html, /app/serverB/index.html und /app/serverB/data.json.

Empfehlung:
- Für neue Nutzer ist dies der beste Einstiegspunkt.
- Für technische Prüfungen sollte zuerst der Server gestartet und danach die Portal-Seite geöffnet werden.

### 4.2 Business Suite: [app/index.html](app/index.html)

Die Business Suite ist ein geführter Workflow für Gründer und Unternehmensentwickler.

Typische Nutzung:
- Unternehmensbasis eingeben
- Branding und Identität definieren
- Produkte und Services beschreiben
- Prozesse und Kontakte festhalten
- Inhalte exportieren oder drucken

Wichtige Hinweise:
- Die Daten werden im Browser gespeichert.
- Ein Reset löscht die lokal gespeicherten Daten.

### 4.3 Bewerbungssuite: [bewerbung.html](bewerbung.html)

Diese Suite dient zur Erstellung eines digitalen Bewerbungs- oder Präsentationsprofils.

Typische Nutzung:
- Name, Rolle und Fokus eintragen
- Medienform auswählen
- Link oder Datei ergänzen
- Medienkarten anlegen
- Vorschau und Exporte verwenden

Hinweis:
- Datei-Uploads werden im Browser verarbeitet und nicht zentral auf einem Server gespeichert.

### 4.4 Server-Runtime: [server/server.js](server/server.js)

Der lokale Server stellt API- und Runtime-Funktionen bereit und ist direkt über das Portal nutzbar.

Portal- und Runtime-Zugang:
- Root-Portal: [index.html](index.html)
- Server-B-Shadow-Ansicht: [app/serverB/index.html](app/serverB/index.html)
- Legacy-Variant: [legacy/index.html](legacy/index.html)

Wichtige Endpunkte:
- /server/api/health
- /server/auth/login
- /server/auth/me
- /server/auth/logout
- /server/api/investor/local
- /server/api/investor/global
- /server/api/investor/production
- /server/api/investor/time-index
- /server/api/investor/complete
- /server/api/workspaces
- /server/api/profiles
- /server/api/schema

Lokaler Admin-Account:
- E-Mail: raymond@serverb.local
- Passwort: serverb2026

---

## 5. Datenmodell und Speicherung

Das Projekt arbeitet aktuell mit zwei Ebenen:

1. Browser-State über localStorage
   - für Formulare, Schritte, Vorschau und UI-Zustände
   - ideal für schnelle Prototypen

2. Runtime-Daten über JSON-Dateien im Ordner [server/data](server/data)
   - Nutzer
   - Sessions
   - Workspaces
   - Profile
   - Investor-Daten

Wichtige lokale Storage-Keys sind unter anderem:
- ucb-business-workspace-state
- portal-application-state-v1
- bewerbung-suite-state-v1
- serverb-role

---

## 6. Typische Arbeitsabläufe

### Arbeitsablauf A: Präsentation vorbereiten

1. [index.html](index.html) öffnen
2. zum Business- oder Bewerbungsmodul navigieren
3. die Felder ausfüllen
4. die Ausgabe prüfen und exportieren

### Arbeitsablauf B: Lokale API testen

1. Server starten mit `node server/server.js`
2. Health-Endpoint prüfen
3. Login- oder Investor-API testen
4. Ergebnisse im Browser oder mit einem API-Tool überprüfen

### Arbeitsablauf C: Inhalte erweitern

1. relevante HTML-, CSS- oder JavaScript-Datei öffnen
2. Anpassungen vornehmen
3. im Browser prüfen
4. bei API-Änderungen den lokalen Server mitverfolgen

---

## 7. Entwicklung und Bearbeitung

### So arbeitet man am Projekt

- HTML-Dateien enthalten die Hauptstruktur
- CSS definiert das visuelle Erscheinungsbild
- JavaScript steuert Interaktion, State und Exports
- der Server ist aktuell ein lokaler Node-Server ohne Build-Schritt

### Empfohlene Arbeitsweise

- Änderungen zuerst im Browser testen
- bei API- oder Datenlogik-Änderungen den Server mitlaufen lassen
- Änderungen klein und nachvollziehbar halten
- Daten im lokalen Speicher regelmäßig prüfen

---

## 8. Häufige Probleme und Lösungen

### Problem: Die Seite wirkt leer oder nicht interaktiv

Mögliche Ursache:
- die Datei wurde nicht aus dem richtigen Ordner geöffnet

Lösung:
- [index.html](index.html) direkt öffnen oder den Server starten und die Root-URL aufrufen

### Problem: Der Server antwortet nicht

Lösung:
- prüfen, ob `node server/server.js` aktiv ist
- die Health-URL testen: http://127.0.0.1:3000/server/api/health

### Problem: Daten sind verschwunden

Ursache:
- Browser-Speicher oder Cache wurde gelöscht

Lösung:
- Eingaben erneut erfassen oder den Zustand neu laden

### Problem: Datei-Uploads oder Exporte funktionieren nicht wie erwartet

Lösung:
- prüfen, ob der Browser die Datei korrekt akzeptiert
- sicherstellen, dass die Seite nicht in einem zu restriktiven Browser-Kontext geöffnet ist

---

## 9. Empfohlene Reihenfolge für neue Nutzer

1. [index.html](index.html) öffnen
2. Business Suite testen
3. Bewerbungssuite testen
4. lokalen Server starten
5. API-Endpunkte verstehen
6. später auf echte Datenbank- und Backend-Integration erweitern

---

## 10. Nächste sinnvolle Schritte

Für die Weiterentwicklung des Systems sind diese Schritte sinnvoll:

- echte Datenbank statt JSON-Dateien einziehen
- Backend-API vollständig ausbauen
- Uploads und Exporte zentralisieren
- Investor-Cockpit, Founder-Workspace und Identity-Raum erweitern
- Hosting für eine echte Produktionsumgebung vorbereiten

---

## 11. Kurzfassung für den Alltag

Wenn du schnell arbeiten willst:

- Portal öffnen: [index.html](index.html)
- Business Workflow öffnen: [app/index.html](app/index.html)
- Bewerbung öffnen: [bewerbung.html](bewerbung.html)
- Server starten: `node server/server.js`
- Health prüfen: http://127.0.0.1:3000/server/api/health

Damit ist das System sofort nutzbar und die wichtigsten Funktionen sind erreichbar.

---

## 12. Admin- und Wartungs-Handbuch

### 12.1 Server verwalten

#### Starten

```bash
node server/server.js
```

#### Prüfen, ob der Server läuft

- Öffne http://127.0.0.1:3000/server/api/health
- Erwartete Antwort: Status 200 und JSON mit `ok: true`

#### Stoppen

- Strg+C im laufenden Terminal drücken

### 12.2 Datenpflege

Die wichtigsten Daten liegen im Ordner [server/data](server/data):

- [server/data/users.json](server/data/users.json)
- [server/data/sessions.json](server/data/sessions.json)
- [server/data/workspaces.json](server/data/workspaces.json)
- [server/data/profiles.json](server/data/profiles.json)
- [server/data/investor.json](server/data/investor.json)

Hinweise:
- Die Dateien sind lokale JSON-Quellen für Prototypen und Tests.
- Bei Änderungen an Strukturen oder Feldern muss die Logik im Server mitangepasst werden.
- Bei Problemen mit Sessions oder Login ist der Inhalt von [server/data/sessions.json](server/data/sessions.json) zu prüfen.

### 12.3 Fehlerbehebung

#### Server startet nicht

Prüfen:
- ob Node.js installiert ist
- ob der Befehl im richtigen Ordner ausgeführt wurde
- ob Port 3000 bereits von einem anderen Prozess belegt ist

#### Health-Endpoint antwortet nicht

Prüfen:
- ob der Server wirklich läuft
- ob die URL korrekt lautet
- ob ein Firewall- oder Proxy-Block vorliegt

#### Login funktioniert nicht

Prüfen:
- ob die Daten in [server/data/users.json](server/data/users.json) vorhanden sind
- ob das Passwort korrekt ist
- ob die Session-Datei nicht beschädigt ist

#### Daten sind plötzlich weg

Prüfen:
- Browser-Storage oder Cache
- Änderungen an [server/data](server/data)
- ob ein neuer Start den Seed-Status neu erzeugt hat

### 12.4 Wartungsempfehlungen

- Regelmäßig die lokalen JSON-Daten prüfen
- Änderungen an der Server-Logik sauber testen
- neue Features zuerst im Browser und dann über den API-Layer verifizieren
- bei Produktivierung auf echte Datenbank und Auth umstellen

### 12.5 Hosting- und Produktivierung

Für eine spätere Bereitstellung sind diese Schritte sinnvoll:

1. echte Datenbank statt JSON-Dateien einbauen
2. Backend-Login und CRUD-Logik zentralisieren
3. Datei-Uploads und Exporte serverseitig absichern
4. HTTPS und sichere Authentifizierung einführen
5. Deployment auf Hostinger, VPS oder ähnlichem vorbereiten

### 12.6 Kurzcheckliste für Administratoren

- [ ] Server läuft
- [ ] Health-Endpoint antwortet
- [ ] Datenordner ist vorhanden
- [ ] wichtige JSON-Dateien sind lesbar
- [ ] Browser-Startseite ist erreichbar
- [ ] Login- oder API-Funktion ist testbar
