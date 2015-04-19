# NodeTypes Referenz

Basis für alle Aktivitäten rund um die Nodes sind die sogenannten **Node-Types**.

Dabei besitzt jede TYPO3CR Node einen Node-Type. Node-Types können in jedem Package definiert werden, indem Sie in der Datei `Configuration/NodeTypes.yaml` deklariert werden. Diese wird automatisiert geladen, wenn sie vorhanden ist.

Jeder Node-Type kann einen oder mehrere Eltern-Typen haben. Wenn diese spezifiziert sind (über die Eigenschaft `superTypes`), werden alle Eigenschaften und Settings der Eltern-Types vererbt.

Zudem können auch sogenannte `childNodes` definiert werden. Diese werden automatisiert angelegt, sobald die Node angelegt wird.

Nachfolgend ein Beispiel für eine NodeTypes-Deklaration:

```
'My.Package:SpecialHeadline':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Special Headline'
    group: 'general'
  properties:
    headline:
      type: 'string'
      defaultValue: 'My Headline Default'
      ui:
        inlineEditable: TRUE
      validation:
        'TYPO3.Neos/Validation/StringLengthValidator':
          minimum: 1
          maximum: 255
```

## Schema

Der NodeType-Defintion liegt ein Schema zu Grunde, welches hier zu finden ist: `Packages/Application/TYPO3.Neos/Resources/Private/Schema/NodeTypes.schema.yaml`

```
type: dictionary
additionalProperties:
  # every property here is a Node Type
  type: dictionary
  properties:
    'properties':
      type: dictionary
      additionalProperties:
        # for each property...
        type: dictionary
        properties:
          'ui':
            # here, we specify ONLY the "ui" part of the schema, as the remaining parts
            # are already specified in the NodeTypes schema of the TYPO3CR package
            type: dictionary
            additionalProperties: FALSE
            properties:

              'label': { type: string, description: "Human-readable label for this property." }

              'reloadIfChanged': { type: boolean, description: "If this property changes, should a page reload occur?" }

              'inlineEditable': { type: boolean, description: "Is this property inline editable, i.e. edited directly on the page through Aloha/Hallo?" }

              'aloha':
                type: dictionary
                additionalProperties: FALSE
                properties:

                  'format':
                    code: TRUE
                    type: 'dictionary'
                    additionalProperties: FALSE
                    properties:
                      'b': { type: boolean }
                      'i': { type: boolean }
                      'u': { type: boolean }
                      'sub': { type: boolean }
                      'sup': { type: boolean }
                      'p': { type: boolean }
                      'h1': { type: boolean }
                      'h2': { type: boolean }
                      'h3': { type: boolean }
                      'pre': { type: boolean }
                      'removeFormat': { type: boolean }

                  'table':
                    additionalProperties: FALSE
                    properties:
                      'table': { type: boolean }

                  'link':
                    additionalProperties: FALSE
                    properties:
                      'a': { type: boolean }

                  'list':
                    additionalProperties: FALSE
                    properties:
                      'ol': { type: boolean }
                      'ul': { type: boolean }

                  'alignment':
                    additionalProperties: FALSE
                    properties:
                      'right': { type: boolean }
                      'left': { type: boolean }
                      'center': { type: boolean }
                      'justify': { type: boolean }
                      'top': { type: boolean }
                      'middle': { type: boolean }
                      'bottom': { type: boolean }

              'inspector':
                type: dictionary
                additionalProperties: FALSE
                properties:

                  'group': { type: string, description: 'Identifier of the inspector group in which this property should be edited. If not set, will not appear in inspector at all.' }

                  'position': { type: integer, description: 'Position inside the inspector group, small numbers are sorted on top' }

                  'editor': { type: string, description: 'Name of the JavaScript Editor Class which is instanciated to edit this element in the inspector.' }

                  'editorOptions': { type: dictionary, description: 'options for the given editor' }

    'ui':
      # here, we specify ONLY the "ui" part of the schema, as the remaining parts
      # are already specified in the NodeTypes schema of the TYPO3CR package
      type: dictionary
      additionalProperties: FALSE
      properties:

        'label': { type: string, description: "Human-readable label for this Node Type." }

        'icon': { type: string, description: "Icon class" }

        'inlineEditable': { type: boolean, description: "If TRUE, it is possible to interact with this Node directly in the content view. If FALSE, an overlay is shown preventing any interaction with the node." }

        'group': { type: string, description: "Name of the group this content element is grouped into for the 'New Content Element' dialog." }

        'inspector':
          type: dictionary
          additionalProperties: FALSE
          properties:

            'groups':
              type: dictionary
              additionalProperties:

                # for each inspector group:
                type: dictionary
                additionalProperties: FALSE
                properties:

                  'label': { type: string, description: "Human-readable label for this Inspector Group." }

                  'position': { type: integer, description: 'Position of the inspector group, small numbers are sorted on top' }

        'search':
          type: dictionary
          additionalProperties: FALSE
          properties:

            'searchCategory': { type: string, description: "If searching for this node type in the search, the results will be grouped by this category." }
```

