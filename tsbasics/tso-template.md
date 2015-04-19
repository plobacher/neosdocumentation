# TypoScript 2.0 Objekt: Template

**Beschreibung:** Rendert ein Fluid-Template, welches durch templatePath angegeben ist

**Vollständiger Name:** `TYPO3.TypoScript:Template`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Array).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\TemplateImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `templatePath` | string, required | Das Template, angeben z.B. mit `resource://` |
| `partialRootPath` | string | Der Pfad, unter dem die Partials zu finden sind |
| `layoutRootPath` | string | Der Pfad, unter dem die Layouts zu finden sind |
| `sectionName` | string | Die Fluid Section `<f:section>` die gerendert werden soll (sofern es eine gibt) |
| `[variablen]` | any | Alle weiteren Strings, werden als Variable an den View weitergreicht. Als Werte sind dort einfache Ausdrücke (Zahlen, Strings), Eel oder TypoScript-Objekte zugelassen |


Verwendet man `ressource://` um auf eine Ressource zuzugreifen, gilt folgende Auflösung:

```
'resource://My.Package/Private/path/to/Template.html'

// wird aufgelöst zu

Packages/My.Package/Resources/Private/path/to/Template.html
```

**Beispiel(e):**

```
myTemplate = TYPO3.TypoScript:Template {
   templatePath = 'resource://My.Package/Private/path/to/Template.html'
   someDataAvailableInsideFluid = 'my data'
}
```

```
page = Page {
   head {
      stylesheets {
         site = TypoScript:Template {
            templatePath = 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/Page/Default.html'
            sectionName = 'stylesheets'
         }
      }

      metadata = TypoScript:Template {
         templatePath = 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/Page/Default.html'
         sectionName = 'metadata'
      }
   }
   body {
      templatePath = 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/Page/Default.html'
      sectionName = 'body'

      parts {
         mainMenu = Menu {
            entryLevel = 1
            templatePath = 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/TypoScriptObjects/MainMenu.html'
            maximumLevels = 3
            site = ${site}
         }
      }

   }
}
```