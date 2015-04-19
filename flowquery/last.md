# FlowQuery: last

**Beschreibung:** Gibt das letzte Element eines Context zurück

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\LastOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/LastOperation.php
```

**Beispiel(e):**

Hier wird zunächst die Rootline ermittelt und dann mittels `last()` das letzte Element ausgewählt. Von diesem wird der Titel zurückgegeben. Wenn es beispielsweise drei Seiten gibt: "Home > Kompendium > FLowQuery" und man steht auf "FlowQuery" dann wird nun "Home" zurückgegeben.

```
${q(node).add(q(node).parents()).last().property('title')}
```
