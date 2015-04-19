# TYPO3 Neos Nodetypes - Text

**Kompletter Name:** TYPO3.Neos.NodeTypes:Text

** Beschreibung:** Ein Text-Element als Inhaltselement

**Konfiguration:**

```
# Text TS Object
prototype(TYPO3.Neos.NodeTypes:Text) {
  text.@process.convertUris = TYPO3.Neos:ConvertUris
}
```

Im zugehörigen Yaml-Abschnitt sieht man, dass `TYPO3.Neos.NodeTypes:Text` von `TYPO3.Neos:Content` und `TYPO3.Neos.NodeTypes:TextMixin` erbt.

```
'TYPO3.Neos.NodeTypes:Text':
  superTypes:
    - 'TYPO3.Neos:Content'
    - 'TYPO3.Neos.NodeTypes:TextMixin'
  ui:
    label: 'Text'
    icon: 'icon-file-text'
    position: 200

# Text mixin
'TYPO3.Neos.NodeTypes:TextMixin':
  abstract: TRUE
  properties:
    text:
      type: string
      defaultValue: ''
      ui:
        inlineEditable: TRUE
        aloha:
          placeholder: '<p>Enter text here</p>'
          autoparagraph: TRUE
          'format':
            'strong': TRUE
            'em': TRUE
            'u': FALSE
            'sub': FALSE
            'sup': FALSE
            'del': FALSE
            'p': TRUE
            'h1': TRUE
            'h2': TRUE
            'h3': TRUE
            'pre': TRUE
            'removeFormat': TRUE
          'table':
            'table': TRUE
          'list':
            'ol': TRUE
            'ul': TRUE
          'link':
            'a': TRUE
```
