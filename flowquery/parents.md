# FlowQuery: parents

**Beschreibung:** Die parents-Operation arbeitet auf TYPO3CR Nodes. Sie iteriert auf allen Context-Elementen und gibt **alle** direkten Eltern-Nodes zurück oder nur diejenigen direkten Eltern-Nodes, die auf den optionalen Filter passen.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\ParentsOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/ParentsOperation.php
```

**WICHTIG:** Die parents-Operation kann mittels `first()` eingeschränkt werden - das Ergebnis ist identisch mit der `parent()` Operation: `${q(node).parents().first()}` ist identisch mit `${q(node).parent()}`

**Beispiel(e):**

Gebe den Titel der "letzten" Eltern-Node aus (also der im Baum ersten Node, die Eltern-Node der aktuellen Node ist):

```
${q(node).parents().last().property('title')}
```
