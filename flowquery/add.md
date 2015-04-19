# FlowQuery: add

**Beschreibung:** Die add Operation fügt weitere Objekt hinzu

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\AddOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/AddOperation.php
```


**Beispiel(e):**

Hier wird die aktuelle Node ermittelt und dazu alle Eltern-Nodes hinzuaddiert. Dies wird beispielsweise verwendet, um eine Breadcrumb-Navigation zu erstellen. Hierfür wird die Rootline der Nodes benötigt, die mit Hilfe des Statements ermittelt wird

```
items = ${q(node).add(q(node).parents())}
```
