# Plugins

## Guestbook

### Package

Zunächst legen wir mit dem Kommandozeilentool ein Package an:

```
$ ./flow kickstart:package Schulung.Guestbook

Created .../Schulung.Guestbook/Classes/Schulung/Guestbook/Controller/StandardController.php
Created .../Schulung.Guestbook/Resources/Private/Layouts/Default.html
Created .../Schulung.Guestbook/Resources/Private/Templates/Standard/Index.html
```

### Domain-Model

Nun wird das Domain-Model angelegt:

```
$ ./flow kickstart:model Schulung.Guestbook Entry "author:string" "email:string" "date:\DateTime" "post:string"

Created .../Schulung.Guestbook/Classes/Schulung/Guestbook/Domain/Model/Entry.php
Created .../Schulung.Guestbook/Tests/Unit/Domain/Model/EntryTest.php
As a new model was generated, don't forget to update the database schema with the respective doctrine:* commands.
```

### Repository

```
$ ./flow kickstart:repository Schulung.Guestbook Entry

Created .../Schulung.Guestbook/Classes/Schulung/Guestbook/Domain/Repository/EntryRepository.php
```

### Controller und Templates anlegen

```
$ ./flow kickstart:actioncontroller Schulung.Guestbook Entry --generate-actions --generate-templates

Created .../Schulung.Guestbook/Classes/Schulung/Guestbook/Controller/EntryController.php
Omitted .../Schulung.Guestbook/Resources/Private/Layouts/Default.html
Created .../Schulung.Guestbook/Resources/Private/Templates/Entry/Index.html
Created .../Schulung.Guestbook/Resources/Private/Templates/Entry/New.html
Created .../Schulung.Guestbook/Resources/Private/Templates/Entry/Edit.html
Created .../Schulung.Guestbook/Resources/Private/Templates/Entry/Show.html
```

### Templates anpassen

Wir passen nun die Datei `Application/Schulung.Guestbook/Resources/Private/Templates/Entry/Index.html` an:

```html
<f:if condition="{entries}">
	<f:then>
		<f:for each="{entries}" as="entry">
			<div id="gb_entry">
				<p>
					Verfasst am
					<f:format.date format="d.m.Y, H:i">{entry.date}</f:format.date>
					von
					<f:link.email email="{entry.email}">{entry.author}</f:link.email>
				</p>
				<p>
					<f:format.nl2br>{entry.post}</f:format.nl2br>
				</p>
			</div>
		</f:for>
	</f:then>
	<f:else>
		<p>Keine Einträge vorhanden!</p>
	</f:else>
</f:if>
<p><f:link.action action="new">Neuer Eintrag</f:link.action></p>
```

Zudem muss auch die Datei `Application/Schulung.Guestbook/Resources/Private/Templates/Entry/New.html` angepasst werden:

```html
<f:form action="create" name="newEntry" object="{entry}">
	<label for="author">Name</label>
	<f:form.textfield property="author" id="author" />
	<br />
	<label for="email">Email</label>
	<f:form.textfield property="email" id="email" />
	<br />
	<label for="post">Eintrag</label>
	<f:form.textarea property="post" id="post" />
	<br />
	<f:form.submit value="Erstellen" /></td>
</f:form>
```

### Validierung und setzen des Datums

```php
<?php
namespace Schulung\Guestbook\Domain\Model;

use TYPO3\Flow\Annotations as Flow;
use Doctrine\ORM\Mapping as ORM;

/**
 * @Flow\Entity
 */
class Entry {

	/**
	 * @var string
	 * @Flow\Validate(type="NotEmpty")
	 */
	protected $author;

	/**
	 * @var string
	 * @Flow\Validate(type="NotEmpty")
	 */
	protected $email;

	/**
	 * @var \DateTime
	 */
	protected $date;

	/**
	 * @var string
	 * @Flow\Validate(type="NotEmpty")
	 */
	protected $post;

	public function __construct() {
		$this->date = new \DateTime('now');
	}

	/**
	 * @return string
	 */
	public function getAuthor() {
		return $this->author;
	}

	/**
	 * @param string $author
	 * @return void
	 */
	public function setAuthor($author) {
		$this->author = $author;
	}

	/**
	 * @return string
	 */
	public function getEmail() {
		return $this->email;
	}

	/**
	 * @param string $email
	 * @return void
	 */
	public function setEmail($email) {
		$this->email = $email;
	}

	/**
	 * @return \DateTime
	 */
	public function getDate() {
		return $this->date;
	}

	/**
	 * @param \DateTime $date
	 * @return void
	 */
	public function setDate(\DateTime $date) {
		$this->date = $date;
	}

	/**
	 * @return string
	 */
	public function getPost() {
		return $this->post;
	}

	/**
	 * @param string $post
	 * @return void
	 */
	public function setPost($post) {
		$this->post = $post;
	}

}
```

