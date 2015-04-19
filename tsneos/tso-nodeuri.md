# Neos TypoScript: Node URI

**Beschreibung:** Erstellt eine URI auf eine Node

**Vollständiger Name:** `TYPO3.Neos:NodeUri`

**TypoScript Definition:** 
```
# Renders an URI pointing to a node
#
prototype(TYPO3.Neos:NodeUri) {
	@class = 'TYPO3\\Neos\\TypoScript\\NodeUriImplementation'
	additionalParams = TYPO3.TypoScript:RawArray
	arguments = TYPO3.TypoScript:RawArray
	additionalParams = TYPO3.TypoScript:RawArray
	argumentsToBeExcludedFromQueryString = TYPO3.TypoScript:RawArray
}
```

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/NodeUri.ts2
```

**Beispiel(e):**

```
nodeLink = TYPO3.Neos:NodeUri {
	node = ${q(node).parent().get(0)}
}
```