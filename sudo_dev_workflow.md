# SUDO DEV WORKFLOW
> Mein Dev Workflow

---

## Tool-Stack

| Zweck | Tool |
|-------|------|
| Ideen & Concept Decks | Claude — WOTA Idea Vault Project |
| Planung & Wissen | Notion (Vision, Stories, ER, UI, Architektur) |
| Features & Sprints | Linear (Backlog, Cycles, Issues) |
| Code & Versionierung | GitHub (sudowota) |

---

## Übersicht

```
Phase 0 → Idee & Concept Deck       (WOTA Idea Vault)
Phase 1 → Vision & Scope            (Notion)
Phase 2 → User Stories              (Notion)
Phase 3 → ER-Modell                 (Notion)
Phase 4 → UI Skizzen                (Notion + Excalidraw)
Phase 5 → Architektur               (Notion)
Phase 6 → Features ins Linear       (Linear)
Phase 7 → Sprint-Zyklus             (Linear + GitHub, wiederholt)
Phase 8 → Done-Definition
```

---

## Phase 0 — Idee & Concept Deck

> Bevor ich plane, validiere ich meine Idee.

**Wo:** Claude Project "WOTA Idea Vault"

**Vorgehen:**
1. Idee entsteht → sofort ins WOTA Idea Vault Project
2. Die 7 Input-Felder ausfüllen (Projektname, Problem, Zielnutzer, Lösung, Tech-Ansatz, Differenzierung, Ziel)
3. Claude generiert das Concept Deck
4. Deck als `.md` Datei ablegen

**Entscheidung danach:**
```
Concept Deck fertig
      ↓
Baue ich das? 
  ├── Nein → Deck archivieren, Idee ruht
  └── Ja   → SUDO DEV WORKFLOW startet (Phase 1)
```

**Ablagestruktur:**
```
WOTA Idea Vault/
├── runit/
│   └── concept-deck.md
├── pairflow/
│   └── concept-deck.md
└── _archive/
```

---

## Phase 1 — Vision & Scope

> Einmalig pro Projekt. Bevor eine einzige Zeile Code geschrieben wird.

**Wo:** Notion — neue Projektseite

**Vorlage:**
```
Projektname:
Was ist es?      (1 Satz)
Für wen?         (Zielnutzer)
Kernproblem:     (Was löst es?)
MVP:             (Kleinste funktionierende Version)
Out of Scope:    (Was kommt NICHT rein — wichtig gegen Scope Creep)
Tech Stack:      (Frontend / Backend / DB / Hosting)
```
---

## Phase 2 — User Stories

> Hier beschreibe ich das Produkt aus Nutzerperspektive. Kein technisches Detail — nur was der Nutzer will.

**Wo:** Notion — Unterseite "User Stories"

**Format:**
```
Als [Nutzertyp] möchte ich [Aktion], damit [Nutzen].
```

**Akzeptanzkriterien pro Story:**
```
✅ Gegeben: [Ausgangssituation]
✅ Wenn:    [Nutzeraktion]
✅ Dann:    [Erwartetes Ergebnis]
```

**Beispiel:**
```
Story: Als CHORSÄNGER möchte ich ein TikTok-Video TEILEN,
       damit ich den Vocal Run als Noten sehen kann.

Akzeptanzkriterien:
✅ Gegeben: Nutzer ist eingeloggt
✅ Wenn:    Nutzer lädt MP4-Datei herunter (max. 30 Sek.)
✅ Dann:    System zeigt transkribierte Noten als Bild an
```

**Prioritäten:**
| Priorität | Bedeutung |
|-----------|-----------|
| 🔴 Hoch   | MVP — ohne das kein Produkt |
| 🟡 Mittel | Wichtig, aber nicht blockernd |
| 🟢 Niedrig | Nice-to-have, später |

---

## Phase 3 — ER-Modell

> Klärt die Datenstruktur bevor ich code.

**Wo:** Notion — Unterseite "ER-Modell"

**Vorgehen:**
1. Welche Entitäten (Objekte) gibt es? → Substantive aus den User Stories
2. Welche Attribute hat jede Entität?
3. Welche Beziehungen bestehen zwischen ihnen?

**Beziehungstypen:**
```
1:1   → Ein User hat einen Account
1:N   → Ein User hat viele Videos
N:M   → Viele Videos haben viele Tags
```

**Beispiel (Runit):**
```
USER
├── _id
├── name
├── email
└── createdAt

VIDEO
├── _id
├── userId (→ USER)
├── fileName
├── duration
└── uploadedAt

TRANSCRIPTION
├── _id
├── videoId (→ VIDEO)
├── notesData (JSON)
└── createdAt

Beziehungen:
USER     1:N  VIDEO
VIDEO    1:1  TRANSCRIPTION
```

---

## Phase 4 — UI Skizzen

> Ich Zeichne bevor ich baue, erst auf Papier, dann auf Figma.

**Wo:** Excalidraw → Screenshot in Notion einbetten

**Was skizzieren:**
- Alle Hauptscreens / Seiten
- Navigation zwischen Screens
- Wo welche Daten angezeigt werden

**Checkliste pro Screen:**
```
[ ] Screen-Name und Zweck klar?
[ ] Welche User Story löst dieser Screen?
[ ] Welche Daten werden angezeigt?
[ ] Welche Aktionen kann der Nutzer ausführen?
[ ] Navigation: Wohin kommt man von hier?
```


---

## Phase 5 — Architektur

> Grob skizzieren. Achtung, Over-Engineering.

**Wo:** Notion — Unterseite "Architektur"