Die Zahl hinter den nachfolgenden Schlüssel bezeichnet die Anzahl der Leerzeichen, die die letzte Option eingerückt werden muss:


## `VendorName.PackageName:NodeTypeName:` (0)

* `VendorName` - hier wird der Vendor angegeben, bei internen NodeTypes ist dies `TYPO3`, ansonsten ein selbst gewählter Name
* `PackageName` - dies ist der Name der Application-Packages oder des Site-Packages
* `NodeTypeName` - hier wird der Name des Node-Type angegeben - dieser darf auf Punkte enthalten (z.B. `Schema.Person`)

Die Angaben müssen von einfachen Anführungszeichen eingeschlossen sein und wie alle NodeType-Deklarationsanweisungen, die keinen direkten Wert (Value) haben mit einem Doppelpunkt abgeschlossen werden.

### `superTypes:` (2)

Dies ist ein Array von Eltern-Nodes, von denen abgeleitet wird.

Hier gibt es zwei Notationen - entweder mittels eckiger Klammern (und dort per Komma getrennt, falls es mehrere Eltern-Nodes gibt) oder zeilenweise mit einem Minus davor:

```
  superTypes: ['TYPO3.Form:Base']

  superTypes: ['TYPO3.Form:Base', 'TYPO3.Form:RemovableMixin']

  superTypes:
    - 'TYPO3.Neos:Node'
    - 'TYPO3.Neos:Hidable'
    - 'TYPO3.Neos:Timable'
```

### `childNodes:` (2)

Dies enthält eine Liste von Kind-Nodes, die automatisiert erstellt werden, wenn eine Node des Typs erstellt wird. Für jede Kind-Node wird der (spätere) Name und der Typ angegeben:

```
  childNodes:
    column0:
      type: 'TYPO3.Neos:ContentCollection'
    column1:
      type: 'TYPO3.Neos:ContentCollection'
    main:
      type: 'TYPO3.Neos:ContentCollection'
```

Dies enthält eine Liste von Kind-Nodes, die automatisiert erstellt werden, wenn eine Node des Typs erstellt wird. Für jede Kind-Node wird der (spätere) Name und der Typ angegeben:


### `childNodes: [childNodeName]:` (4)

Pfad-Name der Child-Node

### `childNodes: [childNodeName]: type:` (6)

Spezifiziert den Typ.

### `childNodes: [childNodeName]: constraints:` (6)

Content constraints - siehe `constraints:`


### `constraints:`(4)

Hiermit werden diejenigen Node-Typen eingeschränkt, die unterhalb diesem angelegt werden (dürfen)

### `constraints: nodeTypes:` (4)

Hierunter werden NodeTypes aufgelistet

### `constraints: nodeTypes: [nodeType]:` (6)

Der konkrete NodeType wird entweder erlaubt oder nicht erlaubt. Es ist auch möglich '*' anzugeben, welches auf alle NodeTypes matcht.

```
    constraints:
      nodeTypes:
        # ALLOW text, DISALLOW Image
        'TYPO3.Neos.NodeTypes:Text': TRUE
        'TYPO3.Neos.NodeTypes:Image': FALSE
        # DISALLOW as Fallback (for not-explicitely-listed node types)
        '*': FALSE
```

### `ui:` (2)

Hier wird die Konfiguration abgelegt, die mit der User-Interface Repräsentation des Node-Types in Verbindung steht.

### `ui: label:` (4)

Das Label, welches zur Anzeige verwendet wird


### `ui: group:` (4)

Wenn es bei dem Node-Type um ein Content-Element handelt, welches im "New Content Element" Dialog anzeigt wird, kann mittels `group` die Gruppe in diesem Dialog spezifiziert werden.

Mögliche Gruppe sind per Default:

* `general`
* `structure`
* `layout`

