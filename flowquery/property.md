# FlowQuery: property

**Beschreibung:** Gibt die Eigenschaften eines Objekts mittels `ObjectAccess` zurück. Erwartet den Name einer Eigenschaft als Argument. Ist der Context leer, wird NULL zurück gegeben. Ansonsten wird der Wert der Eigenschafte des ersten Context-Elements zurück gegegeben.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\PropertyOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/ropertyOperation.php
```

**Beispiel(e):**

Gebe den Titel, den Pfad und den Namen des NodeTypes aus:

```
${q(node).property('title')}
${q(node).property('_path')}
${q(node).property('_nodeType.name')}
```
