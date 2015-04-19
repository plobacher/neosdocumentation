# Syntax von TypoScript 2.0

> Das Seitenrendering in TYPO3 Neos wird durch **TypoScript** realisiert.  
> Damit ist dies die wichtigste Komponente zur Darstellung von Inhalten.  
> Die Versionsbezeichnung 2.0 kommt daher, weil es in TYPO3 CMS ebenfalls ein TypoScript gibt 

Die grundsätzliche Syntax (mit Ausnahme von Includes und Namespaces) von TypoScript 2.0 lautet:

```
pfad operator wert
```

## Pfad ##

Der Pfad besteht entweder aus einem Bezeichner oder aus mehreren Bezeichnern, die mit Hilfe eines Punkts getrennt wird. Die Punkte stehen dabei für die *Hierarchie* des Bestandteils. Ein weiter rechts stehender Bestandteil ist somit dem weiter links stehendem untergeordnet. Alle Bezeichner bilden sinnbildlich eine Baumstruktur, die bei dem ganz links stehenden Bezeichner als Wurzel startet und dann immer weiter nach rechts verzweigt.

Folgende Pfade sind beispielsweise gültig:

```
page
page.template
page.template.pfad
page.10.test
```
## Operator ##

Der Operator kann folgende Werte annehmen:

| Operator | Bedeutung | Beispiel |
| :------- | :------ | :------- |
| = | Zuweisung | `page = Page` |
| > | Löschen des Teilpfades | `page >` |
| < | Kopieren eines Teilpfades | `page < test.bla` |

Wenn wir den Teilpfad löschen, steht dieser *Schlüssel* (und alle **Unterschlüssel**) nicht mehr zur Verfügung. Sämtliche Funktionalität, die mit diesem Unterpfad realisiert wurde, damit ebenfalls nicht mehr.

## Wert ##

Werte können beispielsweise Zeichenketten sein - dies werden in einzelnen Anführungszeichen (Ticks) oder doppelten eingeschlossen:

```
page = 'Hallo Welt'
page = "Hallo Welt"
```

Weiterhin sind als Wert Objekte (`page = Page` oder `test = TypoScript:Array`), Objekt-Pfade (siehe Pfade) oder Eel-Ausdrücke (z.B. `${request.format != 'html'}` - diese behandeln wir später) erlaubt.


## Ausklammern ##

Um die Übersichtlichkeit zu erhöhen, kann man Code ausklammern. Dazu werden geschweifte Klammern verwendet, um gleichen Code zu ersetzen.

Schauen wir uns hierzu den folgenden Code an:

```
page = TypoScript:Array
page.hallo = TypoScript:Array
page.hallo.hello = 'Hallo'
page.hallo.world = ' Welt!'
```

Um die Wiederholung von `page` aufzulösen, kann man dies ausklammern:

```
page = TypoScript:Array
page {
   hallo = TypoScript:Array
   hallo.hello = 'Hallo'
   hallo.world = ' Welt!'
}
```

Nun kann man `hallo` ebenfalls ausklammern:

```
page = TypoScript:Array
page {
   hallo = TypoScript:Array
   hallo {
      hello = 'Hallo'
      world = ' Welt!'
   }
}
```

TypoScript 2.0 weißt hier noch eine Besonderheit auf - eine Zeile, die mit einem Bezeichner und einer öffnenden geschweiften Klammer beginnt, kann mit der vorherigen Zeile zusammengefasst werden:

```
page = TypoScript:Array {
   hallo = TypoScript:Array {
      hello = 'Hallo'
      world = ' Welt!'
   }
}
```

## Überschreiben ##

TypoScript agiert grundsätzlich zeilenweise. Der Parser addiert alle Zeilen geschriebenen TypoScript Code von oben nach unten zusammen und führt diesen in einem zweiten Schritt aus.

Wenn nun *weiter unten* ein Pfad notiert wird, den es *weiter oben* ebenso gibt, wird der obige überschrieben.

```
page = TypoScript:Array {
   hallo = TypoScript:Array {
      hello = 'Hallo'
      world = ' Welt!'
   }
}
page.hallo.world = ' TYPO3 Neos!'
```
Die Ausgabe hier lautet: `Hallo TYPO3 Neos!`


### Includieren

Man kann TypoScript-Code auf weitere Dateien auslagern und diese inkludieren:

```
include: Prototypes/ContentCase.ts2
include: resource://TYPO3.Neos/Private/TypoScript/DefaultTypoScript.ts2
```

Dabei kann man entweder den Pfad relativ angeben oder über die `resource://Vendor.Package/...` Direktive gehen. Dann allerdings lässt man das Verzeichnis `Resources` in der Angabe der URI weg.

```
# Include all .ts2 files in NodeTypes
include: NodeTypes/*
include: resource://Acme.Demo/Private/TypoScript/NodeTypes/*

# Include all .ts2 files in NodeTypes and it's subfolders recursively
include: NodeTypes/**/*
include: resource://Acme.Demo/Private/TypoScript/**/*
```

