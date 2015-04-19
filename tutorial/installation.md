# Installation einer Site


## Composer

Die Installation erfolgt über **Composer**, einem Dependency-Management-System für PHP. Composer muss daher zuerst geladen werden:

```
cd /path/to/neos/directory
curl -s https://getcomposer.org/installer | php
```

## Neos Installation

Nun lädt man Neos über Composer:

```
php ./composer.phar create-project --no-dev typo3/neos-base-distribution TYPO3-Neos-1.0
```
(Möglich wäre auch ein direktes Laden: `http://sourceforge.net/projects/typo3flow/files/TYPO3%20Neos/`).


Meldungen hisichtlich "...is not autoloadable..." können ignoriert werden.

Auf die Frage "Do you want to remove the existing VCS" sollte man mit "n" antworten.

Je nach Setup muss man nun eine "VirtualHost" Eintrag in der Datei `apache.conf` machen:

```
NameVirtualHost *:80 # if needed

<VirtualHost *:80>
    DocumentRoot "/your/htdocs/TYPO3-Neos-1.0/Web/"
    # skip the following line for development
    # SetEnv FLOW_CONTEXT Production
    ServerName neos.dev
</VirtualHost>
```
Wichtig ist die Zeile `# SetEnv FLOW_CONTEXT Production` später wieder einzukommentieren, damit der Live-Server im Production-Mode läuft. Default ist der sogenannte **Development** Mode.


Schließlich wird noch ein Eintrag in der Datei `/etc/hosts` benötigt:

```
127.0.0.1 neos.dev
```

Setup Patrick Lobacher:

```
ln -s TYPO3-Neos-1.0/Web htdocs
```

## Rechte setzen

Sollte die Rechte bereits so gesetzt worden sein, dass sowohl Lese- wie auch Schreibrechte für die Benutzergruppe des Webservers existieren, dann kann man den folgenden Abschnitt überspringen.


```
cd TYPO3-Neos-1.0/
sudo ./flow flow:core:setfilepermissions patricklobacher _www _www
```

Dabei ist statt "patricklobacher" der Shell-User einzusetzen und statt dem ersten "_www" der User unter dem der Webserver läuft und statt dem zweiten "_www" die Gruppe unter dem der Webserver läuft.

User und Gruppe des Webservers stehen normalerweise in der Datei `httpd.conf`.


## Webserver unter Mac OS X Mavericks

Mac OS X Mavericks hat einen - auf PHP basierenden - Webserver eingebaut:

```
cd /your/htdocs/TYPO3-Neos-1.0/Web/
php -S localhost:8000
```

Dieser eignet sich **NICHT** zum Betrieb von TYPO3 Neos!


## Setup

Nun ruft man `http://neos.dev/setup` auf.

Nach dem Check des System verlangt Neos ein Passwort, welches sich unter der angezeigten Lokation befindet, z.B.:

```
/Users/patricklobacher/Sites/neos/TYPO3-Neos-1.0/Data/SetupPassword.txt

The setup password is:

d49zx4ta

After you successfully logged in, this file is automatically deleted for security reasons.
Make sure to save the setup password for later use.
```

