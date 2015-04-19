# Neos TypoScript: Document

**Beschreibung:** Dies ist das Basis-Document innerhalb von Neos

**Vollständiger Name:** `TYPO3.Neos:Document`

**TypoScript Definition:** 
```
# This is the base Document TypoScript object
# It should be extended by all TypoScript objects which render documents or are based on node types extending
# TYPO3.Neos:Document.
#
# Note: This object inherits from TYPO3.TypoScript:Template because most Document types are expected to contain a
# Fluid template. If a Document-based TypoScript object should not render a template you should still extend this
# prototype and override the @class property.
#
prototype(TYPO3.Neos:Document) < prototype(TYPO3.TypoScript:Template) {
	node = ${node}
}
```

**Document leitet von Template ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Document.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `node` | Eel | Enthält die aktuelle Node |


**Erläuterung:**

Der hauptsächliche Unterschied zwischen der Node, die die Seite enthält und einer Node, die Inhalte enthält, ist der Node-Type. Erstere nennt man *Document Nodes* und diese leiten immer vom Node-Type `TYPO3.Neos:Document` ab. 

Document_Nodes sind vom Type `TYPO3.Neos.NodeTypes:Page`.