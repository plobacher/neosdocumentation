# Objekte und Prototypen

TypoScript ist eine hierarchische, objektorientierte und Prototypen- basierte Verarbeitungssprache, die von Neos verwendet wird, um den Content flexibel zu rendern. Während wird die Hierarchie bereits im letzten Kapitel kennenlernen konnten, widmen wir uns nun der Objektorientierung zu.

Objekte haben Eigenschaften, die das Objekt „konfigurieren“ TypoScript hat Zugriff auf den jeweiligen *Context* (z.B. Seitenbaum im Objekt „menu“ oder Seiteneigenschaften im Objekt `page`).

Zudem gibt es *Prozessoren* die die Eigenschaftswerte verändern können (ähnlich den stdWrap-Funktionen in TYPO3 CMS).

Nachdem bereits in TYPO3 CMS TypoScript verwendet wurde, bezeichnet man TypoScript in TYPO3 Neos (bzw. in TYPO3 Flow) mit der Versionsnummer 2.0. Letztlich haben aber beide Versionen (vor allem technisch) nicht allzuviel miteinander zu tun.

* TypoScript wird in TYPO3 Neos ausschließlich zum Rendern von Inhalten im Frontend verwendet (keine Konfiguration mehr von Usern im Backend beispielsweise wie durch TSconfig in TYPO3 CMS üblich)
* TypoScript ist hierarchisch, weil es auch hierarchischen Inhalt rendert
* TypoScript ist Prototypen-basiert (ähnlich wie JavaScript), da es beispielsweise erlaubt die Eigenschaften von allen Instanzen gleichzeitig zu ändern
* TypoScript ist eine Verarbeitungssprache, da es die Werte in einem Kontext verarbeitet und in einem einzigen Ausgabe-Wert überführt
TypoScript ist eine Sprache um TypoScript Objekte zu beschreiben
* Ein TypoScript Objekt besitzt Eigenschaften - sogenannte Properties
* TypoScript Objekte haben Zugriff zu einem „Kontext“, welcher letztlich eine Liste von Variablen ist
* TypoScript überführt diesen Kontext mit Hilfe der Properties in eine Ausgabe
* Intern kann TypoScript auch diesen Kontext verändern, sowie das Rendern von *verschachtelten* Objekten (TypoScript Baum) anstoßen
* TypoScript-Objekte werden durch PHP-Klassen realisiert, welche zur Laufzeit instanziert werden. Dabei kann eine Klasse die Basis von mehreren verschiedenen Objekten sein


## Syntax

Objekte werden immer in UpperCamelCase-Schreibweise notiert und Properties in lowerCamelCase-Schreibweise.

Dabei sind folgende Zeilen Code jeweils gültige Objekt-Zuweisungen:

```
foo = Page
my.object = Text
my.image = TYPO3.Neos.ContentTypes:Image
```

Wertzuweisungen können beispielhaft wie folgt durchgeführt werden:

```
foo.myProperty1 = 'Some Property which Page can access'
my.object.myProperty1 = "Some other property"
my.image.width = ${q(node).property('foo')}
```

## Prototype

Wenn ein TypoScript Objekt instanziiert wird (also wenn man beispielsweise `someImage = Image` schreibt) wird der sogenannte TypoScript *Prototype* dieses Objekts kopiert und als Basis für das neue Objekt verwendet.

Ein Prototype wird über die folgende Syntax erstellt:

```
prototype(MyImage) {
   width = '500px'
   height = '600px'
}
```

Wenn nun der obige Prototyp instanziiert wird, erbt das zugehörige Objekt alle Eigenschaften des kopierten Prototyps.

```
someImage = MyImage
// someImage hat nun eine Breite von 500px und eine Höhe von 600px

someImage.width = '100px'
// Nun haben wir die Höhe von someImage mit dem Wert 100px überschrieben
```

In TypoScript sind Prototypen veränderbar - d.h. sie können leicht angepasst werden:

