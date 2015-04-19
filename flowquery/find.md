# FlowQuery: find

**Beschreibung:** Die find-Operation arbeitet auf den TYPO3CR Nodes und erlaubt es, Nodes zu finden, die durch einen Pfad spezifiziert sind. Die aktulle Node wird dabei verwendet, um relative Pfade aufzulösen.

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\FindOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/FindOperation.php
```

**WICHTIG!: Die find-Operation arbeitet - im Gegensatz zur children Operation - immer rekursiv!**

**Beispiel(e):**

Finde alle Nodes vom Typ "Document" unterhalb der aktuelle Seite:

```
test = ${q(node).find("[instanceof TYPO3.Neos.NodeTypes:Page]")
```

Finde die Node (z.B. eine Content-Collection) mit dem Pfad `main` und darunter alle Kind-Nodes:
```
childNode = ${q(node).find('main').children()}
```

Finde eine Node mit angegebenen Identifier:

```
${q(site).find('#60216562-0ad9-86ff-0b32-7b7072bcb6b2')}
```

Finde alle Nodes vom angegebenen Typ:

```
${q(site).find('[instanceof TYPO3.Neos.NodeTypes:Text]')}
```
