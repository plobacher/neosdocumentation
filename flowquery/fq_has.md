# FlowQuery: has

**Beschreibung:** Filter ein Ergebnisset, indem es prüft, ob der angegebene Selektor, das Objekt, Array, tranversierbares Objekt oder FlowQuery Objekt enthalten ist.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\HasOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/GetOperation.php
```

**Beispiel(e):**

Wenn man `get()` nicht verwendet, bekommt man beim direkten Zugriff eine Fehlermeldung

```
closestParentWithImageChild = ${q(node).parents()
.has('[instanceof TYPO3.Neos.NodeTypes:Image]').first()}
```
