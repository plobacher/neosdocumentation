# TYPO3 Neos Nodetypes - Menu

**Kompletter Name:** TYPO3.Neos.NodeTypes:Menu

** Beschreibung:** Ein Menu als Inhaltselement

**Konfiguration:**

```
# Menu TS Object - extends TYPO3.Neos:Menu and is rendering menus inserted as content elements
prototype(TYPO3.Neos.NodeTypes:Menu) {
  @class = 'TYPO3\\Neos\\TypoScript\\MenuImplementation'

  startingPoint = ${documentNode}

  itemCollection = ${Array.isEmpty(q(node).property('selection') ? q(node).property('selection') : {}) ? NULL : q(node).property('selection')}

  entryLevel = ${q(node).property('startLevel')}
  entryLevel.@process.1 = ${String.toInteger(value)}

  maximumLevels = ${q(node).property('maximumLevels')}
  maximumLevels.@process.1 = ${String.toInteger(value)}

  active.attributes = TYPO3.TypoScript:Attributes {
    class = 'active'
  }
  current.attributes = TYPO3.TypoScript:Attributes {
    class = 'current'
  }
  normal.attributes = TYPO3.TypoScript:Attributes {
    class = 'normal'
  }

  node = ${node}
  items = ${this.items}
}
```

Über `startingPoint = ${documentNode}` wird beispielsweise definiert, dass das Menü ab der aktuellen Seite gerendert werden soll. Zudem werden die Attribute für die Zustände (active, current, normal) vergeben.

```
'TYPO3.Neos.NodeTypes:Menu':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Menu'
    group: 'structure'
    icon: 'icon-sitemap'
    position: 100
    inspector:
      groups:
        options:
          label: 'Options'
          position: 30
  properties:
    startLevel:
      type: string
      defaultValue: '0'
      ui:
        reloadIfChanged: TRUE
        label: 'Starting Level'
        inspector:
          group: 'options'
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            values:
              '-4':
                label: 'Four Levels Above Current Page'
              '-3':
                label: 'Three Levels Above Current Page'
              '-2':
                label: 'Two Levels Above Current Page'
              '-1':
                label: 'One Level Above Current Page'
              '0':
                label: 'Same Level As Current Page'
              '1':
                label: 'First Level Of Website'
              '2':
                label: 'Second Level Of Website'
              '3':
                label: 'Third Level Of Website'
              '4':
                label: 'Fourth Level Of Website'
              '5':
                label: 'Fifth Level Of Website'
              '6':
                label: 'Sixth Level Of Website'
    selection:
      type: 'references'
      ui:
        reloadIfChanged: TRUE
        label: 'Selection'
        inspector:
          group: 'options'
    maximumLevels:
      type: string
      defaultValue: '1'
      ui:
        reloadIfChanged: TRUE
        label: 'Maximum Levels'
        inspector:
          group: 'options'
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            values:
              '1':
                label: '1'
              '2':
                label: '2'
              '3':
                label: '3'
              '4':
                label: '4'
              '5':
                label: '5'
              '6':
                label: '6'
              '7':
                label: '7'
              '8':
                label: '8'
              '9':
                label: '9'
              '10':
                label: '10'
```

```
##
# "ChapterMenu" element, extending the default "Menu"
#
prototype(Site:ChapterMenu) < prototype(TYPO3.Neos.NodeTypes:Menu) {
  attributes.class = 'chapter-menu'
  chapterImageWidth = '100'
  chapterImageHeight = '100'
}
```