### Datenbank Migration

Über ein `./flow doctrine:update` könnte nun Doctrine angewiesen werden, die benötigen Datenbank-Tabellen und Felder zu erzeugen. Dafür würde Doctrine beispielsweise das Model analysieren und die dort enthaltenen Felder entsprechend anlegen.

Wir wollen aber einen anderen Weg gehen, indem wir ein sogenanntes Migration-Script erstellen lassen. Dies hat insbesondere den Vorteil, dass es die Migration mit dem jetzigen Datum speichert und wir die SQL-Befehle (falls benötigt) auch manuell anpassen könnten.

```
$ ./flow doctrine:migrationgenerate

Generated new migration class!

Next Steps:
- Move /Users/patricklobacher/Sites/neos/TYPO3-Neos-1.0/Data/DoctrineMigrations/Version20140519202924.php to YourPackage/Migrations/Mysql/
- Review and adjust the generated migration.
- (optional) execute the migration using ./flow doctrine:migrate
```

Weiter geht's:

```
$ mkdir -p Packages/Application/Schulung.Guestbook/Migrations/Mysql
$ cp Data/DoctrineMigrations/Version20140519202924.php Packages/Application/Schulung.Guestbook/Migrations/Mysql
$ ./flow doctrine:migrate
Migrating up to 20140519202924 from 20131205174631

  ++ migrating 20140519202924

     -> CREATE TABLE schulung_guestbook_domain_model_entry (persistence_object_identifier VARCHAR(40) NOT NULL, author VARCHAR(255) NOT NULL, email VARCHAR(255) NOT NULL, date DATETIME NOT NULL, post VARCHAR(255) NOT NULL, PRIMARY KEY(persistence_object_identifier)) DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci ENGINE = InnoDB

  ++ migrated (0.12s)

  ------------------------

  ++ finished in 0.12
  ++ 1 migrations executed
  ++ 1 sql queries
```

### TypoScript

Nun benötigen wir eine entsprechende TypoScript-Datei: `Packages/Application/Schulung.Guestbook/Resources/Private/TypoScript/Root.ts2`:

```
prototype(Schulung.Guestbook:Display) < prototype(TYPO3.Neos:Plugin)
prototype(Schulung.Guestbook:Display) {
	package = 'Schulung.Guestbook'
	controller = 'Entry'
	action = 'index'
}
```

### NodeType

Damit man das Plugin auswählen kann, wird noch der entsprechende NodeType benötigt - hierfür legen wir die folgende Datei an `Packages/Application/Schulung.Guestbook/Configuration/NodeTypes.yaml`:

```
'Schulung.Guestbook:Display':
  superTypes: ['TYPO3.Neos:Plugin']
  ui:
    lable: 'Guestbook'
    icon: 'icon-user'
```

### TypoScript Einbindung

Das TypoScript eines Packages wird nicht automatisch eingebunden - daher müssen wir es im Site-TypoScript inkludieren. Dies machen wir also in der Datei ``:

```
include: resource://Lobacher.Guestbook/Private/TypoScript/Root.ts2
```

### Policy setzen

Nun sind wir beinahe fertig mit der Erstellung unseres kleinen Plugins. Bevor wir dieses aber verwenden können, müssen wir noch die Benutzerrechte entsprechend einstellen – machen wir dies nicht, erhalten wir eine Fehlermeldung, dass das Plugin nicht aufgerufen werden kann. Hierfür legen wir die Datei `Packages/Application/Schulung.Guestbook/Configuration/Policy.yaml` mit folgendem Inhalt an:

```
resources:
  methods:
    Schulung_Guestbook_EntryAccess: 'method(Schulung\Guestbook\Controller\EntryController->(index|new|create)Action())'
acls:
  Everybody:
    methods:
      Schulung_Guestbook_EntryAccess: GRANT

```

## Person-Plugin

### Package kickstarten

