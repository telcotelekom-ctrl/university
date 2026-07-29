# Codebericht – Gesamtportal Finanziers01

## 1. Überblick

Das Projekt ist aktuell ein browserbasiertes Frontend-System mit einem lokalen Runtime-Layer und einer neu aufgebauten Public-Space-Produktionsstruktur. Die Hauptfunktionalität ist über mehrere sichtbare Module verteilt:

- Root-Portal im Arbeitsroot in [index.html](index.html)
- Guided Founder Workflow in [app/index.html](app/index.html)
- Universal-Bewerbungssuite in [bewerbung.html](bewerbung.html)
- Server-B-Shadow-Runtime in [app/serverB/index.html](app/serverB/index.html)
- neue produktionsorientierte Public-Space-Umgebung in [Finanziers01s](../Finanziers01s)

Die aktive Workflow-Logik sitzt im HTML- und JavaScript-Code der jeweiligen Seiten; zusätzlich gibt es eine neue, sauber organisierte Frontend-Struktur mit responsiven Seiten und funktionalen Modulen.

---

## 2. Dateiübersicht und Verantwortung

### 2.1 [index.html](index.html)
Hauptportal des Arbeitsroots. Es enthält:

- Hero- und Navigationsbereich
- Modulübersicht für Investor-, Business- und Bewerbungssuite
- Bewerbungskonfigurator mit Live-Vorschau
- mehrere Investor-Rechenformulare
- Kontakt- und Profilbereich
- eingebettete Shadow-Ansicht aus [app/serverB/index.html](app/serverB/index.html)

### 2.2 [app/index.html](app/index.html)
Business-Constellation-Suite mit Guided-Workflow. Sie enthält:

- sechs Schritte mit Fortschrittsanzeige
- Pflichtfelder pro Schritt
- Live-Vorschau und Export-Downloads
- Druckansicht
- Initiator-Modal
- lokale Persistenz über localStorage

### 2.3 [bewerbung.html](bewerbung.html)
Universal-Bewerbungssuite als funktionales Präsentationsmodul. Sie enthält:

- Builder-Formular für Name, Rolle, Fokus, Medienform und Beschreibung
- Live-Vorschau
- Medienkarten-Liste
- Dateiupload über FileReader
- Exporte als HTML, Markdown, JSON und PDF-Preview
- lokale Speicherung über localStorage

### 2.4 [app/serverB/index.html](app/serverB/index.html)
Rollenbasierte Shadow-Ansicht mit sichtbaren Bereichen, Drag-and-Drop-Logik und Security-Layer. Die Daten stammen aus [app/serverB/data.json](app/serverB/data.json).

### 2.5 [server/server.js](server/server.js)
Node.js-basierter lokaler Runtime-Server. Er hostet die Projektseiten und stellt API-Endpunkte für Health, Login, Investor-Modelle, Profiles und Workspaces bereit.

### 2.6 [portal.js](portal.js)
Ältere, separat gehaltene Implementierung eines Guided-Workflows. Sie ist als Legacy-Referenz erhalten, aber nicht mehr die aktive Hauptlogik.

### 2.7 [style.css](style.css)
Gemeinsamer Stil-Helfer mit visueller Designbasis.

### 2.8 Neue Produktionsstruktur in [Finanziers01s](../Finanziers01s)
Diese neue Struktur enthält die produktionsnahen Seiten und die Blueprint-Dateien:

- [Finanziers01s/index.html](../Finanziers01s/index.html)
- [Finanziers01s/pages/portal.html](../Finanziers01s/pages/portal.html)
- [Finanziers01s/pages/business.html](../Finanziers01s/pages/business.html)
- [Finanziers01s/pages/bewerbung.html](../Finanziers01s/pages/bewerbung.html)
- [Finanziers01s/pages/investor.html](../Finanziers01s/pages/investor.html)
- [Finanziers01s/pages/identity.html](../Finanziers01s/pages/identity.html)
- [Finanziers01s/assets/css/enterprise.css](../Finanziers01s/assets/css/enterprise.css)
- [Finanziers01s/assets/js/enterprise.js](../Finanziers01s/assets/js/enterprise.js)
- [Finanziers01s/sql/schema.sql](../Finanziers01s/sql/schema.sql)
- [Finanziers01s/api/openapi.yaml](../Finanziers01s/api/openapi.yaml)

---

## 3. Aktuelle technische Architektur

### 3.1 Frontend-Stack
Das Projekt verwendet:

