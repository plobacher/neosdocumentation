# Neos TypoScript: ContentCase

**Beschreibung:** Rendert eine Content-Node und setzt Typ auf den Node Type Namen der aktuellen Node. Wird von ContentCollection verwendet

**Vollständiger Name:** `TYPO3.Neos:ContentCase`

**TypoScript Definition:** 
```
# TYPO3.Neos:ContentCase inherits TYPO3.TypoScript:Case and overrides the default case
# with a catch-all condition for the default case, setting the type variable to
# the name of the current nodes' node type
#
prototype(TYPO3.Neos:ContentCase) < prototype(TYPO3.TypoScript:Case) {
	default {
		@position = 'end'
		condition = TRUE
		type = ${q(node).property('_nodeType.name')}
	}
}
```

Matcher schlägt an, wenn der Name des NodeTypes identisch ist.
Kann zudem um eigene Matcher ergänzt werden.


**ContentCase leitet von Case ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/ContentCase.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `default` |  | Default Matcher |
| `[key]` |  | Zusätzliche Matcher |