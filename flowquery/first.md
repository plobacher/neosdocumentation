# FlowQuery: first

**Beschreibung:** Gibt das erste Element eines Context zurück

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\FirstOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/FirstOperation.php
```

**Beispiel(e):**

Hier wird zunächst die Rootline ermittelt und dann mittels `first()` das erste Element ausgewählt. Von diesem wird der Titel zurückgegeben. Wenn es beispielsweise drei Seiten gibt: "Home > Kompendium > FlowQuery" und man steht auf "FlowQuery" dann wird nun "FlowQuery" zurückgegeben.

```
${q(node).add(q(node).parents()).first().property('title')}
```
