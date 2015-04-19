# Content


## Content-Marker

Um grundsätzlich Content auf der Seite einzufügen, verwenden wir das Objekt `PrimaryContent`. Dieses können wir in der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2` referenzieren:

```
...
footer {
  ...
}
content {
  main = PrimaryContent {
    nodePath = 'main'
  }
}
...
```

Anschließend müssen wir das Template entsprechend anpassen. Folgenden Code nehmen wir dazu raus und ersetzen ihn entsprechend:

```
<section class="white centered">
  <div class="container">
    <div class="row">
      <div class="col-md-4 col-sm-12">
        <span class="icon-headphones type-icon"></span>
        <h2>Trendy brazil choc</h2>
        <p>Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. </p>
        <p><a class="btn btn-default" href="#">All Brazil Choc details</a></p>
      </div>
      <div class="col-md-4 col-sm-12">
        <span class="icon-pacman type-icon"></span>
        <h2>Smokey ecuadorian</h2>
        <p>In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus.</p>
        <p><a class="btn btn-default" href="#">Find out details about Ecuadorian</a></p>
      </div>
      <div class="col-md-4 col-sm-12">
        <span class="icon-user type-icon"></span>
        <h2>The well known one</h2>
        <p>Etiam rhoncus. Maecenas tempus, tellus eget condimentum rhoncus, sem quam semper libero, sit amet adipiscing sem neque sed ipsum. Nam quam nunc, blandit vel, luctus pulvinar, hendrerit id, lorem.</p>
        <p><a class="btn btn-default" href="#">More about Well Known</a></p>
      </div>
    </div>
  </div>
</section>

<section class="beige-bg centered border-top">
  <div class="container">
    <div class="row">
      <div class="col-sm-6">
        <span class="icon-lab type-icon"></span>
        <h2>Homey Blend</h2>
        <p>Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu.</p>
        <p><a class="btn btn-default" href="#">Find out about our homemade blend</a></p>
      </div>
      <div class="col-sm-6">
        <span class="icon-leaf type-icon"></span>
        <h2>Specialtea</h2>
        <p>Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Maecenas nec odio et ante tincidunt tempus. Donec vitae sapien ut libero venenatis faucibus.</p>
        <p><a class="btn btn-default" href="#">Details about our one tea leaf</a></p>
      </div>
    </div>
  </div>
</section>

<section class="white no-padding">
  <div id="carousel-example-generic" class="carousel slide" data-ride="carousel">

    <div class="carousel-inner">
      <div class="item active">
        <a href="BlogArticle1.html">
          <img src="../Images/blogarticle-1-big.jpg" alt="">
          <div class="carousel-caption">
            <h3>A first blog article</h3>
          </div>
        </a>
      </div>
      <div class="item">
        <a href="BlogArticle2.html">
          <img src="../Images/blogarticle-2-big.jpg" alt="">
          <div class="carousel-caption">
            <h3>Yet another blog article</h3>
          </div>
        </a>
      </div>
    </div>

    <a class="left carousel-control" href="#carousel-example-generic" data-slide="prev">
      <span class="glyphicon glyphicon-chevron-left"></span>
    </a>
    <a class="right carousel-control" href="#carousel-example-generic" data-slide="next">
      <span class="glyphicon glyphicon-chevron-right"></span>
    </a>
  </div>
</section>
```

Wir ersetzen den obigen Code mit dem folgenden:

```
{content.main -> f:format.raw()}
```

## Content-Element: Headline, Subheadline, Text

```
'Vendor:YourContentElementName':
  superTypes:
    - 'TYPO3.Neos:Content'
  ui:
    label: 'My first custom content element'
    group: 'general'
  properties:
    headline:
      type: string
      defaultValue: 'Replace by your headline value ...'
      ui:
        label: 'Headline'
        inlineEditable: TRUE
    subheadline:
      type: string
      defaultValue: 'Replace by your subheadline value ...'
      ui:
        label: 'Subheadline'
        inlineEditable: TRUE
    text:
      type: string
      ui:
        label: 'Text'
        reloadIfChanged: TRUE
```

```
prototype(Vendor:YourContentElementName) < prototype(TYPO3.Neos:Content) {
        templatePath = 'resource://Vendor.Site/Private/Templates/TypoScriptObjects/YourContentElementName.html'

        headline = ${q(node).property('headline')}
        subheadline = ${q(node).property('subheadline')}
        text = ${q(node).property('text')}
}
```

```
{namespace neos=TYPO3\Neos\ViewHelpers}
<article>
        <header>
                {neos:contentElement.editable(property: 'headline', tag: 'h2')}
                {neos:contentElement.editable(property: 'subheadline', tag: 'h3')}
        </header>
        <div>
                {neos:contentElement.editable(property: 'text')}
        </div>
