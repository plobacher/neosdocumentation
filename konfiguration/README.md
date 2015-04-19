# Konfiguration

TYPO3 Neos wird über YAML-Dateien konfiguriert. YAML ist eine vereinfachte Auszeichnungssprache (englisch markup language) zur Datenserialisierung, angelehnt an XML (ursprünglich) und an die Datenstrukturen in den Sprachen Perl, Python und C sowie dem in RFC 2822 vorgestellten E-Mail-Format. Zugleich ist YAML ein rekursives Akronym für „YAML Ain’t Markup Language“ (ursprünglich „Yet Another Markup Language“).

Wichtig ist insbesondere, dass die Einrückung innerhalb von YAML immer zwei Leerzeichen betragen muss. Hat man die Option auf der falschen Einrückungsebene, wird diese nicht ausgewertet.

Folgende Dateien spielen eine Rolle bei der Konfiguration:

* `Settings.yaml`
Einstellungen auf Application-Level
* `Objects.yaml`
Zusätzliche Objekt-Konfiguration
* `Routes.yaml`
Stellt Routing-Konfiguration für das MVC-Framework zur Verfügung
* `Views.yaml`
Kann verwendet werden, um die Auflösung der Views im MVC zu beinflussen
* `Policy.yaml`
Stellt die Konfiguration für das Security Framework zur Verfügung
* `Caches.yaml`
Stellt die Konfiguration für das Chaching Framework zur Verfügung

Diese kann man wie folgt auslesen:

```
$ ./flow configuration:listtypes
$ ./flow configuration:show --type Settings
```



## Referenz Configuration/Settings.yaml

Diese Datei wird als erste Konfigurationsdatei aufgerufen. Zu finden ist dort beispielsweise die Datenbank-Anbindung.

`[INSTALL-VERZEICHNIS]` = Installationsverzeichnis von TYPO3 Neos 

*    `TYPO3`
	  Basis-Schlüssel für alle TYPO3 Packages
* 
`TYPO3.Flow`
> Konfiguration für das `TYPO3.Flow` Package

### Flow.aop
  
`TYPO3.Flow.aop`
> Einstellung für das AOP (Aspect Oriented Programming) Framework

`TYPO3.Flow.aop.globalObjects`
> Globale AOP-Einstellungen

`TYPO3.Flow.aop.globalObjects.securityContext`
> Setzen der Security-Context-Klasse. Default-Wert: `TYPO3\Flow\Security\Context`

`TYPO3.Flow.aop.globalObjects.userInformation`
> Setzen der User-Information-Klasse. Default-Wert: `TYPO3\Neos\Service\UserService`
  
### Flow.compatibility

`TYPO3.Flow.compatibility`
> Kompatibilität-Einstellungen

`TYPO3.Flow.compatibility.uriBuilder`
> Einstellungen für den UriBuilder

`TYPO3.Flow.compatibility.uriBuilder.createRelativePaths`
> Angabe, ob relative Pfade erzeugt werden sollen. Default-Wert: `false`

`TYPO3.Flow.configuration`
> Einstellungen bzgl. der Konfiguration

`TYPO3.Flow.configuration.compileConfigurationFiles`
>  Angabe, ob die Konfigurations-Dateien kompliliert oder immer neu geparst werden sollen. Default-Wert: `false`

### Flow.core

`TYPO3.Flow.core`
> Konfiguration für den TYPO3 Flow Core

`TYPO3.Flow.core.context`
>  Angabe des Application-Context. Default: `Development`

`TYPO3.Flow.core.phpBinaryPathAndFilename`
> Pfad zum PHP CLI (Command Line) Executable. Default-Wert: `/usr/bin/php`

`TYPO3.Flow.core.subRequestEnvironmentVariables`
> Konfiguration der Subrequest-Umgebungsvariablen

`TYPO3.Flow.core.subRequestEnvironmentVariables.XDEBUG_CONFIG`
> Die Umgebungsvariable `XDEBUG_CONFIG` wird mit folgedem Wert gefüllt: `idekey=FLOW_SUBREQUEST remote_port=9001`

`TYPO3.Flow.core.subRequestPhpIniPathAndFilename`
>  Angabe eines alternativen PHP.ini Pfades für Subrequests. Default-Wert: `null`

### Flow.error

`TYPO3.Flow.error`
> Einstellungen für das Error-Handling

`TYPO3.Flow.error.exceptionHandler`
> Einstellungen für den Excpeption-Handler

`TYPO3.Flow.error.exceptionHandler.className`
>  Klassenname für den Exception-Handler. Default-Wert: `TYPO3\Flow\Error\DebugExceptionHandler`

`TYPO3.Flow.error.exceptionHandler.defaultRenderingOptions`
> Default-Rendering-Optionen

`TYPO3.Flow.error.exceptionHandler.defaultRenderingOptions.renderTechnicalDetails`
> Rendern der technischen Informationen (Nachricht und Code). Default-Wert: `false`. Im Development-Kontext auf `true` gesetzt.

`TYPO3.Flow.error.exceptionHandler.defaultRenderingOptions.logException`
> Angabe, ob Exceptions in das Logfile (`Data/Logs/Exceptions`) geschrieben werden sollen. Default-Wert: `true`. 

