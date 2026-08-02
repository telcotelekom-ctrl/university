# Master-Dokumentation

Die Projektstruktur besteht aus einem zentralen statischen Portal, einem serverlosen
ShadowOS-Kern und einem optionalen lokalen Node-Backend.

## 1. Sichtbare Ebene (statisch)
- [index.html](index.html) als Hauptportal
- [app/index.html](app/index.html) als App-Startpunkt
- [legacy/index.html](legacy/index.html) als Referenzstruktur

## 2. Kern-Ebene (serverlos)
- [shadow/](shadow) – ShadowOS-Module, Boot über `startShadowOS()`.
- Browser-nativ: WebCrypto-Identität, WASM-Kernel (Browser-Adapter), localStorage-Discovery.
- Kein Node erforderlich; lauffähig auf GitHub Pages.

## 2b. Universal Visual Runtime (UVR) – Produktivsoftware
- Grundsatz: **„Alles ist ein Objekt. Alles ist eine Regel. Alles andere erzeugt die Runtime."**
- Engine: [shadow/uvr-runtime.js](shadow/uvr-runtime.js) mit `UniversalVisualRuntime`,
  `createUvrManifest()`, `createUvrSummary()`, `adaptWordPressToUVR()`.
- Produktions-Manifest: [shadow/portal.vos.json](shadow/portal.vos.json) im `.vos`-Format
  (Manifest `myopenai.portal`, Hardware-Targets desktop/mobile/tv/terminal/vr/legacy).
- Portal-Sektion **„UVR Runtime"** in [index.html](index.html) mit echtem `.vos`-Import
  und `.vos`-Export. Renderer-Auswahl automatisch (`html`/`text`) – OS- und hardwareübergreifend.
- Vision-Seite: [final-cut.html](final-cut.html) (In-N-Out Volume Economy, funktionierende Wertfunktion).
- Gesamtsystem: [finaly-all.html](finaly-all.html) (FINALY ALL: Bildung, Inventur, Sprachen,
  Altersgruppen, Curriculum-Generator, JSON-Datenmodell).
- Developer-Bereich: [developer-universum.html](developer-universum.html) (SERVICESOFTWARE TEL1.NL) –
  28 Sprachen level-schaltbar mit `localStorage`-Speicherung, mehrsprachiger Live-Playground
  (JavaScript echt, andere simuliert), Konzept-Übersetzer, Snippet-Bibliothek, Developer-Curriculum
  und Fortschritts-Tracker.
- Developer-Manifest: [developer-manifest.html](developer-manifest.html) (Präambel, 8 Artikel,
  Code-Standard, signiert von Raymond Demitrio Tel).
- Universale Suche: [suche.html](suche.html) – client-seitige Suchmaschine über die gesamte
  Struktur mit Web-Worker-Pipeline, Vorhersage, Tippfehler-Toleranz, Bezugsworten und Fallback.
  Massentauglich ohne DB-Server-Flaschenhals (CDN, ein Such-Knoten pro Browser).
- Kein Demo: echte Fabrikations-Standardsoftware.

## 3. Optionale Backend-Ebene (nur lokal)
- [server/server.js](server/server.js) für API-, Companion- und WebSocket-Funktionalität
- [server/data](server/data) für lokale Zustände und Inhalte
- Portal degradiert ohne Backend sauber in den Offline-/Shadow-Modus.

## 4. Manifest & Dokumentation
- [MANIFEST_SHADOWOS.md](MANIFEST_SHADOWOS.md) / [shadowos-manifest.html](shadowos-manifest.html) (SHADOWOS Ω∞).
- [university-deploy](university-deploy) spiegelt die public-facing Live-Variante (GitHub Pages).

## 5. Nutzung
- Öffne [index.html](index.html); ShadowOS bootet im Browser.
- Optional das lokale Node-Backend starten, um /api/health, /api/status und /ws/companion zu nutzen.

## Betriebsstatus
- Kern: serverloses ShadowOS, browser-nativ.
- Portal: statisch, live auf GitHub Pages.
- Node-Backend: optional, nur lokal.