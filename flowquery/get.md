# FlowQuery: get

**Beschreibung:** Gibt ein (nicht gewrapptes) Element aus dem Context. Wenn FlowQuery verwendet wird, ist das Resultat immer ein FlowQuery-Set. Mit der Operation `get()` kann man dies vom FlowQuery befreien. Wird kein Argument angegeben, erhält man den gesamten Context zurück, ansonsten das Element an der Stelle des Indexes, den man angibt. Existert der Index nicht, so wird NULL zurück gegeben

**Implementierung:** `TYPO3\Eel\FlowQuery\Operations\GetOperation`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/FlowQueryOperations/GetOperation.php
```

**Beispiel(e):**

Wenn man `get()` nicht verwendet, bekommt man beim direkten Zugriff eine Fehlermeldung

```
// Direkter Zugriff in Fluid mittels {test}
test = ${q(site).children('subpage')}

// Fehler: Catchable Fatal Error: Object of class TYPO3\Eel\FlowQuery\FlowQuery could not be converted to string in ...

// Zugriff mittels {test.properties.title}
${q(site).children('subpage').get(0)}

// Zugriff mittels {test.0.properties.title}
${q(site).children('subpage').get()}
```