```
prototype(MyYouTube) {
   width = '100px'
   height = '500px'
}

// Man kann nun Eigenschaften anpassen
prototype(MyYouTube).width = '400px'

// oder neue Eigenschaften definieren
prototype(MyYouTube).showFullScreen = ${true}
```

Man muß aber den Prototypen nicht neu definieren und anschließend instanziieren - man kann auch einen existierenden Prototypen als Basis verwenden. Dafür leitet man von einem bestehenden TypoScript Prototyp mit Hilfe des `<` Operators ab:

```
prototype(MyImage) < prototype(TYPO3.Neos:Content)

// Der *MyImage* Prototyp enthält nun alle Eigenschaften des
// *Content* Prototyps und kann nun weiter bearbeitet werden.
```

Dies implementiert die sogenannte Prototypen-Vererbung. Dies bedeutet, dass die *Kind-Klasse* (im obigen Beispiel `MyImage`) und die *Eltern-Klasse* (`Content`) weiterhin aneinander gebunden sind: Wird eine Eigenschaft zur Eltern-Klasse hinzugefügt, so steht diese auch in der Kind-Klasse zur Verfügung:

```
prototype(TYPO3.Neos:Content).fruit = 'apple'
prototype(TYPO3.Neos:Content).meal = 'dinner'

prototype(MyImage) < prototype(TYPO3.Neos:Content)
// "MyImage" hat nun die Eigenschaften "fruit = apple" und "meal = dinner"

prototype(TYPO3.Neos:Content).fruit = 'Banana'
// Da "MyImage" die Klasse Content erweitert,
// ist nun ebenfalls "MyImage.fruit = 'Banana'"

prototype(MyImage).meal = 'breakfast'
prototype(TYPO3.TypoScript:Content).meal = 'supper'
// Da die Eigenschaft "meal" der Klasse "MyImage überschrieben wurde,
// hat die Zuweisung in der Eltern-Klasse keine Auswirkung
```

Prototypen-Verberbung ist nur auf globaler Ebene möglich

```
prototype(Foo) < prototype(Bar)
```

Nicht möglich dagegen wären folgende Anweisungen

```
prototype(Foo) < some.prototype(Bar)
other.prototype(Foo) < prototype(Bar)
prototype(Foo).prototype(Bar) < prototype(Baz)
```

### Hierarchische Prototypen

Um ein flexibles Rendering von TypoScript-Objekten zu ermöglichen, können Prototypen an bestimmten Stellen im Render-Baum modifiziert werden. Dies wird dadurch ermöglicht, da TypoScipt Prototypen hierarchisch agieren. Ein Prototyp kann also Teil jedes Pfades innerhalb einer TypoScript Zuweisung sein - eventuell sogar mehrfach:

```
// Setze die Eigenschaft "bar" (bzw. "some.thing")
// für alle Objekte vom Typ "Foo"
prototype(Foo).bar = 'baz'
prototype(Foo).some.thing = 'baz2'

// Für alle Objekte vom Typ "Foo", welche innerhalb des Pfades
// "some.path" auftauchen, setze die Eigenschaft "some"
some.path.prototype(Foo).some = 'baz2'

// Für alle Objekte vom Typ "Bar" die innerhalb von Objekten
// vom Typ "Foo" auftauchen, setze die Eigenschaft "some"
prototype(Foo).prototype(Bar).some = 'baz2'

// Kombination aus allen Möglichkeiten zuvor
prototype(Foo).left.prototype(Bar).some = 'baz2'
```

### Namespaces

Um Namenskollisionen zu vermeiden, können bei der Deklaration Namespaces verwendet werden.

```
// Deklariert einen Namespace "Acme.Demo" für den Prototyp "YouTube"

prototype(Acme.Demo:YouTube) {
   width = '100px'
   height = '500px'
}
```

Der Namespace ist per Konvention der Package-Key, des Packages wo sich das zugehörige TypoScript befindet

Voll qualifizierte Namespaces können an allen Stellen verwendet werden, wo ein Identifier erlaubt ist:


```
prototype(TYPO3.Neos:ContentCollection.Default) < prototype(TYPO3.Neos:Collection)
```

