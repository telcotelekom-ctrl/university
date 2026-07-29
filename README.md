# university

Statische Online-Version des Finanziers01-Portals, veröffentlicht über GitHub Pages.

## Live

Nach Aktivierung von GitHub Pages erreichbar unter:

```
https://telcotelekom-ctrl.github.io/university/
```

## Was online funktioniert (ohne Server)

- Alle HTML-, CSS- und Browser-JavaScript-Seiten
- Formulare, Berechnungen und Vorschau im Browser
- Speicherung über `localStorage` (nur im jeweiligen Gerät/Browser)
- Import und Export von JSON
- Druck- und PDF-Ansichten
- Statische Server-B-Shadow-Ansicht unter `app/serverB/`
- Externe Links (z. B. EGR Plan Studio)

## Was online NICHT funktioniert

GitHub Pages liefert nur statische Dateien aus und führt kein Node.js aus.
Deshalb sind folgende Funktionen aus dem ursprünglichen `server/`-Ordner
online nicht verfügbar:

- Echte Benutzerkonten, Login und Sessions
- Serverseitige Rollen und Berechtigungen
- Geräteübergreifende, zentrale Datenspeicherung
- E-Mail-Versand (SMTP)
- WebSockets und der PSY-TEL-Broadcast-Layer
- Geschützte API-Endpunkte unter `/server/api/*`

Diese Teile benötigen einen dauerhaft laufenden Node-Prozess oder einen
externen Dienst (z. B. Supabase). Sie sind bewusst nicht Teil dieses
statischen Deployments.

## Sicherheit

Dieses Repository enthält absichtlich keine Geheimnisse:
keine `.env`, keine Zugangsdaten, keine privaten Laufzeitdaten, kein `server/`.

## Lizenz

MIT (siehe `LICENSE`).
