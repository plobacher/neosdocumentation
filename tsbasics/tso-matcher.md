# TypoScript 2.0 Objekt: Matcher

**Beschreibung:** Wird nur zusammen mit Case verwendet und stellt ein Element dort dar.

**Vollständiger Name:** `TYPO3.TypoScript:Matcher`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Array).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\MatcherImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `condition` | eel expression, required | Die Bedingung (ist ein Eel-Ausdruck) |
| `type` | ts object | Typ der gesetzt wird |

Wird die Eigenschaft `type` nicht verwendet, so setzt Neos dort automatisch den Typ auf `TYPO3.TypoScript:Matcher`. Über den Matcher kann ein `renderPath` angegeben werden, über den Neos das zu rendernde Element automatisiert bestimmt.


**Beispiel(e):**

```
myCase = TYPO3.TypoScript:Case
myCase {
   someCondition {
      condition = ${... Eel Ausdruck, der entweder TRUE oder FALSE ergibt ... }
      type = 'MyNamespace:My.Special.Type'
   }
   fallback {
      condition = ${true}
      type = 'MyNamespace:My.Default.Type'
   }
}
```

```
root = TYPO3.TypoScript:Case
root {
   shortcut {
      prototype(TYPO3.Neos:Page) {
         body = TYPO3.Neos:Shortcut
      }

      @position = 'start'
      condition = ${q(node).is('[instanceof TYPO3.Neos:Shortcut]')}
      type = 'TYPO3.Neos:Page'
   }

   editPreviewMode {
      @position = 'end 9996'
      condition = ${editPreviewMode != null}
      renderPath = ${'/' + editPreviewMode}
   }
   layout {
      @position = 'end 9997'
      layout = ${q(node).property('layout') != null && q(node).property('layout') != '' ? q(node).property('layout') : q(node).parents('[subpageLayout]').first().property('subpageLayout')}
      condition = ${this.layout != null && this.layout != ''}
      renderPath = ${'/' + this.layout}
   }

   format {
      @position = 'end 9998'
      condition = ${request.format != 'html'}
      renderPath = ${'/' + String.replace(request.format, '.', '/')}
   }

   default {
      @position = 'end 9999'
      condition = TRUE
      renderPath = '/page'
   }
}
```
