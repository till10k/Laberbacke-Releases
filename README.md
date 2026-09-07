# Laberbacke — Auslieferung

Hier liegt die fertige App zum Herunterladen. Der Quelltext liegt woanders und ist privat.

## Herunterladen

Die jeweils neueste Fassung steht unter **[Releases](../../releases/latest)**:

| Datei | Wofür |
|---|---|
| `Laberbacke-<version>.dmg` | Die App |
| `Laberbacke-<version>.dmg.sha256` | Prüfsumme — **vor dem Öffnen vergleichen** |
| `INSTALLATION.txt` | Schritt für Schritt, inklusive Gatekeeper und Bedienungshilfen |
| `DATENSCHUTZ.txt` | Was das Gerät verlässt und was nicht |
| `appcast.json` | Der Fassungsstand, den die App selbst abfragt |

## Voraussetzungen

- **Mac mit Apple Silicon** (M1 oder neuer). Intel-Macs werden nicht unterstützt.
- **macOS 14 oder neuer.**
- Ein Konto, das der Betreiber angelegt hat. Es gibt keine Selbstregistrierung.

## Vor dem ersten Start

Die App ist selbst signiert und **nicht notarisiert**. macOS weist sie beim ersten
Doppelklick deshalb ab — oft mit der irreführenden Meldung, sie sei „beschädigt".
Das ist sie nicht. Der Weg steht in `INSTALLATION.txt`; er dauert einen Klick in
den Systemeinstellungen und ist einmalig.

## Prüfsumme vergleichen

```bash
shasum -a 256 ~/Downloads/Laberbacke-<version>.dmg
```

Der Wert muss zeichengleich mit dem in `Laberbacke-<version>.dmg.sha256` sein.
Stimmt er nicht überein: nicht öffnen.
