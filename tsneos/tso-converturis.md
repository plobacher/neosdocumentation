# Neos TypoScript: Convert URI

**Beschreibung:** Wandelt Node-Referenzen der Form `node://<UUID>` in URIs um 

**Vollständiger Name:** `TYPO3.Neos:ConvertUris`

**TypoScript Definition:** 
```
# ConvertUris implementation
#
# replaces all occurrences of "node://<UUID>" by proper URIs.
#
prototype(TYPO3.Neos:ConvertUris) {
	@class = 'TYPO3\\Neos\\TypoScript\\ConvertUrisImplementation'
	value = ${value}
	node = ${node}
}
```

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/ConvertUris.ts2
```

**Beispiel(e):**

Einsatz als Prozessor:
```
someTextProperty.@process.1 = TYPO3.Neos:ConvertUris
```


```
# Text TS Object
prototype(TYPO3.Neos.NodeTypes:Text) {
	text.@process.convertUris = TYPO3.Neos:ConvertUris
}

# Image TS Object
prototype(TYPO3.Neos.NodeTypes:Image) {
	maximumWidth = 2560
	maximumHeight = 2560
	imageClassName = ${q(node).property('alignment') ? ('typo3-neos-alignment-' + q(node).property('alignment')) : ''}
	allowCropping = FALSE
	allowUpScaling = FALSE
	link.@process.convertUris = TYPO3.Neos:ConvertUris {
		forceConversion = true
	}
}

# TextWithImage TS Object
prototype(TYPO3.Neos.NodeTypes:TextWithImage) < prototype(TYPO3.Neos.NodeTypes:Image) {
	text.@process.convertUris = TYPO3.Neos:ConvertUris
}
```