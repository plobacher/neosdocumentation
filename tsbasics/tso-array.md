# TypoScript 2.0 Objekt: Array

**Beschreibung:** Rendert verschachtelte TypoScript Objekte und fügt deren Ausgabe zusammen

**Vollständiger Name:** `TYPO3.TypoScript:Array`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Array).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\ArrayImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `<key>` | string | TypoScript Objekte |
| `<key>.@position` | string | Positionierungsangabe |

Der Key kann entweder aus Zahlen oder Buchstaben (bzw. eine Kombination daraus) bestehen.


**Eigenschaften (Positionierungsangabe):**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `start [priority]` | string | Je höher die Priorität, desto früher wird das Objekt hinzugefügt. Wenn keine Priorität angegeben wird, wird das Element hinter allen Elementen mit Priorität einsortiert |
| `[numeric ordering]` | string | Position (aufsteigend sortiert) |
| `end [priority]` | string | Je höher die Priorität, desto später wird das Objekt hinzugefügt. Wenn keine Priorität angegeben wird, wird das Element vor allen Elementen mit Priorität einsortiert |
| `before [namedElement] [optionalPriority]` | string | Fügt dieses Element vor dem Element "namedElement" ein. Gibt es mehrere Statements, so entscheidet die Priorität wie weit das Element vor "namedElement" positioniert wird; es gilt also je höher, desto näher. Statements ohne Priorität werden am weitesten vor dem Element platziert. Wenn "namedElement" nicht existiert, wird das Element nach allen "start" Positionen platziert. |
| `after [namedElement] [optionalPriority]` | string | Analog zu "before" nur genau andersherum ("nach namendElement", "vor allen end Positionen",...) |


**Beispiel(e):**

```
myArray = TYPO3.TypoScript:Array {
   o1 = TYPO3.Neos.NodeTypes:Text
   o1.@position = 'start 12'
   o2 = TYPO3.Neos.NodeTypes:Text
   o2.@position = 'start 5'
   o2 = TYPO3.Neos.NodeTypes:Text
   o2.@position = 'start'
   o3 = TYPO3.Neos.NodeTypes:Text
   o3.@position = '10'
   o4 = TYPO3.Neos.NodeTypes:Text
   o4.@position = '20'
   o5 = TYPO3.Neos.NodeTypes:Text
   o5.@position = 'before o6'
   o6 = TYPO3.Neos.NodeTypes:Text
   o6.@position = 'end'
   o7 = TYPO3.Neos.NodeTypes:Text
   o7.@position = 'end 20'
   o8 = TYPO3.Neos.NodeTypes:Text
   o8.@position = 'end 30'
   o9 = TYPO3.Neos.NodeTypes:Text
   o9.@position = 'after o8'
}
```

Wenn das `@position` Argument nicht angegeben wird, wird der Array-Schlüssel direkt verwendet:

```
myArray = TYPO3.TypoScript:Array {
   10 = TYPO3.Neos.NodeTypes:Text
   20 = TYPO3.Neos.NodeTypes:Text
}
```