```
$ ./flow kickstart:package Schulung.Person

Created .../Schulung.Person/Classes/Schulung/Person/Controller/StandardController.php
Created .../Schulung.Person/Resources/Private/Layouts/Default.html
Created .../Schulung.Person/Resources/Private/Templates/Standard/Index.html
```

### NodeTypes

```
#
# Schema Person
'Schulung.Person:Schema.Person':
  abstract: true
  ui:
    inspector:
      groups:
        person:
          label: 'Person'
          position: 1
  properties:
    personName:
      type: string
      ui:
        label: 'Name'
        reloadIfChanged: TRUE
        inspector:
          group: person


#
# Schema Postal Address
'Schulung.Person:Schema.PostalAddress':
  abstract: true
  ui:
    inspector:
      groups:
        postalAddress:
          label: 'Postal Address'
          position: 2
  properties:
    postalAddressStreetAddress:
      type: string
      ui:
        label: 'Street Address'
        reloadIfChanged: TRUE
        inspector:
          group: postalAddress
    postalAddressPostalCode:
      type: string
      ui:
        label: 'Postal Code'
        reloadIfChanged: TRUE
        inspector:
          group: postalAddress
    postalAddressLocality:
      type: string
      ui:
        label: 'Locality'
        reloadIfChanged: TRUE
        inspector:
          group: postalAddress
    postalAddressRegion:
      type: string
      ui:
        label: 'Region'
        reloadIfChanged: TRUE
        inspector:
          group: postalAddress
    postalAddressCountry:
      type: string
      ui:
        label: 'Country'
        reloadIfChanged: TRUE
        inspector:
          group: postalAddress

#
# Person
'Schulung.Person:Person':
  superTypes:
    - 'TYPO3.Neos:Document'
    - 'Schulung.Person:Schema.PostalAddress'
    - 'Schulung.Person:Schema.Person'
  ui:
    label: 'Person'
    icon: 'icon-user'
    group: person
  childNodes:
    profile:
      type: 'TYPO3.Neos:ContentCollection'

#
# Contact Address
'Schulung.Person:ContactAddress':
  superTypes:
    - 'TYPO3.Neos:Content'
  nodeLabelGenerator: 'Schulung\Person\Domain\Model\PersonNodeLabelGenerator'
  ui:
    label: 'Contact Address'
    group: 'person'
    inspector:
      groups:
        document:
          label: 'Address'
          position: 1
  properties:
    person:
      type: reference
      ui:
        label: 'Person'
        reloadIfChanged: true
        inspector:
          group: 'document'
          editorOptions:
            nodeTypes:
              - 'Schulung.Person:Person'
```

### Settings.yaml

Um eine neue Gruppe im New Content Element Wizard anzulegen, wird eine `Settings.yaml` benötigt:

```
TYPO3:
  Neos:
    nodeTypes:
      groups:
        person:
          position: 'start'
          label: 'Schulung Node'
```

### TypoScript

`Root.ts2`

```
include: Library/ContactAddress.ts2
include: Library/Person.ts2
```

`ContactAddress.ts2`

```
prototype(Schulung.Person:ContactAddress) >
prototype(Schulung.Person:ContactAddress) < prototype(TYPO3.Neos:Content) {
	templatePath = 'resource://Schulung.Person/Private/Templates/NodeTypes/ContactAddress.html'

	person = ${node.properties.person}
	hasPerson = ${node.properties.person ? TRUE : FALSE}

	attributes = TYPO3.TypoScript:Attributes {
		class = 'person-profile-inline'
		style = 'background: #CCC; padding: 10px; margin-bottom: 10px;'
		data-ttree-region = ${this.person.properties.postalAddressRegion}
		data-ttree-country = ${this.person.properties.postalAddressCountry}
	}

	personName = ${this.person.properties.personName}
	postalAddressStreetAddress = ${this.person.properties.postalAddressStreetAddress}
	postalAddressCountry = ${this.person.properties.postalAddressCountry}
	postalAddressPostalCode = ${this.person.properties.postalAddressPostalCode}
	postalAddressLocality = ${this.person.properties.postalAddressLocality}
	postalAddressRegion = ${this.person.properties.postalAddressRegion}
}
```

`Person.ts2`

