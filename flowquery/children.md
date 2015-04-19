# FlowQuery: children

**Beschreibung:** Die children-Operation gibt die Kind-Nodes der aktuellen Node zurück. Dies sind bei einer Seite beispielsweise die Sektionen und dort die Content-Bereiche.

Es ist zudem möglich eine Filter-Option anzugeben: `...children('main')...`

**Implementierung:** `TYPO3\TYPO3CR\Eel\FlowQueryOperations\ChildrenOperation`

**Datei:**
```
Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Eel/FlowQueryOperations/ChildrenOperation.php
```

**WICHTIG!: Die children-Operation arbeitet - im Gegensatz zur find Operation - NIE rekursiv. Es werden also lediglich die direkt untergeordneten Kinder ermittelt!**

**Beispiel(e):**

Gebe den Pfad des Kindes unterhalb der aktuellen Node aus:

```
${q(node).children().property('_path')}

// Ausgabe z.B.
/sites/website/main
```

Selektiere mehrere Nodes:

```
${q(node).children("[instanceof My.Package:Post], [instanceof My.Package:Bar]")}
```

* `children('foo')`: Selektiert ein Kinde-Objekt mit dem Pfad "foo"
* `children('foo').children('bar')`: Selektiert das Kind-Objekt mit dem Namen "bar" innerhalb des Kind-Objekt mit dem Namen "foo"
* `children('foo[a=b]').children('bar[c=d]')`: Wie das Beispiel davor, aber nur wenn das Attribut "a" den Wert "b" und das Attribut "c" den Wert "d" hat
