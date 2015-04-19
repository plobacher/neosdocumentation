# FlowQuery: is

**Beschreibung:** Überprüft, ob mindestens eines der Elemente im Kontext einem angegebenen Filter entspricht

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\IsOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/IsOperation.php
```

**Beispiel(e):**

Wenn die aktuelle Node vom Typ "Seite" ist, wird diese verwendet, wenn nicht, wird die Site-Node verwendet:

```
${q(node).is('[instanceof TYPO3.Neos.NodeTypes:Page]') ? q(node) : q(site)}
```
