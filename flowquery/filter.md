# FlowQuery: filter

**Beschreibung:** Die filter Operation limitiert das Ergebnis-Set der Nodes. Der Filter-Ausdruck wird mittels Fizzle notiert und unterstützt die folgenden Operatoren:

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\FilterOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/Object/FilterOperation.php
```

**Syntax:**
```
[ [<value>] <operator> <operand> ]
```

Die Operatoren sind dabei wie folgt belegt:

* `=` (Gleichheit)
* `$=` (Wert endet mit dem Operanden)
* `^=` (Wert beginnt mit dem Operanden)
* `*=` (Wert enthält den Operanden)
* `instanceof` (Prüft ob der Wert eine Instanz des Operanden ist)

**Beispiel(e):**

Selektiere alle Kinder und suche dort alle Nodes vom Typ "Page". Wähle davon die erste aus und gib den Pfad zurück.

```
${q(node).children().filter('[instanceof TYPO3.Neos.NodeTypes:Page]').first().property('_path')}
```


* `filter('[attribute="value"]')`: Selects an object if it has an attribute `attribute` with value `value`
* `filter("[  attribute      =   'value'  ]")`: See above
* `filter('[attribute=  Foo.Bar  ]'`: See above; you can leave out the quotes if your value does not contain whitespace, or any of `"'[]`.
* `filter('[attribute1=value1][attribute2=value2]')`: Selects an object only if BOTH conditions match
* `filter('foo[attribute=bar]')`: object identifier and attribute selectors are both supported.
* `filter('[a*= b]')`, `filter('[a^= b]')`, `filter('[a$= b]')`: Substring match, beginning-of-string-match, end-of-string-match
* `filter('[instanceof foo]')`: select the object if it is instance of foo
* `filter('[instanceof "foo"]')`: same as above
