# TypoScript 2.0 Objekt: ResourceUri

**Beschreibung:** Rendert Resource URIs

**Vollständiger Name:** `TYPO3.TypoScript:ResourceUri`

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
| `path` | string | Die Lokation der Resource - kann entweder ein Pfad relativ zum Ordner `Resources/Public/` sein oder `resource://... URI` |
| `package` | string | Package-Key (wird nur für relative Addressierung benötigt) |
| `resource` | resource | Wenn dies angegeben wird, wird dieses anstelle von `path` und `package` verwendet |
| `localize` | string | Prüft, ob eine Resource-Lokalisierung versucht werden soll (Default TRUE) |



**Beispiel(e):**

```
image = TYPO3.TypoScript:ResourceUri {
   path = 'resource://Lobacher.Guestbook/Public/Images/Rocky_150.png'
 }

 // Ergebnis
 http://neos.dev/_Resources/Static/Packages/Lobacher.Guestbook/Images/Rocky_150.png
```