`TYPO3.Flow.error.exceptionHandler.renderingGroups`
> Konfiguration von Rendering-Groups (mit deren Hilfe man individuelle Templates rendern kann).

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions` 
> Konfiguration für den Fehler "Seite nicht gefunden"

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.matchingStatusCodes` 
> Status-Code für den der Fehler gelten soll. Default-Wert: `- 404` (Array)

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options`                     
> Weitere Optionen.

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.logException`
> Angabe, ob diese Exception geloggt werden soll. Default-Wert: false

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.templatePathAndFilename`                             
> Pfad zum Fehler-Template (View). Default-Wert: `'resource://TYPO3.Neos/Private/Templates/Error/Index.html'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.variables`               
> Variablen, die an den View übergeben werden

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.variables.errorDescription`
> Fehlermeldung. Default-Wert: `'Sorry, the page you requested was not found.'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.variables.errorTitle`
> Fehlertitel. Default-Wert: `'Page Not Found'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.layoutRootPath`
> Layout-Root-Pfad. Default-Wert: `'resource://TYPO3.Neos/Private/Layouts/'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.notFoundExceptions.options.format`
> Format für den View. Default-Wert: `html`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions`
> Konfiguration für den Fehler: "Datenbank-Verbindung gestört"

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.matchingExceptionClassNames`
> Klassenname für den Fehler. Default-Wert: `- TYPO3\Flow\Persistence\Doctrine\Exception\DatabaseException` (Array)

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options`
> Weitere Optionen.

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.templatePathAndFilename`                        
> Pfad zum Fehler-Template (View). Default-Wert: `'resource://TYPO3.Neos/Private/Templates/Error/Index.html'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.variables` 
> Variablen, die an den View übergeben werden

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.variables.errorDescription`
> Fehlermeldung. Default-Wert: `'Sorry, we detected an error with your database. Check your logfiles in Data/Logs/* for more information.'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.variables.errorTitle`
> Fehlertitel. Default-Wert: `'Database Error'` 

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.variables.setupMessage`
>  Setup-Nachricht. Default-Wert: ` 'You might want to configure or check your database configuration in the setup.'` 

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.layoutRootPath`
> Layout-Root-Pfad. Default-Wert: `'resource://TYPO3.Neos/Private/Layouts/'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.databaseConnectionExceptions.options.format`
> Format für den View. Default-Wert: `html`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException`
> Konfiguration für den Fehler: "Homepage fehlt"  

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.matchingExceptionClassNames`
> Klassenname für den Fehler. Default-Wert: `- TYPO3\Neos\Routing\Exception\NoHomepageException` (Array)  

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options`
> Weitere Optionen.  

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.templatePathAndFilename`                        
> Pfad zum Fehler-Template (View). Default-Wert: `'resource://TYPO3.Neos/Private/Templates/Error/Index.html'`  

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.layoutRootPath`
> Layout-Root-Pfad. Default-Wert: `'resource://TYPO3.Neos/Private/Layouts/'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.format`
> Format für den View. Default-Wert: `html`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.variables` 
> Variablen, die an den View übergeben werden

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.variables.errorDescription`
> Fehlermeldung. Default-Wert: `'Either no site has been defined yet or the site does not contain a homepage.'`

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.variables.errorTitle`
> Fehlertitel. Default-Wert: `'Missing Homepage'` 

`TYPO3.Flow.error.exceptionHandler.renderingGroups.noHomepageException.options.variables.setupMessage`
> Setup-Nachricht. Default-Wert: ` 'You might want to create or import a site in the setup.'` 

`TYPO3.Flow.error.errorHandler`
> Einstellungen für den Error-Handler

`TYPO3.Flow.error.errorHandler.exceptionalErrors`
> Error-Codes, die behandelt werden. Default-Wert: `['%E_USER_ERROR%', '%E_RECOVERABLE_ERROR%', '%E_WARNING%', '%E_NOTICE%', '%E_USER_WARNING%', '%E_USER_NOTICE%', '%E_STRICT%']`

### Flow.http

`TYPO3.Flow.http`
> Einstellung hinsichtlich des HTTP-Handlings

`TYPO3.Flow.http.baseUri`
> Angabe der Base-URL. Default-Wert: `null`

`TYPO3.Flow.http.chain`
> Konfiguration der HTTP-Chain (bestehend aus Routing, Dispatching, ...)

`TYPO3.Flow.http.chain.preprocess`
> Angaben zum Preprocessing der HTTP-Requests

`TYPO3.Flow.http.chain.preprocess.position`
> Position in der Chain. Default-Wert: `'before process'`

`TYPO3.Flow.http.chain.preprocess.chain`
> Sub-Chain Angaben. Default-Wert: `{  }`

`TYPO3.Flow.http.chain.process`
> Angaben zum Prozess

`TYPO3.Flow.http.chain.process.chain`
> Sub-Chain im Prozess

`TYPO3.Flow.http.chain.process.chain.routing`
> Routing-Informationen

`TYPO3.Flow.http.chain.process.chain.routing.position`
> Position in der Chain. Default-Wert: `'start'`

`TYPO3.Flow.http.chain.process.chain.routing.component`
> Klassenname der Komponente.Default-Wert: `TYPO3\Flow\Mvc\Routing\RoutingComponent`              

`TYPO3.Flow.http.chain.process.chain.dispatching`
> Dispatching-Informationen

`TYPO3.Flow.http.chain.process.chain.dispatching.component`
> Klassenname der Komponente.Default-Wert: `TYPO3\Flow\Mvc\DispatchComponent` 

`TYPO3.Flow.http.chain.process.chain.ajaxWidget`
> Informationen zum Ajax-Widget

`TYPO3.Flow.http.chain.process.chain.ajaxWidget.position`
> Position in der Chain. Default-Wert: `'before routing'`

`TYPO3.Flow.http.chain.process.chain.ajaxWidget.component`
> Klassenname der Komponente.Default-Wert: `TYPO3\Fluid\Core\Widget\AjaxWidgetComponent`     

`TYPO3.Flow.http.chain.postprocess`
> Angaben zum Proprocessing der HTTP-Requests

`TYPO3.Flow.http.chain.postprocess.chain`
> Sub-Chain Angaben.

`TYPO3.Flow.http.chain.postprocess.chain.standardsCompliance`
> Angaben zum Standards-Compliance Mode des HTTP-Responses

`TYPO3.Flow.http.chain.postprocess.chain.standardsCompliance.position`
> Position in der Chain. Default-Wert: `'end'`

`TYPO3.Flow.http.chain.postprocess.chain.standardsCompliance.component`
> Klassenname der Komponente. Default-Wert: `TYPO3\Flow\Http\Component\StandardsComplianceComponent` 

### TYPO3.Flow.Log

`TYPO3.Flow.log`
> Einstellungen zum Logging

`TYPO3.Flow.log.systemLogger`
> Einstellungen des System Loggers

`TYPO3.Flow.log.systemLogger.logger`
> Zugehörige Logger-Klasse. Default-Wert: `TYPO3\Flow\Log\Logger`

`TYPO3.Flow.log.systemLogger.backend`
> Zugehöriges Backend. Default-Wert: `TYPO3\Flow\Log\Backend\FileBackend`

`TYPO3.Flow.log.systemLogger.backendOptions`
> Optionen des Logger-Backends

`TYPO3.Flow.log.systemLogger.backendOptions.logFileURL`
> Pfad des Logfiles. Default-Wert: `/[INSTALL-VERZEICHNIS]/Data/Logs/`System_Development.log

`TYPO3.Flow.log.systemLogger.backendOptions.createParentDirectories`
> Angabe, ob Elternverzeichnise angelegt werden dürfen. Default-Wert: `true`

`TYPO3.Flow.log.systemLogger.backendOptions.severityThreshold`
> Severity-Threshold. Default-Wert: `7`

`TYPO3.Flow.log.systemLogger.backendOptions.maximumLogFileSize`
> Maximale Größe des Logfiles in Bytes. Default-Wert: `10485760` (Entspricht 10 MB)

`TYPO3.Flow.log.systemLogger.backendOptions.logFilesToKeep`
> Anzahl Logfiles, die aufbewahrt werden. Default-Wert: `1`

`TYPO3.Flow.log.systemLogger.backendOptions.logMessageOrigin`
> Mitloggen, wer den Log-Eintrag ausgelöst hat. Default-Wert: `false`

`TYPO3.Flow.log.securityLogger`
> Einstellungen des System Loggers

`TYPO3.Flow.log.securityLogger.backend`
> Zugehöriges Backend. Default-Wert: `TYPO3\Flow\Log\Backend\FileBackend`

`TYPO3.Flow.log.securityLogger.backendOptions`
> Optionen des Logger-Backends

`TYPO3.Flow.log.securityLogger.backendOptions.logFileURL`
> Pfad des Logfiles. Default-Wert: `/[INSTALL-VERZEICHNIS]/Data/Logs/Security_Development.log

`TYPO3.Flow.log.securityLogger.backendOptions.createParentDirectories`
> Angabe, ob Elternverzeichnise angelegt werden dürfen. Default-Wert: `true`

`TYPO3.Flow.log.securityLogger.backendOptions.severityThreshold`
> Severity-Threshold. Default-Wert: `7`

`TYPO3.Flow.log.securityLogger.backendOptions.maximumLogFileSize`
> Maximale Größe des Logfiles in Bytes. Default-Wert: `10485760` (Entspricht 10 MB)

