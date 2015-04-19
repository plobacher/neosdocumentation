# Eel Helper: Date

**Beschreibung:** Enthält Datums-Helper-Funktionen

**Implementierung:** `TYPO3\Eel\Helper\DateHelper`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/Helper/DateHelper.php
```

**API:**

* `parse($string, $format)`   
Wandelt einen String anhand eines Formats in ein DateTime-Objekt um
* `format($date, $format)`   
Wandelt ein Datum (oder Interval) anhand eines Formats in einen String um
* `now()`   
Gibt das aktuelle DateTime-Objekt zurück
* `today()`   
Gibt das heutige DateTime-Objekt zurück
* `add($date, $interval)`   
Addiert ein Interval zu einem Datum und gibt das resultierende DateTime-Objekt zurück
* `subtract($date, $interval)`   
Subtrahiert ein Interval von einem Datum und gibt das resultierende DateTime-Objekt zurück
* `diff($dateA, $dateB)`   
Ermittelt die Differenz zwischen zwei Datums und gibt ein DateInterval-Objekt zurück
* `dayOfMonth(\DateTime $dateTime)`   
Gibt den Tag des Monates (als Integer) eines Datums zurück
* `month(\DateTime $dateTime)`   
Gibt den Monat (als Integer) eines Datums zurück
* `year(\DateTime $dateTime)`   
Gibt das Jahr eines Datums zurück
* `hour(\DateTime $dateTime)`   
Gibt die Stunde eines Datums zurück
* `minute(\DateTime $dateTime)`   
Gibt die Minute eines Datums zurück
* `second(\DateTime $dateTime)`   
Gibt die Sekunde eines Datums zurück

**Beispiel(e):**

Zusammenfügen aller Nodes: 
```
${Array.join(q(site).find('[instanceof TYPO3.Neos.NodeTypes:Page]').get())}

// Ergebnis
Augabe des aktuellen Jahres
```
${Date.year(Date.now())}
```

