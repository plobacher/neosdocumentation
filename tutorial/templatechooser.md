# Template Chooser


## Status Quo

Schaut man sich die Datei `Packages/Application/TYPO3.Neos.NodeTypes/Configuration/NodeTypes.yaml` an, so findet sich darin bereits der Template-Chooser vordefiniert - allerdings noch ohne weitere Funktion:

```
'TYPO3.Neos.NodeTypes:Page':
  superTypes: ['TYPO3.Neos:Document']
  childNodes:
    main:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    layout:
    type: string
    ui:
      label: 'Layout for this page only'
      reloadIfChanged: TRUE
      inspector:
        group: 'layout'
        editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
        editorOptions:
          placeholder: 'Inherit from parent'
          values:
            '':
              label: ''
    subpageLayout:
    type: string
    ui:
      label: 'Layout for subpages of this page'
      inspector:
        group: 'layout'
        editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
        editorOptions:
          placeholder: 'Inherit from parent'
          values:
            '':
              label: ''
  ui:
    label: 'Page'
    icon: 'icon-file'
    inspector:
      groups:
        document:
          label: 'Title'
        layout:
          label: 'Layout'
          position: 150
```

## Erweitern der Definition um Templates

Um nun diese Definition zu erweitern, schreiben wir in die Datei `` folgenden Code:

```
'TYPO3.Neos.NodeTypes:Page':
  properties:
    layout:
      ui:
        inspector:
          editorOptions:
            values:
              'default':
                label: 'Default'
              'about':
                label: 'About page'
    subpageLayout:
      ui:
        inspector:
          editorOptions:
            values:
              'default':
                label: 'Default'
              'about':
                label: 'About page'
```

## Erweitern der TypoScript-Definition

Nun müssen wir die TypoScript-Definition in der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2` anpassen:

```
default < page

about < page
about.body {
	templatePath = 'resource://Schulung.Website/Private/Templates/Page/About.html'
}
```

Dafür muss natürlich das Template umkopiert werden und entsprechend mit Markern und Sektionen versehen werden.


## Template aufgrund des NodeTypes auswählen

```
prototype(VendorName.VendorSite:Page) < prototype(TYPO3.Neos:Page) {
	body.templatePath = 'resource//VendorName.VendorSite/Private/Templates/Page/Default.html'
	# Your further page configuration here
}

prototype(VendorName.VendorSite:EmployeePage) < prototype(VendorName.VendorSite:Page) {
	body.templatePath = 'resource//VendorName.VendorSite/Private/Templates/Page/Employee.html'
	# Your further employee page configuration here
}

root.employeePage {
	condition = ${q(node).is('[instanceof VendorName.VendorSite:Employee]')}
	renderPath = '/employeePage'
}

page = VendorName.VendorSite:Page
employeePage = VendorName.VendorSite:EmployeePage
```
