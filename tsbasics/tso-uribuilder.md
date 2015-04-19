# TypoScript 2.0 Objekt: UriBuilder

**Beschreibung:** Rendert eine URL die auf eine(n) Controller/Action zeigt

**Vollständiger Name:** `TYPO3.TypoScript:UriBuilder`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:UriBuilder) {
   @class = 'TYPO3\\TypoScript\\TypoScriptObjects\\UriBuilderImplementation'
   additionalParams = TYPO3.TypoScript:RawArray
   arguments = TYPO3.TypoScript:RawArray
   argumentsToBeExcludedFromQueryString = TYPO3.TypoScript:RawArray

   @exceptionHandler = 'TYPO3\\TypoScript\\Core\\ExceptionHandlers\\AbsorbingHandler'
}
```

**UriBuilder leitet von Template ab und hat damit auch desses Eigenschaften!**

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `package` | string | Package |
| `subpackage` | string | Subpackage |
| `controller` | string | Controller |
| `action` | string | Action |
| `arguments` | array | Controller-Argumente |
| `format` | string | Format (wie z.B. `html`) |
| `section` | string | Anker (`#`) |
| `additionalParams` | array | Zusätzliche Query-Parameter, die im Gegensatz zu $arguments kein Prefix erhalten (überschreibt $arguments) |
| `argumentsToBeExcludedFromQueryString` | array | Argumente, die von der URI entfernt werden. Nur aktiv, wenn addQueryString = TRUE ist|
| `addQueryString` | boolean | Wenn der Wert auf TRUE ist, werden die aktuell vorhandenen Query-Parameter beibehalten |
| `absolute` | boolean | Ist der Wert TRUE, wird die URL absolut gerendert |


**Beispiel(e):**

```
page.head.canonical = TYPO3.TypoScript:Tag {
   tagName = 'link'
   attributes {
      rel = 'canonical'
      href = TYPO3.TypoScript:UriBuilder {
         package = 'TYPO3.Neos'
         controller = 'Frontend\\\\Node'
         action = 'show'
         absolute = TRUE
         arguments {
            node = ${node}
         }
      }
   }
}
```