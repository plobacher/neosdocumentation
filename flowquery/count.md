# FlowQuery: count

**Beschreibung:** Gibt die Anzahl der Elemente im Context zurück

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\CountOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/CountOperation.php
```

**Beispiel(e):**

Anzahl aller Seiten in der aktuellen Site:

```
${q(site).find('[instanceof TYPO3.Neos.NodeTypes:Page]').count()}
```
