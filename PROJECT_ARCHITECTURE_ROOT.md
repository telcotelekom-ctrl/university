# Projektarchitektur – Root-System

## 1. Ziel und Rolle des Systems

Das Root-System ist die zentrale Plattform dieses Workspace. Es bündelt aktuell drei Ebenen in einem gemeinsamen Produktkontext:

- das bestehende Frontend-Portal im Arbeitsroot
- den lokalen Server-B-Runtime-Layer für API- und Datenlogik
- eine neue, sauber strukturierte Public-Space-Produktionsumgebung in [Finanziers01s](../Finanziers01s)

Die aktuelle Umsetzung ist bewusst browserbasiert, lokal nutzbar und auf Produktreife ausgelegt. Sie dient als Präsentationsplattform, funktionaler Prototyp, Datenarchitektur-Blueprint und Basis für spätere Backend- und Hosting-Integration.

---

## 2. Aktueller Systemumfang

### 2.1 Arbeitsroot-Portal
Das Hauptportal liegt im Arbeitsroot in [index.html](index.html). Es enthält:

- Hero- und Navigationsbereich
- Business- und Bewerbungsmodule
- Investor-Rechenformulare
- Kontakt- und Profilbereiche
- eingebettete Shadow-Ansicht aus [app/serverB/index.html](app/serverB/index.html)

### 2.2 Business Suite
Die Guided-Workflow-Suite befindet sich in [app/index.html](app/index.html). Sie enthält:

- sechs Schritte mit Fortschritt und Vorschau
- Exportfunktionen
- Druckansicht
- Initiator-Modal
- lokale Persistenz über localStorage

### 2.3 Bewerbungssuite
Die Bewerbungssuite ist in [bewerbung.html](bewerbung.html) umgesetzt. Sie enthält:

- Profilbuilder
- Medienkarten und Uploadlogik
- Exportfunktionen
- Vorschau und Persistenz

### 2.4 Server-B-Shadow-Runtime
Die Rolle- und Sichtbarkeitsansicht in [app/serverB/index.html](app/serverB/index.html) arbeitet mit [app/serverB/data.json](app/serverB/data.json) und ergänzt das System um einen sichtbaren API-/Runtime-Layer.

### 2.5 Neue Public-Space-Produktionsumgebung
Die neue, saubere Public-Space-Struktur liegt in [Finanziers01s](../Finanziers01s) und enthält:

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

## 3. Architekturprinzipien

Die aktuelle Architektur folgt diesen Prinzipien:

- browserbasiert und lokal ausführbar
- Vanilla HTML, CSS und JavaScript statt Frameworks
- modulare Seitenstruktur mit klaren Verantwortlichkeiten
- lokale Persistenz über localStorage und JSON-Dateien
- API-Integration über den lokalen Runtime-Layer
- responsive, produktionsnahes UI für Desktop, Tablet und Mobile

---

## 4. Aktueller technischer Zustand

### 4.1 Frontend-Layer
Die Oberfläche besteht aus statischen HTML-Seiten und gemeinsam genutztem CSS/JS. Die Seiten sind direkt im Browser nutzbar und bleiben auch dann funktional, wenn keine externe API verfügbar ist.

### 4.2 Runtime-Layer
Der lokale Node.js-Server in [server/server.js](server/server.js) läuft auf Port 3000 und stellt Endpunkte bereit für:

- Health-Check
- Login und Sessions
- Investor-Berechnungen
- Profile und Workspaces
- Schema- und Strukturinformationen

### 4.3 Daten- und Persistenzmodell
Die aktuelle Architektur arbeitet mit zwei Ebenen:

1. Browser-State über localStorage
2. Runtime-Daten über JSON-Dateien im Ordner [server/data](server/data)

Verfügbare Daten-Dateien:

- [server/data/users.json](server/data/users.json)
- [server/data/sessions.json](server/data/sessions.json)
- [server/data/workspaces.json](server/data/workspaces.json)
- [server/data/profiles.json](server/data/profiles.json)
- [server/data/investor.json](server/data/investor.json)

Wichtige lokale Storage-Keys im Frontend:

- ucb-business-workspace-state
- portal-application-state-v1
- bewerbung-suite-state-v1
- serverb-role
- finanziers01s-investor-v1
- finanziers01s-business-v1
- finanziers01s-application-v1
- finanziers01s-identity-v1

---

## 5. Vollständiger Inhalt der aktuellen Codebasis

