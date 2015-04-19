# TYPO3 Neos Nodetypes - Multi-Column

**Kompletter Name:** TYPO3.Neos.NodeTypes:MultiColumn

** Beschreibung:** Ein Element, um mehrere Content-Elemente nebeneinander zu positionieren

**Konfiguration:**

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

'TYPO3.Neos.NodeTypes:TwoColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Two column content'
    position: 200
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

'TYPO3.Neos.NodeTypes:ThreeColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Three column content'
    position: 300
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

'TYPO3.Neos.NodeTypes:FourColumn':
  superTypes: ['TYPO3.Neos.NodeTypes:Column']
  ui:
    label: 'Four column content'
    position: 400
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