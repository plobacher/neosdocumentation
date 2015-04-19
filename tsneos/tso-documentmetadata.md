# Neos TypoScript: DocumentMetadata

**Beschreibung:** Rendert einen Meta-Tag mit Attributen

**Vollständiger Name:** `TYPO3.Neos:DocumentMetadata`

**TypoScript Definition:** 
```
# DocumentMetadata implementation
#
# Renders a meta tag with attributes about the current document node
#
prototype(TYPO3.Neos:DocumentMetadata) < prototype(TYPO3.TypoScript:Tag) {
	tagName = 'div'
	forceClosingTag = TRUE
	attributes {
		id = 'neos-document-metadata'
	}

	@process.contentElementWrapping = TYPO3.Neos:ContentElementWrapping
	@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
}
```

**DocumentMetadata leitet von Tag ab und hat damit auch dessen Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/DocumentMetadata.ts2
```

**Beispiel(e):**

```
# Required for the backend to work.
neosBackendDocumentNodeData = TYPO3.Neos:DocumentMetadata {
	@position = 'before body'
	@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
}
```

Ausgabe (nur im NICHT-Live-Workspace!):
```
<div typeof="typo3:TYPO3.Neos.NodeTypes:Page" about="/sites/website@user-admin" class="neos-contentelement" data-__sitename="Website" data-__siteroot="/sites/website@user-admin" data-neos-__workspacename="live" data-neos-_typoscript-path="page&lt;TYPO3.Neos:Page&gt;/neosBackendDocumentNodeData" data-neos-_removed="false" data-neosdatatype-_removed="xsd:boolean" data-neos-_hidden="false" data-neosdatatype-_hidden="xsd:boolean" data-neos-_hidden-before-date-time="" data-neosdatatype-_hidden-before-date-time="xsd:date" data-neos-_hidden-after-date-time="" data-neosdatatype-_hidden-after-date-time="xsd:date" data-neos-title="Home" data-neos-_hidden-in-index="false" data-neosdatatype-_hidden-in-index="xsd:boolean" data-neos-layout="" data-neos-subpage-layout="" data-neos-__nodetype="TYPO3.Neos.NodeTypes:Page" id="neos-page-metainformation"></div>
```