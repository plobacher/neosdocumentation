# Neos TypoScript: Menu

**Beschreibung:** Über dieses Objekte werden Basis-Menüs erzeugt 

**Vollständiger Name:** `TYPO3.Neos:Menu`

**TypoScript Definition:** 
```
# TYPO3.Neos:Menu provides basic menu rendering
#
prototype(TYPO3.Neos:Menu) < prototype(TYPO3.TypoScript:Template) {
  @class = 'TYPO3\\Neos\\TypoScript\\MenuImplementation'
  templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/Menu.html'
  node = ${node}
  items = ${this.items}
  filter = 'TYPO3.Neos:Document'
  attributes = TYPO3.TypoScript:Attributes

  active.attributes = TYPO3.TypoScript:Attributes {
    class = 'active'
  }
  current.attributes = TYPO3.TypoScript:Attributes {
    class = 'current'
  }
  normal.attributes = TYPO3.TypoScript:Attributes {
    class = 'normal'
  }

  @exceptionHandler = 'TYPO3\\Neos\\TypoScript\\ExceptionHandlers\\NodeWrappingHandler'

  @cache {
    mode = 'cached'
    entryIdentifier {
      documentNode = ${documentNode}
      domain = ${site.context.currentDomain}
    }
    entryTags {
      1 = 'NodeType_TYPO3.Neos:Document'
    }
  }
}
```

**Menu leitet von Template ab und hat damit auch desses Eigenschaften!**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Menu.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `entryLevel` | string | Seitenbaumebene, auf der das Menü beginnt  |
| `lastLevel` | integer | Seitenbaumebene, auf der das Menü endet  |
| `startingPoint` | node | Startpunkt des Menüs  |
| `maximumLevels` | integer | Maximale Anzahl von Unterebenen (Default ist 1, muss überschrieben werden, um mehr Ebenen zu darzustellen) |
| `renderHiddenInIndex` | boolean | Auch Menüelemente anzeigen, die `hiddenInIndex` gesetzt haben? |
| `itemCollection` | array | Eine Collection von Nodes, dessen Elemente vor das eigentliche Menü gerendert werden |
| `filter` | string | Angabe des Objekt-Types, der berücksichtigt werden soll (z.B. `TYPO3.Neos:Document`)  |
| `items` | string | Eel Ausruck, der die Items bestimmt, die im Menü enthalten sein sollen  |

Es gibt zudem vier Constanten:

STATE_NORMAL, STATE_CURRENT, STATE_ACTIVE und STATE_absent - diese stehen in der Property `state` der Node zur Verfügung.


**Beispiel(e):**

TypoScript für ein Menü:
```
page = Page
page.body {
  templatePath = 'resource://sesc.testsite/Private/Templates/Page/Default.html'
  sectionName = 'body'
  parts {
    menu = Menu {
      entryLevel = 1
      maximumLevels = 3
    }
  }
}
```

HTML-Template:
```
{namespace neos=TYPO3\Neos\ViewHelpers}
{namespace ts=TYPO3\TypoScript\ViewHelpers}
<ul{attributes -> f:format.raw()}>
  <f:render section="itemsList" arguments="{items: items}" />
</ul>

<f:section name="itemsList">
  <f:for each="{items}" as="item">
    <li{ts:render(path:'{item.state}.attributes', context: {item: item}) -> f:format.raw()}>
    <neos:link.node node="{item.node}" />
    <f:if condition="{item.subItems}">
      <ul>
        <f:render section="itemsList" arguments="{items: item.subItems}" />
      </ul>
    </f:if>
    </li>
  </f:for>
</f:section>
```