# TYPO3 Neos Nodetypes - Four-Column

**Kompletter Name:** TYPO3.Neos.NodeTypes:FourColumn

** Beschreibung:** Ein Element mit vier Spalten

**Konfiguration:**

```
# Four Column TS Object
prototype(TYPO3.Neos.NodeTypes:FourColumn) >
prototype(TYPO3.Neos.NodeTypes:FourColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)
```

```
'TYPO3.Neos.NodeTypes:FourColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Four column content'
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'
    column1:
      type: 'TYPO3.Neos:ContentCollection'
    column2:
      type: 'TYPO3.Neos:ContentCollection'
    column3:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    layout:
      defaultValue: '25-25-25-25'
      ui:
        reloadIfChanged: TRUE
        inspector:
          editorOptions:
            values:
              '25-25-25-25':
                label: '25% / 25% / 25% / 25%'
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