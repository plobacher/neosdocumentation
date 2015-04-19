# Neos TypoScript: BreadcrumbMenu

**Beschreibung:** Rendert eine Breadcrumb-Navigation

**Vollständiger Name:** `TYPO3.Neos:BreadcrumbMenu`

**TypoScript Definition:** 
```
# TYPO3.Neos:BreadcrumbMenu provides a breadcrumb navigation based on menu items.
#
prototype(TYPO3.Neos:BreadcrumbMenu) < prototype(TYPO3.Neos:Menu) {
   templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/BreadcrumbMenu.html'
   itemCollection = ${q(node).add(q(node).parents('[instanceof TYPO3.Neos:Document]')).get()}

   attributes.class = 'breadcrumb'
}

```

**Breadcrumb leitet von TYPO3.Neos:Menu (und dieses von Template) ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/BreadcrumbMenu.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `templatePath` | resource | Pfad zum Fluid-Template, welches das Menü abbildet |
| `itemCollection` | Eel | Enthält alle Elemente der Breadcrumb |


**Beispiel(e):**

```
breadcrumb = BreadcrumbMenu {
   templatePath = 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/TypoScriptObjects/BreadcrumbMenu.html'
   itemCollection = ${q(node).add(q(node).parents())}
}
```

Fluid-Template:
```
{namespace neos=TYPO3\Neos\ViewHelpers}
{namespace ts=TYPO3\TypoScript\ViewHelpers}
<f:if condition="{items}">
   <ul{attributes -> f:format.raw()}>
   <f:for each="{items}" as="item" reverse="TRUE">
      <li{ts:render(path:'{item.state}.attributes', context: {item: item}) -> f:format.raw()}>
         <f:if condition="{item.state} == 'current'">
            <f:then>
               {item.label}
            </f:then>
            <f:else>
               <neos:link.node node="{item.node}" />
            </f:else>
         </f:if>
      </li>
   </f:for>
   </ul>
</f:if>
```