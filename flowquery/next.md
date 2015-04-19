# FlowQuery: next

**Beschreibung:** Die next-Operation arbeitet auf TYPO3CR Nodes. Die Operation iteriert über alle Context-Element und gibt jeden folgenden Geschwister-Node zurück bzw. die die durch den Filter-Ausdruck gefiltert werden.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\NextOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/NextOperation.php
```

**Beispiel(e):**

Gebe den nächsten Node zurück:

```
${q(documentNode).next('[instanceof TYPO3.Neos.NodeTypes:Page]').get(0)

// Ausgabe beispielsweise (wenn man auf der Seite parallel vor /produkte ist)
Node /sites/website/produkte@live[TYPO3.Neos.NodeTypes:Page]
```
