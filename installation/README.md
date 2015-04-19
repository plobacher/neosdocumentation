# Installation von TYPO3 Neos

## Systemvoraussetzungen

* Webserver (empfohlen ist Apache 2.x mit aktiviertem mod_rewrite Modul)
* PHP 5.3.7 - 5.4.x (minimal wäre PHP 5.3.2 - dort kann es zu Problemen kommen)
* Folgende Funktionen müssen in PHP aktiviert sein: `system`, `shell_exec`, `escapeshellcmd`, `escapeshellarg`, `proc_open` und `exec`
* php.ini: `memory_limit = 512M` oder höher (empfohlen 1014M)
* php.ini: `xdebug.max_nesting_level = 500` (sofern xdebug verwendet wird)
* php.ini: Fügen sie die folgende Optionen ans Ende hinzu: `detect_unicode = Off`
* php.ini: Zudem muss Magic_Quotes ausgeschaltet werden: `magic_quotes_gpc = Off`
* php.ini: Die Kommandozeile von Flow benötigt ferner noch eine Zeitzoneneinstellung: `date.timezone= "Europe/Berlin"`

* Wichtig ist auch, dass das PHP auf der Kommandozeile ebenfalls mindestens Version 5.3.7 ist (und über die angegebenen php.ini Einstellungen verfügt) - dies kann mit dem folgenden Befehl überprüft werden. `php --version`
* MySQL 5.1.50 - 5.x.x (zum Beispiel - grundsätzlich kann jede zum Doctrine DBAL kompatible Datenbank verwendet werden).
* Zugang zur Konsole - als *root User*, wenn die Zugangsrechte vom Hoster nicht entsprechend gesetzt worden sind. Bei den meisten Hostern ist dies aber der Fall - dann reicht ein normaler User

## PHP CLI

Zuerst muss geprüft werden, wo sich die `php.ini` Datei der PHP-CLI befindet:

```
$ php -i | grep php.ini

Configuration File (php.ini) Path => /etc
Loaded Configuration File => /etc/php.ini
```

Hier wird die Datei `/etc/php.ini` verwendet und man kann diese direkt zum Schreiben öffnen - wenn die letzte Zeile fehlt, muss die Datei angelegt werden. Folgende Einstellungen sollten darin enthalten sein:

```
date.timezone= "Europe/Berlin"
memory_limit = 512M
max_execution_time = 300
mysql.default_socket = /Applications/MAMP/tmp/mysql/mysql.sock
pdo_mysql.default_socket = /Applications/MAMP/tmp/mysql/mysql.sock
```

Der Pfad der letzten beiden Angaben kann beispielsweise wie folgt ermittelt werden:

```
$ find / -print | grep mysql.sock
```


## Ort der Installation

Die Installation wird in einem Verzeichnis *außerhalb* des Document Roots vorgenommen. Innerhalb der Installation gibt es ein Verzeichnis `Web` auf welches das Docucment Root gelegt wird.

```
/pfad/zum/Webserver
   |-TYPO3-Neos
   |---Build
   |---...
   |---Web (Document Root)
```

## Composer

Die Installation erfolgt über "Composer" - einem Dependency Manager für PHP.
Dafür ist Zugang zur Konsole nötig

```
cd /pfad/zum/webserver/
curl -s https://getcomposer.org/installer | php
```

Zur Installation von Composer unter Windows gibt es hier Infos: `http://getcomposer.org/doc/00-intro.md#installation-windows`


Dies legt die Datei `composer.phar` im aktuellen Verzeichnis an.
Will man den Composer zentral verwenden, kann man ihn auch verschieben/kopieren

```
mv composer.phar /usr/local/bin/composer
```

## Laden der TYPO3 Neos Sourcen durch Composer

Laden von TYPO3 Neos via Composer (in einer Zeile notieren!):

```
php /path/to/composer.phar create-project --no-dev typo3/neos-base-distribution TYPO3-Neos-1.2
```

Dies sorgt für die Installation von TYPO3 Flow, Neos und den benötigten Modulen (inkl. 3rd Party wie Doctrine 2, Aloha, ...). Anschließend erhält man ein Verzeichnis TYPO3-Neos, welches die letzte stabile Version von Neos enthält.

### Laden des Development Masters

Will man den Development Master laden, so kann man diese wie folgt machen:

```
php ./composer.phar create-project typo3/neos-base-distribution neos dev-master
```

### Alternative Quellen für TYPO3 Neos

Auf Sourceforge steht die aktuelle Neos Version zum Download als zip, tar.gz und tar.bz2 bereit:

```
http://sourceforge.net/projects/typo3flow/files/TYPO3%20Neos/
```

Laden der aktuellsten GIT-Version von TYPO3 Neos:

```
git clone git://git.typo3.org/Neos/Distributions/ Base.git TYPO3-Neos && cd TYPO3-Neos
```

Anschließend müssen dann noch die Abhängigkeiten geladen werden:

```
composer install --dev
```

## Setzen der Berechtigungen

Anschließend werden die Datei-Rechte in der Konsole gesetzt (falls nötig):

