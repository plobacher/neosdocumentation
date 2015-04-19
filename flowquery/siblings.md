# FlowQuery: siblings

**Beschreibung:** Die parents-Operation arbeitet auf TYPO3CR Nodes. Sie iteriert auf allen Context-Elementen und gibt alle Geschwister-Knoten zurück.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\SiblingsOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/SiblingsOperation.php
```

**Beispiel(e):**

Gebe den Titel ersten Geschwister Node zurück:

```
${q(node).siblings().first().property('title')}
```
