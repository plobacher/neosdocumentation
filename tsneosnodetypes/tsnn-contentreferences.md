# TYPO3 Neos Nodetypes - Content References

**Kompletter Name:** TYPO3.Neos.NodeTypes:ContentReferences

** Beschreibung:** Eine Content-Referenz als Inhaltselement

**Konfiguration:**

```
# "Insert content references" TS Object
prototype(TYPO3.Neos.NodeTypes:ContentReferences) {
  referenceNodes = TYPO3.TypoScript:Collection {
    collection = ${q(node).property('references')}
    itemRenderer = TYPO3.Neos:ContentCase
    itemName = 'node'
  }
}
```

Yaml:

```
'TYPO3.Neos.NodeTypes:ContentReferences':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Insert content references'
    icon: 'icon-copy'
    position: 800
    inspector:
      groups:
        references:
          label: 'References'
          position: 10
  properties:
    references:
      type: 'references'
      ui:
        inspector:
          group: 'references'
          editorOptions:
            nodeTypes: ['TYPO3.Neos:Content']
        label: 'Select'
        reloadIfChanged: TRUE
```