Diese werden in der Datei `Packages/Application/TYPO3.Neos/Configuration/Settings.yaml` im Schlüssel `TYPO3.Neos.nodeTypes.groups` definiert.

Will man ein eigene Gruppe etablieren, so muss man diese zunächst in der Datei `Settings.yaml` definieren - im folgenden Beispiel wird die Gruppe `person` mit dem Label `Personen` definiert:

```
TYPO3:
  Neos:
    nodeTypes:
      groups:
        person:
          position: 'start'
          label: 'Personen'
```

### `ui: icon:` (4)

Hiermit setzt man das UI-Icon des NodeTypes.

Momentan ist es lediglich möglich, ein vordefiniertes Set an Icons zu verwenden, die in **Font Awesome** definiert wurden: `http://fortawesome.github.io/Font-Awesome/icons/`.


### `ui: inlineEditable:` (4)

Wenn dieser Wert auf `TRUE` gesetzt wird, ist es möglich, dass man im Content-View direkt mit der Node interagieren kann. Sobald der Wert auf `FALSE` steht, wird per Overlay eine Interaktion mit der Node verhindert. Wenn der Wert nicht angegeben wurde, geht Neos weiter zu einer Property, die den Wert `ui.inlineEditable` gesetzt hat.

### `ui: inspector:` (4)

Hiermit werden die Inspector-Eigenschaften für den Node-Type definiert.

### `ui: inspector: groups:` (6)

Definiert eine Gruppe im Inspector, welche später dafür verwendet werden kann, um Eigeschaften zu gruppieren.

### `ui: inspector: groups: [groupName]:` (8)

Hiermit (`[groupName]:`) wird der konkrete Gruppenname bezeichnet - z.B. `document:`

### `ui: inspector: groups: [groupName]: label:` (10)

Damit wird das Label für die Gruppe festgelegt

### `ui: inspector: groups: [groupName]: position` (10)

Position der Inspector-Gruppe. Je kleiner die Zahl, desto weiter oben wird die Gruppe positioniert.

### `ui: inspector: groups: [groupName]: tab` (10)

Name des Tabs, auf dem die Gruppe positioniert werden soll

### `ui: inspector: tabs:` (6)

Definiert einen Tab im Inspector, welche später dafür verwendet werden kann, um Eigeschaften auf Tabs zu gruppieren.

### `ui: inspector: tabs: [tabName]:` (8)

Hiermit (`[tabName]:`) wird der konkrete Tab-Name bezeichnet - z.B. `stats:`

### `ui: inspector: tabs: [tabName]:label` (10)

Damit wird das Label für den Tab festgelegt

## `ui: inspector: tabs: [tabName]: position` (10)

Position der Tabs. Je kleiner die Zahl, desto weiter links wird der Tab positioniert.

### `ui: inspector: tabs: [tabName]:icon` (10)

Damit wird das Icon für den Tab festgelegt


### `properties:` (2)

Eine Liste von benannten Eigenschaften für diesen Node-Type.


### `properties: [propertyName]:` (4)

Hiermit (`[propertyName]:`) wird die konkrete Eigenschaft bezeichnet - z.B. `metaDescription:`

### `properties: [propertyName]: type:` (6)

Hiermir wird der Datentyp der Eigenschaft festgelegt. Dies kann ein einfacher Typ (wie in PHP) sein (z.B. `string`), ein voll Qualifizierter PHP-Klassenname (z.B `TYPO3\Media\Domain\Model\ImageVariant`) oder aber eines der drei Spezial-Typen `date`, `references`, oder `reference` sein.

Mit `date` kann man Datums/Zeiten als DateTime-Objekt speichern. Mittels `reference` und `references` speichert man Referenzen, die auf andere Nodes zeigen. Dabei akzeptiert `reference` nur einzelne Nodes oder Node-Identifier, während `references` ein Array (aus Nodes bzw. Node-Identifier) akzeptiert

### `properties: [propertyName]: defaultValue:` (6)

Hiermit kann ein Default-Wert eingestellt werden, der zum Zeitpunkt der Erstellung der Node verwendet wird. Der Typ muss zu dem in `type:` spezifierten passen.

### `properties: [propertyName]: ui:` (6)

Hiermit die Darstellung der Eigenschaft in der UI spezifiziert.

### `properties: [propertyName]: ui: label:` (8)

Label der Eigenschaft

### `properties: [propertyName]: ui: reloadIfChanged:` (8)