**Vorlage:**
```
FRONTEND
└── [Framework] — z.B. React, TS
    └── Komponenten / Pages

BACKEND
└── [Framework] — z.B. Express.js
    ├── Routes
    ├── Controller
    ├── Middleware
    └── Models

DATENBANK
└── [DB] — z.B. MongoDB, PostgreSQL

EXTERNE SERVICES
└── z.B. Auth (JWT), Storage (S3), AI-API
```

**Dateistruktur (Beispiel Node/Express):**
```
project/
├── src/
│   ├── routes/
│   ├── controllers/
│   ├── models/
│   ├── middleware/
│   └── config/
├── tests/
├── .env
├── .gitignore
└── package.json
```

---

## Phase 6 — Features ins Linear

> Nach der Planung wandern alle Features als Issues in Linear. 

**Wo:** Linear — neues Projekt anlegen

**Linear-Setup pro Projekt:**
```
1. Neues Project in Linear anlegen (= mein Projektname)
2. Alle User Stories → einzelne Issues erstellen
3. Priorität setzen (Urgent / High / Medium / Low)
4. Label vergeben: Feature · Bug · Refactor · Docs · Test
5. MVP-Issues markieren → das ist dein erster Cycle
```

**Issue-Titel Konvention:**
```
[Feature]  User kann Video hochladen
[Feature]  Transkription wird als Noten angezeigt
[Bug]      Login schlägt bei falschem Passwort nicht fehl
[Docs]     README mit Setup-Guide schreiben
[Test]     Auth-Middleware testen
```

**Tipp:** Jede User Story aus Phase 2 = mindestens 1 Linear Issue. Große Stories in kleinere Issues aufteilen.

---

## Phase 7 — Sprint-Zyklus (Cycles in Linear)

> Wiederholt sich jede Woche. Das Herzstück des Workflows.
> In Linear heißen Sprints "Cycles".

### Sonntag — Sprint Planning (15 min)

```
1. Linear öffnen → Backlog ansehen
2. Neuen Cycle erstellen (1 Woche)
3. 3–5 Issues in den Cycle ziehen (nie mehr als 5)
4. Cycle-Ziel formulieren: "Diese Woche möchte ich X fertig haben"
```

---

### Täglich — Mini-Check (5 min)

```
1. Was habe ich gestern gemacht?
2. Was mache ich heute?
3. Gibt es einen Blocker? → Als Kommentar im Linear Issue notieren
```

---

### Git-Disziplin (pro Feature)

**Branch-Struktur:**
```
main
 └── develop
      ├── feature/login
      ├── feature/dashboard
      ├── fix/token-bug
      └── refactor/user-controller
```

**Commit-Konvention (Englisch):**
```
feat:     add JWT login route
fix:      resolve token expiry bug
test:     add auth middleware tests
docs:     update README setup guide
refactor: clean up user controller
chore:    update dependencies
```

**Tipp:** Linear Issues mit GitHub verbinden → Commits werden automatisch im Issue verlinkt.

**Regel:** Ein Commit = Eine Sache. Nie mehrere Features in einem Commit.

---

### Freitag — Sprint Review (15 min)

```
1. Linear Cycle schließen
2. Was ist Done? → bleibt Done
3. Was ist nicht fertig? → zurück in Backlog
4. Lesson Learned notieren (1 Satz in Notion)
5. Nächste Woche: Was ist die Priorität?
```

**Lesson Learned Format (Notion):**
```
Cycle X — [Datum]
Problem:  Ich habe zu viele Issues eingeplant
Lösung:   Nächste Woche max. 3 Issues statt 5
```

---

## Phase 8 — Done-Definition

> Ein Issue gilt erst als fertig wenn alle Punkte erfüllt sind.

```
[ ] Code läuft lokal ohne Fehler
[ ] Mindestens 1 Test geschrieben
[ ] Commit mit sauberem Message
[ ] Branch gemergt in develop
[ ] Linear Issue auf "Done" gesetzt
[ ] Kein offensichtlicher Bug
[ ] Kein console.log vergessen
```

---

## Tool-Setup Übersicht

**Notion-Struktur:**
```
📁 SUDO DEV
 └── 📁 Projekte
      └── 📁 [Projektname]
           ├── 📄 Vision & Scope
           ├── 📄 User Stories
           ├── 📄 ER-Modell
           ├── 📄 UI Skizzen (Excalidraw Screenshots)
           ├── 📄 Architektur
           └── 📄 Lesson Learned (Sprint Reviews)
```

**Linear-Struktur:**
```
🗂 [Projektname]
 ├── 📋 Backlog (alle Issues)
 ├── 🔄 Active Cycle (aktuelle Woche)
 └── ✅ Done
```

**GitHub-Struktur:**
```
github.com/sudowota/[projektname]
 ├── main
 └── develop
      └── feature/* / fix/* / refactor/*
```

---

## Schnellreferenz — Was mache ich wann?

| Wann | Was | Wo |
|------|-----|----|
| Neue Idee | Concept Deck generieren | WOTA Idea Vault (Claude) |
| Projekt startet | Phase 1–5 durchlaufen | Notion |
| Features definiert | Alle Issues anlegen | Linear |
| Jede Woche | Cycle planen (SO) + Review (FR) | Linear |
| Täglich | Mini-Check, Blocker notieren | Linear |
| Neues Feature coden | Branch erstellen → coden → testen → mergen | GitHub |
| Bug gefunden | `fix/` Issue in Linear + Branch in GitHub | Linear + GitHub |
| Task fertig? | Done-Definition checken | — |

---

## Die wichtigste Regel

> **Nie mehr als 5 aktive Issues gleichzeitig.**  
> Alles andere lebt im Linear Backlog — aus den Augen, aus dem Kopf, aber nicht verloren.

---

*SUDO DEV WORKFLOW — Moses Luta*
