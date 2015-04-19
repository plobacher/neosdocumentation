# TypoScript Kontext

Per Default gibt es fünf verschiedene Kontext-Variablen, auf die insbesondere innerhalb von Eel-Ausdrücken mittels `${...}` zugegriffen werden kann:

## node

Die Kontext-Variable `node` bezeichnet immer die aktuelle Node.


### node.identifier

Gibt die UUID der Node zurück.


### node.properties

Über diesen Schlüssel können die Eigenschaften der Node abgefragt werden. Bei einer Seite sind dies beispielsweise per Default:

* `name`: Name des Nodes, z.B. `Website`
* `title`: Titel des Nodes, z.B. `Home`
* `state`: Status der Node, z.B. `1`
* `siteResourcesPackageKey`: z.B. `Lobacher.Website`

Sobald man weitere Eigenschaften im Inspektor auswählt und speichert, erhält man diese ebenfalls:

* layout
* subpageLayout
* u.a.

Gespeichert werden diese Daten in der Tabelle `typo3_typo3cr_domain_model_nodedata` im Feld `properties`.

```
a:6:{s:4:"name";s:7:"Website";s:5:"title";s:4:"Home";s:5:"state";s:1:"1";s:23:"siteResourcesPackageKey";s:16:"Lobacher.Website";s:6:"layout";s:0:"";s:13:"subpageLayout";s:0:"";}
```

### Zugriff über FlowQuery

Will man allerdings auf weitere Attribute zugreifen (z.B. `hiddenInIndex`, `hiddenBeforeDate`,...), die in der obigen Tabelle als eigenständige Spalten existieren, so kommt man mit Eel nicht mehr weiter. Hier muss man FlowQuery und dessen Funktion `property()` verwenden - z.B.:

```
page = ${q(node).property('_hiddenInIndex')}
```

Diese Eigenschaften haben einen Unterstrich, da sie als intern gekennzeichnet sind. 

Damit ist es möglich folgende Informationen von einer Node zu bekommen:

* `_workspace.name` (Workspace-Informationen, hier der Name z.B. `live` - weitere Unterschlüssel sind `baseWorkspace`, `rootNodeData)
* `_path` (z.B. `/sites/neosdemotypo3org/download`)
* `_properties.[propertyName]` (z.B. `_properties.name` ergibt `Home`)
* `_nodeType` (z.B. `TYPO3.Neos.NodeTypes:Page`)
* `_visible` (Ob die Seite sichtbar ist oder nicht, z.B. `1` für sichtbar)
* `_accessible` (ob die Seite mit den aktuellen Zugriffsrechten aufgerufen werden kann, z.B. `1` für Zugriff möglich)
* `_removed` (ob die Seite entfernt wurde, z.B. `1` für ja)
* `_hiddenBeforeDateTime` (Vor diesem Datum ist die Node nicht sichtbar. Ist vom Typ DateTime, daher Abfrage z.B. mittels `_hiddenAfterDateTime.date` ergibt z.B. `2014-04-18 00:00:00`)
* `_hiddenAfterDateTime` (Nach diesem Datum ist die Node nicht sichtbar. Ist vom Typ DateTime, daher Abfrage z.B. mittels `_hiddenAfterDateTime.date` ergibt z.B. `2014-04-18 00:00:00`)
* `_hiddenInIndex` (z.B. `1`)
* `_accessRoles.[role]`
* `_parent.name` (Eltern-Node, hier der Name, z.B. `sites`. Weitere Schlüssel sind alle hier aufgeführten)
* `_parentPath` (Nodepfad der Eltern-Node, z.B. `/sites`)
* `_depth` (Tiefe des Levels im globalen Node-Tree, z.B. `2`)
* `_index` (Sorting-Index, z.B. `200`)
* `_contextPath` (Node-Pfad mit Content-Informationen wie beispielsweise den Workspacenamen, wenn dieser nicht `live` ist, z.B. `/sites/mysitecom/homepage/about@user-admin`)
`_identifier` (die UUID der Node, z.B. `d34e7f68-6641-7c0f-4efc-d9d2c58f0a65`)

Definiert werden die möglichen Schlüssel in der Datei `Packages/Application/TYPO3.TYPO3CR/Classes/TYPO3/TYPO3CR/Domain/Model/NodeData.php`


## documentNode

Die Kontext-Variable `documentNode` bezeichnet immer die nächstgelegene Node (zur aktuellen Node), die vom Typ `TYPO3.Neos:Document` ist. Wenn diese bereits ein Document ist, so sind `node` und `documentNode` identisch


### node.identifier

Gibt die UUID der `documentNode` zurück.


### documentNode.properties

Diese sind zu `node.properties` identisch.


## site

Hiermit wird die Site-Node (`/sites/[sitename]` z.B. `/sites/neosdemotypo3org`) angesprochen.

Um zum Beispiel die aktuelle Domain zu ermitteln (als Objekt vom Typ `TYPO3\Flow\Domain\Model\Domain`) kann man folgendes Eel-Code verwenden:

```
currentDomain = ${site.context.currentDomain}
```

### site.identifier

Gibt die UUID der Site-Node zurück.


## request

Hiermit hat man Zugriff auf das Request-Objekt. Informationen hierzu sind in der Datei `Packages/Framework/TYPO3.Flow/Classes/TYPO3/Flow/Mvc/ActionRequest.php` zu finden.

* `request.format` (gibt das Format, z.B. `html` zurück)
* `request.controllerActionName` (der Name der Action, z.B. `show`)
* `request.controllerPackageKey` (Package-Key des aktuellen Controllers, z.B. `TYPO3.Neos`)
* `request.controllerSubPackageKey` (Sub-Package-Key des aktuellen Controllers sofern vorhanden)
* `request.controller` (Name des Controllers, z.B. `Frontend\Node`)
* `request.dispatched` (Angabe, ob der Request dispatched wurde, z.B. `1`)