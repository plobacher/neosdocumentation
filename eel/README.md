# Eel - Embedded Expression Language

Über Objekte können wir Strukturen und über einfache Typen können wir Strings, Zahlen und Boolesche Werte deklarieren. 

Meistens benötigt man aber etwas mehr und will beispielsweise auf den Kontext zugreifen oder auf dynamische Daten. Hier kommt Eel ins Spiel.

Eel ist ein Subset von JavaScript und erlaubt uns Ausdrücke zu formulieren.

Während TypoScript Zuweisungen und Prozessoren beinhaltet, kann man mit Eel Ausdrücke der Art `myObject.foo = ${q(node).property('bar')}` formulieren. Die Embedded Expression Language (Eel) ist ein Baustein um Domain Specific Languages (DSL) zu erstellen. Eel stellt eine reichhaltige Syntax zur Verfügung um beliebige Ausdrücke zu erstellen, damit sich der Autor der DSL auf die Semantik konzentrieren kann:

```
${foo.bar} 						// Traversal
${foo.bar()} 					// Methoden-Aufruf
${foo.bar().baz()} 				// Verketter Methoden-Aufruf

${foo.bar("arg1", true, 42)} 	// Methoden-Aufruf mit Argumenten
${12 + 18.5} 					// Kalkulation
${foo == bar} 					// Vergleiche

${foo.bar(12+7, foo == bar)} 	// Alles kombiniert
${[foo, bar]} 					// Array Literal
${{foo: bar, baz: test}} 		// Object Literal
```

Dabei hat Eel folgende Charakteristika:

* Jeder Eel-Ausdruck wird mittels `${...}` notiert
* Eel ist JavaScript sehr ähnlich (da es ein Subset davon implementiert hat)
* Eel unterstützt **keine** Variablen-Zuweisungen oder Kontrollstrukturen
* Eel unterstützt die üblichen JavaScript Operatoren für Arithmetik und Vergleiche
* Eel unerstützt den Dreifach-Operator für Vergleiche: `<condition> ? <ifTrue> : <ifFalse>`
* Sobald Eel auf eine Objekt-Eigenschaft zugreift, wird der entsprechende Getter aufgerufen
* Objekt-Zugriff über die Offset-Notation wird wie folgt unterstützt: `foo['bar']`
* Eel selbst definiert keine Funktion oder Variablen, sondern verwendet das ***Eel Context Array***. Funktionen und Objekte, auf die man zugreifen will, können dort definiert werden.
* Daher eignet sich Eel perfekt als "domain-specific language construction kit", welches die Syntax, nicht aber die Semantik der DSL (Domain Specific Language) zur Verfügung stellt.

Für Eel innerhalb von TypoScript ist die Sematik wie folgt definiert:

* Alle Variablen des TypoScript Kontextes sind im Eel Kontext zugänglich
* Die spezielle Variable `this` zeigt immer auf die aktuelle TypoScript Objekt Implementierung
* Es gibt eine Funktion `q()`, die ihre Argumente in einem FlowQuery-Objekt einhüllt

## Eel Helper

Per Default gibt es die folgenden Eel Helper, die im Default-Kontext der Eel-Ausdrücke erhältlich sind:

* `String`, definiert in `TYPO3\Eel\Helper\StringHelper`
* `Array`, definiert in `TYPO3\Eel\Helper\ArrayHelper`
* `Date`, definiert in `TYPO3\Eel\Helper\DateHelper`
* `Configuration`, definiert in `TYPO3\Eel\Helper\ConfigurationHelper`
* `Math`, definiert in `TYPO3\Eel\Helper\MathHelper`
* `Json`, definiert in `TYPO3\Eel\Helper\JsonHelper`
* `Security`, definiert in `TYPO3\Eel\Helper\SecurityHelper`
* `Translation`, definiert in `TYPO3\Flow\I18n\EelHelper\TranslationHelper`
* `Neos.Node`, definiert in `TYPO3\Neos\TypoScript\Helper\NodeHelper`
* `Neos.Link`, definiert in `TYPO3\Neos\TypoScript\Helper\LinkHelper`
* `Neos.Array`, definiert in `TYPO3\Neos\TypoScript\Helper\ArrayHelper`
* `Neos.Rendering`, definiert in `TYPO3\Neos\TypoScript\Helper\RenderingHelper`

Definiert werden die Helper im Schlüssel `TYPO3.TypoScript.defaultContext`.