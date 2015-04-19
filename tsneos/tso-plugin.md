# Neos TypoScript: Plugin

**Beschreibung:** Jedes Plugin sollte von diesem Typ ableiten 

**Vollständiger Name:** `TYPO3.Neos:Plugin`

**TypoScript Definition:** 
```
# Abstract Plugin Implementation
# This should be extended by all plugin Content Elements
#
prototype(TYPO3.Neos:Plugin) >
prototype(TYPO3.Neos:Plugin) < prototype(TYPO3.Neos:Content) {
  @class = 'TYPO3\\Neos\\TypoScript\\PluginImplementation'

  @cache {
    mode = 'uncached'
    context {
      1 = 'node'
      2 = 'documentNode'
    }
  }
}
```

**Plugin leitet von Content ab und hat damit auch dessen Eigenschaften!**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Plugin.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `package` | string | Angabe des Package-Keys  |
| `subpackage` | integer | Angabe des Subpackage-Keys  |
| `controller` | string | Angabe des Controllers, der aufgerufen werden soll |
| `action` | string | Angabe der Action, die aufgerufen werden soll |
| `argumentNamespace` | string | ??? |


**Beispiel(e):**

```
prototype(Sarkosh.CdCollection:Plugin) < prototype(TYPO3.Neos:Plugin)
prototype(Sarkosh.CdCollection:Plugin) {
  package = 'Sarkosh.CdCollection'
  controller = 'Standard'
  action = 'index'
}
```

`Configuration/NodeTypes.yaml`:
```
'Sarkosh.CdCollection:Plugin':
    superTypes: ['TYPO3.Neos:Plugin']
    ui:
      label: 'CD Collection'
      group: 'plugins'
    options:
      pluginViews:
        'CollectionShow':
          label: 'Show Collection'
          controllerActions:
            'Sarkosh\CdCollection\Controller\CollectionController': ['show']
        'CollectionOverview':
          label: 'Collection Overview'
          controllerActions:
            'Sarkosh\CdCollection\Controller\CollectionController': ['overview']

```