Wenn der Wert auf `TRUE` steht, dann wird das ganze Element serverseitig neu geredert, sobald sich der Wert der damit spezifizierten Eigenschaft ändert. Dies funktioniert nur mit Eigenschaften, die im Property-Inspektor dargestellt werden

### `properties: [propertyName]: ui: inlineEditable:` (8)

Ist der Wert `TRUE`, dann kann man diese Eigenschaft Inline editieren, d.h. über den Aloha-Editor direkt auf der Seite.

### `properties: [propertyName]: ui: aloha:` (8)

Über diesen Schlüssel kann man die Format-Optionen einstellen, die der User für diese Eigenschaft im Aloha zur Verfügung hat:

```
        aloha:
          'format':
            'b': TRUE
            'i': TRUE
            'u': TRUE
            'sub': TRUE
            'sup': TRUE
            'p': TRUE
            'h1': TRUE
            'h2': TRUE
            'h3': TRUE
            'pre': TRUE
            'removeFormat': TRUE
          'table':
            'table': TRUE
          'link':
            'a': TRUE
          'list':
            'ol': TRUE
            'ul': TRUE
          'alignment':
            'right': TRUE
            'left': TRUE
            'center': TRUE
            'justify': TRUE
            'top': TRUE
            'middle': TRUE
            'bottom': TRUE
          'formatlesspaste':
            'button': TRUE # Show toggle button for formatless pasting.
            'formatlessPasteOption': FALSE # Whether the format less pasting should be enable by default.
#           'strippedElements': ['a'] # If not set the default value is used.
```

Deaktivieren von Optionen funktioniert wie folgt:

```
        aloha:
          'format': []
          'table': []
          'link': []
          'list': []
          'alignment': []
          'formatlesspaste':
            'button': FALSE
            'formatlessPasteOption': TRUE
```

### `properties: [propertyName]: ui: inspector:` (8)

Über diesen Schlüssel kann man die UI-Einstellungen für den Inspector des jeweiligen Feldes konfigurieren.

### `properties: [propertyName]: ui: inspector: group:` (10)

Gibt die Gruppe an, in welche die Eigenschaft einsortiert wird. Wenn diese nicht angegeben wird, kann die Eigenschaft nicht editiert werden. Die Referenz erfolgt auf den Eintrag im Schlüssel `ui.inspector.groups`

### `properties: [propertyName]: ui: inspector: position:` (10)

Die Reihenfolge des Elements innerhalb der Inspector-Gruppe. Je kleiner die Zahl, desto weiter oben.

### `properties: [propertyName]: ui: inspector: editor:` (10)

Enthält den Namen der (JavaScript) Editor-Klasse, der für die Bearbeitung verwendet wird.

Folgende Werte sind per Default hier möglich (diese werden mit einfachen Ticks notiert - z.B. `editor: 'TYPO3.Neos/Inspector/Editors/BooleanEditor'`):

* `TYPO3.Neos/Inspector/Editors/BooleanEditor` -  Eine Checkbox, für Eigenschaften vom Typ `boolean`
* `TYPO3.Neos/Inspector/Editors/DateTimeEditor` - Ein Datepicker, für Eigenschaften vom Typ `date`
* `TYPO3.Neos/Inspector/Editors/CodeEditor` - Ein HTML-Editor mit Syntax Highlighting
* `TYPO3.Neos/Inspector/Editors/ImageEditor` - Ein Image-Editor, der Cropping und Veränderung der Größe zulässt, für Eigenschaften vom Typ `TYPO3\Media\Domain\Model\ImageVariant`
* `TYPO3.Neos/Inspector/Editors/ReferenceEditor` - Ein Selektor mit Autocomplete auf eine Referenz zu einer anderen Node, für Eigenschaften vom Typ `reference`
* `TYPO3.Neos/Inspector/Editors/ReferencesEditor` - Ein Selektor mit Autocomplete auf mehrere Referenzen zu anderen Nodes, für Eigenschaften vom Typ `references`
* `TYPO3.Neos/Inspector/Editors/SelectBoxEditor` - Ein Selectbox
* `TYPO3.Neos/Inspector/Editors/TextFieldEditor` - Ein Textfeld, für Eigenschaften vom Typ `string` und `integer`

Folgende Editoren werden intern von Neos verwendet:

* `TYPO3.Neos/Inspector/Editors/MasterPluginEditor`
* `TYPO3.Neos/Inspector/Editors/PluginViewEditor`
* `TYPO3.Neos/Inspector/Editors/PluginViewsEditor`