`TYPO3.Flow.log.securityLogger.backendOptions.logFilesToKeep`
> Anzahl Logfiles, die aufbewahrt werden. Default-Wert: `1`

`TYPO3.Flow.log.securityLogger.backendOptions.logIpAddress`
> IP-Adresse mitloggen. Default-Wert: `true`

`TYPO3.Flow.log.sqlLogger`
> Einstellungen des System Loggers

`TYPO3.Flow.log.sqlLogger.backend`
> Zugehöriges Backend. Default-Wert: `TYPO3\Flow\Log\Backend\FileBackend`

`TYPO3.Flow.log.sqlLogger.backendOptions`
> Optionen des Logger-Backends

`TYPO3.Flow.log.sqlLogger.backendOptions.logFileURL`
> Pfad des Logfiles. Default-Wert: `/[INSTALL-VERZEICHNIS]/Data/Logs/Query_Development.log

`TYPO3.Flow.log.sqlLogger.backendOptions.createParentDirectories`
> Angabe, ob Elternverzeichnise angelegt werden dürfen. Default-Wert: `true`

`TYPO3.Flow.log.sqlLogger.backendOptions.severityThreshold`
> Severity-Threshold. Default-Wert: `7`

`TYPO3.Flow.log.sqlLogger.backendOptions.maximumLogFileSize`
> Maximale Größe des Logfiles in Bytes. Default-Wert: `10485760` (Entspricht 10 MB)

`TYPO3.Flow.log.sqlLogger.backendOptions.logFilesToKeep`
> Anzahl Logfiles, die aufbewahrt werden. Default-Wert: `1`

### TYPO3.Flow.i18n

`TYPO3.Flow.i18n`
> Einstellungen zur Internationalisierung

`TYPO3.Flow.i18n.defaultLocale`
> Default Locale Einstellungen. Default-Wert: `en`

`TYPO3.Flow.i18n.fallbackRule`
> Fallback-Regeln

`TYPO3.Flow.i18n.fallbackRule.strict`
> Strict. Default-Wert: `false`

`TYPO3.Flow.i18n.fallbackRule.order`
> Reihenfolge. Default-Wert: `{  }`

### TYPO3.Flow.object

`TYPO3.Flow.object`
> Generelle Einstellungen zum Objekt-Handling

`TYPO3.Flow.object.registerFunctionalTestClasses`
> Angabe, ob funtionelle Test-Klassen registriert werden sollen. Default-Wert: `false`

`TYPO3.Flow.object.excludeClasses`
> Angabe der Klassen, die exkludiert werden sollen. Default-Wert:
```
  'Doctrine.*':
    - '.*'
  'doctrine.*':
    - '.*'
  'symfony.*':
    - '.*'
  'phpunit.*':
    - '.*'
  mikey179.vfsStream:
    - '.*'
  Composer.Installers:
    - '.*'
  imagine.imagine:
    - 'Imagine\\Test\\.*'
```

### TYPO3.Flow.package

`TYPO3.Flow.package`
> Angaben zum Package-Handling

`TYPO3.Flow.package.inactiveByDefault`
> Per Default inaktive Packages. Default-Wert: `- Composer.Installers` (Array)

`TYPO3.Flow.package.packagesPathByType`
> Pfad-Typ Zuordnung. Default-Wert:
```
  typo3-flow-package: Application
  typo3-flow-framework: Framework
  typo3-flow-site: Sites
  typo3-flow-plugin: Plugins
```

### TYPO3.Flow.persistence 

`TYPO3.Flow.persistence`
> Angaben zur Persistence-Schicht

`TYPO3.Flow.persistence.backendOptions`
> Einstellungen des Backendends

`TYPO3.Flow.persistence.backendOptions.driver`
> Datenbank-Treiber. Default-Wert: `pdo_mysql`

`TYPO3.Flow.persistence.backendOptions.host`
> Datenbank-Host. Default-Wert: `[DB_HOST]`

`TYPO3.Flow.persistence.backendOptions.dbname`
> Datenbank-Host. Default-Wert: `[DB_DBNAME]`

`TYPO3.Flow.persistence.backendOptions.user`
> Datenbank-Host. Default-Wert: `[DB_USER]`

`TYPO3.Flow.persistence.backendOptions.password`
> Datenbank-Host. Default-Wert: `[DB_PASSWORD]`

`TYPO3.Flow.persistence.backendOptions.charset`
> Datenbank-Host. Default-Wert: `utf8`

`TYPO3.Flow.persistence.cacheAllQueryResults`
> Angabe, ob die Query-Resultate gecached werden sollen. Default-Wert: `false`

`TYPO3.Flow.persistence.doctrine`
> Einstellungen zur Persistenz-Schicht "Doctrine"

`TYPO3.Flow.persistence.doctrine.enable`
> Angabe, ob Doctrine verwendet werden soll. Default-Wert: `true`

`TYPO3.Flow.persistence.doctrine.sqlLogger`
> Angabe des SQL-Loggers. Default-Wert: `null`

`TYPO3.Flow.persistence.doctrine.eventListeners`
> Konfiguration der Event-Listener. Default-Wert:
```
  TYPO3\Media\Domain\EventListener\ImageEventListener:
    events:
      - prePersist
      - preUpdate
      - postRemove
    listener: TYPO3\Media\Domain\EventListener\ImageEventListener
  TYPO3\Neos\Domain\EventListener\AccountPostEventListener:
    events:
      - postPersist
      - postUpdate
      - postRemove
    listener: TYPO3\Neos\Domain\EventListener\AccountPostEventListener
```

###TYPO3.Flow.reflection

`TYPO3.Flow.reflection`
>  Angaben zur Reflektion (Auswerten der Doc-Comments @tags in Annotations)

`TYPO3.Flow.reflection.ignoredTags`
> Doc-Comments Tags, die von der Reflektion ignoriert werden. Default-Wert:
```
  - api
  - package
  - subpackage
  - license
  - copyright
  - author
  - const
  - see
  - todo
  - scope
  - fixme
  - test
  - expectedException
  - expectedExceptionMessage
  - expectedExceptionCode
  - depends
  - dataProvider
  - group
  - codeCoverageIgnore
  - requires
  - Given
  - When
  - Then
  - BeforeScenario
  - AfterScenario
  - fixtures
  - Isolated
  - AfterFeature
  - BeforeFeature
  - BeforeStep
  - AfterStep
  - WithoutSecurityChecks
```

`TYPO3.Flow.reflection.logIncorrectDocCommentHints` 
> Angabe, ob inkorrekte Doc-Comments geloggt werden sollen. Default-Wert: `false`

### TYPO3.Flow.resource 
       
`TYPO3.Flow.resource`
> Angaben zum Resource-Handling

`TYPO3.Flow.resource.publishing`
> Konfiguration zum Publizieren von Ressourcen

`TYPO3.Flow.resource.publishing.detectPackageResourceChanges`
> Angabe, ob Änderungen an Ressourcen bemerkt werden sollen. Default-Wert: `true`

`TYPO3.Flow.resource.publishing.fileSystem` 
> Konfiguration des Datei-Systems

`TYPO3.Flow.resource.publishing.mirrorMode`
> Mirror-Mode. Default-Wert: `link`

### TYPO3.Flow.security 

`TYPO3.Flow.security`
> Einstellungen für das Sicherheits-Framework

`TYPO3.Flow.security.enable`
> Angabe, ob das Sicherheitsframework aktiviert ist. Default-Wert: `true`

`TYPO3.Flow.security.firewall`
> Konfiguration der Firewall

`TYPO3.Flow.security.firewall.rejectAll`
> Angabe, ob alle Verbindungen zurückgewiesen werden sollen. Default-Wert: `false`

`TYPO3.Flow.security.firewall.filters`
> Konfiguration der Filter. Default-Wert:
```
  -
    patternType: CsrfProtection
    patternValue: null
    interceptor: AccessDeny
