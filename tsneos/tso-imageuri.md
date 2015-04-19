# Neos TypoScript: Image URI

**Beschreibung:** Erzeugt ein Image-Tag bzw. eine Image-URI

**Vollständiger Name:** `TYPO3.Neos:ImageUri`

**TypoScript Definition:** 
```
# ImageUri object works exactly the same way as the uri.image ViewHelper in the TYPO3.Media package
prototype(TYPO3.Neos:ImageUri) {
	@class = 'TYPO3\\Neos\\TypoScript\\ImageUriImplementation'
	maximumWidth = 2560
	maximumHeight = 2560
	allowCropping = FALSE
	allowUpScaling = FALSE
	@exceptionHandler = 'TYPO3\\TypoScript\\Core\\ExceptionHandlers\\AbsorbingHandler'
}

# ImageTag object works exactly the same way as image ViewHelper in the TYPO3.Media package
prototype(TYPO3.Neos:ImageTag) < prototype(TYPO3.TypoScript:Tag) {
	asset = 'pass-the-media-asset'
	maximumWidth = 2560
	maximumHeight = 2560
	allowCropping = FALSE
	allowUpScaling = FALSE
	@override.asset = ${this.asset}
	@override.maximumWidth = ${this.maximumWidth}
	@override.maximumHeight = ${this.maximumHeight}
	@override.allowCropping = ${this.allowCropping}
	@override.allowUpScaling = ${this.allowUpScaling}

	tagName = 'img'
	attributes {
		src = TYPO3.Neos:ImageUri {
			asset = ${asset}
			maximumWidth = ${maximumWidth}
			maximumHeight = ${maximumHeight}
			allowCropping = ${allowCropping}
			allowUpScaling = ${allowUpScaling}
		}
	}
}
```

**Dateien:**
```
Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/DefaultTypoScript.ts2

Packages/Application/TYPO3.Neos/Resources/Private/TypoScript/Prototypes/ImageUri.ts2
```

**Beispiel(e):**

```
imageUri = TYPO3.Neos:ImageUri {
	asset = ${q(node).property('image')}
	maximumWidth = 2560
	maximumHeight = 1280
	@if.image = ${q(node).property('image')}
}

<f:if condition="{landingPage}">
	<div class="main-header{f:if(condition: imageUri, then: ' image" style="background-image: url({imageUri});')}"{f:if(condition: imageTitleText, then: ' title="{imageTitleText}"')}>
		<div class="container">
			{content.teaser -> f:format.raw()}
		</div>
	</div>
</f:if>
```