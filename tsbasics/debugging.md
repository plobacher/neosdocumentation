# TypoScript Debugging

## Aktives TypoScript

Um sich das gesamte TypoScript kurz vor dem Parsing anzuzeigen, muss man in die folgende Datei gehen:

```
Packages/Application/TYPO3.Neos/Classes/TYPO3/Neos/Domain/Service/TypoScriptService.php
```

Etwa in Zeile 155 kann man dort folgenden Code (mittlere Zeile) hinterlegen:

```
...
	$mergedTypoScriptCode .= $this->getTypoScriptIncludes($this->appendTypoScriptIncludes);

	echo $mergedTypoScriptCode; die();

	return $this->typoScriptParser->parse($mergedTypoScriptCode, $siteRootTypoScriptPathAndFilename);
...
```

### Kontext-Variablen

Es gibt einige Kontext-Variablen, die in der Datei `Packages/Application/TYPO3.Neos/Classes/TYPO3/Neos/View/TypoScriptView.php` ca. in Zeile 87 definiert sind:

```
$typoScriptRuntime->pushContextArray(array(
	'node' => $currentNode,
	'documentNode' => $this->getClosestDocumentNode($currentNode),
	'site' => $currentSiteNode,
	'account' => $this->securityContext->canBeInitialized() ? $this->securityContext->getAccount() : NULL,
	'editPreviewMode' => isset($this->variables['editPreviewMode']) ? $this->variables['editPreviewMode'] : NULL
));
```

Später kommt noch der Request via `'request' => $this->controllerContext->getRequest()` hinzu.

Diese bedeuten wie wie folgt:

* `node`: Die aktuelle Node
* `documentNode`: Die Document-Node (vom Typ `TYPO3.Neos:Document`) auf der die aktuelle Node liegt. Wenn diese bereits ein Document ist, so sind `node` und `documentNode` identisch
* `request`: Das Request-Objekt
* `site`: Die Site-Node (`/sites/[sitename]` z.B. `/sites/neosdemotypo3org`)
* `account`: Der Frontend-User
* `editPreviewMode`: Der Editiermodus (`inPlace`, `print`, ...)