# FlowQuery: closest

**Beschreibung:** Die closest-Operation arbeitet auf TYPO3CR Nodes. Für jeden Node im Context wir der erste Node ermittelt, der durch Testen des Nodes selbst ermttelt wird und anschließendem Testen der Vorfahren bis ein Ergebnis gefunden wird.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\ClosestOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/ClosestOperation.php
```

**Beispiel(e):**

Suche den Pfad "produkte":

```
${q(node).closest('produkte').property('_path')}

// Ausgabe wenn "unterhalb" von "produkte" - z.B. /sites/website/produkte/produkt1
/sites/website/produkte
```
