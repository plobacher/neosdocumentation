# Neos TypoScript: Plugin View

**Beschreibung:** Während der Typ Plugin auch als *Master Plugin* bezeichnet wird, kann man mit Plugin Views Ansichten (Controller/Action-Kombinationen) eines Plugin darstellen (wird normalerweise nicht erweitert)

**Vollständiger Name:** `TYPO3.Neos:PluginView`

**TypoScript Definition:** 
```
# PluginView Implementation
# This represents a View that is always bound to a master Plugin
# Usually you won't need to extend this
#
prototype(TYPO3.Neos:PluginView) >
prototype(TYPO3.Neos:PluginView) < prototype(TYPO3.Neos:Content) {
  @class = 'TYPO3\\Neos\\TypoScript\\PluginViewImplementation'
  @cache {
    mode = 'uncached'
    context {
      1 = 'node'
    }
  }
}
```

**PluginView leitet von Plugin ab und hat damit auch dessen Eigenschaften!**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/PluginView.ts2
```

**Beispiel(e):**

Yaml Konfiguration um das Plugin Views Feature zu zeigen. Alle Einträge unter `controllerActions` erzeugen neue Views:

```
##
# A simple "Flickr" plugin that demonstrates the "PluginViews"-feature
#
'TYPO3.NeosDemoTypo3Org:Flickr':
  superTypes: ['TYPO3.Neos:Plugin']
  ui:
    label: 'Flickr photo feed'
    icon: 'icon-rss'
    inspector:
      groups:
        'feed':
          label: 'Feed'
  options:
    'pluginViews':
      'UserFeed':
        label: 'User feed'
        controllerActions:
          'TYPO3\NeosDemoTypo3Org\Controller\FlickrController': ['userStream']
  properties:
    'tags':
      type: string
      defaultValue: ''
      ui:
        label: 'Tag(s) for the flickr feed'
        reloadIfChanged: TRUE
        inspector:
          group: 'feed'
```

Definition:
```
'TYPO3.Neos:PluginView':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Plugin View'
    group: 'plugins'
    inspector:
      groups:
        pluginViews:
          label: 'Plugin Views'
          position: 100
  nonEditableOverlay: false
  properties:
    plugin:
      type: string
      ui:
        label: 'Master View'
        reloadIfChanged: TRUE
        inspector:
          group: 'pluginViews'
          position: 20
          editor: 'TYPO3.Neos/Inspector/Editors/MasterPluginEditor'
    view:
      type: string
      ui:
        label: 'Plugin View'
        reloadIfChanged: TRUE
        inspector:
          group: 'pluginViews'
          position: 20
          editor: 'TYPO3.Neos/Inspector/Editors/PluginViewEditor'

```
