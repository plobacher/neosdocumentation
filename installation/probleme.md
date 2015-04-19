# Installationsprobleme

Dafür sorgen, dass nur passende Sourcen (und keine DEV-Sourcen) geladen werden:

https://gist.github.com/aertmann/d147aded4191ed23bef4

---

Sollte es zu Duplicate-Key Fehlern kommen, kann das folgende helfen:

```
./flow node:repair
./flow doctrine:update
```

Weitere Hilfe: https://review.typo3.org/37191

---

Wenn es zu Fehlern kommt, liegt es oftmals an Berechtigungsproblemen - daher immer Apache-Errorlog und PHP-Errorlog prüfen. Überprüfung der `open basedir` Direktive!

---

Nachschauen, ob das Verzeichnis `Libraries/mikey179` existiert.

---

Wenn die Meldung kommt, dass die Methode `contruct()` keine Parameter hat:

```
/Users/patricklobacher/Sites/neos110/TYPO3-Neos-1.1-Beta/Packages/Framework/TYPO3.Flow/Classes/TYPO3/Flow/Core/Bootstrap.php


// Context per Default reinschreiben
public function __construct($context="Development") {
```
---
Wenn eine Meldung kommt, dass `igbinary` in der falschen Version vorliegt.

```
/Users/patricklobacher/Sites/neos110/TYPO3-Neos-1.1-Beta/Packages/Framework/TYPO3.Flow/Classes/TYPO3/Flow/Cache/Frontend/VariableFrontend.php

// Zeile auskommentieren
$this->useIgBinary = extension_loaded('igbinary');
```

---