Definiert man keinen Namespace, wird per Default (innerhalb von TYPO3 Neos) immer `TYPO3.Neos` verwendet. Wenn daher beispielsweise `Page` verwendet wird, wird dies intern aufgelöst zu `TYPO3.Neos:Page`.

Man kann aber auch eine Namespace-Direktive verwenden um einen eigenen Namespace zu verwenden:

```
namespace Foo = Acme.Demo

// Die folgenden beiden Anweisungen sind identisch
video = Acme.Demo:YouTube
video = Foo:YouTube
```

ACHTUNG: Die Namespace Deklarationen gelten nicht nur in der Datei in der sie definiert sind, sondern global!


## Properties

Auch wenn TypoScript-Objekte direkt auf ihren Kontext zugreifen können, sollte man dennoch Eigenschaften (Properties) dafür verwenden

```
// Wir nehmen an, dass es eine Eigenschaft "foo=bar"
// im aktuellen Kontext an dieser Stelle gibt
myObject = MyObject

// Explizites Zuweisen des Wertes der Variable "foo"
// aus dem aktuellen Kontext und Zuweisen an die
// "foo" Eigenschaft des Objektes "myObject"
// Dies macht den Datenfluss sichtbarer
myObject.foo = ${foo}
```

Während `myObject` sich auf die Annahme verlassen könnte, dass es eine Variable `foo` innerhalb des TypoScript Kontext gibt, existiert keine Möglichkeit (ausser einer Dokumentation), um dies an die Aussenwelt zu kommunizieren.

Objekte sollten daher ausschliesslich eigene Eigenschaften verwenden, um den Output zu generieren, um damit unabhängig vom Kontext zu werden.

Lediglich bei der Prototypen-Definition kann man direkt auf den Kontext zugreifen:

```
// Hier wird ein explizites Mapping zwischen der Kontext Variable "foo"
// und der Eigenschaft "foo" hergestellt
prototype(MyObject).foo = ${foo}
```


## Manipulation des Kontext

Der TypoScript-Kontext kann direkt manipuliert werden, indem man die `@override` Meta-Eigenschaft verwendet:

```
myObject = MyObject
myObject.@override.bar = ${foo * 2}
```

Der obige Code erzeugt nun eine weitere Kontext-Variable mit dem Namen "bar" und dem doppelten Wert von "foo".


## Prozessoren

Prozessoren erlauben es, TypoScript Eigenschaften zu manipulieren:

```
myObject = MyObject {
   property = 'some value'
   property.@process.1 = ${'before ' + value + ' after'}
}
// Das Ergebnis ist nun "before some value after"
```

Es können auch mehrere Prozessoren verwendet werden.  Die Reihenfolge ergibt sich aus der numerische Position im TypoScript (Zahlenangabe nach `@process`) - ein `@process.2` würde demnach nach `@process.1` verarbeitet werden.

Man kann für Prozessoren auch eine erweiterte Syntax verwenden:

```
myObject = MyObject {
   property = 'some value'
   property.@process.someWrap {
      expression = ${'before ' + value + ' after'}
      @position = 'start'
    }
}
// Das Ergebnis ist nun "before some value after"
```

Hiermit kann man einen eigenen Namen (hier "someWrap") verwenden und vor allem `@position` verwenden.

Prozessoren sind Eel (Embedded Expression Language) Ausdrücke bzw. TypoScript Objekte, die auf Werte des Kontextes angewendet werden. Das aktuelle Objekt erreicht man via `this`.


## Conditions

Conditions können allen Werte hinzugefügt werden, um eine Evaluierung des Wertes zu verhindern.
Dies wird mithilde der `@if` Meta-Eigenschaft durchgeführt:


```
myObject = Menu {
   @if.1 = ${q(node).property('showMenu') == true}
}
# results in the menu object only being evaluated if the node's showMenu property is ``true``
```

Hier wird das Menu-Objekt nur dann ausgewertet, wenn die Eigenschaft `showMenu` der aktuellen Node auf den Wert `true` gesetzt wurde.
