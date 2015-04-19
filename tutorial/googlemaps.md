# Google Maps

Die Idee dahinter ist, dass man ein Content-Objekt "Google-Maps" einfügen kann, welches eine Location anzeigt. Diese wird per Koordinaten im Inspektor festgelegt.


Zunächst muss also erst einmal die NodeTypes Definition erweitert werden `Schulung.Website/Configuration/NodeTypes.yaml`:

```
'Schulung.Website:GoogleMaps':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    inlineEditable: FALSE
    label: 'Google Map'
    inspector:
      groups:
        address:
          label: 'Address'
          position: 5
  properties:
    latitude:
      type: 'string'
      ui:
        label: 'Latitude'
        reloadIfChanged: true
        inspector:
          group: 'address'
    longitude:
      type: 'string'
      ui:
       label: 'Longitude'
       reloadIfChanged: true
       inspector:
         group: 'address'
```

## TypoScript

Im eigenen TypoScript `Schulung.Website/Resources/Private/TypoScripts/Library/NodeTypes/GoogleMaps.ts2` fragen wir nun die Koordinaten ab und setzen ein Flag, wenn Werte übergeben wurden:

```
prototype(Schulung.Website:GoogleMaps) {
	isLatitudeAndLongitudeSet = ${!(String.isBlank(q(node).property('longitude')) || String.isBlank(q(node).property('latitude')))}
}
```

Das TypoScript muss nun im Haupt-TypoScript unter `Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2` eingebunden werden:

```
namespace: TS=TYPO3.TypoScript
...
include: NodeTypes/GoogleMaps.ts2
...
page = Page {
```

## Template laden

Der NodyType muss nun natürlich auch gerendert werden - dafür wird ein Template `GoogleMaps.html` an die Stelle `Schulung.Website/Resources/Private/Templates/NodeTypes` gelegt:

```
<f:if condition="{isLatitudeAndLongitudeSet}">
	<f:then>
		<iframe width="100%" height="400" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" src="http://maps.google.com/maps?hl=en&amp;ie=UTF8&amp;ll={latitude},{longitude}&amp;t=m&amp;z=14&amp;output=embed"></iframe>
	</f:then>
	<f:else>
		<p>Please set latitude and longitude for center of this map in the inspector!</p>
	</f:else>
</f:if>
```
