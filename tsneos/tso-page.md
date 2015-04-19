# Neos TypoScript: Page

**Beschreibung:** Haupt-Einstiegspunkt um eine Seite zu rendern. Rendert das `<html>` Tag und alles darin enthaltene

**Vollständiger Name:** `TYPO3.Neos:Page`

**TypoScript Definition:** 
```
# TYPO3.Neos:Page is the default object used for rendering in most sites
#
prototype(TYPO3.Neos:Page) >
prototype(TYPO3.Neos:Page) < prototype(TYPO3.TypoScript:Http.Message) {

   doctype = '<!DOCTYPE html>'
   ...
}
```

**Page leitet von TYPO3.TypoScript:Http.Message (und dieses von Array) ab und hat damit auch desses Eigenschaften!**

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/Page.ts2
```

**Eigenschaften:**

| Property | Type | Beschreibung |
| :------- | :------ | :------- |
| `doctype` | string | Der Doctype - Default ist `<!DOCTYPE html>` |
| `htmlTag` | TYPO3.TypoScript:Tag | Der öffnende `<html>` Tag |
| `htmlTag.attributes.*` | array of strings | Attribute die zum `<html>` Tag zugefügt werden |
| `headerComment` | TYPO3.TypoScript:Template | Rendert den Neos-Lizenz Kommentar |
| `headTag` | TYPO3.TypoScript:Tag | Der öffnende `<head>` Tag |
| `head` | TYPO3.TypoScript:Array | Das Markup, welches in den Bereich `<head>` hinzugefügt wird |
| `head.characterSetMetaTag` | TYPO3.TypoScript:Tag | Rendert den `<meta charset="..." />` Tag |
| `head.titleTag` | TYPO3.TypoScript:Tag | Der `<title>` Tag |
| `head.neosBackendHeader` | TYPO3.TypoScript:Template | Lädt vom Neos Backend benötigten Code in den Header |
| `head.javascripts` | TYPO3.TypoScript:Array | Scripte, welche inkludiert werden sollen |
| `head.stylesheets` | TYPO3.TypoScript:Array | Styles, welche inkludiert werden sollen |
| `closingHeadTag` | string | Der schließende `<head>` Tag |
| `body.templatePath` | String | Pfad zum Fluid Template, welches verwendet wird, um den Bereich innerhalb des `<body>` Tags zu rendern |
| `bodyTag` | TYPO3.TypoScript:Tag | Der öffnende `<body>` Tag |
| `bodyTag.attributes.*` | array of strings | Attribute die zum `<body>` Tag zugefügt werden |
| `neosBackendDocumentNodeData` | String | Wird für das Neos-Backend benötigt |
| `body` | TYPO3.TypoScript:Template | HTML-Markup innerhalb des `<body>` Tags |
| `body.node` | Eel | Ermittelt die aktuelle Node und weist diese an `node` zu |
| `body.javascripts` | TYPO3.TypoScript:Array | Skripte, die vor dem schließenden `<body>` Tag inkludiert werden |
| `body.*` | mixed | Da `<body>` per Default durch `TYPO3.TypoScript:Template` definiert wird, können alle Eigenschaften (wie z.B. `sectionName`) hier gesetzt werden |
| `neosBackendContainer` |  TYPO3.TypoScript:Template | Wird vom Neos-Backend benötigt |
| `lastVisitedNodeScript` |  TYPO3.TypoScript:Tag | Wird vom Neos-Backend benötigt. Schreibt ein Script heraus, welches ermöglicht, dass man nach dem Login zur zuletzt besuchten Seite weitergeleitet wird |
| `closingBodyTag` |  string | Der schließende `<body>` Tag |
| `closingHtmlTag` |  string | Der schließende `<html>` Tag |


**Beispiel(e):**

Rendern einer einfachen Website:
```
page = Page
page.body.templatePath = 'resource://My.Package/Private/MyTemplate.html'
// the following line is optional, but recommended for base CSS inclusions etc
page.body.sectionName = 'main'
```

Rendern von Inhalten im Body:
```
page.body {
   sectionName = 'body'
   content.main = PrimaryContent {
      nodePath = 'main'
   }
}

// Fluid
<html>
   <body>
      <f:section name="body">
         <div class="container">
            {content.main -> f:format.raw()}
         </div>
      </f:section>
   </body>
