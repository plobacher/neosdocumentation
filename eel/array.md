# Eel Helper: Array

**Beschreibung:** Enthält Array Helper-Funktionen

**Implementierung:** `TYPO3\Eel\Helper\ArrayHelper`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/Helper/ArrayHelper.php
```

**Basis:** https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

**API:**

* `concat($array1, $array2, $array_ = NULL)`   
Fügt Arrays (oder Werte) zu einem neuen Array zusammen
* `join(array $array, $separator = ',')`   
Fügt Werte eines Arrays mit einem Separator-Zeichen zu einem String zusammen
* `slice(array $array, $begin, $end = NULL)`   
Extrahiert einen Teil des Arrays
* `reverse(array $array)`   
Dreht die Reihenfolge des Arrays um
* `keys(array $array)`   
Gibt die Array-Schlüssel zurück
* `length(array $array)`   
Gibt die Länge (Anzahl der Elemente) des Arrays zurück
* `isEmpty(array $array)`   
Prüft, ob das Array leer ist und gibt in diesem Fall TRUE zurück
* `first(array $array)`   
Gibt das erste Element des Arrays zurück
* `last(array $array)`   
Gibt das letzte Element des Arrays zurück
* `indexOf(array $array, $searchElement, $fromIndex = NULL)`   
Überprüft, ob ein Element im Array existiert und gibt im Erfolgsfall den Schlüssl zurück
* `random(array $array)`   
Gibt ein zufälliges Element aus dem Array zurück
* `sort(array $array)`   
Sortiert das Array über natsort() (erst Ziffern, dann Buchstaben)
* `shuffle(array $array, $preserveKeys = TRUE)`   
Ordnet das Array zufällig neu an
* `pop(array $array)`   
Entfernt das letzte Element des Arrays
* `push(array $array, $element)`   
Fügt ein (oder mehrere Elemente) am Ende des Arrays ein
* `shift(array $array)`   
Entfernt das erste Element eines Arrays
* `unshift(array $array, $element)`   
Fügt ein (oder mehrere Elemente) am Anfang des Arrays ein
* `splice(array $array, $offset, $length = 1, $replacements = NULL)`
Ersetzt eine Anzahl Elemente durch neue Elemente


**Beispiel(e):**

Zusammenfügen aller Nodes: 
```
${Array.join(q(site).find('[instanceof TYPO3.Neos.NodeTypes:Page]').get())}

// Ergebnis
Node /sites/website/subpage/subpage1@live[TYPO3.Neos.NodeTypes:Page],Node /sites/website/subpage@live[TYPO3.Neos.NodeTypes:Page],Node /sites/website/produkte@live[TYPO3.Neos.NodeTypes:Page],Node /sites/website/produkte/produkt1@live[TYPO3.Neos.NodeTypes:Page],Node /sites/website/produkte/produkt1/produkt11@live[TYPO3.Neos.NodeTypes:Page]
```