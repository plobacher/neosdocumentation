# TYPO3 Neos Nodetypes - Page

**Kompletter Name:** TYPO3.Neos.NodeTypes:Page

** Beschreibung:** Eine Seite

**Konfiguration:**

```
'TYPO3.Neos.NodeTypes:Page':
  superTypes: ['TYPO3.Neos:Document']
  childNodes:
    main:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    layout:
     type: string
     ui:
       label: 'Layout for this page only'
       reloadIfChanged: TRUE
       inspector:
         group: 'layout'
         editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
         editorOptions:
           placeholder: 'Inherit from parent'
           values:
             '':
               label: ''
    subpageLayout:
     type: string
     ui:
       label: 'Layout for subpages of this page'
       inspector:
         group: 'layout'
         editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
         editorOptions:
           placeholder: 'Inherit from parent'
           values:
             '':
               label: ''
  ui:
    label: 'Page'
    icon: 'icon-file'
    inspector:
      groups:
        document:
          label: 'Title'
        layout:
          label: 'Layout'
          position: 150
```