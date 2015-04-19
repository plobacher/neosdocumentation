# TYPO3 Neos Nodetypes - Image

**Kompletter Name:** TYPO3.Neos.NodeTypes:Headline

** Beschreibung:** Ein Bild als Inhaltselement

**Konfiguration:**

```
# Image TS Object
prototype(TYPO3.Neos.NodeTypes:Image) {
  maximumWidth = 2560
  maximumHeight = 2560
  imageClassName = ${q(node).property('alignment') ? ('typo3-neos-alignment-' + q(node).property('alignment')) : ''}
  allowCropping = FALSE
  allowUpScaling = FALSE
  link.@process.convertUris = TYPO3.Neos:ConvertUris {
    forceConversion = true
  }
}
```

Im zugehörigen Yaml-Abschnitt sieht man, dass `TYPO3.Neos.NodeTypes:Image` von `TYPO3.Neos:Content` und `TYPO3.Neos.NodeTypes:ContentImageMixin` erbt.

```
'TYPO3.Neos.NodeTypes:Image':
  superTypes:
    - 'TYPO3.Neos:Content'
    - 'TYPO3.Neos.NodeTypes:ContentImageMixin'
  ui:
    label: 'Image'
    icon: 'icon-picture'
    position: 300

# Image mixin
'TYPO3.Neos.NodeTypes:ImageMixin':
  abstract: TRUE
  ui:
    inspector:
      groups:
        image:
          label: 'Image'
          position: 5
  properties:
    image:
      type: TYPO3\Media\Domain\Model\ImageVariant
      ui:
        label: 'Image'
        reloadIfChanged: TRUE
        inspector:
          group: 'image'
          position: 50
    alternativeText:
      type: string
      ui:
        label: 'Alternative text'
        reloadIfChanged: TRUE
        inspector:
          group: 'image'
          position: 100
    title:
      type: string
      ui:
        label: 'Title'
        reloadIfChanged: TRUE
        inspector:
          group: 'image'
          position: 150
```