- HTML für Struktur
- CSS für Layout, Branding und Oberfläche
- Vanilla JavaScript für Interaktivität und State-Handling
- localStorage für Persistenz
- JSON-Dateien im Server-Ordner für Runtime-Daten
- Fetch für API- und Fallback-Requests
- FileReader für Uploads in der Bewerbungssuite

### 3.2 Runtime-Stack
Für die Server-B-Erweiterung wurde ein lokaler Node.js-Layer hinzugefügt. Er ist aktuell ein Prototyp, aber funktionsfähig im lokalen Setup.

### 3.3 Produktive Public-Space-Struktur
Die neue Struktur unter [Finanziers01s](../Finanziers01s) ist bewusst modular und responsive aufgebaut. Sie enthält separate Seiten für Portal, Business, Bewerbung, Investor und Identity und nutzt zentrale Styles und Skripte.

---

## 4. Detaillierte Funktionsbeschreibung

### 4.1 Root-Portal in [index.html](index.html)
Die Hauptseite bündelt folgende Funktionen:

- Hero- und Navigationsbereich
- Business- und Bewerbungsmodule
- Investor-Kalkulationsformulare
- Kontakt- und Profilbereiche
- eingebettete Server-B-Shadow-Ansicht

### 4.2 Investor-Kalkulator in [index.html](index.html)
Die Kalkulator-Module sind für folgende Szenarien angelegt:

- lokale Kapitalflüsse
- globale BPP-Modelle
- Produktionskosten
- Zeitkosten-Leitzahl
- kombinierte Berechnung

Die neue Public-Space-Variante in [Finanziers01s/pages/investor.html](../Finanziers01s/pages/investor.html) implementiert diese Logik direkt mit lokalem Ergebnis-Rendering und Persistenz.

### 4.3 Business Suite in [app/index.html](app/index.html)
Die Business-Suite ist der Guided-Founder-Workflow. Sie ist aufgebaut als sechs Schritte, die den Nutzer durch Unternehmensbasis, Branding, Produkte, Prozesse, Kontakte und Exporte leiten.

Die neue Variante in [Finanziers01s/pages/business.html](../Finanziers01s/pages/business.html) ergänzt das Muster um eine Live-Summary und Exportfunktion.

### 4.4 Bewerbungssuite in [bewerbung.html](bewerbung.html)
Die Bewerbungssuite ist ein eigenständiges, interaktives Profil- und Medienmodul. Die Funktionalität umfasst:

- Formularfelder für Name, Rolle, Fokus, Medienform und Beschreibung
- Listenstruktur für Medienkarten
- optionalen Dateiupload mit FileReader
- Exporte und Vorschau

Die neue Variante in [Finanziers01s/pages/bewerbung.html](../Finanziers01s/pages/bewerbung.html) übernimmt diese Funktionalität in einer saubereren Seitenstruktur.

### 4.5 Server B in [app/serverB/index.html](app/serverB/index.html)
Server B ist ein sichtbarer Shadow-Frame, der über [app/serverB/data.json](app/serverB/data.json) arbeitet. Die Oberfläche zeigt:

- Module je Rolle
- Bereiche je Rolle
- Sicherheitsinformationen
- Drag-and-Drop-Interaktion

Die neue Public-Space-Struktur bindet die gleiche Datenbasis über die Runtime-Statuslogik ein.

---

## 5. Persistenz- und Zustandsmodell

Die aktuelle Architektur arbeitet mit mehreren Persistenzschichten:

### 5.1 Browser-State
- localStorage für Workflows, Formulare und UI-Zustände
- z. B. ucb-business-workspace-state, bewerbung-suite-state-v1, serverb-role

### 5.2 Runtime-Daten
- JSON-Dateien im Ordner [server/data](server/data)
- u. a. [server/data/users.json](server/data/users.json), [server/data/profiles.json](server/data/profiles.json), [server/data/workspaces.json](server/data/workspaces.json)

### 5.3 Neue Public-Space-Storage-Keys
Die neue Struktur verwendet zusätzlich:

- finanziers01s-investor-v1
- finanziers01s-business-v1
- finanziers01s-application-v1
- finanziers01s-identity-v1

---

## 6. Runtime- und Datenfluss

### 6.1 API-Endpunkte
Der lokale Server in [server/server.js](server/server.js) stellt aktuell Endpunkte für Health, Auth, Investor-Modelle, Workspaces und Profiles bereit.

### 6.2 Datenhaltung
Aktuell wird auf drei Ebenen gespeichert:

