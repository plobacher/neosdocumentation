# TYPO3 Neos Nodetypes - Html

**Kompletter Name:** TYPO3.Neos.NodeTypes:Html

** Beschreibung:** Ein Element welches HTML-Code einfügt

**Konfiguration:**

```
'TYPO3.Neos.NodeTypes:Html':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'HTML'
    icon: 'icon-code'
    position: 500
    inspector:
      groups:
        html:
          label: 'HTML'
          position: 10
  properties:
    source:
      type: string
      ui:
        label: 'HTML Content'
        reloadIfChanged: TRUE
        inspector:
          group: 'html'
          editor: 'TYPO3.Neos/Inspector/Editors/CodeEditor'
          editorOptions:
            buttonLabel: 'Edit HTML source'
      defaultValue: '<p>Enter HTML here</p>'
```
