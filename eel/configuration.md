# Eel Helper: Configuration

**Beschreibung:** Enthält Configuration-Helper-Funktionen

**Implementierung:** `TYPO3\Eel\Helper\ConfigurationHelper`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/Helper/ConfigurationHelper.php
```

**API:**

* `setting($settingPath)`   
Liefert den Wert aus der Konfiguration (settings.yaml) am angegebenen Pfad zurück

**Beispiel(e):**


```
Configuration.setting('TYPO3.Flow.core.context') === 'Production'
Configuration.setting('Acme.Demo.speedMode') === 'light speed'

// Configuration/Settings.yaml
TYPO3:
  Flow:
    core:
      phpBinaryPathAndFilename: /usr/bin/php
      context: Production
    persistence:
      backendOptions:
        driver: pdo_mysql
```