</article>
```

## Content-Element: Youtube

Wir bennötigen zuerst eine NodeType Definition für das Element:

```
'Acme.Demo:YouTube':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    group: 'general'
    label: 'YouTube Video'
    inspector:
      groups:
        video:
          label: 'Video'
  properties:
    videoUrl:
      type: string
      ui:
        label: 'Video URL'
        reloadIfChanged: TRUE
        inspector:
          group: 'video'
```

Nun eine Erweiterung des TypoScripts:

```
prototype(Schulung.Website:YouTube) < prototype(TYPO3.Neos:Content) {
        templatePath = 'resource://Acme.Demo/Private/Templates/TypoScriptObjects/YouTube.html'
        videoUrl = ${q(node).property('videoUrl')}
        width = '640'
        height = '360'
}
```

Schließlich das Template:

```
<iframe width="{width}" height="{height}" src="{videoUrl}" frameborder="0" allowfullscreen></iframe>
```

Zudem ist auch eine manuelle Einbindung möglich:

```
page.body.parts.teaserVideo = Schulung.Website:YouTube {
  videoUrl = 'http://youtube.com/.....'
}
```

## Content-Element: Quote

Für das Zitat-Element müssen wir die Datei `Packages/Sites/Schulung.Website/Configuration/NodeTypes.yaml` erweitern:

```
'Schulung.Website:Quote':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Zitat'
    inspector:
       groups:
         quoteproperties:
           label: 'Zitat Optionen'
           position: 5
    icon: 'icon-file-text'
  properties:
    blockquote:
      type: string
      ui:
        label: 'Zitat'
        inlineEditable: TRUE
        reloadIfChanged: TRUE
    sourcetitle:
      type: string
      defaultValue: 'Titel der Zitat-Quelle'
      ui:
        label: 'Titel der Zitat-Quelle'
        inspector:
          group: 'quoteproperties'
        reloadIfChanged: TRUE
```

Nun kann das Element bereits eingefügt werden. TYPO3 Neos erwartet nun per Default ein Template an der Stelle `Packages/Sites/Schulung.Website/Private/Templates/NodeTypes/Quote.html`, um das Element zu rendern. Wir werden dies im TypoScript überschreiben.

Dazu fügen wir folgenden Code an das Ende der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2` ein:

```
# Quote TypoScript Object
prototype(Schulung.Website:Quote) < prototype(TYPO3.Neos:Content) {
   templatePath = 'resource://Schulung.Website/Private/Templates/TypoScriptObjects/Quote.html'
   blockquote = ${q(node).property('blockquote')}
   sourceurl = ${q(node).property('sourceurl')}
   sourcetitle = ${q(node).property('sourcetitle')}
}
```

Nun müssen wir ein Verzeichnis `TypoScriptObjects` innerhalb von `Packages/Site/Schulung.Website/Private/Templates/` an (sofern noch nicht vorhanden) und legen dorthinein eine Datei `Quote.html` mit folgendem Inhalt:

```
{namespace t=TYPO3\Neos\ViewHelpers}
<t:contentElement node="{node}">
    <blockquote cite="{f:uri.external(uri: '{sourceurl}', defaultScheme: 'http')}">
        <t:contentElement.editable property="blockquote">
            {blockquote}
        </t:contentElement.editable>
    </blockquote>
    <f:if condition="{sourceurl}">
        <f:then>
            <f:link.external uri="{sourceurl}" defaultScheme="http">{sourcetitle}</f:link.external>
        </f:then>
        <f:else>
            {sourcetitle}
       </f:else>
    </f:if>
</t:contentElement>
```

Zur optimalen Darstellung benötigen wir nun noch ein Stylesheet.
Legen wir dazu also eine Datei `Quote.css` im Verzeichnis `Packages/Sites/Schulung.Website/Resources/Public/Css/` mit dem folgenden Inhalt an:

```
blockquote {
    background: #f9f9f9;
    border-left: 10px solid #ccc;
    margin: 1.5em 10px;
    padding: .5em 10px;
    quotes:"\201C""\201D""\2018""\2019";
}
blockquote:before {
    color:#ccc;
    content:open-quote;
    font-size:4em;
    line-height:.1em;
    margin-right:.25em;
    vertical-align:-.4em;
}
blockquote p {
    display:inline;
}
```

