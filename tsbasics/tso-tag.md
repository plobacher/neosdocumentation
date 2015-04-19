# TypoScript 2.0 Objekt: Tag

**Beschreibung:** Mit diesem TypoScript Objekt werden HTML-Tags mit Attributen und zusätzlichem Inhalt gerendert.

**Vollständiger Name:** `TYPO3.TypoScript:Tag`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Tag) {
   @class = 'TYPO3\\TypoScript\\TypoScriptObjects\\TagImplementation'
   attributes = TYPO3.TypoScript:Attributes
   omitClosingTag = FALSE
   selfClosingTag = FALSE
}
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `tagName` | string | Name des Tags, der gerendert werden soll - default ist `<div>` |
| `omitClosingTag` | boolean | Angabe, ob der Inhalt `content` und der schließende Tag gerendert werden soll - default ist FALSE |
| `selfClosingTag` | boolean | Angabe, ob der Tag selbstschließend ist - default ist FALSE |
| `content` | string | Hier wird der Inhalt des Elements angeben für den Fall, dass das Tag nicht selbst schließend ist und das schließende Tag nicht übergangen wird. |
| `attributes` | TYPO3.TypoScript:Attributes | Angabe der Attribute für den Tag. |


Die Liste der selbst schließenden Tags ist in der Datei `Packages/Application/TYPO3.TypoScript/Classes/TYPO3/TypoScript/TypoScriptObjects/TagImplementation.php` festgelegt: 'area', 'base', 'br', 'col', 'command', 'embed', 'hr', 'img', 'input', 'keygen', 'link', 'meta', 'param', 'source', 'track', 'wbr'.

Wenn man die Eigenschaft `selfClosingTag` auf TRUE setzt und der `tagName` einem aus der Liste entspricht, wird der Tag direkt geschlossen, anstelle ein End-Tag zu rendern.

**Beispiel(e):**

```
htmlTag = TYPO3.TypoScript:Tag {
   @position = 'start'
   tagName = 'html'
   omitClosingTag = TRUE

   attributes {
      version = 'HTML+RDFa 1.1'
      xmlns = 'http://www.w3.org/1999/xhtml'
      xmlns:typo3 = 'http://www.typo3.org/ns/2012/Flow/Packages/Neos/Content/'
      xmlns:xsd = 'http://www.w3.org/2001/XMLSchema#'
   }
}
```

Das Ergebnis lautet wie folgt:

```
<html version="HTML+RDFa 1.1" xmlns="http://www.w3.org/1999/xhtml" xmlns:typo3="http://www.typo3.org/ns/2012/Flow/Packages/Neos/Content/" xmlns:xsd="http://www.w3.org/2001/XMLSchema#">
```