# TYPO3 Neos Nodetypes - Asset List

**Kompletter Name:** TYPO3.Neos.NodeTypes:AssetList

** Beschreibung:** Eine Asset-Liste als Inhaltselement

**Konfiguration:**

```
prototype(TYPO3.Neos.NodeTypes:AssetList).@class = 'TYPO3\\Neos\\NodeTypes\\TypoScriptObjects\\AssetListImplementation'
```

Yaml:

```
'TYPO3.Neos.NodeTypes:AssetList':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Asset list'
    icon: 'icon-folder-open-alt'
    position: 700
    inspector:
      groups:
        resources:
          label: 'Resources'
          position: 5
  properties:
    assets:
      type: array<TYPO3\Media\Domain\Model\Asset>
      ui:
        inspector:
          group: 'resources'
        label: 'Assets'
```