```
prototype(TYPO3.Neos:PrimaryContent).SchulungPersonPerson {
	condition = ${q(node).is('[instanceof Schulung.Person:Person]')}
	type = 'Schulung.Person:Person'
	@position = 'start'
}

prototype(Schulung.Person:Person) < prototype(TYPO3.TypoScript:Template) {
	templatePath = 'resource://Schulung.Person/Private/Templates/NodeTypes/Person.html'

	attributes = TYPO3.TypoScript:Attributes {
		class = 'person-profile-page'
		data-ttree-region = ${node.properties.postalAddressRegion}
		data-ttree-country = ${node.properties.postalAddressCountry}
	}

	personName = ${node.properties.personName}
	postalAddressStreetAddress = ${node.properties.postalAddressStreetAddress}
	postalAddressCountry = ${node.properties.postalAddressCountry}
	postalAddressPostalCode = ${node.properties.postalAddressPostalCode}
	postalAddressLocality = ${node.properties.postalAddressLocality}
	postalAddressRegion = ${node.properties.postalAddressRegion}

	profile = TYPO3.Neos:ContentCollection {
		nodePath = 'profile'
	}
}
```

### TypoScript einbinden

```
include: resource://Schulung.Person/Private/TypoScript/Root.ts2
```

### Templates

`Packages/Application/Schulung.Person/Resources/Private/Templates/NodeTypes/ContactAddress.html`

```html
{namespace neos=TYPO3\Neos\ViewHelpers}
<div{attributes -> f:format.raw()}>
	<f:if condition="{hasPerson}">
		<f:then>
			<div itemscope itemtype="http://schema.org/Person">
				<div style="font-weight: bold;" itemprop="name">{personName}</div>
				<div itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
					<div itemprop="streetAddress">
						{postalAddressStreetAddress}
					</div>
					<div>
						<span itemprop="addressCountry">{postalAddressCountry}</span> -
						<span itemprop="postalCode">{postalAddressPostalCode}</span>
						<span itemprop="addressLocality">{postalAddressLocality}</span>
					</div>
				</div>
			</div>
		</f:then>
		<f:else>
			<strong>
				Please select a Person<br/>
				in the Inspector
			</strong>
		</f:else>
	</f:if>
</div>
```

`Packages/Application/Schulung.Person/Resources/Private/Templates/NodeTypes/Person.html`

```html
{namespace neos=TYPO3\Neos\ViewHelpers}
<div{attributes -> f:format.raw()}>
	<div itemscope itemtype="http://schema.org/Person">
		<h1 itemprop="name">{personName}</h1>
		<span itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
			<span itemprop="streetAddress">
				{postalAddressStreetAddress}
			</span> |
			<span itemprop="addressCountry">{postalAddressCountry}</span>,
			<span itemprop="postalCode">{postalAddressPostalCode}</span>,
			<span itemprop="addressLocality">{postalAddressLocality}</span>,
			<span itemprop="addressRegion">{postalAddressRegion}</span>
		</span>
	</div>

	<div class="customer-profile">
		{profile -> f:format.raw()}
	</div>
</div>
```

### NodeLabelGenerator

`Packages/Application/Schulung.Person/Classes/Schulung/Person/Domain/Model/PersonNodeLabelGenerator.php`

```php
<?php
namespace Schulung\Person\Domain\Model;

use TYPO3\Flow\Annotations as Flow;
use TYPO3\TYPO3CR\Domain\Model\AbstractNodeData;
use TYPO3\TYPO3CR\Domain\Model\DefaultNodeLabelGenerator;
use TYPO3\TYPO3CR\Domain\Model\NodeInterface;

/**
 * The default node label generator; used if no-other is configured
 *
 * @Flow\Scope("singleton")
 */
class PersonNodeLabelGenerator extends DefaultNodeLabelGenerator {

	/**
	 * Render a node label
	 *
	 * @param \TYPO3\TYPO3CR\Domain\Model\AbstractNodeData $nodeData
	 * @param boolean $crop
	 * @return string
	 */
	public function getLabel(AbstractNodeData $nodeData, $crop = TRUE) {
		if ($nodeData->hasProperty('person') === TRUE && $nodeData->getProperty('person')) {
			$label = 'Link to: ' . strip_tags($nodeData->getProperty('person')->getProperty('personName'));
		} else {
			$label = parent::getLabel($nodeData, FALSE);
		}

		if ($crop === FALSE) {
			return $label;
		}

		$croppedLabel = \TYPO3\Flow\Utility\Unicode\Functions::substr($label, 0, NodeInterface::LABEL_MAXIMUM_CHARACTERS);
		return $croppedLabel . (strlen($croppedLabel) < strlen($label) ? ' ...' : '');
	}
}
```