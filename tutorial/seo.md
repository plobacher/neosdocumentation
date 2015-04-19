# SEO

Zunächst wird eine Datei `Configuration/NodeTypes.Mixins.yaml` benötigt:

```
#
# SEO <meta> tags mixins
#
'Schulung.Website:SeoMetaTagsMixin':
  abstract: TRUE
  ui:
    inspector:
      groups:
        seometa:
          label: 'Meta Tags'
          position: 100
          tab: seo
  properties:
    metaDescription:
      type: string
      ui:
        label: 'Description'
        inspector:
          group: 'seometa'
          position: 10
          editor: 'TYPO3.Neos/Inspector/Editors/TextAreaEditor'
          editorOptions:
            placeholder: 'max. 156 characters'
      validation:
        'TYPO3.Neos/Validation/StringLengthValidator':
          maximum: 156
    metaKeywords:
      type: string
      ui:
        label: 'Keywords'
        inspector:
          group: 'seometa'
          position: 20
          editor: 'TYPO3.Neos/Inspector/Editors/TextAreaEditor'
          editorOptions:
            placeholder: 'comma separated, max. 255 chars'
      validation:
        'TYPO3.Neos/Validation/StringLengthValidator':
          maximum: 255
    metaRobotsNoindex:
      type: boolean
      ui:
        label: 'Hide from search engines (noindex)'
        inspector:
          group: 'seometa'
          position: 30
    metaRobotsNofollow:
      type: boolean
      ui:
        label: 'Do not follow links (nofollow)'
        inspector:
          group: 'seometa'
          position: 40


#
# Twitter Card mixin
#
'TYPO3.Neos.Seo:TwitterCardMixin':
  abstract: TRUE
  ui:
    inspector:
      groups:
        twittercardsettings:
          label: 'Twitter Card Settings'
          position: 10
          tab: twitter
        twittercardcontent:
          label: 'Twitter Card Content'
          position: 20
          tab: twitter
  properties:
    twitterCardType:
      type: string
      defaultValue: ~
      ui:
        label: 'Card Type'
        inspector:
          group: 'twittercardsettings'
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            values:
              ~:
                label: 'None'
              'summary':
                label: 'Summary Card'
              'summary_large_image':
                label: 'Summary Card with Large Image'
              'photo':
                label: 'Photo Card'
    twitterCardCreator:
      type: string
      ui:
        label: 'Creator Handle'
        inspector:
          group: 'twittercardsettings'
          editorOptions:
            placeholder: '@johnexample'
      validation:
        'TYPO3.Neos/Validation/RegularExpressionValidator':
          regularExpression: '/@[a-z0-9_]{1,15}/i'
    twitterCardTitle:
      type: string
      ui:
        label: 'Title'
        inspector:
          group: 'twittercardcontent'
          editor: 'TYPO3.Neos/Inspector/Editors/TextAreaEditor'
          editorOptions:
            placeholder: 'max. 70 characters'
      validation:
        'TYPO3.Neos/Validation/StringLengthValidator':
          maximum: 70
    twitterCardDescription:
      type: string
      ui:
        label: 'Description'
        inspector:
          group: 'twittercardcontent'
          editor: 'TYPO3.Neos/Inspector/Editors/TextAreaEditor'
          editorOptions:
            placeholder: 'max. 200 characters'
      validation:
        'TYPO3.Neos/Validation/StringLengthValidator':
          maximum: 200
    twitterCardImage:
      type: TYPO3\Media\Domain\Model\ImageInterface
      ui:
        label: 'Card Image'
        inspector:
          group: 'twittercardcontent'
          editorOptions:
            features:
              crop: TRUE
```

Nun wird die Datei `Configuration/NodeTypes.yaml` verändert:

```
#
# Add mixins; and a SEO tab to the inspector
#
'TYPO3.Neos:Document':
  superTypes:
    'Schulung.Websites.TitleTagMixin': 'Schulung.Websites:TitleTagMixin'
    'Schulung.Websites.SeoMetaTagsMixin': 'Schulung.Websites:SeoMetaTagsMixin'
    'Schulung.Websites.TwitterCardMixin': 'Schulung.Websites:TwitterCardMixin'
  ui:
    inspector:
      tabs:
        seo:
          label: 'SEO'
          position: 30
          icon: 'icon-bullseye'
        twitter:
          label: 'twitter'
          position: 40
          icon: 'icon-twitter'

'TYPO3.Neos:Shortcut':
  superTypes:
    'TYPO3.Neos.Seo.TitleTagMixin': ~
    'TYPO3.Neos.Seo.SeoMetaTagsMixin': ~
    'TYPO3.Neos.Seo.TwitterCardMixin': ~
```

