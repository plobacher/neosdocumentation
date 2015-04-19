# Kontakt-Formular

## Installation des Swift-Mailer-Packages

Zunächst muss das Paket `TYPO3.SwiftMailer` installiert werden:

```
$ cd Packages/Application
$ git clone git://git.typo3.org/Packages/TYPO3.SwiftMailer.git

```

Dann im Package-Manager installieren

## Settings

Zunächst einmal muss der Speicherort des Formulars in der Datei `Packages/Sites/Schulung.Website/Configuration/Settings.yaml` konfiguriert werden:

```
TYPO3:
  Form:
    yamlPersistenceManager:
      savePath: 'resource://Schulung.Website/Private/Form/'
    presets:
      bootstrap:
        title: 'Twitter bootstrap'
        parentPreset: 'default'
        formElementTypes:
          'TYPO3.Form:Base':
            renderingOptions:
              layoutPathPattern: 'resource://Schulung.Website/Private/Templates/ContactForm/{@type}.html'
          'TYPO3.Form:FormElement':
            properties:
              elementClassAttribute: 'form-control'
          'TYPO3.Form:MultiLineText':
            properties:
              elementClassAttribute: 'form-control'
```

## NodeType des Formulars anlegen

Nun müssen wir die NodeType-Definition unter `` erweitern:

```
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
'TYPO3.Neos.NodeTypes:Form':
  properties:
    formIdentifier:
      ui:
        inspector:
          editorOptions:
            values:
              '': ~
              # Maps to the file Schulung.Website/Resources/Private/Form/contact-form.yaml
              'contact-form':
                label: 'Kontakt-Formular'
```

## Kontaktformular anlegen

Nun benötigen wir ein Kontaktformular - dafür legen wir zunächst einen Ordner `Form` unterhalb von `Packages/Sites/Schulung.Website/Resources/Private/Form` an und dort eine Datei `contact-form.yaml` mit dem folgenden Inhalt:

```
type: 'TYPO3.Form:Form'
identifier: contact-form
label: Contact
renderingOptions:
    submitButtonLabel: Send
renderables:
  -
    type: 'TYPO3.Form:Page'
    identifier: page-one
    label: Contact
    renderables:
      -
        type: 'TYPO3.Form:SingleLineText'
        identifier: name
        label: Name
        validators:
          - identifier: 'TYPO3.Flow:NotEmpty'
        properties:
          placeholder: Name
        defaultValue: ''
      -
        type: 'TYPO3.Form:SingleLineText'
        identifier: email
        label: E-Mail
        validators:
          - identifier: 'TYPO3.Flow:NotEmpty'
          - identifier: 'TYPO3.Flow:EmailAddress'
        properties:
          placeholder: 'E-Mail'
        defaultValue: ''
      -
        type: 'TYPO3.Form:MultiLineText'
        identifier: message
        label: Message
        validators:
          - identifier: 'TYPO3.Flow:NotEmpty'
        properties:
          placeholder: 'Your Message'
        defaultValue: ''
finishers:
  -
    identifier: 'TYPO3.Form:Email'
    options:
      templatePathAndFilename: resource://Schulung.Website/Private/Templates/Email/Message.txt
      subject: Contact from example.net
      recipientAddress: office@example.net
      recipientName: 'Office of Company'
      senderAddress: server@example.net
      senderName: Server example.net
      replyToAddress: office@example.net
      format: plaintext
  -
    identifier: 'TYPO3.Form:Confirmation'
    options:
      message: >
        <h3>Thank you for your feedback</h3>
        <p>We will process it as soon as possible.</p>
```

## Email-Text

Nun legen wir noch die Datei `Packages/Sites/Schulung.Website/Resources/Private/Templates/Email/Message.txt` an (Ordner `Email` muss ebenfalls angelegt werden):

```

``