- Browser-State via localStorage
- Runtime-Daten in JSON-Dateien im Ordner [server/data](server/data)
- zukünftige persistente Struktur über [Finanziers01s/sql/schema.sql](../Finanziers01s/sql/schema.sql)

### 6.3 Verifikation
Die Runtime wurde lokal verifiziert. Der Health-Endpoint antwortet erfolgreich, und die Server-B-Daten werden korrekt ausgeliefert.

---

## 7. Produktions- und Hosting-Konzept

### 7.1 Aktueller Zustand
Die Plattform ist aktuell kein vollständiger Backend-Stack im klassischen Sinn, aber sie hat eine klare Backend- und Datenarchitektur-Blueprint erhalten.

### 7.2 Hostinger-spezifische Einordnung
Für Hostinger wäre die sinnvolle Aufteilung:

1. Frontend-Hosting
   - alle HTML-, CSS-, JS- und Medien-Dateien im öffentlichen Root-Verzeichnis

2. API-/Runtime-Layer
   - Node.js- oder vergleichbare Runtime

3. Datenbank-Layer
   - MySQL/MariaDB auf Basis von [Finanziers01s/sql/schema.sql](../Finanziers01s/sql/schema.sql)

### 7.3 Empfohlene nächste Stufe
Die nächste Stufe wäre:

1. Backend-API vollständig implementieren
2. Auth- und CRUD-Logik auf echte Datenbank umstellen
3. Dateiuploads und Exporte zentralisieren
4. Deployment für Hostinger oder VPS vorbereiten

---

## 8. Stärken und Grenzen

### Stärken

- hohe Präsentationsqualität
- gute Browser- und Offline-Nutzung
- klare Trennung von Portal, Workflow und Bewerbung
- funktionale Exporte, Live-Vorschau und Server-B-Prototyp
- konsistente Navigation über interne Anker
- neue strukturierte Public-Space-Produktionsumgebung

### Grenzen

- echtes Backend und Datenbank-Layer sind noch nicht vollständig verbunden
- Exporte und Uploads müssen weiter serverseitig zentralisiert werden
- die Legacy-Module sind noch nicht vollständig in die neue Struktur migriert

---

## 9. Erweiterungs- und Innovationsfelder

### 9.1 Schnell realisierbare Ideen

- Dashboard-Ansichten für Unternehmensstatus, Investoren und Bewerber ergänzen
- bestehende Formulare mit einer echten Datenbank verbinden
- Exporte um PDF-, CSV- und Präsentations-Formate erweitern
- Rollen- und Freigabeeinstellungen in die UI einbauen
- einfache AI-Assistenz für Zusammenfassungen, Vorschläge und Übersetzungen hinzufügen

### 9.2 Starke Zukunftsoptionen

- White-Label-Plattform für Agenturen und Beratungsunternehmen
- B2B-Portal für Investment- oder Accelerator-Programme
- Bewerber- und Talentmanagement-Plattform mit Status-Tracking
- Dokumenten- und Wissenstransfer-System für Teams und Partner
- Mobil- und Offline-Variante als Progressive Web App

### 9.3 Ausbau mit den vorhandenen Mitteln

Die bestehende Basis kann direkt für diese Richtung genutzt werden:

- Frontend-Seiten und UI-Module als Kern für neue Produktbereiche
- lokal laufender Server als API-Layer für erste Tests und Prototypen
- JSON- und Storage-Mechaniken als schnelle Persistenzschicht
- SQL-Schema und API-Contract als Blueprint für die produktive Version
- vorhandene Export- und Render-Logik für Präsentation, Dokumentation und Sharing

### 9.4 Empfehlung für die nächste Produktphase

1. alle Formulare und Workflows an eine zentrale Datenhaltung koppeln
2. Auth, Rollen und Audit-Logs ergänzen
3. die wichtigsten Workflows in einem gemeinsamen Dashboard bündeln
4. die Plattform um AI- und Automatisierungskomponenten erweitern
5. sie für Hostinger, VPS oder Cloud-Deployment vorbereiten

---

## 10. Fazit

Die aktuelle Codebasis ist bereits ein funktionaler, gut strukturierter Frontend-Ansatz mit einem lokal laufenden Server-B-Prototyp und einer neuen, produktionsnahen Public-Space-Struktur. Sie ist für Demo, Präsentation, frühe Produktvalidierung, moderne Erweiterungen und eine saubere Weiterentwicklung bestens geeignet und stellt damit eine solide Basis für die nächste Stufe dar.
