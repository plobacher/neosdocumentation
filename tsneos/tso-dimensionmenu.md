# Neos TypoScript: DimensionMenu

**Beschreibung:** Rendert eine Content-Dimensionen-Navigation

**Vollständiger Name:** `TYPO3.Neos:DimensionMenu`

**TypoScript Definition:** 
```
# TYPO3.Neos:DimensionMenu provides basic dimension (e.g. language) menu rendering
prototype(TYPO3.Neos:DimensionMenu) < prototype(TYPO3.Neos:Menu) {
   @class = 'TYPO3\\Neos\\TypoScript\\DimensionMenuImplementation'

   templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/DimensionMenu.html'

   absent.attributes = TYPO3.TypoScript:Attributes {
      class = 'normal'
   }

   # Example:
   # name of the dimension to use (required)
   # dimension = 'language'

   # list of presets, if the default order should be overridden
   # presets = ${['en_US']}
}
```

**Breadcrumb leitet von TYPO3.Neos:Menu (und dieses von Template) ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/DimensionMenu.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `dimension` | string | Die Content-Dimension |
| `presets` | array | Wenn gesetzt, werden die Presets von hier und nicht von den Settings genommen |

**Beispiel(e):**

```
languageMenu = TYPO3.Neos:DimensionMenu {
   dimension = 'language'
}
```

Fluid-Template:
```
{namespace neos=TYPO3\Neos\ViewHelpers}
{namespace ts=TYPO3\TypoScript\ViewHelpers}
<ul{attributes -> f:format.raw()}>
<f:for each="{items}" as="item">
   <li{ts:render(path:'{item.state}.attributes', context: {item: item}) -> f:format.raw()}>
      <f:if condition="{item.node}">
         <f:then>
            <neos:link.node node="{item.node}">{item.label}</neos:link.node>
         </f:then>
         <f:else>
            {item.label}
         </f:else>
      </f:if>
   </li>
</f:for>
</ul>
```