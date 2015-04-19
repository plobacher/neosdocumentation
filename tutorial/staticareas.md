# Statische Bereiche definieren

Die Idee ist, das eine statische Area "Footer" geschaffen wird, die nur auf einer Seite gepflegt, aber von jeder Seite aus inkludiert wird.

## NodeType mit Area footer

Die Datei `Packages/Sites/Schulung.Website/Configuration/NodeTypes.yaml` muss zunächst um einen eigenen NodeType ergänzt werden:

```
'Vendor.SitePackageName:HomePage':
  superTypes: ['TYPO3.Neos.NodeTypes:Page']
  ui:
    label: 'Homepage'
  childNodes:
    footer:
      type: 'TYPO3.Neos:ContentCollection'
```

## TypoScript hinzufügen

In der Datei `` wird nun das entsprechende TypoScript hinzugefügt:

```
content {
	main = PrimaryContent {
  	nodePath = 'footer'
  }
}
```

## HTML-Template ergänzen

Auf das HTML-Template muss entsprechend angepasst werden:

```
<div class="col-sm-3">
	<p>{content.footer -> f:format.raw()}</p>
</div>
```

## TypoScript für alle Seiten passend machen

Legt man nun eine Seite an und füllt in die Area `footer` Inhalte ein, so werden diese bereits angezeigt. Allerdings klappt dies spötestens bei einer anderen Seite nicht mehr - wir müssen also das Script entsprechend anpassen:

```
footer = TYPO3.Neos:ContentCollection {
	// nodePath = ${q(site).find('footer').property('_path')}
  // collection = ${q(site).children('footer').children()}
	nodePath = ${q(site).find('homepage').children('footer').property('_path')}
  collection = ${q(site).find('homepage').children('footer').children()}
}
```

## Überprüfung ob alle Nodes existieren

Sollten einmal nicht alle Nodes eines Typs automatisch generiert werden, so können diese wie folgt überprüft werden:

```
./flow node:autocreatechildnodes --node-type TYPO3.Neos.NodeTypes:Homepage
```