</html>
```

Inkludieren von Stylesheets im Header
```
page.head.stylesheets.mySite = TYPO3.TypoScript:Template {
   templatePath = 'resource://My.Package/Private/MyTemplate.html'
   sectionName = 'stylesheets'
}
```

Body-Attribute hinzufügen:
```
page.bodyTag.attributes.class = 'body-css-class1 body-css-class2'
```

Default-Definition von TYPO3.Neos:Page:
```
# TYPO3.Neos:Page is the default object used for rendering in most sites
#
prototype(TYPO3.Neos:Page) >
prototype(TYPO3.Neos:Page) < prototype(TYPO3.TypoScript:Http.Message) {

   doctype = '<!DOCTYPE html>'
   doctype.@position = 'start 100'

   # Only the opening html tag for the page. This is done to avoid deep nesting of TypoScript paths for integrators.
   htmlTag = TYPO3.TypoScript:Tag {
      @position = 'start'
      tagName = 'html'
      omitClosingTag = TRUE

      attributes {
         version = 'HTML+RDFa 1.1'
         version.@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
         xmlns = 'http://www.w3.org/1999/xhtml'
         xmlns.@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
         xmlns:typo3 = 'http://www.typo3.org/ns/2012/Flow/Packages/Neos/Content/'
         xmlns:typo3.@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
         xmlns:xsd = 'http://www.w3.org/2001/XMLSchema#'
         xmlns:xsd.@if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
      }
   }

   headerComment = TYPO3.TypoScript:Template {
      @position = 'before headTag'
      templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/NeosLicenseHeader.html'
   }

   # The opening head tag for the page. This is done to avoid deep nesting of TypoScript paths for integrators.
   headTag = TYPO3.TypoScript:Tag {
      @position = 'after htmlTag'
      tagName = 'head'
      omitClosingTag = TRUE
   }

   # The content of the head tag, integrators can add their own head content in this array.
   head = TYPO3.TypoScript:Array {
      @position = 'after headTag'

      characterSetMetaTag = TYPO3.TypoScript:Tag {
         @position = 'start 10'
         tagName = 'meta'
         attributes {
            charset = 'UTF-8'
         }
      }

      titleTag = TYPO3.TypoScript:Tag {
         tagName = 'title'
         content = ${q(node).property('title')}
      }

      neosBackendHeader = TYPO3.TypoScript:Template {
         @position = 'end 10000'
         templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/NeosBackendHeaderData.html'
         node = ${node}

         @cache {
            mode = 'uncached'
            context {
               1 = 'node'
            }
         }
         @if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
      }

      neosBackendEndpoints = TYPO3.TypoScript:Template {
         @position = 'end 10001'
         templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/NeosBackendEndpoints.html'
         node = ${node}
         account = ${account}

         @cache {
            mode = 'uncached'
            context {
               1 = 'node'
               2 = 'account'
            }
         }
         @if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
      }

      # Script includes in the head should go here
      javascripts = TYPO3.TypoScript:Array

      # Link tags for stylesheets in the head should go here
      stylesheets = TYPO3.TypoScript:Array
   }

   closingHeadTag = '</head>'
   closingHeadTag.@position = 'after head'

   # The opening body tag for the page. This is done to avoid deep nesting of TypoScript paths for integrators.
   bodyTag = TYPO3.TypoScript:Tag {
      @position = '20'
      tagName = 'body'
      omitClosingTag = TRUE
   }

   # Required for the backend to work.
   neosBackendDocumentNodeData = TYPO3.Neos:DocumentMetadata {
      @position = 'before body'
      @if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
   }

   # Content of the body tag. To be defined by the integrator.
   body = TYPO3.TypoScript:Template {
      @position = 'after bodyTag'
      node = ${node}
      site = ${site}

      # Script includes before the closing body tag should go here
      javascripts = TYPO3.TypoScript:Array
      # This processor appends the rendered javascripts Array to the rendered template
      @process.appendJavaScripts = ${value + this.javascripts}
   }

   # Required for the backend to work.
   neosBackendContainer = TYPO3.TypoScript:Template {
      @position = 'before closingBodyTag'
      templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/NeosBackendContainer.html'
      node = ${node}

      @cache {
         mode = 'uncached'
         context {
            1 = 'node'
         }
      }
      @if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
   }

   # This enables redirecting to the last visited page after login
   lastVisitedNodeScript = TYPO3.TypoScript:Tag {
      @position = 'before closingBodyTag'

      tagName = 'script'
      attributes {
         data-neos-node = ${q(node).property('_identifier')}
         src = TYPO3.TypoScript:ResourceUri {
            path = 'resource://TYPO3.Neos/Public/JavaScript/LastVisitedNode.js'
         }
      }
   }

   neosBackendFooter = TYPO3.TypoScript:Template {
      @position = 'after lastVisitedNodeScript 10000'
      templatePath = 'resource://TYPO3.Neos/Private/Templates/TypoScriptObjects/NeosBackendFooterData.html'
      node = ${node}
      @if.onlyRenderWhenNotInLiveWorkspace = ${node.context.workspace.name != 'live'}
   }

   closingBodyTag = '</body>'
   closingBodyTag.@position = 'end 100'

   closingHtmlTag = '</html>'
   closingHtmlTag.@position = 'end 200'


   @cache {
      mode = 'cached'
      entryIdentifier {
         documentNode = ${node}
         domain = ${site.context.currentDomain}
      }
      entryTags {
         1 = ${'Node_' + node.identifier}
      }
   }

   @exceptionHandler = 'TYPO3\\Neos\\TypoScript\\ExceptionHandlers\\PageHandler'
}


```