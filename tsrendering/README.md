# TypoScript Rendering

Sämtliche Ausgaben in TYPO3 Neos werden durch TypoScript gerendert.

Durch die Datei `Packages/Application/TYPO3.Neos/Configuration/Settings.yaml` wird definiert, dass die TypoScript-Root-Definitionen der Packages `TYPO3.TypoScript` und `TYPO3.Neos` geladen werden.

```
TYPO3:
  Neos:
    typoScript:
      autoInclude:
        'TYPO3.TypoScript': TRUE
        'TYPO3.Neos': TRUE
```

## 1 - Root-Definition in TYPO3.TypoScript

Zuerst wird die folgende Datei ausgewertet:

```
Packages/Application/TYPO3.TypoScript/Resources/Private/TypoScript/Root.ts2
```

Dort enthalten sind vor allem die Basis-Prototypen:

* [Array](../tsbasics/tso-array.md) (Rendert verschachtelte TypoScript Objekte und fügt deren Ausgabe als String zusammen)
* [RawArray](../tsbasics/tso-rawarray.md) (Baut ein Array auf und gibt es als solches auch wieder zurück)
* [Template](../tsbasics/tso-template.md) (Rendert ein Fluid-Template, welches durch templatePath angegeben ist)
* [Collection](../tsbasics/tso-collection.md) (Iteriert über eine Collection aus Objekten und rendert jedes Element mit Hilfe eines itemRenderer)
* [Case](../tsbasics/tso-case.md) (Verhält sich wie PHP’s switch/case Befehl)
* [Matcher](../tsbasics/tso-matcher.md) (Stellt einen Fall im Case dar)
* [Value](../tsbasics/tso-value.md) (TypoScript Objekt-Wrapper für Werte)
* [Http.ResponseHead](../tsbasics/tso-httpresponsehead.md) (Generiert einen Standard HTTP Response Header)
* [Http.Message](../tsbasics/tso-httpresponsehead.md) (Anwendung des Http.ResponseHead)
* [Attributes](../tsbasics/tso-attributes.md) (Wird verwendet, um HTML-Tag Attribute zu rendern)
* [Tag](../tsbasics/tso-tag.md) (Rendern von HTML-Tags mit Attributen und zusätzlichem Inhalt)
* [UriBuilder](../tsbasics/tso-uribuilder.md) (Rendert eine URL die auf eine(n) Controller/Action zeigt)
* [ResourceUri](../tsbasics/tso-resource.md) (Rendert Resource URIs) 

## 2 - Root-Definition in TYPO3.Neos

Dann wird die folgende Datei ausgewertet:

```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Root.ts2
```

Hier werden zwei weitere Dateien inkludiert:

```
include: resource://TYPO3.Neos/Private/TypoScript/DefaultTypoScript.ts2
include: resource://TYPO3.Neos/Private/TypoScript/RawContentMode.ts2
```

### 2a - DefaultTypoScript.ts2 ###

In dieser Datei werden alle Neos-Prototypen definiert:

