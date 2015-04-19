# TypoScript Overview

Um ein Gefühl für TypoScript zu erhalten, fangen wir mit einfachen Beispielen an. In den folgenden Kapitel wird dabei jeder Aspekt ausführlich vertieft und erläutert:


## Strings

Starten wir mit einer einfachen Deklaration. Dies kann ein String, eine Zahl oder ein Boolscher Ausdruck sein:


```
page = 'Hello world!'
```

Führt zur Ausgabe:

```
Hello world!
```

## Zahlen 

```
page = 42
```

Die Ausgabe lautet:

```
42
```

## Boolscher Wert 

```
page = TRUE
```

Die Ausgabe lautet:

```
1
```
Bei `FALSE` gibt es keine Ausgabe!


## Objekte 

```
page = TypoScript:Array {
	hello = 'Hello'
	world = ' world!'
}
```

Die Ausgabe lautet:

```
Hello world!
```

Objekt-Deklarationen können auch zu einem späteren Zeitpunkt erweitert werden:

```
output = Array {
	hello = 'Hello'
}

output.world = ' world!'
```

Die Ausgabe lautet:

```
Hello world!
```

## Ausdrücke

Über Eel (Embedded Expression Language) können Ausdrücke eingebracht werden:

```
page = ${'Hello' + ' world!'}
```
Die Ausgabe lautet:

```
Hello world!
```

Es gibt diverse Helper-Objekte (`String`, `Array`, `Math`) deren Funktionen man auf einen Eel-Ausdruck anwenden kann.

Im nachfolgenden Beispiel ermitteln wir einen Teilstring (substring) mit Hilfe der Funktion `String.substr`. An der Stelle 33 wird ein 12 Zeichen langer String herausgetrennt und zurückgegeben:

```
page = ${String.substr("Das Standard-Beispiel ist: <code>Hello world!</code>.", 33, 12)}
```

Die Ausgabe lautet:

```
Hello world!
```

Man kann über die Funktion `String.split` einen String nach einem Trennzeichen (hier `,`) zerteilen. Die einzelnen Bestandteile landen in einem Array, dessen Elemente von 0 beginnend durchnummeriert sind. Um also das dritte Element zu erhalten, mus man den Index 2 verwenden.

```
page = ${String.split('Hallo Welt!,¡Hola Mundo!,Hello world!', ',')[2]}
```

Die Ausgabe lautet:

```
Hello world!
```

Mit Hilfe der Funktion `Array.reverse` kann man die Reihenfolge eines Arrays umdrehen. Hier wird zunächst die Reihenfolge invertiert und anschließend die Elemente zusammenaddiert und ausgegeben.

```
page = ${Array.join(Array.reverse(['world!', 'Hello']), ' ')}
```

Die Ausgabe lautet:

```
Hello world!
```

## Kontext

Richtig mächtig wird Eel aber dann, wenn die Daten aus Nodes oder anderen Objekte ermittelt werden.

Beim Frontend-Rendering greifen wir in TYPO3 Neos auf eine Node zu, die über die URL - wie z.B. `/home/about-us.html` ermittelt wird. 

Diese Node wird TypoScript in den sogenannten "Kontext" übergeben und kann über Ausdrücke in Eel angesprochen werden.

Nehmen wir einmal an wir wollen den Seitentitel der aktuellen Seite auslesen:

```
page = ${'<title>' + node.properties.title + '</title>'}
```