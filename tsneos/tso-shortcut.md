# Neos TypoScript: Shortcut

**Beschreibung:** Shortcuts sind ein Documententyp, der selbst keinen Inhalt anzeigt, sondern auf eine Zielseite weiterleitet. 

**Vollständiger Name:** `TYPO3.Neos:Shortcut`

**TypoScript Definition:** 
```
# TYPO3.Neos.Shortcut is given a representation for editing purposes
#
prototype(TYPO3.Neos:Shortcut) < prototype(TYPO3.TypoScript:Template) {
  templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/Shortcut.html'

  targetMode = ${q(node).property('targetMode')}
  firstChildNode = ${q(node).children('[instanceof TYPO3.Neos:Document]').get(0)}
  target = ${q(node).property('target')}
  targetConverted = ${Neos.Link.hasSupportedScheme(this.target) ? Neos.Link.convertUriToObject(this.target, node) : null}
  targetSchema = ${Neos.Link.getScheme(this.target)}

  node = ${node}

  @exceptionHandler = 'TYPO3\\Neos\\TypoScript\\ExceptionHandlers\\NodeWrappingHandler'
}
```

**Shortcut leitet von Template ab und hat damit auch desses Eigenschaften!**


**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Shortcut.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `targetMode` | string | Modus der Weiterleitung (spezifische Seite, Elternseite, erste Kind-Seite)  |
| `targetNode` | string | Node auf die Weitergeleitet wird  |
| `firstChildNode` | string | Erste Child-Node |
| `target` | string | Target |
| `targetSchema` | string | Schema (wie `http` oder `https`) |
| `targetConverted` | mixed | Zielobjekt oder `NULL` |

**Beispiel(e):**

Yaml-Definition:
```
'TYPO3.Neos:Shortcut':
  superTypes: ['TYPO3.Neos:Document']
  ui:
    label: 'Shortcut'
    icon: 'icon-share'
    inspector:
      groups:
        document:
          label: 'Shortcut options'
  properties:
    targetMode:
      type: string
      defaultValue: 'firstChildNode'
      ui:
        label: 'Target mode'
        reloadIfChanged: TRUE
        inspector:
          group: 'document'
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            values:
              firstChildNode:
                label: 'First child node'
              parentNode:
                label: 'Parent node'
              selectedNode:
                label: 'Selected node'
    targetNode:
      type: reference
      ui:
        label: 'Target node'
        inspector:
          group: 'document'
```

HTML-Template:
```
{namespace neos=TYPO3\Neos\ViewHelpers}
<div id="neos-shortcut">
  <p>
    <f:switch expression="{targetMode}">
      <f:case value="selectedNode">
        This is a shortcut to a specific page.<br />
        Click <neos:link.node node="{targetNode}">here</neos:link.node> to continue to the page.
      </f:case>
      <f:case value="firstChildNode">
        This is a shortcut to the first child page.<br />
        Click <neos:link.node node="{firstChildNode}">here</neos:link.node> to continue to the page.
      </f:case>
      <f:case value="parentNode">
        This is a shortcut to the parent page.<br />
        Click <neos:link.node node="{node.parent}">here</neos:link.node> to continue to the page.
      </f:case>
    </f:switch>
  </p>
</div>
```