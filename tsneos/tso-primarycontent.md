# Neos TypoScript: Primary Content

**Beschreibung:** Dieses Objekt sollte dafür verwendet werden, um den Haupt-Content (`main`) der Website zu rendern. 

**Vollständiger Name:** `TYPO3.Neos:PrimaryContent`

**TypoScript Definition:** 
```
# Primary content should be used to render the main content of a site and
# provides an extension point for other packages
#
prototype(TYPO3.Neos:PrimaryContent) < prototype(TYPO3.TypoScript:Case) {
  nodePath = 'to-be-defined-by-user'

  @override.nodePath = ${this.nodePath}
  @ignoreProperties = ${['nodePath']}

  default {
    prototype(TYPO3.Neos:ContentCollection) {
      nodePath = ${nodePath}
    }

    condition = TRUE
    type = 'TYPO3.Neos:ContentCollection'
    @position = 'end'
  }
}
```

**PrimaryContent leitet von Case ab und hat damit auch desses Eigenschaften!**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/PrimaryContent.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `nodePath` | sting | Identifier der Node, die per Main Content gerendert werden soll  |



**Beispiel(e):**

Minimal-Beipiel zum Rendern von Content:
```
page = Page
page.body {
   sectionName = 'body'
   content.main = PrimaryContent {
      nodePath = 'main'
   }
}
```

Rendern der Content-Node `main`:
```
page1 = TYPO3.Neos:Page
page1.body {
  templatePath = ${fixturesDirectory + '/WebsiteTemplate.html'}
  content {
    teaser = TYPO3.Neos:ContentCollection
    teaser.nodePath = 'teaser'

    main = TYPO3.Neos:PrimaryContent
    main.nodePath = 'main'

    sidebar = TYPO3.Neos:ContentCollection
    sidebar.nodePath = 'sidebar'
  }
  title = ${q(node).property('title')}
}
```

Austauschen des Inhalts, falls eine Bedingung erfüllt ist:
```
prototype(TYPO3.Neos:PrimaryContent).elasticSearch {
  condition =  ${q(request).property('arguments.search')}
  type = 'Lobacher.Website:SearchResult'
}

prototype(Lobacher.Website:SearchResult) < prototype(TYPO3.TypoScript:Template){
  templatePath = 'resource://Lobacher.Website/Private/Templates/TypoScriptObjects/SearchResult.html'
  searchTerm = ${q(request).property('arguments.search')}
  ...
}

```

