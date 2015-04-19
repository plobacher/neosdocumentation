# TypoScript 2.0 Objekt: Http.ResponseHead

**Beschreibung:** Generiert einen Standard HTTP Response Header

**Vollständiger Name:** `TYPO3.TypoScript:Http.ResponseHead`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Http.ResponseHead).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\Http\\ResponseHeadImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `httpVersion` | string | HTTP-Version (Default ist `HTTP/1.1`) |
| `statusCode` | integer | Status-Code (Default ist `200`) |
| `headers` | array | Array mit Header-Daten |


**Beispiel(e):**

```
prototype(TYPO3.TypoScript:Http.Message) < prototype(TYPO3.TypoScript:Array) {
	httpResponseHead = TYPO3.TypoScript:Http.ResponseHead
	httpResponseHead.@position = 'start 1000'
}

page = TYPO3.TypoScript:Http.Message {
   httpResponseHead {
      statusCode = 404
      headers.Content-Type = 'application/json'
   }
}
```