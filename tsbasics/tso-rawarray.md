# TypoScript 2.0 Objekt: RawArray

**Beschreibung:** Baut ein Array auf und gibt es als solches auch wieder zurück (im Gegensatz zum Objekt Array, welches am Ende einen String erzeugt)

**Vollständiger Name:** `TYPO3.TypoScript:RawArray`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:RawArray).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\RawArrayImplementation'
```

**RawArray leitet von Array ab und hat damit auch desses Eigenschaften!**

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

Keine weiteren.

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