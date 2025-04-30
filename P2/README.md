## Aufgabe 1

### Hauptfunktionen:

* Aufgabe hinzufügen: Titel (Pflichtfeld), Beschreibung (optional).
* Aufgabe als "erledigt" markieren (z. B. Checkbox).
* Aufgabenliste anzeigen (Titel, Beschreibung, Status).

### Ziele:

* Einfache Bedienung ohne komplexe Features.
* Klare visuelle Darstellung der Aufgaben.
* Zuverlässige Speicherung der Aufgaben (z. B. lokal im Browser oder in einer Datei).

### Nicht-funktionale Anforderungen:

* Die App soll auf mobilen Geräten und Desktop-Browsern funktionieren (responsives Design).
* Daten sollen zwischen Sessions gespeichert werden (z. B. via localStorage).

### Risikoanalyse:

* Was passiert, wenn der Benutzer eine leere Aufgabe hinzufügt? (Validierung benötigt!)
* Wie wird mit Duplikaten umgegangen?

### Erweiterbarkeit:

* Soll die App später um Kategorien oder Deadlines erweitert werden können?

## Aufgabe 3

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Einkaufen gehen",
      "description": "Milch, Brot, Eier",
      "done": false,
      "priority": "medium"  // Optional für spätere Erweiterung
    },
    {
      "id": 2,
      "title": "Meeting vorbereiten",
      "description": "Präsentation finalisieren",
      "done": true,
      "priority": "high"
    }
  ]
}
```

## Aufgabe 4

 | Testfall	| Aktion | Erwartetes Ergebnis |
 | --- | --- | --- |
| Aufgabe hinzufügen | Aufgabe erscheint in der Liste |
|	Aufgabe erledigen | Visuelle Markierung (durchgestrichen) | 
|	Leeren Titel hinzufügen| Fehlermeldung, keine Speicherung | 
|	Browser-Neustart | Daten bleiben erhalten | 
|	Duplikat hinzufügen | Warnung/Unterscheidung |