```

`TYPO3.Flow.security.authentication` 
> Einstellungen zur Authentifizierung

`TYPO3.Flow.security.authentication.providers`
> Konfiguration der Authentifizierungsprovider

`TYPO3.Flow.security.authentication.providers.Typo3SetupProvider`
> Konfiguration des TYPO3-Setup Provides. Default-Wert:
```
  Typo3SetupProvider:
    provider: FileBasedSimpleKeyProvider
    providerOptions:
      keyName: SetupKey
      authenticateRoles:
        - 'TYPO3.Setup:Administrator'
    requestPatterns:
      controllerObjectName: 'TYPO3\Setup\Controller\.*|TYPO3\Setup\ViewHelpers\Widget\Controller\.*'
    entryPoint: WebRedirect
    entryPointOptions:
      uri: setup/login
```

`TYPO3.Flow.security.authentication.providers.Typo3BackendProvider`
> Konfiguration des TYPO3-Backend Provides. Default-Wert:
```
  provider: PersistedUsernamePasswordProvider
  requestPatterns:
    controllerObjectName: 'TYPO3\Neos\Controller\.*|TYPO3\Neos\Service\.*|TYPO3\Media\Controller\.*'
  entryPoint: WebRedirect
  entryPointOptions:
    routeValues:
      '@package': TYPO3.Neos
      '@controller': Login
      '@action': index
      '@format': html
```

`TYPO3.Flow.security.authentication.authenticationStrategy`
> Authentifizierungsstrategie. Default-Wert: `oneToken`
            
`TYPO3.Flow.security.authorization`
> Konfiguration der Authorisierung

`TYPO3.Flow.security.authorization.accessDecisionVoters`
> Klassen, die das Voting für die Authorisierung übernehmen. Default-Wert: `- TYPO3\Flow\Security\Authorization\Voter\Policy` (Array)
`TYPO3.Flow.security.authorization.allowAccessIfAllVotersAbstain`  
  Zugang zulassen, wenn Voter verichten. Default-Wert: `false`

`TYPO3.Flow.security.csrf`
> Konfiguration für den CSFR (Cross-Site-Request-Forgery) Schutz

`TYPO3.Flow.security.csrf.csrfStrategy`
> CSFR-Strategie. Default-Wert: `onePerSession`

`TYPO3.Flow.security.cryptography::
> Kryptographische Konfigurationen

`TYPO3.Flow.security.cryptography.hashingStrategies:: 
> Strategie für das (normale) Hashing. Default-Wert:
```
  default: bcrypt
  fallback: pbkdf2
  pbkdf2: TYPO3\Flow\Security\Cryptography\Pbkdf2HashingStrategy
  bcrypt: TYPO3\Flow\Security\Cryptography\BCryptHashingStrategy
  saltedmd5: TYPO3\Flow\Security\Cryptography\SaltedMd5HashingStrategy
```

`TYPO3.Flow.security.cryptography.Pbkdf2HashingStrategy::  
> Konfiguration für das PBKDF2 (Password-Based Key Derivation Function 2) Hashing                  
```
  dynamicSaltLength: 8
  iterationCount: 10000
  derivedKeyLength: 64
  algorithm: sha256
```

`TYPO3.Flow.security.cryptography.BCryptHashingStrategy:: 
> Konfiguration für das bcrypt Hashing. Default-Wert:
```
  cost: 14
```

`TYPO3.Flow.security.cryptography.RSAWalletServicePHP::                 :
> Konfiguration für den RSA-Wallet-Service. Default-Wert:
```
  keystorePath: /Users/patricklobacher/Sites/neos120/TYPO3-Neos-1.2/Data/Persistent/RsaWalletData
  openSSLConfiguration: {  }
```
  
### TYPO3.Flow.session
 
`TYPO3.Flow.session`
> Konfiguration des Sessions-Handlings

`TYPO3.Flow.session.inactivityTimeout`
> Timeout ins Sekunden bei Inaktivität. Default-Wert: `3600` (entspricht 1h)

`TYPO3.Flow.session.name`
> Name der Session. Default-Wert: `TYPO3_Flow_Session`

`TYPO3.Flow.session.garbageCollection`
> Konfiguration der Garbage Collection

`TYPO3.Flow.session.garbageCollection.probability`
> Angabe in % wann die Garbage Collection anspringt. Default-Wert: `30`

`TYPO3.Flow.session.garbageCollection.maximumPerRun`
> Anzahl Objekte, die pro Durchlauf entsorgt werden. Default-Wert: `1000`

`TYPO3.Flow.session.cookie`
> Konfiguration des Session-Cookies

`TYPO3.Flow.session.cookie.lifetime`
> Lifetime des Session-Cookies. Default-Wert: `0` (Cookie ist aktiv, bis Browser-Fenster geschlossen wird)

`TYPO3.Flow.session.cookie.path`
> Der Pfad der Domain, in dem das Cookie zu Verfügung steht. Default-Wert: `/` (gilt für alle Pfade der Domain)

`TYPO3.Flow.session.cookie.secure`
> Angabe, ob das Cookie nur über sichere Verbindungen gesendet wird. Default-Wert: `false` 

`TYPO3.Flow.session.cookie.httponly`
> Angabe, ob PHP versuchen soll, das httponly-Flag zu senden wenn das Session-Cookie gesetzt wird. Default-Wert: `true` 
`TYPO3.Flow.session.cookie.domain`
> Die Cookie-Domain. Damit die Cookies auf allen Subdomains zur Verfügung stehen, muss der Domain wie in ein Punkt vorangestellt werden. Default-Wert: `null` 

### TYPO3.Flow.utility

`TYPO3.Flow.utility`
> Konfiguration für die Utility-Klassen.

`TYPO3.Flow.utility.environment`
> Konfiguration der Umgebung

`TYPO3.Flow.utility.environment.temporaryDirectoryBase`
> Pfad zum Temp-Verzeichnis. Default-Wert: `[INSTALL-VERZEICHNIS]/Data/Temporary/`

`TYPO3.Flow.utility.environment.lockStrategyClassName`
> Klassenname für das Handling der FLOCK-Strategie. Default-Wert: `TYPO3\Flow\Utility\Lock\FlockLockStrategy`
  
### TYPO3.Form

`TYPO3.Form`
> Konfiguration für das TYPO3 Form Package

`TYPO3.Form.yamlPersistenceManager`
> Angaben zur Persistierung der Formulare

`TYPO3.Form.yamlPersistenceManager.savePath`
> Pfad, unter der die Formulare zu finden sind. Default-Wert: `'resource://TYPO3.NeosDemoTypo3Org/Private/Form/'` (aus dem Demo-Paket)

`TYPO3.Form.supertypeResolver`
> Konfiguration der Supertype-Resolver

