# FlowQuery: cacheLifetime

**Beschreibung:** Ermittelt die minimale Cache-Lifetime für die spezifizierten Nodes

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\CacheLifetimeOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/CacheLifetimeOperation.php
```

**Beispiel(e):**

```
q(node).context({'invisibleContentShown':true}).children().cacheLifetime()
```