* [ContentCase](../tsneos/tso-contentcase.md) (Rendert eine Content-Node, bei NodeType Name Gleichheit)
* [Document](../tsneos/tso-document.md) (Basis-Document innerhalb von Neos)
* [Content](../tsneos/tso-content.md) (Alle Content-Elemente leiten von diesem Basis Objekt ab)
* [PrimaryContent](../tsneos/tso-primarycontent.md) (Rendering des Haupt-Inhalts)
* [ContentCollection](../tsneos/tso-contentcollection.md) (Container für Content-Elemente)
* [Page](../tsneos/tso-page.md) (Default-Objekt für eine Seite)
* [Shortcut](../tsneos/tso-shortcut.md) (Leitet auf eine andere Seite weiter)
* [BreadcrumbMenu](../tsneos/tso-breadcrumb.md) (Realisiert ein Breadcrumb-Menü)
* [DimensionMenu](../tsneos/tso-dimensionmenu.md) (Realisiert ein Dimension-Menü)
* [Menu](../tsneos/tso-menu.md) (Realisiert ein Menü)
* [Plugin](../tsneos/tso-plugin.md) (Rendert eine Action eines Controllers)
* [PluginView](../tsneos/tso-pluginview.md) (Rendert einen View eines Plugins)
* [ConvertNodeUris](../tsneos/tso-converturis.md) (Wandelt Node-Referenzen in URIs um)
* [DocumentMetadata](../tsneos/tso-documentmetadata.md) (Rendert einen Meta-Tag mit Attributen)
* [ContentElementWrapping](../tsneos/tso-contentelementwrapping.md) (Wrappt Content-Elemente mit Metadaten wie Klassen und IDs)
* [NodeUri](../tsneos/tso-nodeuri.md) (Erstellt einen Link zu einer Node)
* [ImageUri](../tsneos/tso-imageuri.md) (Erzeugt ein Image-Tag bzw. eine Image-URI)

Zusätzlich wird hier das Root-Element `root` definiert, welches für das *Grundrendering* verantwortlich ist:

```
# The root matcher used to start rendering in Neos
#
# The default is to use a render path of "page", unless the requested format is not "html"
# in which case the format string will be used as the render path (with dots replaced by slashes)
#
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

	@cache {
		mode = 'cached'

		entryIdentifier {
			node = ${node}
			editPreviewMode = ${editPreviewMode}
			format = ${request.format}
			domain = ${site.context.currentDomain}
		}

		entryTags {
			# Whenever the node changes the matched condition could change
			1 = ${'Node_' + documentNode.identifier}
			# Whenever one of the parent nodes changes the layout could change
			2 = ${'DescendantOf_' + documentNode.identifier}
		}
	}

	# Catch all unhandled exceptions at the root
	@exceptionHandler = 'TYPO3\\Neos\\TypoScript\\ExceptionHandlers\\PageHandler'
}
```

Fehlt diese Konfiguration, kommt es zu folgender Fehlermeldung:

```
Exception while rendering
root:
No "root" TypoScript object found. Please make sure to define one in your TypoScript configuration. (20140413133335b575f8)
```

Dies liegt daran, dass in der Datei `Packages/Application/TYPO3.Neos/Classes/TYPO3/Neos/View/TypoScriptView.php` die Eigenschaft `$typoScriptPath` auf `root` gesetzt wurde.

Ganz unten in der Konfiguration ist zudem zu sehen, dass - wenn keine andere Option eingestellt ist - der "default" Fall aufgerufen wird, der wiederum den TypoScript Pfad `/page` erwartet - d.h. ein:

```
page = ...
```

Ruft man nämlich ein leeres TYPO3 Neos auf, so erhält man folgenden Fehlermeldung:

```
Exception while rendering
page:
No "page" TypoScript object found. Please make sure to define one in your TypoScript configuration. (201404080756282adc80)
```

### 2b - RawContentMode.ts2 ###

Hier wird vor allem das TypoScript Objekt `rawContent = Page` aufgebaut, welches zur Darstellung des Raw-Content-Modes im Backend verwendet wird. Die Definition dafür (dass beispielsweise `rawContent` als typoScriptRenderingPath verwendet wird), steht in der Datei `Packages/Application/TYPO3.Neos/Configuration/Settings.yaml`

```
TYPO3:
  Neos:
    userInterface:
      editPreviewModes:
        rawContent:
          isEditingMode: TRUE
          isPreviewMode: FALSE
          typoScriptRenderingPath: 'rawContent'
          title: 'Raw Content'
          position: 200
```

Geladen wird folgender TypoScript Code:

