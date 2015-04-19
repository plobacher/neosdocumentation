# Neos TypoScript: Content Collection

**Beschreibung:** Eine Content Collection enthält selbst keine eigenen Eigenschaften, sondern eine geordnete Liste von Child Nodes, die ihrerseits gerendert werden.

**Vollständiger Name:** `TYPO3.Neos:ContentCollection`

**TypoScript Definition:** 
```
# Default case for ContentCollection TS Object
#
prototype(TYPO3.Neos:ContentCollection) < prototype(TYPO3.Neos:Content) {
  @class = 'TYPO3\\Neos\\TypoScript\\ContentCollectionImplementation'

  nodePath = 'to-be-set-by-user'

  itemName = 'node'
  itemRenderer = TYPO3.Neos:ContentCase

  attributes.class = 'neos-contentcollection'

  # You may override this to get your content collection from a different place than the current node.
  # The Eel helper is used to provide a better error message if no content collection could be found.
  @override.contentCollectionNode = ${Neos.Node.nearestContentCollection(node, this.nodePath)}

  @process.contentElementWrapping {
    node = ${contentCollectionNode}
  }

  @cache {
    mode = 'cached'

    entryIdentifier {
      collection = ${contentCollectionNode}
      domain = ${site.context.currentDomain}
    }

    entryTags {
      1 = ${'DescendantOf_' + contentCollectionNode.identifier}
      2 = ${'Node_' + contentCollectionNode.identifier}
    }

    maximumLifetime = ${q(contentCollectionNode).context({'invisibleContentShown': true}).children().cacheLifetime()}
  }
}

prototype(TYPO3.Neos:Content) {
  prototype(TYPO3.Neos:ContentCollection) {
    # Make ContentCollection inside content node types embedded by default.
    # Usually there's no need for a separate cache entry for container content elements, but depending on the use-case
    # the mode can safely be switched to 'cached'.
    @cache {
      mode = 'embed'
    }
  }
}

```

**ContentCollection leitet von Content (und dies von Template) ab und hat damit auch desses Eigenschaften! Zudem erweitert die Klasse ContentCollectionImplementation die Klasse AbstractCollectionImplementation aus dem Paket TYPO3.TypoScript und hat somit auch dessen Eigenschaften.**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/ContentCollection.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `nodePath` | string | Identifier der Node, die die Content Collection enthält, der gerendert werden soll |
| `tagName` | string | Tag (Default ist `<div>` ) der angezeigt wird, wenn keine Child-Nodes vorhanden sind - in diesem Fall wird im Backend ein Button/Link angezeigt, um neue Elemente anzulegen |
| `itemName` | string | Item-Name (Default ist 'node') |
| `itemRenderer` | string | Für das Rendering verwendetes Objekt (Default ist 'TYPO3.Neos:ContentCase') |
| `attributes` | array | Attribute für das Rendering des Tags  |

**Beispiel(e):**

Multiple Contentelemente:
```
// Yaml (Sites/Vendor.Site/Configuration/NodeTypes.yaml)

'Vendor:Box':
  superTypes:
    - 'TYPO3.Neos:Content'
  ui:
    group: Structure
    label: Box
    icon: icon-columns
    inlineEditable: true
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'

// TypoScript (Sites/Vendor.Site/Resources/Private/TypoScripts/Library/NodeTypes.ts2)

prototype(Vendor:Box) < prototype(TYPO3.Neos:Content) {
        templatePath = 'resource://Vendor.Site/Private/Templates/TypoScriptObjects/Box.html'
        columnContent = TYPO3.Neos:ContentCollection
        columnContent {
                nodePath = 'column0'
        }
}

// HTML (Sites/Vendor.Site/Private/Templates/TypoScriptObjects/Box.html)

{namespace ts=TYPO3\TypoScript\ViewHelpers}

<div class="container box">
        <div class="column">
                <ts:render path="columnContent" />
        </div>
</div>
```

Multiple Contentelemente (inkl. Option "collapsed":
```
// Yaml (Sites/Vendor.Site/Configuration/NodeTypes.yaml)

'Vendor:Box':
  superTypes:
    - 'TYPO3.Neos:Content'
  ui:
    group: Structure
    label: Box
    icon: icon-columns
    inlineEditable: true
    inspector:
      groups:
        display:
          label: Display
          position: 5
  properties:
    collapsed:
      type: boolean
      ui:
        label: Collapsed
        reloadIfChanged: true
        inspector:
          group: display
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'
      
// TypoScript (Sites/Vendor.Site/Resources/Private/TypoScripts/Library/NodeTypes.ts2)

prototype(Vendor:Box) < prototype(TYPO3.Neos:Content) {
        templatePath = 'resource://Vendor.Site/Private/Templates/TypoScriptObjects/Box.html'
        columnContent = TYPO3.Neos:ContentCollection
        columnContent {
                nodePath = 'column0'
        }
        collapsed = ${q(node).property('collapsed')}
}

// HTML (Sites/Vendor.Site/Private/Templates/TypoScriptObjects/Box.html)

{namespace ts=TYPO3\TypoScript\ViewHelpers}

<f:if condition="{collapsed}">
        <button>open the collapsed box via js</button>
</f:if>
<div class="container box {f:if(condition: collapsed, then: 'collapsed', else: '')}>
        <div class="column">
                <ts:render path="columnContent" />
        </div>
</div>
```

