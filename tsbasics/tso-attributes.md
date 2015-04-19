# TypoScript 2.0 Objekt: Attributes

**Beschreibung:** Wird verwendet, um HTML-Tag Attribute zu rendern. Dieses Objekt wird beispielsweise von `TYPO3.TypoScript:Tag` verwendet. Kann aber auch standalone verwendet werden, um z.B. Attribute in Fluid-Templates zu rendern.

**Vollständiger Name:** `TYPO3.TypoScript:Attributes`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Attributes) {
   @class = 'TYPO3\\TypoScript\\TypoScriptObjects\\AttributesImplementation'
}
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `[attributeName] = [value]` | mixed | Als Wert kann ein String, eine Zahl, ein Eel-Ausdruck oder ein Objekt verwendet werden |

**Beispiel(e):**

```
attributes = TYPO3.TypoScript:Attributes {
   foo = 'bar'
   class = TYPO3.TypoScript:RawArray {
      class1 = 'class1'
      class2 = 'class2'
   }
}
```

Das Ergebnis lautet wie folgt:

```
foo="bar" class="class1 class2"
```