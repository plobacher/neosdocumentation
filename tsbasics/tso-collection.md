# TypoScript 2.0 Objekt: Collection

**Beschreibung:** Iteriert über eine Collection (aus Objekten) und rendert jedes Element mit Hilfe eines `itemRenderer`

**Vollständiger Name:** `TYPO3.TypoScript:Collection`

**TypoScript Definition:** 
```
prototype(TYPO3.TypoScript:Array).@class = 'TYPO3\\TypoScript\\TypoScriptObjects\\CollectionImplementation'
```

**Datei:**
```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `collection` | array/iterable, required | Das Array oder der Iterator über den interiert wird |
| `itemName` | string,required | Der Name, unter dem jedes Element verfügbar gemacht wird |
| `iterationName` | string | Meta-Infos über die Iteration: `index` (beginnend bei 0), `cycle` (beginned bei 1), `isFirst`, `isLast`. |
| `iterationRenderer` | nested TS object | Dieses TypoScript Objekt wird einmal je Durchlauf aufgerufen und dessen Resultat verbunden |


**Beispiel(e):**

```
myCollection = TYPO3.TypoScript:Collection {
   collection = ${[1, 2, 3]}
   itemName = 'element'
   itemRenderer = TYPO3.TypoScript:Template
   itemRenderer.templatePath = '...'
   itemRenderer.element = ${element}
}
```

```
titleTag {
   // Title-Tag überschreiben mit einer Breadcrumb
   content = TYPO3.TypoScript:Collection {
      // Hole alle Eltern-Dokumente mit Ausnahme der Homepage
      collection = ${q(documentNode).add(q(documentNode).parents()).slice(0, -1).get()}
      itemName = 'node'
      iterationName = 'nodeIterator'
      // Implodiere alle Node-Titel mit einem -
      itemRenderer = ${q(node).property('title') + (nodeIterator.isLast ? '' : ' - ')}
      // Füge den allgemeinen Seitennamen hinzu (oder TYPO3 Neos als Default)
      @process.siteName = ${(value ? value + ' - ' : '') + 'TYPO3 Neos'}
   }
}
```