`TYPO3.Form.supertypeResolver.hiddenProperties`
> Angabe der versteckten Formular-Felder. Default-Wert: `{ }`

`TYPO3.Form.presets`
> Vorgaben

`TYPO3.Form.presets.default`
> Default-Vorgaben (können von speziellen überschrieben werden). Default-Wert:
```
  // Titel des Formular
  title: Default
  // Spezielle Stylesheets
  stylesheets: {  }
  // Spezielle JavaScripte
  javaScripts: {  }
  // Formular-Elemente
  formElementTypes:
    // Base-Typ. Gilt für alle Elemente
    'TYPO3.Form:Base':
      // Angaben, wo Templates, Partials und Layouts zu finden sind
      renderingOptions:
        templatePathPattern: 'resource://{@package}/Private/Form/{@type}.html'
        partialPathPattern: 'resource://{@package}/Private/Form/Partials/{@type}.html'
        layoutPathPattern: 'resource://{@package}/Private/Form/Layouts/{@type}.html'
        skipUnknownElements: false
        translationPackage: TYPO3.Flow
    // <form> Element
    'TYPO3.Form:Form':
      // Erbt vom Base-Typ
      superTypes:
        - 'TYPO3.Form:Base'
      rendererClassName: TYPO3\Form\Core\Renderer\FluidFormRenderer
      renderingOptions:
        renderableNameInTemplate: form
    'TYPO3.Form:RemovableMixin': {  }
    'TYPO3.Form:ReadOnlyFormElement':
      superTypes:
        - 'TYPO3.Form:Base'
        - 'TYPO3.Form:RemovableMixin'
      implementationClassName: TYPO3\Form\FormElements\GenericFormElement
      renderingOptions:
        renderableNameInTemplate: element
    // Generelles Formular-Element
    'TYPO3.Form:FormElement':
      superTypes:
        - 'TYPO3.Form:Base'
        - 'TYPO3.Form:RemovableMixin'
      implementationClassName: TYPO3\Form\FormElements\GenericFormElement
      properties:
        containerClassAttribute: input
        elementClassAttribute: ''
        elementErrorClassAttribute: error
      renderingOptions:
        renderableNameInTemplate: element
    'TYPO3.Form:Page':
      superTypes:
        - 'TYPO3.Form:Base'
        - 'TYPO3.Form:RemovableMixin'
      implementationClassName: TYPO3\Form\Core\Model\Page
      renderingOptions:
        renderableNameInTemplate: page
    'TYPO3.Form:PreviewPage':
      superTypes:
        - 'TYPO3.Form:Page'
    'TYPO3.Form:Section':
      superTypes:
        - 'TYPO3.Form:FormElement'
      implementationClassName: TYPO3\Form\FormElements\Section
      renderingOptions:
      renderableNameInTemplate: section
    'TYPO3.Form:TextMixin': {  }
    'TYPO3.Form:SingleLineText':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:TextMixin'
    'TYPO3.Form:Password':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:TextMixin'
    'TYPO3.Form:PasswordWithConfirmation':
      superTypes:
        - 'TYPO3.Form:Password'
      implementationClassName: TYPO3\Form\FormElements\PasswordWithConfirmation
      properties:
        elementClassAttribute: input-medium
        confirmationLabel: Confirmation
        confirmationClassAttribute: input-medium
    'TYPO3.Form:MultiLineText':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:TextMixin'
      properties:
        elementClassAttribute: xxlarge
    'TYPO3.Form:SelectionMixin': {  }
    'TYPO3.Form:SingleSelectionMixin':
      superTypes:
        - 'TYPO3.Form:SelectionMixin'
    'TYPO3.Form:MultiSelectionMixin':
      superTypes:
        - 'TYPO3.Form:SelectionMixin'
    'TYPO3.Form:Checkbox':
      superTypes:
        - 'TYPO3.Form:FormElement'
      properties:
        elementClassAttribute: add-on
        value: 1
    'TYPO3.Form:MultipleSelectCheckboxes':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:MultiSelectionMixin'
    'TYPO3.Form:MultipleSelectDropdown':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:MultiSelectionMixin'
      properties:
        elementClassAttribute: xlarge
    'TYPO3.Form:SingleSelectRadiobuttons':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:SingleSelectionMixin'
    'TYPO3.Form:SingleSelectDropdown':
      superTypes:
        - 'TYPO3.Form:FormElement'
        - 'TYPO3.Form:SingleSelectionMixin'
    'TYPO3.Form:DatePicker':
      superTypes:
        - 'TYPO3.Form:FormElement'
      implementationClassName: TYPO3\Form\FormElements\DatePicker
      properties:
        elementClassAttribute: small
        timeSelectorClassAttribute: mini
        dateFormat: Y-m-d
        enableDatePicker: true
        displayTimeSelector: false
    'TYPO3.Form:FileUpload':
      superTypes:
        - 'TYPO3.Form:FormElement'
      implementationClassName: TYPO3\Form\FormElements\FileUpload
      properties:
        allowedExtensions:
          - pdf
          - doc
    'TYPO3.Form:ImageUpload':
      superTypes:
        - 'TYPO3.Form:FormElement'
      implementationClassName: TYPO3\Form\FormElements\ImageUpload
      properties:
        allowedTypes:
          - jpeg
          - png
          - bmp
    'TYPO3.Form:StaticText':
      superTypes:
        - 'TYPO3.Form:ReadOnlyFormElement'
      properties:
        text: ''
    'TYPO3.Form:HiddenField':
      superTypes:
        - 'TYPO3.Form:FormElement'
  // Konfiguration der Finisher
  finisherPresets:
    'TYPO3.Form:Closure':
      implementationClassName: TYPO3\Form\Finishers\ClosureFinisher
      options: {  }
    'TYPO3.Form:Confirmation':
      implementationClassName: TYPO3\Form\Finishers\ConfirmationFinisher
      options: {  }
    'TYPO3.Form:Email':
      implementationClassName: TYPO3\Form\Finishers\EmailFinisher
      options: {  }
    'TYPO3.Form:FlashMessage':
      implementationClassName: TYPO3\Form\Finishers\FlashMessageFinisher
      options: {  }
    'TYPO3.Form:Redirect':
      implementationClassName: TYPO3\Form\Finishers\RedirectFinisher
      options: {  }
    // Konfiguration der Validatoren
    validatorPresets:
      'TYPO3.Flow:NotEmpty':
        implementationClassName: TYPO3\Flow\Validation\Validator\NotEmptyValidator
      'TYPO3.Flow:DateTimeRange':
        implementationClassName: TYPO3\Flow\Validation\Validator\DateTimeRangeValidator
      'TYPO3.Flow:Alphanumeric':
        implementationClassName: TYPO3\Flow\Validation\Validator\AlphanumericValidator
      'TYPO3.Flow:Text':
        implementationClassName: TYPO3\Flow\Validation\Validator\TextValidator
      'TYPO3.Flow:StringLength':
        implementationClassName: TYPO3\Flow\Validation\Validator\StringLengthValidator
      'TYPO3.Flow:EmailAddress':
        implementationClassName: TYPO3\Flow\Validation\Validator\EmailAddressValidator
      'TYPO3.Flow:Integer':
        implementationClassName: TYPO3\Flow\Validation\Validator\IntegerValidator
      'TYPO3.Flow:Float':
        implementationClassName: TYPO3\Flow\Validation\Validator\FloatValidator
      'TYPO3.Flow:NumberRange':
        implementationClassName: TYPO3\Flow\Validation\Validator\NumberRangeValidator
      'TYPO3.Flow:RegularExpression':
        implementationClassName: TYPO3\Flow\Validation\Validator\RegularExpressionValidator
      'TYPO3.Flow:Count':
        implementationClassName: TYPO3\Flow\Validation\Validator\CountValidator
```

