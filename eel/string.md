# Eel Helper: String

**Beschreibung:** Enthält String-Helper-Funktionen

**Implementierung:** `TYPO3\Eel\Helper\StringHelper`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/Helper/StringHelper.php
```

**Basis:** https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String

**API:**

* `substr($string, $start, $length = NULL)`   
Gibt einen Teil aus einem String zurück, definiert durch Start und Länge
* `substring($string, $start, $end = NULL)`   
Gibt einen Teil aus einem String zurück, definiert durch Start und Ende
* `charAt($string, $index)`   
Gibt den Buchstaben an der Position index zurück
* `endsWith($string, $search, $position = NULL)`   
Testet, ob ein String mit einem angegebenen String aufhört
* `indexOf($string, $search, $fromIndex = NULL)`   
Gibt die erste Position zurück, an der ein angegebener String in einem String gefunden wird
* `lastIndexOf($string, $search, $toIndex = NULL)`   
Gibt die letzte Position zurück, an der ein angegebener String in einem String gefunden wird
* `pregMatch($string, $pattern)`   
Gibt ein Array mit Treffern zurück, die bei einer regulären Suche im String ermittelt werden
* `pregReplace($string, $pattern, $replace)`   
Suchen und Ersetzen anhand eines regulären Ausdrucks. Zurückgegeben wird der ersetzte String
* `replace($string, $search, $replace)`   
Suchen und Ersetzen - zurückgegeben wird der ersetzte String
* `split($string, $separator = NULL, $limit = NULL)`   
Splitet einen String anhand eines Separators und gibt ein Array zurück
* `startsWith($string, $search, $position = NULL)`   
Testet, ob ein String mit einem angegebenen String anfängt
* `toLowerCase($string)`   
Wandelt einen String in Kleinbuchstaben um und liefert diesen String wieder zurück
* `firstLetterToUpperCase($string)`   
Wandelt in einem String den ersten Buchstaben in einen Großbuchstaben um und liefert diesen String wieder zurück
* `firstLetterToLowerCase($string)`   
Wandelt in einem String den ersten Buchstaben in einen Kleinbuchstaben um und liefert diesen String wieder zurück
* `stripTags($string)`   
Entfernt Whitespaces am Anfang und Ende des Strings
* `trim($string)`   
Prüft, ob ein String leer ist oder lediglich Whitespaces beinhaltet
* `toString($value)`   
Wandelt den Wert in einen String um
* `toInteger($string)`   
Wandelt den Wert in einen Integer-Wert um
* `toFloat($string)`   
Wandelt den Wert in einen Float-Wert um
* `toBoolean($string)`   
Wandelt den Wert in einen Booleschen-Wert um
* `rawUrlEncode($string)`   
Gibt einen String zurück, in dem alle nicht-alphanumerischen Zeichen außer `-`,`_`,`.`(RFC 3986) durch ein Prozentzeichen (%) gefolgt von zwei Hex-Werten ersetzt wurden. 
* `rawUrlDecode($string)`
Dekodiert einen String, der nach RFC 3986 enkodiert wurde
* `htmlSpecialChars($string, $preserveEntities = FALSE)`
Wandelt Sonderzeichen in HTML-Codes um (z.B. `&`in `&amp;` oder `>` in `&gt;`)
* `crop($string, $maximumCharacters, $suffix = '')`
Schneidet einen String nach einer Anzahl Zeichen ab
* `cropAtWord($string, $maximumCharacters, $suffix = '')`
Schneidet einen String nach einer Anzahl Zeichen ab und beachtet dabei die Wordgrenzen
* `cropAtSentence($string, $maximumCharacters, $suffix = '')`
Schneidet einen String nach einer Anzahl Zeichen ab und beachtet dabei die Satzgrenzen
* `md5($string)`
Ermittelt den MD5-Hash eines Strings


**Beispiel(e):**


```
String.substr('Hello, World!', 7, 5) === 'World'
String.substr('Hello, World!', 7) === 'World!'
String.substr('Hello, World!', -6) === 'World!'

String.substring('Hello, World!', 7, 12) === 'World'
String.substring('Hello, World!', 7) === 'World!'

String.endsWith('Hello, World!', 'World!') === true
```