```
cd TYPO3-Neos
sudo ./flow flow:core:setfilepermissions shelluser wwwuser wwwgroup
```

(Weitere Infos: http://docs.typo3.org/flow/TYPO3FlowDocumentation/TheDefinitiveGuide/PartII/Installation.html#file-permissions)

* shelluser: Dies ist der User, mit dem man in der Konsole eingeloggt ist - kann mittels `whoami herausgefunden werden
* wwwuser: Der User, unter dem der Webserver läuft (steht in der Datei `httpd.conf`) - unter Mac OS X z.B. `_www`
* wwwgroup: Die Gruppe, unter dem der Webserver läuft (steht in der Datei `httpd.conf`) - unter Mac OS X z.B. `_www`


## Virtual Host Eintrag

Eintrag für Apache:

```
NameVirtualHost *:80 # sofern benötigt
<VirtualHost *:80>

	DocumentRoot "/pfad/zum/webserver/TYPO3-Neos/Web/"
	# Während der Entwicklung sollte die folgende Zeile
	# auskommentiert werden, denn dies stellt den Context auf
	# "Production" - dies bedeutet: kein Logging, mit Caching, ...
	# Default ist "Development"
	SetEnv FLOW_CONTEXT Production
	ServerName neos.demo

</VirtualHost>
```

Eintrag in `/etc/hosts` (`C:\windows\system32\drivers\etc\hosts`)

```
127.0.0.1 neos.demo
```

## Setup

Aufruf der Setup-Routine durch:

```
http://neos.demo/setup/
```

### Setup: Passwort

Das Passwort (merken!) wird bei jeder Installation neu generiert und befindet in der Datei im angezeigten Pfad.

Die Datei mit dem Passwort wird anschließend wieder gelöscht. Hat man das Passwort vergessen, muss man die Datei

```
/pfad/zum/webserver/TYPO3-Neos/Data/Persistent/FileBasedSimpleKeyService/SetupKey
```

löschen und das Setup erneut aufrufen


### Setup: Datenbank

Nun wird das Datenbank-Setup durchgeführt.

Die Voreinstellung hierzu ist MySQL, der Treiber kann aber durch Editieren der Datei `Configuration/Settings.yaml` geändert werden.

```
TYPO3:
  Flow:
    persistence:
      backendOptions:
        dbname: ''         # adjust to your database name
        user: ''           # adjust to your database user
        password: ''       # adjust to your database password
```

Sollte als DB-Host `127.0.0.1` nicht funktionieren, so kann man probieren stattdessen `localhost` dort einzutragen. Man kann entweder eine bestehende DB auswählen oder eine neue anlegen.

### Setup: Admin-User

Anschließend wird der Administrator-Benutzer angelegt.

Weitere Benutzer können später in der Benutzerverwaltung angelegt werden.
Zusätzliche Benutzer-Daten könnne ebenfalls später in der Benutzerverwaltung zugefügt werden.

Manuell kann man einen Benutzer ebenfalls anlegen - in der Konsole:

```
./flow typo3.neos:user:create username password firstname lastname
```

### Setup: Demo-Site oder leere Site

Nun kann man entweder eine Demo-Site importieren (empfohlen).

Oder mit einer leeren Website starten . Sobald in die beide unteren Formularfelder etwas eingetragen ist, wird eine neue Site angelegt.


## Zugänge

Die Zugänge lauten nun wie folgt:

* Frontend: `http://neos.demo/`
* Backend `http://neos.demo/neos/`
* Setup: `http://neos.demo/setup/`


### Update einer existierenden Installation

Um eine existierende Installation auf den letzten Patch-Level Release zu heben, kann man folgendes machen:

```
$ composer update --no-dev "typo3/*"
$ ./flow flow:cache:flush --force
$ ./flow doctrine:migrate
```

### Upgrade auf Development Master

Um auf den aktuellen Entwicklungsstand umzuschalten, kann folgendes verwendet werden

```
$ cd /installation-root/

$ composer require --no-update "typo3/neos:dev-master"
$ composer require --no-update "typo3/neos-nodetypes:dev-master"
$ composer require --no-update "typo3/neosdemotypo3org:dev-master"
$ composer require --no-update "typo3/neos-kickstarter:dev-master"
$ composer require --no-update "typo3/buildessentials:dev-master"

$ composer update

$ ./flow flow:cache:flush --force
$ ./flow doctrine:migrate
$ ./flow flow:cache:flush --force
```

### Installieren von weiteren Paketen

Wenn das Package auf Packagist (https://packagist.org) erhältlich ist, kann es wie folgt installiert werden:

```
composer require <vendor/package>

// z.B. 
composer require typo3/neos-googleanalytics
```

Wenn das Paket nicht auf Packagist ist, muss man folgenden Code in die Datei `composer.json` eintragen und anschließend `composer update` ausführen:

```
"repositories": [
    {
        "type": "git",
        "url": "git://github.com/acme/demo.git"
    },
    ...
],
...
"require": {
    ...,
    "acme/demo": "dev-master"
}
```
