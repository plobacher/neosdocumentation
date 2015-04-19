# TYPO3 Neos Nodetypes - Text with Image

**Kompletter Name:** TYPO3.Neos.NodeTypes:TextWithImage

** Beschreibung:** Ein Text-Element als Inhaltselement

**Konfiguration:**

```
# TextWithImage TS Object
prototype(TYPO3.Neos.NodeTypes:TextWithImage) < prototype(TYPO3.Neos.NodeTypes:Image) {
  text.@process.convertUris = TYPO3.Neos:ConvertUris
}
```

Im zugehörigen Yaml-Abschnitt sieht man, dass `TYPO3.Neos.NodeTypes:TextWithImage` von `TYPO3.Neos:Content`, `TYPO3.Neos.NodeTypes:TextMixin` und `TYPO3.Neos.NodeTypes:ContentImageMixin` erbt.

```
'TYPO3.Neos.NodeTypes:TextWithImage':
  superTypes:
    - 'TYPO3.Neos:Content'
    - 'TYPO3.Neos.NodeTypes:TextMixin'
    - 'TYPO3.Neos.NodeTypes:ContentImageMixin'
  ui:
    label: 'Text with Image'
    icon: 'icon-picture'
    position: 400

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

# Content image mixin
'TYPO3.Neos.NodeTypes:ContentImageMixin':
  abstract: TRUE
  superTypes:
    - 'TYPO3.Neos.NodeTypes:ImageMixin'
    - 'TYPO3.Neos.NodeTypes:LinkMixin'
    - 'TYPO3.Neos.NodeTypes:ImageCaptionMixin'
    - 'TYPO3.Neos.NodeTypes:ImageAlignmentMixin'
  properties:
    link:
      ui:
        inspector:
          group: 'image'
```