Nun müssen wir das Stylesheet noch entsprechend einbinden:

```
...
<f:section name="stylesheets">
  ...
  <link rel="stylesheet" href="{f:uri.resource(path: 'Css/Quote.css', package: 'Schulung.Website')}" media="all" />
</f:section>
...
```

## Video-Grid-Element

```
'Acme.Demo:VideoGrid':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    group: 'structure'
    label: 'Video Grid'
  childNodes:
    video0:
      type: 'Acme.Demo:YouTube'
    video1:
      type: 'Acme.Demo:YouTube'
    text0:
      type: 'TYPO3.Neos.NodeTypes:Text'
    text1:
      type: 'TYPO3.Neos.NodeTypes:Text'
```

```
prototype(Acme.Demo:VideoGrid) {
  // templatePath = 'resource://Acme.Demo/Private/Templates/TypoScriptObjects/VideoGrid.html'

  videoRenderer = Acme.Demo:YouTube
  textRenderer = TYPO3.Neos.NodeTypes:Text

  video0 = ${q(node).children('video0').get(0)}
  video1 = ${q(node).children('video1').get(0)}

  text0 = ${q(node).children('text0').get(0)}
  text1 = ${q(node).children('text1').get(0)}
}
```

```
{namespace ts=TYPO3\TypoScript\ViewHelpers}
<ts:render path="videoRenderer" context="{node: video0}" />
<ts:render path="textRenderer" context="{node: text0}" />
<br />
<ts:render path="videoRenderer" context="{node: video1}" />
<ts:render path="textRenderer" context="{node: text1}" />
```



## Content-Strukturelement: Content-Section

Wenn wir den Inhalt analysieren, den wir vorhin ersetzt haben, fällt uns bei allen drei Abschnitten der folgende Aufbau auf:

```
<section class="white centered">
  <div class="container">
  ...
  </div>
</section>
```

Lediglich die Attribute in der `class` Eigenschaft der `section` ändert sich. Möglich ist hier z.B.

* `white centered`
* `beige-bg centered border-top`
* `white no-padding`

Wir wollen diesen Container nun über ein Inhaltselement realisieren. Dafür fügen wir folgenden Code in die Datei `sPackages/Sites/Schulung.Website/Configuration/NodeTypes.yaml` ein:


```
'Schulung.Website:Section':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Content Section!'
    icon: 'icon-columns'
    inlineEditable: true
    inspector:
      groups:
        style:
          label: 'Style'
          position: 10
  childNodes:
    content:
      type: 'TYPO3.Neos:ContentCollection'
  properties:
    background:
      type: string
      defaultValue: 'white'
      ui:
        label: 'Background Color'
        reloadIfChanged: true
        inspector:
          group: style
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            placeholder: 'Select Background Color'
            values:
              'white':
                label: 'White'
              'beige-bg':
                label: 'Beige'
              'brown-bg':
                label: 'Brown'
    border:
      type: string
      defaultValue: ''
      ui:
        label: 'Border'
        reloadIfChanged: true
        inspector:
          group: style
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            placeholder: 'Select Borders'
            values:
              '':
                label: 'No Border'
              'border-top':
                label: 'Border Top'
              'border-top-simple':
                label: 'Simple Border Top'
    centered:
      type: boolean
      ui:
        label: 'Center?'
        reloadIfChanged: true
        inspector:
          group: style
    nopadding:
      type: boolean
      ui:
        label: 'No Padding?'
        reloadIfChanged: true
        inspector:
          group: style
```

Nun legen wir die Datei `Sites/Schulung.Website/Resources/Private/Templates/NodeTypes/Section.html` mit dem folgenden Inhalt an:

```
<section class="{background} {f:if(condition:centered, then: 'centered')} {border} {f:if(condition:nopadding, then: 'no-padding')}">
    <div class="container">
        {content -> f:format.raw()}
    </div>
</section>
```

Nun müssen wir noch die TypoScript-Definition erweitern - dies geschieht in der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2`:

```
prototype(Schulung.Website:Section) {
  content = TYPO3.Neos:ContentCollection {
    nodePath = 'content'
  }
}
```

## Content-Element: Two Column

Wenn wir uns den vorhin entfernten Code wieder anschauen, stellen wir fest, dass es ein zweispaltiges Elemente gab, mit dem folgenden Aufbau:

```
<div class="row">
  <div class="col-sm-6">
  ...
  </div>
  <div class="col-sm-6">
  ...
  </div>