`TYPO3.form.presets.typo3.setup`
> Spezielle Konfiguration für das TYPO3 Setup Formular. Default-Wert:
```
  title: 'Setup Elements'
  parentPreset: default
  formElementTypes:
    'TYPO3.Form:Base':
      renderingOptions:
        layoutPathPattern: 'resource://TYPO3.Setup/Private/Form/Layouts/{@type}.html'
    'TYPO3.Form:Form':
      renderingOptions:
        templatePathPattern: 'resource://TYPO3.Setup/Private/Form/{@type}.html'
    'TYPO3.Setup:LinkElement':
      superTypes:
        - 'TYPO3.Form:ReadOnlyFormElement'
      properties:
        text: ''
        class: btn
        href: ''
    'TYPO3.Setup:DatabaseSelector':
      superTypes:
        - 'TYPO3.Form:FormElement'
      properties:
        elementClassAttribute: form-control
    'TYPO3.Form:SingleLineText':
      properties:
        elementClassAttribute: form-control
    'TYPO3.Form:Password':
      properties:
        elementClassAttribute: form-control
    'TYPO3.Form:PasswordWithConfirmation':
      renderingOptions:
        templatePathPattern: 'resource://TYPO3.Setup/Private/Form/{@type}.html'
      properties:
        elementClassAttribute: form-control
        confirmationClassAttribute: form-control
    'TYPO3.Form:Checkbox':
      renderingOptions:
        templatePathPattern: 'resource://TYPO3.Setup/Private/Form/{@type}.html'
      properties:
        elementClassAttribute: checkbox
    'TYPO3.Form:MultipleSelectDropdown':
      properties:
        elementClassAttribute: form-control
    'TYPO3.Form:SingleSelectDropdown':
      renderingOptions:
        templatePathPattern: 'resource://TYPO3.Setup/Private/Form/{@type}.html'  
```

`TYPO3.form.presets.bootstrap`
> Spezielle Konfiguration für das Bootstrap Formular. Default-Wert:
```
  title: 'Twitter bootstrap'
  parentPreset: default
  formElementTypes:
    'TYPO3.Form:Base':
      renderingOptions:
        layoutPathPattern: 'resource://TYPO3.NeosDemoTypo3Org/Private/Templates/ContactForm/{@type}.html'
    'TYPO3.Form:FormElement':
      properties:
        elementClassAttribute: form-control
    'TYPO3.Form:MultiLineText':
      properties:
        elementClassAttribute: form-control
```

### TYPO3.DocTools

`TYPO3.DocTools`
> Konfiguration des DocTools Packages

`TYPO3.DocTools.bundles`
> Konfiguration der Bundles

`TYPO3.DocTools.bundles.Form`
> Konfiguration des Bundles "Form". Default-Wert:
```
  documentationRootPath: [INSTALL-VERZEICHNIS]/Packages/Application/TYPO3.Form/Documentation/Guide/source
  renderedDocumentationRootPath: [INSTALL-VERZEICHNIS]/Data/Temporary/Documentation/Form
  configurationRootPath: [INSTALL-VERZEICHNIS]/Packages/Application/TYPO3.Form/Documentation/Guide/source
  imageRootPath: [INSTALL-VERZEICHNIS]/Packages/Application/TYPO3.Form/Documentation/Guide/Images/
```

`TYPO3.DocTools.bundles.Neos`
> Konfiguration des Bundles "Neos". Default-Wert:
```
  documentationRootPath: [INSTALL-VERZEICHNIS]/Packages/Application/TYPO3.Neos/Documentation/
  configurationRootPath: [INSTALL-VERZEICHNIS]/Packages/Application/TYPO3.DocTools/Resources/Private/Themes/TYPO3/
  renderedDocumentationRootPath: [INSTALL-VERZEICHNIS]/Data/Temporary/Documentation/TYPO3.Neos/
  renderingOutputFormat: html
  renderByDefault: false
```

### TYPO3.Imagine

`TYPO3.Imagine`
> Konfiguration der Image-Bibliothek "Imagine"

`TYPO3.Imagine.driver`
> Treiber für die Bilderzeugung. Default-Wert: `Gd`

`TYPO3.Imagine.profile`
> Profile für die Bilderzeugung. Default-Wert:
```
  RGB: color.org/sRGB_IEC61966-2-1_black_scaled.icc
  CMYK: Adobe/CMYK/USWebUncoated.icc
  Grayscale: colormanagement.org/ISOcoated_v2_grey1c_bas.ICC
```
    
### TYPO3.Media

`TYPO3.Media`
> Konfiguration des Media-Packages

`TYPO3.Media.image`
> Einstellungen für die Bilder

`TYPO3.Media.image.defaultOptions`
> Default Einstellungen

`TYPO3.Media.image.defaultOptions.quality`
> Qualität der erzeugten Bilder. Default-Wert: `90`

`TYPO3.Media.bodyClasses`
> Body-Klassen. Default-Wert: `'neos neos-module media-browser'`

`TYPO3.Media.scripts`
> JavaScripte die geladen werden. Default-Wert:
```
  - 'resource://TYPO3.Neos/Public/Library/jquery/jquery-2.0.3.js'
  - 'resource://TYPO3.Neos/Public/Library/bootstrap-components.js'
```

`TYPO3.Media.styles`
> Stylesheets die geladen werden. Default-Wert:
```
  - 'resource://TYPO3.Media/Public/Libraries/plupload/jquery.plupload.queue/css/jquery.plupload.queue.css'
  - 'resource://TYPO3.Media/Public/Styles/Main.css'
  - 'resource://TYPO3.Neos/Public/Styles/Neos.css'
  - 'resource://TYPO3.Media/Public/Styles/Main.css'
```

### TYPO3.Neos

`TYPO3.Neos`
> Konfiguration des TYPO3 Neos Packages

`TYPO3.Neos.typoScript`
> Einstellungen hinsichtlich TypoScript

`TYPO3.Neos.typoScript.autoInclude`
> Aus den folgenden Packages wird automatisch das zugehörige TypoScript (Datei: `Resources/Private/TypoScript/Root.ts2`) inkludiert. Default-Wert:
```
  TYPO3.Media: true
  TYPO3.TypoScript: true
  TYPO3.Neos: true
  TYPO3.Neos.NodeTypes: true
```

`TYPO3.Neos.typoScript.enableObjectTreeCache`
> Angabe, ob TypoScript-Objekte gecached werden sollen. Default-Wert: `false`

`TYPO3.Neos.nodeTypes`
> Einstellungen für die NodeTypes des New-NodeType-Element Wizards

`TYPO3.Neos.nodeTypes.groups`
> Einstellungen für die NodeType-Gruppen

`TYPO3.Neos.nodeTypes.general`
> Einstellungen für die Gruppe "normal"
```
  position: start
  label: General
```

