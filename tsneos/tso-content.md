# Neos TypoScript: Content

**Beschreibung:** Alle Content-Elemente (welche im Backend auswählbar sind) leiten von diesem Basis Objekt ab

**Vollständiger Name:** `TYPO3.Neos:Content`

**TypoScript Definition:** 
```
# This is the base Content TypoScript object
# It must be extended by all elements that are selectable in the backend
#
# Note: This object inherits from TYPO3.TypoScript:Template because most Content Elements are expected to contain a
# Fluid template. If a Content Element does not render a template (like it is the case for the Plugin Content Elements)
# you should still extend this prototype and override the @class property (see TYPO3.Neos:Plugin).
#
prototype(TYPO3.Neos:Content) < prototype(TYPO3.TypoScript:Template) {
	node = ${node}

	attributes = TYPO3.TypoScript:Attributes
	attributes.class = ''

	# The following is used to automatically append a class attribute that reflects the underlying node type of a TypoScript object,
	# for example "typo3-neos-nodetypes-form", "typo3-neos-nodetypes-headline", "typo3-neos-nodetypes-html", "typo3-neos-nodetypes-image", "typo3-neos-nodetypes-menu" and "typo3-neos-nodetypes-text"
	# You can disable the following line with:
	# prototype(TYPO3.Neos:Content) {
	#   attributes.class.@process.nodeType >
	# }
	# in your site's TypoScript if you don't need that behavior.
	attributes.class.@process.nodeType = TYPO3.TypoScript:Case {
		@override.nodeTypeClassName = ${String.toLowerCase(String.pregReplace(q(node).property('_nodeType.name'), '/[[:^alnum:]]/', '-'))}

		classIsString {
			condition = ${q(value).count() == 1}
			renderer = ${String.trim(value + ' ' + nodeTypeClassName)}
		}

		classIsArray {
			condition = ${q(value).count() > 0}
			renderer = ${Array.push(value, nodeTypeClassName)}
		}
	}

	# The following line must not be removed as it adds required meta data to all content elements in backend
	@process.contentElementWrapping = TYPO3.Neos:ContentElementWrapping

	@exceptionHandler = 'TYPO3\\Neos\\TypoScript\\ExceptionHandlers\\NodeWrappingHandler'
}
```

**Content leitet von Template ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Content.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `node` | Eel | Enthält die aktuelle Node |
| `value` | Eel | Enthält der Wert value |

**Erläuterung:**

Will man kein Template verwenden, so muss man den Prototypen erweitern und die @class Eigenschaft überschreiben (siehe TYPO3.Neos:Plugin)

**Beispiel(e):**

```
# Basic implementation of a flexible MultiColumn element, not exposed directly but inherited by all specific MultiColumn content elements
prototype(TYPO3.Neos.NodeTypes:MultiColumn) < prototype(TYPO3.Neos:Content) {
	templatePath = 'resource://TYPO3.Neos.NodeTypes/Private/Templates/NodeTypes/MultiColumn.html'
	layout = ${q(node).property('layout')}
	attributes.class = ${'container columns-' + q(node).property('layout')}
	columns = TYPO3.TypoScript:Collection {
		collection = ${q(node).children('[instanceof TYPO3.Neos:ContentCollection]')}
		itemRenderer = TYPO3.Neos.NodeTypes:MultiColumnItem
		itemName = 'node'
	}
}
```

```
prototype(Acme.Demo:YouTube) < prototype(TYPO3.Neos:Content) {
		templatePath = 'resource://Acme.Demo/Private/Templates/TypoScriptObjects/YouTube.html'
		videoUrl = ${q(node).property('videoUrl')}
		width = '640'
		height = '360'
	}
```