Nun muss die Datei `Resources/Private/TypoScript/Root.ts2` geändert werden:

```
#
# TYPO3.Neos:Page is the default object used for rendering in most sites,
# so TYPO3.Neos.Seo extends this default object
#
prototype(TYPO3.Neos:Page) {
  head {
    titleTag {
      default = TYPO3.TypoScript:Collection {
        // Retrieve all parent document nodes excluding the homepage
        collection = ${q(documentNode).add(q(documentNode).parents()).slice(0, -1).get()}
        itemName = 'node'
        iterationName = 'nodeIterator'
        // Implode node titles with a dash
        itemRenderer = ${q(node).property('title') + (nodeIterator.isLast ? '' : ' - ')}
        // Always add general site name as suffix
        @process.siteName = ${(value ? String.stripTags(value) + ' - ' : '') + site.context.currentSite.name}
      }

      content = ${q(node).property('titleOverride') ? q(node).property('titleOverride') : this.default}
    }

    metaDescriptionTag = TYPO3.TypoScript:Tag {
      tagName = 'meta'
      attributes {
        name = 'description'
        content = ${q(node).property('metaDescription')}
      }
      @if.isNotBlank = ${!String.isBlank(q(node).property('metaDescription'))}
    }

    metaKeywordsTag = TYPO3.TypoScript:Tag {
      tagName = 'meta'
      attributes {
        name = 'keywords'
        content = ${q(node).property('metaKeywords')}
      }
      @if.isNotBlank = ${!String.isBlank(q(node).property('metaKeywords'))}
    }

    metaRobotsTag = TYPO3.TypoScript:Tag {
      tagName = 'meta'
      attributes {
        name = 'robots'
        content = ${(q(node).property('metaRobotsNoindex') ? 'noindex' : 'index') + ',' + (q(node).property('metaRobotsNofollow') ? 'nofollow' : 'follow')}
      }
    }

    alternateLanguageLinks = TYPO3.Neos:DimensionMenu {
      @if.languageDimensionExists = ${Configuration.setting('TYPO3.TYPO3CR.contentDimensions.language') != null}
      @if.onlyRenderWhenInLiveWorkspace = ${node.context.workspace.name == 'live'}
      dimension = 'language'
      templatePath = 'resource://TYPO3.Neos.Seo/Private/Templates/TypoScriptObjects/AlternateLanguageLinks.html'
    }

    twitterCard = TYPO3.TypoScript:Array {
      @if.isEnabledBlank = ${!String.isBlank(q(node).property('twitterCardType'))}
      @if.isEnabled = ${q(node).property('twitterCardType') != null}

      cardTypeTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:card'
          content = ${q(node).property('twitterCardType')}
        }
      }

      cardSiteTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:site'
          content = ${Configuration.setting('TYPO3.Neos.Seo.twitterCard.siteHandle')}
        }
        @if.isSet = ${Configuration.setting('TYPO3.Neos.Seo.twitterCard.siteHandle') != null}
      }

      cardCreatorTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:creator'
          content = ${q(node).property('twitterCardCreator')}
        }
        @if.isNotBlank = ${!String.isBlank(q(node).property('twitterCardCreator'))}
      }

      cardTitleTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:title'
          content = ${q(node).property('twitterCardTitle')}
        }
        @if.isNotBlank = ${!String.isBlank(q(node).property('twitterCardTitle'))}
      }

      cardDescriptionTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:description'
          content = ${q(node).property('twitterCardDescription') ? q(node).property('twitterCardDescription') : q(node).property('metaDescription')}
        }
        @if.isNotBlank = ${!String.isBlank((q(node).property('twitterCardDescription') ? q(node).property('twitterCardDescription') : q(node).property('metaDescription')))}
      }

      cardImageTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:image:src'
          content = TYPO3.Neos:ImageUri {
            asset = ${q(node).property('twitterCardImage')}
            maximumWidth = 2000
            maximumHeight = 2000
          }
        }
        @if.isImageSet = ${q(node).property('twitterCardImage') != null}
      }

      cardUrlTag = TYPO3.TypoScript:Tag {
        tagName = 'meta'
        attributes {
          name = 'twitter:url'
          content = TYPO3.Neos:NodeUri {
            node = ${node}
            absolute = TRUE
          }
        }
      }
    }
  }
}
```