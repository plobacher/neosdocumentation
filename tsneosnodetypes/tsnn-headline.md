# TYPO3 Neos Nodetypes - Headline

**Kompletter Name:** TYPO3.Neos.NodeTypes:Headline

** Beschreibung:** Eine Headline als Inhaltselement

**Konfiguration:**

```
# Headline TS Object
prototype(TYPO3.Neos.NodeTypes:Headline) {
  title.@process.convertUris = TYPO3.Neos:ConvertUris
}
```

Im zugehörigen Yaml-Abschnitt sieht man, dass `TYPO3.Neos.NodeTypes:Headline` von `TYPO3.Neos:Content` und `TYPO3.Neos.NodeTypes:TitleMixin` erbt.

** Dateien **

```
Packages/Application/TYPO3.Neos.NodeTypes/Configuration/NodeTypes.Mixins.yaml
Packages/Application/TYPO3.Neos.NodeTypes/Configuration/NodeTypes.Content.yaml
```

**Yaml-Konfig**

```
'TYPO3.Neos.NodeTypes:Headline':
  superTypes:
    - 'TYPO3.Neos:Content'
    - 'TYPO3.Neos.NodeTypes:TitleMixin'
  ui:
    label: 'Headline'
    icon: 'icon-font'
    position: 100

# Title mixin
'TYPO3.Neos.NodeTypes:TitleMixin':
  abstract: TRUE
  properties:
    title:
      type: string
      defaultValue: '<h1>Enter headline here</h1>'
      ui:
        inlineEditable: TRUE
        aloha:
          'format':
            'p': FALSE
            'h1': TRUE
            'h2': TRUE
            'h3': TRUE
            'removeFormat': TRUE
          'link':
            'a': TRUE
```
