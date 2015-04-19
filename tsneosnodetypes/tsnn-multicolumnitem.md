# TYPO3 Neos Nodetypes - Multi-Column-Item

**Kompletter Name:** TYPO3.Neos.NodeTypes:MultiColumnItem

** Beschreibung:** Ein Element innerhalb eines Multi-Column Containers

**Konfiguration:**

```
# Abstract render definition for a single content column in a multi column element
prototype(TYPO3.Neos.NodeTypes:MultiColumnItem) < prototype(TYPO3.TypoScript:Template) {
  node = ${node}
  templatePath = 'resource://TYPO3.Neos.NodeTypes/Private/Templates/NodeTypes/MultiColumnItem.html'
  attributes = TYPO3.TypoScript:Attributes {
    class = 'column'
  }
  columnContent = TYPO3.Neos:ContentCollection {
    nodePath = '.'
  }
}

# Two Column TS Object
prototype(TYPO3.Neos.NodeTypes:TwoColumn) >
prototype(TYPO3.Neos.NodeTypes:TwoColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)

# Three Column TS Object
prototype(TYPO3.Neos.NodeTypes:ThreeColumn) >
prototype(TYPO3.Neos.NodeTypes:ThreeColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)

# Four Column TS Object
prototype(TYPO3.Neos.NodeTypes:FourColumn) >
prototype(TYPO3.Neos.NodeTypes:FourColumn) < prototype(TYPO3.Neos.NodeTypes:MultiColumn)
```

Yaml:

```
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
