# FlowQuery: slice

**Beschreibung:** Wenn keine weiteren Argumente angegeben werden, wird der komplette Context zurückgegeben. Ansonsten wird aus dem Context eine Menge Elemente herausgeschnittem die an einem Punkt (offset) beginnt und eine Länge (length) hat.

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\SliceOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/SliceOperation.php
```

**Beispiel(e):**

Gebe fünf Elemente ab dem Index 1 zurück:

```
${q(site).find('[instanceof TYPO3.Neos.NodeTypes:Page]').slice(1,5)}
```

```
// Die ersten 5 Elemente
${q(node).children("[instanceof My.Package:Post]").slice(0, 5)
// Elemente 1-6
${q(node).children("[instanceof My.Package:Post]").slice(1, 6)
```
