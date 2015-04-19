# TYPO3 Media TypoScript Objekte

Zu den ViewHelpern `image` und `uri.image` gibt es auch korrespondierende TypoScript-Objekte:


## ImageUri object works exactly the same way as Media:Uri.Image view helper
prototype(TYPO3.Media:ImageUri) {
	@class = 'TYPO3\\Media\\TypoScriptObjects\\ImageUriImplementation'
	maximumWidth = 2560
	maximumHeight = 2560
	allowCropping = FALSE
	allowUpScaling = FALSE
	@exceptionHandler = 'TYPO3\\TypoScript\\Core\\ExceptionHandlers\\AbsorbingHandler'
}

## ImageTag object works exactly the same way as Media:Image view helper
prototype(TYPO3.Media:ImageTag) < prototype(TYPO3.TypoScript:Tag) {
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
		src = TYPO3.Media:ImageUri {
			asset = ${asset}
			maximumWidth = ${maximumWidth}
			maximumHeight = ${maximumHeight}
			allowCropping = ${allowCropping}
			allowUpScaling = ${allowUpScaling}
		}
	}
}