```
prototype(TYPO3.Neos:RawContent) >
prototype(TYPO3.Neos:RawContent) < prototype(TYPO3.TypoScript:Template) {
	templatePath = 'resource://TYPO3.Neos/Private/Templates/RawContentMode/TypoScriptObjects/GeneralContentCollectionRendering.html'
	columns = TYPO3.TypoScript:Collection {
		collection = ${q(node).children('[instanceof TYPO3.Neos:ContentCollection]')}
		itemName = 'node'
		itemRenderer = TYPO3.TypoScript:Template {
			templatePath = 'resource://TYPO3.Neos/Private/Templates/RawContentMode/TypoScriptObjects/ContentCollectionTemplate.html'
			node = ${node}
			attributes = TYPO3.TypoScript:Attributes {
				class = 'column'
			}
			columnContent = TYPO3.Neos:ContentCollection {
				nodePath = '.'
			}

		}
	}
}

rawContent = TYPO3.Neos:Page {
	head {
		stylesheets = TYPO3.TypoScript:Template {
			templatePath = 'resource://TYPO3.Neos/Private/Templates/RawContentMode/Page/Default.html'
			sectionName = 'headerIncludes'
		}
	}

	bodyTag.attributes.class = 'neos-raw-content-mode'

	body {
		templatePath = 'resource://TYPO3.Neos/Private/Templates/RawContentMode/Page/Default.html'
		sectionName = 'body'

		allContentCollections = TYPO3.Neos:PrimaryContent {
			nodePath = '.'
			default.type = 'TYPO3.Neos:RawContent'
		}
	}
}
```

### 3 - TypoScript in TYPO3.Neos.NodeTypes ###

NodeTypes sind Elemente, die im Backend eingefügt werden können, also z.B. Headlines, Images, Content-Referenzen, MultiColumn, Menu, ...

Da in der Datei `Packages/Application/TYPO3.Neos.NodeTypes/Configuration/Settings.yaml` eine entsprechende Konfiguration vorhanden ist, wird die Datei `Packages/Application/TYPO3.Neos.NodeTypes/Resources/Private/TypoScript/Root.ts2` geladen.

```
TYPO3:
  Neos:
    typoScript:
      autoInclude:
        'TYPO3.Neos.NodeTypes': TRUE
```

Geladen wird folgende Datei:

* [NodeTypes TypoScript](../tsneosnodetypes/tsnn-ts.md)

Dort enthalten sie die folgenden Objekte:

* [NodeTypes Menu](../tsneosnodetypes/tsnn-menu.md) (Menü-Objekt)
* [NodeTypes Headline](../tsneosnodetypes/tsnn-headline.md) (Headline-Objekt)
* [NodeTypes Image](../tsneosnodetypes/tsnn-image.md) (Image-Objekt)
* [NodeTypes Text](../tsneosnodetypes/tsnn-text.md) (Text-Objekt)
* [NodeTypes TextWithImage](../tsneosnodetypes/tsnn-textimage.md) (TextMitBild-Objekt)
* [NodeTypes MultiColumn](../tsneosnodetypes/tsnn-multicolumn.md) (Mehrspalter-Objekt)
* [NodeTypes MultiColumnItem](../tsneosnodetypes/tsnn-multicolumnitem.md) (Mehrspalter-Einzel-Objekt)
* [NodeTypes Form](../tsneosnodetypes/tsnn-form.md) (Formular-Objekt)
* [NodeTypes AssetList](../tsneosnodetypes/tsnn-assetlist.md) (Asset-Listen-Objekt)
* [NodeTypes ContentReferences](../tsneosnodetypes/tsnn-contentrefereces.md) (Content-Reference-Objekt)
* [NodeTypes Html](../tsneosnodetypes/tsnn-html.md) (HTML-Objekt)

### 4 - TypoScript der Website ###

Das TypoScript der Website wird automatisch inkludiert, wenn es sich an folgenden Aufbau hält:

```
resource://MyVendor.MySite/Private/TypoScripts/Root.ts2
```

### 5 - TypoScript des Package ###

Das TypoScript eines Packages wird automatisch inkludiert, wenn es sich an folgenden Aufbau hält:

```
resource://MyVendor.MyPackage/Private/TypoScript/Root.ts2
```
