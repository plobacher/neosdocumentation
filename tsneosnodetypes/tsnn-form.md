# TYPO3 Neos Nodetypes - Form

**Kompletter Name:** TYPO3.Neos.NodeTypes:Form

** Beschreibung:** Ein Formular als Inhaltselement

**Konfiguration:**

```
# Form TS Object
prototype(TYPO3.Neos.NodeTypes:Form) {
  presetName = 'default'
  @cache {
    mode = 'uncached'
    context {
      1 = 'node'
      2 = 'documentNode'
    }
  }
}
```

Yaml:

```
'TYPO3.Neos.NodeTypes:Form':
  superTypes: ['TYPO3.Neos:Content']
  ui:
    label: 'Form'
    icon: 'icon-envelope-alt'
    position: 600
    inspector:
      groups:
        form:
          label: 'Form'
          position: 30
  properties:
    formIdentifier:
      type: string
      ui:
        label: 'Form identifier'
        reloadIfChanged: TRUE
        inspector:
          group: form
          editor: 'TYPO3.Neos/Inspector/Editors/SelectBoxEditor'
          editorOptions:
            placeholder: 'Select the Form identifier'
            values:
              '':
                label: ''
```

```
##
# Set the default preset for the "Form" element
#
prototype(TYPO3.Neos.NodeTypes:Form) {
  presetName = 'bootstrap'
}

// NodeTypes.yaml

##
# Adjust the "Form" node type:
# Remove the empty select option and register the "contact-form"-Form
#
'TYPO3.Neos.NodeTypes:Form':
  properties:
    'formIdentifier':
      ui:
        inspector:
          editorOptions:
            values:
              '': ~
              'contact-form':
                label: 'Contact form'

// Settings.yaml

TYPO3:
  Form:
    yamlPersistenceManager:
      savePath: 'resource://TYPO3.NeosDemoTypo3Org/Private/Form/'
    presets:
      bootstrap:
        title: 'Twitter bootstrap'
        parentPreset: 'default'
        formElementTypes:
          'TYPO3.Form:Base':
            renderingOptions:
              layoutPathPattern: 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/ContactForm/{@type}.html'
          'TYPO3.Form:FormElement':
            properties:
              elementClassAttribute: 'form-control'
          'TYPO3.Form:MultiLineText':
            properties:
              elementClassAttribute: 'form-control'
```