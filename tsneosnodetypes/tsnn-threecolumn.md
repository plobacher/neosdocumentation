# TYPO3 Neos Nodetypes - Three-Column

**Kompletter Name:** TYPO3.Neos.NodeTypes:ThreeColumn

** Beschreibung:** Ein Element mit drei Spalten

**Konfiguration:**

```
# Three Column TS Object
prototype(TYPO3.Neos.NodeTypes:ThreeColumn) >
prototype(TYPO3.Neos.NodeTypes:ThreeColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)
```

```
'TYPO3.Neos.NodeTypes:ThreeColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Three column content'
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'
    column1:
      type: 'TYPO3.Neos:ContentCollection'
    column2:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    layout:
      defaultValue: '33-33-33'
      ui:
        reloadIfChanged: TRUE
        inspector:
          editorOptions:
            values:
              '33-33-33':
                label: '33% / 33% / 33%'
              '50-25-25':
                label: '50% / 25% / 25%'
              '25-50-25':
                label: '25% / 50% / 25%'
              '25-25-50':
                label: '25% / 25% / 50%'
```

```
'TYPO3.Neos.NodeTypes:Column':
  superTypes: ['TYPO3.Neos:Content']
  abstract: TRUE
  ui:
    group: 'structure'
    label: 'Column'
    icon: 'icon-columns'
    inlineEditable: TRUE
    inspector:
      groups:
        column:
          label: 'Columns'
          position: 10
  properties:
    layout:
      type: string
      ui:
        label: 'Layout'
        inspector:
          group: 'column'
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
```