Die Editoren befinden sich im Verzeichnis: `Packages/Application/TYPO3.Neos/Resources/Public/JavaScript/Content/Inspector/Editors/`

#### Eigene Editoren können wie folgt registriert werden:

Dies kann entweder geschehen, indem man einen Namespace für eine Gruppe von Editoren definiert oder aber indem man den Pfad zu einem Editor direkt spezifiziert.

Jeder dataType hat seinesEditor-Set, welche Optionen wie die folgenden haben können:

```
TYPO3:
  Neos:
    userInterface:
      inspector:
        dataTypes:
          'string':
            editor: 'TYPO3.Neos/Editors/TextFieldEditor'
            editorOptions:
              placeholder: 'This is a placeholder'
```

Auf Ebene der Optionen kann dies wie folgt überschrieben werden:

```
TYPO3:
  Neos:
    userInterface:
      inspector:
        properties:
          'string':
            editor: 'My.Package/Editors/TextFieldEditor'
            editorOptions:
              placeholder: 'This is my custom placeholder'
```

Die Registrierung eines Namespaces er auf eine Gruppe von Editoren zeigt, geht folgendermaßen:

* Erstelle einen  Ordner, der die JavaScript-Sourcen der Editoren enthält
* Benennen die Dateien jeweils `PropertyTypeEditor` (anstelle `PropertyType` wird der Name notiert)
* Nun wird der Pfad als **requirejs path mapping** registriert, indem man die folgende `Settings.yaml` verwendet:

```
TYPO3:
  Neos:
    userInterface:
      requireJsPathMapping:
        'My.Package/Inspector/Editors': 'resource://My.Package/Public/Scripts/Path/To/Folder'

```

Nun kann der Editor in der `NodeTypes.yaml` verwendet werden:

```
'My.Package:NodeType':
  properties:
    myProperty:
      type: 'string'
      ui:
        inspector:
          editor: 'My.Package/Inspector/Editors/PropertyTypeEditor'
          editorOptions:
            optionName: 'optionValue'
```

Es ist zudem möglich, bereits Default-Werte in der `Setiings.yaml` zu setzen:

```
TYPO3:
  Neos:
    userInterface:
      inspector:
        editors:
          'My.Package/Inspector/Editors/PropertyTypeEditor':
            editorOptions:
              optionName: 'optionValue'
```

Spezifische Editoren können wie folgt registriert werden:

```
TYPO3:
  Neos:
    userInterface:
      inspector:
        editors:
          'TYPO3.Neos/BooleanEditor':
            path: 'resource://TYPO3.Neos/Public/JavaScript/Content/Inspector/Editors/BooleanEditor'
```

### `properties: [propertyName]: ui: inspector: editorOptions:` (10)


Benannte Editor-Optionen für die jeweiligen Editoren:

#### Optionen für: `TYPO3.Neos/Inspector/Editors/TextFieldEditor`

```
editorOptions:
  placeholder: 'Inherit from parent'
  values:
    '':
      label: ''
    center:
      label: 'Center'
```

#### Optionen für: `TYPO3.Neos/Inspector/Editors/ReferenceEditor`

```
editorOptions:
  nodeTypes:
    - 'Schulung.Person:Person'
```

#### Optionen für: `TYPO3.Neos/Inspector/Editors/CodeEditor`

```
    style:
      type: string
      ui:
        label: 'CSS'
        reloadIfChanged: TRUE
        inspector:
          group: 'code'
          editor: 'TYPO3.Neos/Inspector/Editors/CodeEditor'
          editorOptions:
            buttonLabel: 'Edit CSS source'
            highlightingMode: 'text/css'
```

#### Optionen für: `TYPO3.Neos/Inspector/Editors/ImageEditor`

Hier wird das "Aspekt-Ratio" gesetzt:

```
editorOptions:
  crop:
    aspectRatio:
      options:
        square:
          width: 1
          height: 1
          label: 'Square'
        fourFive:
          width: 4
          height: 5
      enableOriginal: TRUE
      allowCustom: TRUE
      locked:
        width: 0
        height: 0
```

Deaktivierung von Optionen (hier der "square"-Option):

```
Acme.Demo:Image':
  properties:
    image:
      ui:
        inspector:
          editorOptions:
            crop:
              aspectRatio:
                options:
                  square: ~
```

#### Optionen für: `TYPO3.Neos/Inspector/Editors/SelectBoxEditor`

```
editorOptions:
  placeholder: 'Select Background Color'
  values:
    '-4':
      label: 'Four Levels Above Current Page'
    firstChildNode:
      label: 'First child node'
```