### 5.1 Root-Dateien
- [index.html](index.html) – Hauptportal mit Investor-, Business- und Bewerbungsfunktionen
- [bewerbung.html](bewerbung.html) – Bewerbungssuite mit Export und Vorschau
- [style.css](style.css) – gemeinsamer Stil-Helfer
- [portal.js](portal.js) – Legacy-Referenz für Workflow-Logik
- [PROJECT_ARCHITECTURE_ROOT.md](PROJECT_ARCHITECTURE_ROOT.md) – Architektur-Dokumentation
- [ROOT_CODE_REPORT.md](ROOT_CODE_REPORT.md) – Code- und Funktionsbericht

### 5.2 App-Ordner
- [app/index.html](app/index.html) – Guided Founder Workflow mit sechs Schritten
- [app/serverB/index.html](app/serverB/index.html) – Shadow-Frame-Ansicht
- [app/serverB/data.json](app/serverB/data.json) – Server-B-Datenmodell und Rollenstruktur

### 5.3 Server-Ordner
- [server/server.js](server/server.js) – Node.js-Server mit API-Routen und Seed-Daten
- [server/README.md](server/README.md) – kurze Runtime-Anleitung
- [server/db/schema.sql](server/db/schema.sql) – SQL-Blueprint für spätere Migration
- [server/data](server/data) – JSON-Seed-Daten

### 5.4 Neue Produktionsstruktur
- [Finanziers01s/index.html](../Finanziers01s/index.html) – neue responsive Landingpage
- [Finanziers01s/pages/portal.html](../Finanziers01s/pages/portal.html) – Portalbereich
- [Finanziers01s/pages/business.html](../Finanziers01s/pages/business.html) – Business Suite mit Formular und Export
- [Finanziers01s/pages/bewerbung.html](../Finanziers01s/pages/bewerbung.html) – Bewerbungsmodul
- [Finanziers01s/pages/investor.html](../Finanziers01s/pages/investor.html) – Investor Rechnung und Ergebnisdarstellung
- [Finanziers01s/pages/identity.html](../Finanziers01s/pages/identity.html) – Identity- und Copyright-Workflow
- [Finanziers01s/assets/css/enterprise.css](../Finanziers01s/assets/css/enterprise.css) – responsives Enterprise-Layout
- [Finanziers01s/assets/js/enterprise.js](../Finanziers01s/assets/js/enterprise.js) – funktionale Module und Persistenzlogik
- [Finanziers01s/sql/schema.sql](../Finanziers01s/sql/schema.sql) – vollständige MySQL-Schema-Definition
- [Finanziers01s/api/openapi.yaml](../Finanziers01s/api/openapi.yaml) – API-Contract mit Request/Response-Beispielen

---

## 6. Funktionale Aussage der aktuellen Plattform

Die Plattform enthält aktuell:

- einen produzierbaren Frontend-Portalaufbau
- einen Server-B-ähnlichen Runtime-Layer mit Health- und Datenendpunkten
- Business-, Bewerbungs-, Investor- und Identity-Workflows
- lokale Speicherung und Exportmechaniken
- eine saubere, responsive Public-Space-Struktur für spätere Bereitstellung

---

## 7. Aktueller Status und nächste Schritte

### Bereits umgesetzt
- Root-Portal und alle Kernmodule sind vorhanden
- Server-B-Integration ist adressierbar und lokal verifiziert
- neue Produktionsstruktur ist aufgebaut
- SQL-Blueprint und API-Contract liegen vor

### Noch offen
- echte Datenbank-Anbindung statt JSON-Seed-Daten
- vollständige Backend-API-Implementierung mit Auth, CRUD und Datei-Upload
- Deployment für Hostinger oder VPS
- weitere Konsolidierung aller Legacy-Komponenten in die neue Struktur

---

## 8. Erweiterungsideen und Zukunftsvision

### 8.1 Produktvision: Universal Company OS

Aus dem heutigen Portal kann ein vollständiges, modular aufgebautes Unternehmens- und Investoren-OS werden. Die Plattform kann nicht nur Präsentation und Bewerbung abbilden, sondern auch:

- Unternehmensprofile und Identität verwalten
- Investor- und Kapitalprozesse begleiten
- Bewerber- und Talentprozesse strukturieren
- Inhalte, Dokumente und Workflows in einem gemeinsamen Rahmen bündeln
- Rollen, Zugriffe und Sichtbarkeit für verschiedene Zielgruppen sauber abbilden

Die bestehende Struktur aus Frontend, Server-Runtime, Datenmodell und Schema ist hierfür bereits eine starke Ausgangsbasis.

### 8.2 Konkrete Erweiterungsmodule

#### 8.2.1 Investor Cockpit
Ein Dashboard für Investoren mit:

