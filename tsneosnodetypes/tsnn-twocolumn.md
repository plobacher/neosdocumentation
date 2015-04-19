# TYPO3 Neos Nodetypes - Two-Column

**Kompletter Name:** TYPO3.Neos.NodeTypes:TwoColumn

** Beschreibung:** Ein Element mit zwei Spalten

**Konfiguration:**

```
# Two Column TS Object
prototype(TYPO3.Neos.NodeTypes:TwoColumn) >
prototype(TYPO3.Neos.NodeTypes:TwoColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)
```

```
'TYPO3.Neos.NodeTypes:TwoColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Two column content'
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'
    column1:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    layout:
      defaultValue: '50-50'
      ui:
        reloadIfChanged: TRUE
        inspector:
          editorOptions:
            values:
              '50-50':
                label: '50% / 50%'
              '75-25':
                label: '75% / 25%'
              '25-75':
                label: '25% / 75%'
              '66-33':
                label: '66% / 33%'
              '33-66':
                label: '33% / 66%'
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