`TYPO3.Neos.nodeTypes.structure`
> Einstellungen für die Gruppe "structure"
```
  position: 100
  label: Structure
```

`TYPO3.Neos.nodeTypes.plugins`
> Einstellungen für die Gruppe "plugins"
```
  position: 200
  label: Plugins
```

`TYPO3.Neos.userInterface`
> Einstellungen des User Interfaces

`TYPO3.Neos.userInterface.loadMinifiedJavascript`
> Angabe, ob das JavaScript im User Interface minifiziert werden soll. Default-Wert: `true`

`TYPO3.Neos.userInterface.requireJsPathMapping`
> Mapping für require.js. Default-Wert:
```
  TYPO3.Neos/Validation: 'resource://TYPO3.Neos/Public/JavaScript/Shared/Validation/'
  TYPO3.Neos/Inspector/Editors: 'resource://TYPO3.Neos/Public/JavaScript/Content/Inspector/Editors/'
```

`TYPO3.Neos.userInterface.navigateComponent`
> Einstellungen der Navigationskomponente (links im User Interface)

`TYPO3.Neos.userInterface.navigateComponent.nodeTree`
> Einstellung des Node-Baumes

`TYPO3.Neos.userInterface.navigateComponent.nodeTree.loadingDepth`
> Anzahl Level, die beim Start geladen werden. Default-Wert: `4`

`TYPO3.Neos.userInterface.navigateComponent.nodeTree.presets`
> Vorgaben für den Node-Baum

`TYPO3.Neos.userInterface.navigateComponent.nodeTree.presets.default`
> Default Vorgaben für den Node-Baum                   

`TYPO3.Neos.userInterface.navigateComponent.nodeTree.presets.default.baseNodeType`
> Basis-Node-Type (beim Erstellen). Default-Wert: `'TYPO3.Neos:Document'`

`TYPO3.Neos.userInterface.inspector`
> Konfiguration des Inspektors (rechte Seite im User Interface)

`TYPO3.Neos.userInterface.inspector.dataTypes`
> Konfiguration der verfügbaren Daten-Typen. Default-Wert:
```
  string:
    editor: TYPO3.Neos/Inspector/Editors/TextFieldEditor
  integer:
    editor: TYPO3.Neos/Inspector/Editors/TextFieldEditor
  boolean:
    editor: TYPO3.Neos/Inspector/Editors/BooleanEditor
  array:
    editor: TYPO3.Neos/Inspector/Editors/SelectBoxEditor
    editorOptions:
      multiple: true
      placeholder: Choose
  TYPO3\Media\Domain\Model\ImageVariant:
    editor: TYPO3.Neos/Inspector/Editors/ImageEditor
    editorOptions:
      maximumFileSize: null
      crop:
        aspectRatio:
          options:
            square:
              width: 1
              height: 1
              label: Square
            fourFive:
              width: 4
              height: 5
            fiveSeven:
              width: 5
              height: 7
            twoThree:
              width: 2
              height: 3
            fourThree:
              width: 4
              height: 3
            sixteenNine:
              width: 16
              height: 9
          enableOriginal: true
          allowCustom: true
          locked:
            width: 0
            height: 0
    TYPO3\Media\Domain\Model\Asset:
      editor: TYPO3.Neos/Inspector/Editors/AssetEditor
    array<TYPO3\Media\Domain\Model\Asset>:
      editor: TYPO3.Neos/Inspector/Editors/AssetEditor
      editorOptions:
        multiple: true
    date:
      editor: TYPO3.Neos/Inspector/Editors/DateTimeEditor
      editorOptions:
        format: d-m-Y
    reference:
      editor: TYPO3.Neos/Inspector/Editors/ReferenceEditor
    references:
      editor: TYPO3.Neos/Inspector/Editors/ReferencesEditor
```

`TYPO3.Neos.userInterface.editPreviewModes`
> Konfiguration der PreviewModes (obere Seite im User Interface). Default-Wert:
```
  inPlace:
    isEditingMode: true
    isPreviewMode: false
    typoScriptRenderingPath: ''
    title: In-Place
    position: 100
  rawContent:
    isEditingMode: true
    isPreviewMode: false
    typoScriptRenderingPath: rawContent
    title: 'Raw Content'
    position: 200
  desktop:
    isEditingMode: false
    isPreviewMode: true
    typoScriptRenderingPath: ''
    title: Desktop
    position: 100
  print:
    isEditingMode: false
    isPreviewMode: true
    typoScriptRenderingPath: print
    title: Print
    position: 200
```

`TYPO3.Neos.moduleConfiguration`
> Konfiguration der User Interface Module

`TYPO3.Neos.moduleConfiguration.widgetTemplatePathAndFileName`
> Pfad zum Widget-Template. Default-Wert: `'resource://TYPO3.Neos/Private/Templates/Module/Widget.html'`

`TYPO3.Neos.modules`
> Spezielle Konfiguration der einzelnen Module. Default-Wert:
```
  management:
    label: Management
    controller: \TYPO3\Neos\Controller\Module\ManagementController
    description: 'Contains multiple modules related to management of content'
    icon: icon-briefcase
    resource: TYPO3_Neos_Backend_Module_Management
  submodules:
    workspaces:
      label: Workspaces
      controller: \TYPO3\Neos\Controller\Module\Management\WorkspacesController
      description: 'This module contains the overview of all elements within the current workspace and it enables to continue the review and publishing workflow for them.'
      icon: icon-th-large
      resource: TYPO3_Neos_Backend_Module_Management_Workspaces
    media:
      label: Media
      controller: \TYPO3\Neos\Controller\Module\Management\AssetController
      description: 'This module allows managing of media assets including pictures, videos, audio and documents.'
      icon: icon-camera
      resource: TYPO3_Neos_Backend_Module_Media_ManageAssets
    administration:
      label: Administration
      controller: \TYPO3\Neos\Controller\Module\AdministrationController
      description: 'Contains multiple modules related to administration'
      icon: icon-gears
      resource: TYPO3_Neos_Backend_Module_Administration
      submodules:
        users:
          label: 'User Management'
          controller: \TYPO3\Neos\Controller\Module\Administration\UsersController
          description: 'The User Management module provides you with an overview of all backend users. You can group them by their properties so you are able to monitor their permissions, filemounts, member groups etc.. This module is an indispensable tool in order to make sure the users are correctly configured.'
          icon: icon-group
          actions:
            new:
              label: 'Create user'
              title: 'Create a new user'
              resource: TYPO3_Neos_Backend_Module_Administration_Users
        packages:
          label: 'Package Management'
          controller: \TYPO3\Neos\Controller\Module\Administration\PackagesController
          description: 'The Package Management module provides you with an overview of all packages. You can activate and deactivate individual packages, import new packages and delete existing packages. It also provides you with the ability to freeze and unfreeze packages in development context.'
          icon: icon-archive
          resource: TYPO3_Neos_Backend_Module_Administration_Packages
        sites:
          label: 'Sites Management'
          controller: \TYPO3\Neos\Controller\Module\Administration\SitesController
          description: 'The Sites Management module provides you with an overview of all sites. You can edit, add and delete information about your sites, such as adding a new domain.'
          icon: icon-globe
          actions:
            newSite:
              label: 'Create site'
              title: 'Create a new site'
              resource: TYPO3_Neos_Backend_Module_Administration_Sites
        configuration:
          label: Configuration
          controller: \TYPO3\Neos\Controller\Module\Administration\ConfigurationController
          description: 'The Configuration module provides you with an overview of all configuration types.'
          icon: icon-list-alt
          resource: TYPO3_Neos_Backend_Module_Administration_Configuration
    user:
      label: User
      controller: \TYPO3\Neos\Controller\Module\UserController
      hideInMenu: true
      resource: TYPO3_Neos_Backend_Module_User
      submodules:
        usersettings:
        label: 'User Settings'
        controller: \TYPO3\Neos\Controller\Module\User\UserSettingsController
        description: 'This module allows you to customize your backend user profile. Here you can change your active system language, name and email address. You may also configure other general features in the system.'
        icon: icon-user
        resource: TYPO3_Neos_Backend_Module_User_UserSettings
```

