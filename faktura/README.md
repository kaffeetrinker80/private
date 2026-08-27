# Faktura

**Rechnungen & Angebote als einzelne HTML-Datei – offline, ohne Server, mit SEPA-QR.**

Eine einzelne HTML-Datei zum Erstellen von Rechnungen und Angeboten. Kein Server, kein Build,
keine Abhängigkeiten, keine Tracker – einfach `Faktura_1.3.0.html` im Browser öffnen.
Alle Daten bleiben auf dem eigenen Gerät bzw. im selbst gewählten Arbeitsordner.

## Funktionen

- **Angebot und Rechnung** in einem Dokument – umschaltbar, inkl. eigener Nummernkreise
- **Positionen wahlweise mit Stundensatz** (Stunden × Satz) oder als Pauschalbeträge
- **Kleinunternehmer (§ 19 UStG) oder Umsatzsteuer-Ausweis** mit frei wählbarem Satz
- **SEPA-Zahlungs-QR** nach EPC-Standard, offline erzeugt – scannbar mit jeder Banking-App
- **Profile**: mehrere Absender (z.B. zwei Gewerbe) in einer Installation, jederzeit umschaltbar
- **Rückgängig / Wiederherstellen** über Knöpfe oder `Strg+Z` / `Strg+Y`
- **Kundenverwaltung** je Profil
- **Bearbeitungsstand je Dokument** direkt in der Kopfleiste: einzeln abhakbare Stufen mit Datum –
  Rechnung *Gestellt · Bezahlt · Gebucht*, Angebot *Versendet · Angenommen*.
  *Storniert* bzw. *Abgelehnt* überschreibt die Anzeige, ohne die erfassten Stufen zu löschen
- **Arbeitsordner (OneDrive, iCloud Drive, lokal)**: Ordner einmal pro Gerät wählen,
  alles Weitere legt das Tool selbst an – damit arbeitet man auf mehreren Rechnern am selben Stand
- **Dokumentenübersicht** aller gesicherten Rechnungen und Angebote mit Suche, Jahres-, Art- und Statusfilter,
  inklusive Summe der offenen Beträge
- **Protokoll** aller Aktionen (angelegt, gesichert, gedruckt, Status geändert) mit Gerätekennung
- **Automatische Entwurfssicherung** lokal und im Arbeitsordner – auch geräteübergreifend
- **Druck-/PDF-Layout** für A4 mit Faltmarken und Fensterumschlag-Adresszeile,
  sechs Farbschemata mit Vorschau und Abfrage vor jedem Druck: kräftig für den PDF-Versand
  oder druckfreundlich fürs Papier

## Erste Schritte

1. `Faktura_1.3.0.html` herunterladen und im Browser öffnen (Chrome oder Edge empfohlen).
2. Beim ersten Start öffnen sich die Einstellungen: Absender, Steuerangaben und Bankverbindung eintragen.
3. Optional **Arbeitsordner wählen** (⚙ oder das Ordner-Feld oben rechts) – z.B. einen Ordner in OneDrive.
4. Fertig. `💾 Sichern` legt das Dokument im Verlauf und im Arbeitsordner ab, `⎙ Drucken / PDF` erzeugt die Ausgabe.

## Ordnerstruktur

Nach der Auswahl eines Arbeitsordners – z.B. `OneDrive/Gewerbe/Rechnungstool/` – legt das Tool
selbstständig an:

```
Rechnungstool/
├─ Profil/
│  └─ profil.json          Absenderprofile, Bankverbindungen, Kunden
├─ Rechnungen/
│  ├─ 2026/
│  │  ├─ Re_R2026-001_2026-06-14_Musterfirma.json
│  │  └─ An_A2026-004_2026-07-02_Beispiel-GmbH.json
│  └─ 2027/
└─ System/
   ├─ index.json           Verlauf (Metadaten, Status) – jederzeit neu erzeugbar
   ├─ log.jsonl            Protokoll, zeilenweise angehängt
   └─ autosave.json        aktueller Entwurf, geräteübergreifend
```

Jedes Dokument ist eine eigene kleine Datei. Das ist bewusst so: beim Speichern wird nur diese eine
Datei angefasst, was Sync-Konflikte über mehrere Geräte praktisch ausschließt.
`index.json` ist lediglich ein Suchindex – geht er verloren, erzeugt
**Ordner neu einlesen** ihn vollständig aus den vorhandenen Dokumenten neu.

## Mehrere Geräte

Denselben Ordner auf jedem Gerät einmal auswählen; die Freigabe bleibt gespeichert.
Beim Start gleicht das Tool Profile, Verlauf und Entwurf ab. Wurde zuletzt auf einem anderen Gerät
gearbeitet, fragt es nach, ob dieser Entwurf übernommen werden soll.

Die Ordner-Anbindung nutzt die File System Access API und funktioniert in **Chrome und Edge am Desktop**.
In Safari und auf Mobilgeräten läuft alles Übrige unverändert – dort werden Dokumente lokal im Browser
gespeichert und lassen sich über `⋯ → Als JSON exportieren / JSON-Datei laden` austauschen.

## Datenschutz

Im Quelltext stehen keinerlei personenbezogene Daten. Es gibt keine Netzwerkaufrufe außer dem Laden
der Schriftarten von Google Fonts; wer auch das vermeiden will, entfernt die `<link>`-Zeile im
`<head>` – die Datei bleibt voll funktionsfähig und nutzt dann Systemschriften.

`.gitignore` schließt eigene Profil- und Rechnungsdaten aus, damit beim Forken nichts Privates
versehentlich im Repository landet. `beispiel-profil.json` zeigt das Format eines Profils.

## Tastenkürzel

| Kürzel | Funktion |
| --- | --- |
| `Strg`/`Cmd` + `S` | Dokument sichern |
| `Strg`/`Cmd` + `Z` | Rückgängig |
| `Strg`/`Cmd` + `Y` | Wiederherstellen |
| `Esc` | Dialoge und Menüs schließen |

## Hinweis

Die Vorlage erzeugt Dokumente nach üblichen Pflichtangaben, ersetzt aber keine steuerliche Beratung.
Ob die Angaben im konkreten Fall vollständig sind, klärt am besten das Steuerbüro.

## Beim Forken anpassen

Die Fußzeile unter dem Dokument enthält einen Feedback-Link auf eine feste E-Mail-Adresse
(`cryptopower@outlook.de`). Wer das Tool für sich übernimmt, ersetzt sie im `<footer>` bzw. in der
Zeile mit `footer-feedback` im Script. Die Fußzeile wird beim Drucken ausgeblendet und erscheint
nie auf der Rechnung.

## Lizenz

MIT – siehe `LICENSE`.