- Live-Übersicht über Unternehmensdaten
- Szenario- und Sensitivitätsberechnungen
- Vergleich von Funding-Optionen
- Export nach PDF, CSV oder Präsentationsformat

#### 8.2.2 Founder Workspace
Ein strukturierter Arbeitsbereich für Gründer mit:

- Aufgaben- und Meilensteinverwaltung
- Unternehmensstatus und Fortschrittsübersicht
- Dokumenten- und Mediensammlung
- automatischer Zusammenfassungs- und Berichtsgenerator

#### 8.2.3 Bewerbung und Talent Pipeline
Eine erweiterte Bewerbungspipeline mit:

- Bewerberprofilen und Lebensläufen
- Status-Tracking pro Rolle oder Projekt
- Bewertungslogik und Priorisierung
- Export von Shortlists und Auswahllisten

#### 8.2.4 Identity, Compliance und Dokumentenraum
Ein sicherer Bereich für:

- Unternehmensidentität und Rechtstexte
- Signatur- und Freigabeprozesse
- Dokumentenablage und Versionshistorie
- Zugang über Rollen und Freigaben

#### 8.2.5 Content- und Marketing-Hub
Ein zentraler Content-Bereich mit:

- Unternehmensstorytelling
- Fallstudien und News
- Portfolio- und Projektseiten
- automatischer Veröffentlichung über Templates

### 8.3 Nutzung der vorhandenen Mittel

Die vorhandenen Bausteine lassen sich direkt für diese Erweiterung nutzen:

- HTML-, CSS- und JavaScript-Seiten als Basis für neue Module
- der lokale Node.js-Server als API- und Runtime-Schicht
- JSON-Dateien und lokale Storage-Keys als schnelle Prototypen
- SQL-Schema und OpenAPI-Blueprint als Grundlage für echte Datenbankintegration
- bestehende Export- und Vorschau-Mechaniken für PDF, HTML und JSON
- Rollen- und Shadow-Struktur aus Server B für zukünftige Zugangskonzepte

### 8.4 Gute Erweiterungsmöglichkeiten mit den vorhandenen Mitteln

#### 8.4.1 Schnelle Wins
- Formularzustände dauerhaft speichern und wiederherstellen
- Exporte in PDF, CSV und Präsentationsformat erweitern
- Dashboard-Ansichten für Business-, Investor- und Bewerbungsdaten bauen
- Mehrsprachigkeit und Template-System einführen
- einfache AI-Assistenz für Zusammenfassungen und Textgenerierung ergänzen

#### 8.4.2 Mittelfristige Erweiterungen
- echte Datenbank-Anbindung mit PostgreSQL oder SQLite
- Login, Sessions und Rollenverwaltung serverseitig ausbauen
- Uploads, Dokumenten- und Medienverwaltung integrieren
- automatisierte Benachrichtigungen, Workflows und Erinnerungen implementieren
- PWA- und Mobile-Optimierung für Offline- und Touch-Nutzung

#### 8.4.3 Langfristige Visionen
- White-Label-Lösung für Agenturen, Berater oder Start-up-Programme
- SaaS-ähnliches Produkt mit Abonnement- und Nutzerverwaltung
- API-Ökosystem für externe Partner und Integrationen
- Analytics- und Reporting-Plattform für alle Workflows
- globale Plattform mit mehreren Marken, Branchen und Templates

### 8.5 Konkreter Fahrplan für die nächste Phase

1. Backend und Datenbank verbinden
2. Auth- und Rollenmodell vollständig ausbauen
3. zentrale State-Engine für alle Module etablieren
4. Dokumenten- und Medienverwaltung hinzufügen
5. AI-Assistenz und automatische Zusammenfassungen integrieren
6. Deployment und Hosting auf Hostinger, VPS oder Cloud vorbereiten

### 8.6 Chancen und Wirkung

Die größte Chance liegt darin, aus einer reinen Präsentations- und Demo-Umgebung ein echtes Produkt zu machen. Damit könnten aus dem aktuellen Setup:

- ein Gründer-Tool,
- ein Kapital- und Investor-Portal,
- eine Bewerbungs- und Talentplattform,
- ein internes Unternehmens-OS,
- oder ein whitelabel-fähiges Produkt

werden.

---

## 9. Fazit

Die Plattform ist jetzt nicht nur ein statischer Prototyp, sondern ein funktionaler, dokumentierter und strukturiert erweiterbarer Basisaufbau. Der Arbeitsroot enthält das bestehende Produkt, die neue produktionsnahe Struktur bietet eine klare Zukunftsarchitektur, und die vorhandenen Mittel reichen aus, um das System schrittweise in eine echte, skalierbare Plattform zu überführen.
