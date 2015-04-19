# Neos TypoScript: ContentElementWrapping

**Beschreibung:** Fügt Meta Daten Attribute zu den zu verarbeitenden Content Elementen im Backend hinzu (z.B. `class`, `rel`, `typeof`, `about`, `inlineEditable`, `data-__sitename`, `data-__siteroot`, `data-neos-__workspacename`, 'data-neos-_typoscript-path', `data-neos-__nodetype`, `data-neosdatatype-...`, u.s.w.)

**Vollständiger Name:** `TYPO3.Neos:ContentElementWrapping`

**TypoScript Definition:** 
```
# ContentElementWrapping implementation
#
# Used as processor this adds metadata attributes to the corresponding TypoScript object
# This is used to render required data-node-* attributes to content elements in the backend
#
prototype(TYPO3.Neos:ContentElementWrapping) {
	@class = 'TYPO3\\Neos\\TypoScript\\ContentElementWrappingImplementation'
	node = ${node}
	value = ${value}
}
```

**Das Hinzufügen von Klassen wird durch den `ContentElementWrappingService` übernommen: `Packages/Application/TYPO3.Neos/Classes/TYPO3/Neos/Service/ContentElementWrappingService.php`**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/ContentElementWrapping.ts2
```

**Beispiel(e):**

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

```
<div typeof="typo3:TYPO3.Neos:ContentCollection" about="/sites/website/main@user-admin" class=" neos-not-inline-editable neos-contentcollection" rel="typo3:content-collection" tabindex="0" data-neos-__workspacename="live" data-neos-_typoscript-path="page&lt;TYPO3.Neos:Page&gt;/body&lt;TYPO3.TypoScript:Template&gt;/content/main&lt;TYPO3.Neos:PrimaryContent&gt;/default&lt;TYPO3.TypoScript:Matcher&gt;/element&lt;TYPO3.Neos:ContentCollection&gt;" data-neos-_removed="false" data-neosdatatype-_removed="xsd:boolean" data-neos-__nodetype="TYPO3.Neos:ContentCollection">
<div typeof="typo3:TYPO3.Neos.NodeTypes:Text" about="/sites/website/main/text1@user-admin" class="neos-contentelement typo3-neos-nodetypes-text" tabindex="0" data-neos-__workspacename="live" data-neos-_typoscript-path="page&lt;TYPO3.Neos:Page&gt;/body&lt;TYPO3.TypoScript:Template&gt;/content/main&lt;TYPO3.Neos:PrimaryContent&gt;/default&lt;TYPO3.TypoScript:Matcher&gt;/element&lt;TYPO3.Neos:ContentCollection&gt;/itemRenderer&lt;TYPO3.Neos:ContentCase&gt;/default&lt;TYPO3.TypoScript:Matcher&gt;/element&lt;TYPO3.Neos.NodeTypes:Text&gt;" data-neos-_removed="false" data-neosdatatype-_removed="xsd:boolean" data-neos-_hidden="false" data-neosdatatype-_hidden="xsd:boolean" data-neos-_hidden-before-date-time="" data-neosdatatype-_hidden-before-date-time="xsd:date" data-neos-_hidden-after-date-time="" data-neosdatatype-_hidden-after-date-time="xsd:date" data-neos-text="&lt;p&gt;This is the homepage&lt;/p&gt;" data-neos-__nodetype="TYPO3.Neos.NodeTypes:Text">
```