</div>

```

Dies müssen wir nun als nächstes realisieren. Dafür schreiben wir die Objekt `MultiColumn` und `MultiColumnItem` um. Diese inkludieren wir grundsätzlich in der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2`:


```
include: resource://Schulung.Meta/Private/TypoScript/Root.ts2
include: NodeTypes/MultiColumn.ts2
include: NodeTypes/MultiColumnItem.ts2

namespace: TS=TYPO3.TypoScript
...
```

Um die beiden Dateien zu hosten, legen wir ein Verzeichnis `NodeTypes` innerhalb von `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/` an und erstellen dort die Dateien `MultiColumn.ts2` und `MultiColumnItem.ts2`:

```
##
# Adjust "MultiColumn" element to Twitter bootstrap CSS classes
#
prototype(TYPO3.Neos.NodeTypes:MultiColumn) {
  attributes.class = 'row'
  columns.iterationName = 'multiColumnIteration'
}
```

```
##
# Adjust "MultiColumnItem" element to Twitter bootstrap CSS classes
#
prototype(TYPO3.Neos.NodeTypes:MultiColumnItem) {
  attributes.class = ${'col-sm-' + String.split(q(node).parent().property('layout'), '-')[multiColumnIteration.index]}
}

```

Nun fehlt noch die NodeType-Defintion in der Datei `Packages/Sites/Schulung.Website/Configuration/NodeTypes.yaml`:

```
##
# Adjust the "TwoColumn" node type:
# Disable some of the layout options, override labels and set the default layout
#
'TYPO3.Neos.NodeTypes:TwoColumn':
  properties:
    'layout':
      defaultValue: '6-6'
      ui:
        inspector:
          editorOptions:
            values:
              '50-50': ~
              '75-25': ~
              '25-75': ~
              '66-33': ~
              '33-66': ~
              '6-6':
                label: '50% / 50%'
              '8-4':
                label: '66% / 33%'
              '4-8':
                label: '33% / 66%'
```

## Content-Element: Teaser

Jetzt, wo wir ein zweispaltiges Element haben, können wir darauf die Teaser platzieren.

Der Teaser selbst ist wieder ein NodeType, den wir in der Datei `Packages/Sites/Schulung.Website/Configuration/NodeTypes.yaml` anlegen:

```
'Schulung.Website:Teaser':
  superTypes: ['TYPO3.Neos.NodeTypes:Headline', 'TYPO3.Neos.NodeTypes:Text']
  ui:
    label: 'Teaser'
    icon: 'icon-file-text'
    inspector:
      groups:
        style:
          label: 'Style'
          position: 10
  properties:
    title:
      defaultValue: '<h2>Enter headline here</h2>'
      ui:
        aloha:
          format:
            h1: FALSE
            h4: TRUE
            h5: TRUE
            h6: TRUE
    icon:
      type: string
      defaultValue: ''
      ui:
        label: 'Icon'
        reloadIfChanged: true
        inspector:
          group: style
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            placeholder: 'Select Icon'
            values:
              '':
                label: ''
              'icon-pacman':
                label: 'PACMAN!'
              'icon-user':
                label: 'User'
              'icon-headphones':
                label: 'Headphones'
    linktext:
      type: string
      defaultValue: 'Link here'
      ui:
        inlineEditable: true
    link:
      type: reference
      ui:
        label: 'Link Target'
        inspector:
          group: style
```

Nun benötigen wir noch ein entsprechendes HTML-Template, welches wir als Datei `Packages/Sites/Schulung.Website/Resources/Private/Templates/NodeTypes/Teaser.html` anlegen und mit folgendem Inhalt füllen:

```
{namespace neos=TYPO3\Neos\ViewHelpers}
<div>
  <span class="{icon} type-icon"></span>
  {neos:contentElement.editable(property: 'title')}

  {neos:contentElement.editable(property: 'text')}
  <f:if condition="{link}">
    <p><neos:link.node node="{link}" class="btn btn-default">{neos:contentElement.editable(property: 'linktext', tag: 'span')}</neos:link.node></p>
  </f:if>
</div>
```


## Content-Element: Three Column:

Analog zum Zweispalter können wir auch einen Drei-Spalter konzipieren. Basis ist erneut die Datei `Packages/Sites/Schulung.Website/Configuration/NodeTypes.yaml`:

```
##
# Adjust the "ThreeColumn" node type:
# Disable some of the layout options, override labels and set the default layout
#
'TYPO3.Neos.NodeTypes:ThreeColumn':
  properties:
    'layout':
      defaultValue: '4-4-4'
      ui:
        inspector:
          editorOptions:
            values:
              '33-33-33': ~
              '50-25-25': ~
              '25-50-25': ~
              '25-25-50': ~
              '4-4-4':
                label: '33% / 33% / 33%'
              '6-3-3':
                label: '50% / 25% / 25%'
              '3-6-3':
                label: '25% / 50% / 25%'
              '3-3-6':
                label: '25% / 25% / 50%'
```

## Content-Element: Carousel

Wir wollen nun als nächstes ein Carousel-Element erstellen, welches Images-Nodes rendert, die per JavaScript animiert werden. Auch hier starten wir in der Datei `NodeTypes.html`:

```
##
# A "Carousel" content element that renders "Image" child nodes into a JavaScript based slideshow
#
'Schulung.Website:Carousel':
  superTypes: ['TYPO3.Neos:Content']
  childNodes:
    carouselItems:
      type: 'TYPO3.Neos:ContentCollection'
  ui:
    label: 'Carousel'
    group: 'plugins'
    icon: 'icon-picture'
    inlineEditable: TRUE
```

In der Datei `Packages/Sites/Schulung.Website/Resources/Private/TypoScripts/Library/Root.ts2` müssen wir nun die entsprechende TypoScript-Definition hinzufügen:

```
##
# "Carousel" element
#
prototype(Schulung.Website:Carousel) {
  carouselitems = TYPO3.Neos:ContentCollection {
    nodePath = 'carouselitems'
    iterationName = 'carouselitemsIteration'
    attributes.class = 'carousel-inner'
  }

  carouselitemArray = ${q(node).children('carouselitems').children('[instanceof TYPO3.Neos.NodeTypes:Image]')}

  // Enhance image prototype for the carousel
  prototype(TYPO3.Neos.NodeTypes:Image) {
    // Render images in the carousel with a special template.
    templatePath = 'resource://Schulung.Website/Private/Templates/TypoScriptObjects/Carouselitem.html'

    attributes.class = ${'item' + (carouselIitemsIteration.isFirst ? ' active' : '')}

    // We want to use the item iterator in the template so we have to store it in ts.
    iteration = ${carouselitemsIteration}
  }
}
```

Das Haupt-Template wiederum platzieren wir hier: `Packages/Sites/Schulung.Website/Resources/Private/Templates/NodeTypes/Carousel.html` :

```
{namespace neos=TYPO3\Neos\ViewHelpers}
{namespace ts=TYPO3\TypoScript\ViewHelpers}
<div{attributes -> f:format.raw()}>
  <div class="carousel slide" id="c{node.identifier}">
    <!-- Indicators -->
    <ol class="carousel-indicators">
      <f:for each="{carouselitemArray}" as="item" iteration="itemIterator">
        <li data-target="#c{node.identifier}" data-slide-to="{itemIterator.index}" class="{f:if(condition: itemIterator.isFirst, then: 'active')}"></li>
      </f:for>
    </ol>

    <!-- Wrapper for slides -->
    {carouselItems -> f:format.raw()}

    <!-- Controls -->
    <a class="left carousel-control" href="#c{node.identifier}" data-slide="prev">
      <span class="icon-prev"></span>
    </a>
    <a class="right carousel-control" href="#c{node.identifier}" data-slide="next">
      <span class="icon-next"></span>
    </a>
  </div>
</div>
```

Schließlich wird noch ein Template benötigt um die Image-Items zu rendern, für das wir die Datei `CarouselItem.html` im Verzeichnis `Packages/Sites/Schulung.Website/Private/Templates/TypoScriptObjects/` anlegen:

```
{namespace neos=TYPO3\Neos\ViewHelpers}
{namespace media=TYPO3\Media\ViewHelpers}
<div{attributes -> f:format.raw()}>
  <f:if condition="{image}">
    <f:then>
      <media:image image="{image}" alt="{alternativeText}" title="{title}" maximumWidth="{maximumWidth}" maximumHeight="{maximumHeight}" />
    </f:then>
    <f:else>
      <img src="{f:uri.resource(package: 'TYPO3.Neos', path: 'Images/dummy-image.png')}" title="Dummy image" alt="Dummy image" />
    </f:else>
  </f:if>
  <div class="carousel-caption">
    <f:if condition="{hasCaption}">
      {neos:contentElement.editable(property: 'caption')}
    </f:if>
  </div>
</div>
```