Hier ist es seit 1.2.0 auch möglich, die Optionen dynamisch zu ermitteln:

```
'Acme.Demo:FAQ':
  properties:
    questions:
      ui:
        inspector:
          editor: 'Content/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            dataSourceIdentifier: 'questions'
            # alternatively using a custom uri:
            dataSourceUri: 'custom-route/end-point'
```

Hierzu gehört eine Klasse, welche das Interface `TYPO3\\Neos\\Service\\DataSource\\DataSourceInterface` implementiert - idealerweise indem die Klasse `TYPO3\\Neos\\Service\\DataSource\\AbstractDataSource` abgeleitet wird.

Seit Version 1.2.0 werden auch multiple Werte und Gruppierung unterstützt:

```
'Acme.Demo:Test':
  properties:
    multiple: TRUE
    allowEmpty: TRUE
    placeholder: 'Choose'
    values:
      a:
        label: 'A'
        group: 'x'
        icon: 'icon-legal'
      b:
        label: 'B'
        group: 'x'
        icon: 'icon-fire'
```


### `properties: [propertyName]: validation:` (6)

Hier wird eine Liste an Validatoren angegeben, die auf die Eigenschaft angewendet wird. Unterhalb davon werden die Validation-Optionen notiert.

Beispiel:

```
properties:
  headline:
    type: 'string'
    defaultValue: 'My Headline Default'
    ui:
      inlineEditable: TRUE
    validation:
      'TYPO3.Neos/Validation/StringLengthValidator':
        minimum: 1
        maximum: 255
```

Es gibt per Default folgende Validatoren:

* `TYPO3.Neos/Validation/AbstractValidator` - auf diesem abstrakten Validator basieren eigene Validatoren
* `TYPO3.Neos/Validation/AlphanumericValidator` - Optionen: `regularExpression`
* `TYPO3.Neos/Validation/CountValidator` - Optionen: `minimum`, `maximum`
* `TYPO3.Neos/Validation/DateTimeRangeValidator` - Optionen: `latestDate`, `earliestDate`
* `TYPO3.Neos/Validation/DateTimeValidator`
* `TYPO3.Neos/Validation/EmailAddressValidator` - Optionen: `regularExpression`
* `TYPO3.Neos/Validation/FloatValidator`
* `TYPO3.Neos/Validation/IntegerValidator`
* `TYPO3.Neos/Validation/LabelValidator` - Optionen: `regularExpression`
* `TYPO3.Neos/Validation/NumberRangeValidator` - Optionen: `minimum`, `maximum`
* `TYPO3.Neos/Validation/RegularExpressionValidator` - Optionen: `regularExpression`
* `TYPO3.Neos/Validation/StringLengthValidator` - Optionen: `minimum`, `maximum`
* `TYPO3.Neos/Validation/StringValidator`
* `TYPO3.Neos/Validation/TextValidator`
* `TYPO3.Neos/Validation/UuidValidator` - Optionen: `regularExpression`

#### Eigene Validatoren

Man kann eigene Validatoren auf zwei Wegen registrieren. Entweder indem man einen Namespace für eine Gruppe von Validatoren definiert oder aber indem man den Pfad zu einem Validator direkt spezifiziert.

Die Registrierung eines Namespaces der auf eine Gruppe von Validatoren zeigt, geht folgendermaßen:

* Erstelle einen  Ordner, der die JavaScript-Sourcen der Validatoren enthält
* Benennen die Dateien jeweils `DataTypeValidator` (anstelle `DataType` wird der Name notiert)
* Nun wird der Pfad als **requirejs path mapping** registriert, indem man die folgende `Settings.yaml` verwendet:

```
TYPO3:
  Neos:
    userInterface:
      requireJsPathMapping:
        'My.Package/Validation': 'resource://My.Package/Public/Scripts/Path/To/Folder'

```

Nun kann man den Validator für die Eigenschaft in der `NodeTypes.yaml` konfigurieren:

```
'My.Package:NodeType':
  properties:
    myProperty:
      type: 'string'
      validation:
        'My.Package/Validation/DataTypeValidator': []
```

Um lediglich einen spezifischen Validator zu verwenden, kann man in der `Settings.yaml `wie folgt vorgehen:

```
TYPO3:
  Neos:
    userInterface:
      validators:
        'My.Package/Validation/CustomValidator':
          path: 'resource://My.Package/Public/Scripts/Path/To/File/Without/Js/Extension'
```
