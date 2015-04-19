# TypoScript 2.0 Objekt: Value

**Beschreibung:** TypoScript Objekt-Wrapper für Wert

**Vollständiger Name:** `TYPO3.TypoScript:Value`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Value).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\ValueImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `value` | mixed, required | Der Wert |

**Beispiel(e):**

```
myValue = Value {
   myValue.value = 'Hello World'
}
```

Dies kann vereinfacht werden, indem der Wert direkt zugewiesen wird:

```
myValue = 'Hello World'
```