### TYPO3.Twitter

`TYPO3.Twitter`
> Konfiguration des Twitter Packages

`TYPO3.Twitter.Bootstrap`
> Konfiguration des Twitter Bootstrap Packages

`TYPO3.Twitter.viewHelpers`
> Einstellungen für die ViewHelper

`TYPO3.Twitter.viewHelpers.partialRootPath`
> Pfad für die Partials, die in den ViewHelpern verwendet werden. Default-Wert: `'resource://TYPO3.Twitter.Bootstrap/Private/Partials/'`

`TYPO3.Twitter.viewHelpers.templates`
> Mapping: Templates/ViewHelpers. Default-Wert:
```
  TYPO3\Twitter\Bootstrap\ViewHelpers\Navigation\MenuViewHelper: 'resource://TYPO3.Twitter.Bootstrap/Private/Templates/Navigation/Menu.html'
```

### TYPO3.Setup

`TYPO3.Setup`
> Konfiguration für das Setup Package

`TYPO3.Setup.initialPasswordFile`
> Position der initialen Passwort-Datei. Default-Wert: `[INSTALL-VERZEICHNIS]/Data/SetupPassword.txt

`TYPO3.Setup.stepOrder`
> Reihenfolge der Setup-Stufen. Default-Wert:
```
  - database
  - administrator
  - siteimport
  - final
```

`TYPO3.Setup.steps`
> Konfiguration der spezifischen Stufen. Default-Wert:
```
  database:
    className: TYPO3\Setup\Step\DatabaseStep
    requiredConditions:
      -
        className: TYPO3\Setup\Condition\PdoDriverCondition
  final:
    className: TYPO3\Neos\Setup\Step\FinalStep
  administrator:
    className: TYPO3\Neos\Setup\Step\AdministratorStep
    requiredConditions:
      -
        className: TYPO3\Setup\Condition\DatabaseConnectionCondition
  siteimport:
    className: TYPO3\Neos\Setup\Step\SiteImportStep
      requiredConditions:
        -
          className: TYPO3\Setup\Condition\DatabaseConnectionCondition
```

`TYPO3.Setup.view`
> Einstellungen für den View

`TYPO3.Setup.view.title`
> Titel für den View. Default-Wert: `'TYPO3 Neos Setup'`

`TYPO3.Setup.http`
> Einstellungen für den HTTP-Handler

`TYPO3.Setup.http.chain`
> Einstellungen für die HTTP-Chain

`TYPO3.Setup.http.chain.preprocess`
> Einstellungen für den HTTP-Chain Propozessor

`TYPO3.Setup.http.chain.preprocess.configureRouting`
> Einstellungen für das Routing

`TYPO3.Setup.http.chain.preprocess.configureRouting.position`
> Position des Routings

`TYPO3.Setup.http.chain.preprocess.configureRouting.component`
> Klasse für das Handling. Default-Wert: `TYPO3\Setup\Core\ConfigureRoutingComponent`
  
### TYPO3.TYPO3CR

`TYPO3.TYPO3CR`
> Konfiguration für das TYPO3 Content Repository

`TYPO3.TYPO3CR.contentDimensions`
> Konfiguration der Content-Dimensionen

`TYPO3.TYPO3CR.contentDimensions.language`
> Konfigurationn der Content-Dimension "language" (Sprache). Default-Wert:
```
  default: en_US
  defaultPreset: en_US
  presets:
    all: null
    en_US:
      label: 'English (US)'
      values:
        - en_US
      uriSegment: en
    en_UK:
      label: 'English (UK)'
      values:
        - en_UK
        - en_US
      uriSegment: uk
    de:
      label: German
      values:
        - de
        - en_UK
        - en_US
      uriSegment: de
    fr:
      label: French
      values:
        - fr
        - de
        - en_US
      uriSegment: fr
    nl:
      label: Dutch
      values:
        - nl
        - en_US
      uriSegment: nl
    dk:
      label: Danish
      values:
        - dk
        - en_US
      uriSegment: dk
    lv:
      label: Latvian
      values:
        - lv
        - en_US
      uriSegment: lv
```

`TYPO3.TYPO3CR.labelGenerator`
> Einstellungen für den Label-Generator

`TYPO3.TYPO3CR.labelGenerator.eel`
> Spezifische Einstellungen für Eel

`TYPO3.TYPO3CR.labelGenerator.eel.defaultContext`
> Einstellungen des Default-Kontextes. Default-Wert:
```  
  String: TYPO3\Eel\Helper\StringHelper
  Array: TYPO3\Eel\Helper\ArrayHelper
  Date: TYPO3\Eel\Helper\DateHelper
  Configuration: TYPO3\Eel\Helper\ConfigurationHelper
  Math: TYPO3\Eel\Helper\MathHelper
  Json: TYPO3\Eel\Helper\JsonHelper
```

### TYPO3.TypoScript

`TYPO3.TypoScript`
> Konfiguration des TYPO3 TypoScript Packages

`TYPO3.TypoScript.rendering`
> Konfiguration für das Rendering. Default-Wert:
```
  exceptionHandler: TYPO3\TypoScript\Core\ExceptionHandlers\ThrowingHandler
  innerExceptionHandler: TYPO3\TypoScript\Core\ExceptionHandlers\BubblingHandler
```

`TYPO3.TypoScript.debugMode`
> Angabe, ob der Debug-Mode eingeschaltet werden soll. Default-Wert: `false`

`TYPO3.TypoScript.enableContentCache`
> Angabe, ob der Content-Cache eingeschaltet werden soll. Default-Wert: `true`

`TYPO3.TypoScript.defaultContext`
> Konfiguration des Default-Kontextes. Default-Wert:
```
  String: TYPO3\Eel\Helper\StringHelper
  Array: TYPO3\Eel\Helper\ArrayHelper
  Date: TYPO3\Eel\Helper\DateHelper
  Configuration: TYPO3\Eel\Helper\ConfigurationHelper
  Math: TYPO3\Eel\Helper\MathHelper
  Json: TYPO3\Eel\Helper\JsonHelper
  Neos.Node: TYPO3\Neos\TypoScript\Helper\NodeHelper
  Neos.Link: TYPO3\Neos\TypoScript\Helper\LinkHelper
```


#### Beispiel:
```
TYPO3:
  Flow:
    core:
      phpBinaryPathAndFilename: /usr/bin/php
    persistence:
      backendOptions:
        driver: pdo_mysql
        dbname: neos110b1
        user: root
        password: geheimespasswort
        host: 127.0.0.1
```
