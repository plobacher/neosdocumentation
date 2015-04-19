# FlowQuery: prev

**Beschreibung:** Die prev-Operation arbeitet auf TYPO3CR Nodes. Die Operation iteriert über alle Context-Element und gibt jeden vorhergehende Geschwister-Node zurück bzw. die die durch den Filter-Ausdruck gefiltert werden.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\PrevOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/PrevOperation.php
```

**Beispiel(e):**

Gebe den vorhergehenden Node zurück:

```
${q(documentNode).prev('[instanceof TYPO3.Neos.NodeTypes:Page]').get(0)

// Ausgabe beispielsweise (wenn man auf der Seite parallel nach /subpage ist)
Node /sites/website/subpage@live[TYPO3.Neos.NodeTypes:Page]
```
