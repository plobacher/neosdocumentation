# Eel Helper: Math

**Beschreibung:** Enthält mathematische Helper-Funktionen

**Implementierung:** `TYPO3\Eel\Helper\MathHelper`

**Datei:**
```
Packages/Framework/TYPO3.Eel/Classes/TYPO3/Eel/Helper/MathHelper.php
```

**Basis:** https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Math

**API:**

* `getE()`
Gibt die Euler-Konstante (ca. 2.718) zurück
* `getLN2()`
Gibt den natürlichen Logorithmus zur Basis 2 zurück (ca. 0.693)
* `getLN10()`
Gibt den natürlichen Logorithmus zur Basis 10 zurück (ca. 2.303)
* `getLOG2E()`
Gibt den Logorithmus E zur Basis 2 zurück (ca. 1.443)
* `getLOG10E()`
Gibt den Logorithmus E zur Basis 10 zurück (ca. 0.434)
* `getPI()`
Gibt die Kreiszahl PI zurück (ca. 3.14159)
* `getSQRT1_2()`
Gibt die Quadratwurzel von 0.5 zurück (ca. 0.707)
* `getSQRT2()`
Gibt die Quadratwurzel von 2 zurück (ca. 1.414)
* `abs($x = 'NAN')`
Gibt den Absolutwert einer Zahl zurück
* `acos($x)`
Gibt den Arcus-Kosinus einer Zahl (in Radiant) zurück
* `acosh($x)`
Gibt den Arcus-Kosinus-Hyperbolicus einer Zahl (in Radiant) zurück
* `asin($x)`
Gibt den Arcus-Sinus einer Zahl (in Radiant) zurück
* `asinh($x)`
Gibt den Arcus-Sinus-Hyperbolicus einer Zahl (in Radiant) zurück
* `atan($x)`
Gibt den Arcus-Tangens einer Zahl (in Radiant) zurück
* `atanh($x)`
Gibt den Arcus-Tangens-Hyperbolicus einer Zahl (in Radiant) zurück
* `atan2($y, $x)`
Arcus-Tangens mit zwei Parametern (Umrechnung Kartesiche- in Polar-Koordinaten)
* `cbrt($x)`
Gibt die dritte Wurzel zurück
* `ceil($x)`
Aufrunden: Liefert die nächste ganze Zahl, die größer oder gleich der angegebenen Zahl ist.
* `cos($x)`
Gibt den Kosinus einer Zahl zurück
* `cosh($x)`
Gibt den Kosinus-Hyperbolicus einer Zahl zurück
* `exp($x)`
Gibt die Exponential-Funktion (e^x) einer Zahl zurück
* `expm1($x)`
Gibt die Exponential-Funktion Minus 1 (e^x-1) einer Zahl zurück
* `floor($x)`
Abrunden: Liefert die nächste ganze Zahl, die kleiner oder gleich der angegebenen Zahl ist.
* `isFinite($x)`
Prüft, ob der übergebene Parameter $x ein gültiger endlicher Wert ist
* `isInfinite($x)`
Die Funktion prüft ob ein Wert unendlich, oder besser nicht-endlich ist
* `isNaN($x)`
Prüft ob der Parameter $x keine darstellbare Zahl ist, wie z.B. das Ergebnis von acos(1.01)
* `hypot($x, $y, $z_ = NULL)`
hypot() berechnet die Länge der Hypotenuse eines rechtwinkligen Dreiecks aus den Längen der beiden Katheten bzw. den Abstand eines Punktes (x,y) vom Ursprung. Dies entspricht sqrt(x*x + y*y)
* `log($x)`
Berechnet den natürlichen Logarithus zur Basis e einer Zahl
* `log1p($x)`
log1p() berechnet log(1 + $x) auf eine Weise die auch dann noch genaue Ergebnisse liefert wenn der Wert von number nur sehr klein ist. log() liefert in solchen Fällen auf Grund von Rundungsfehlern oft nur den Wert von log(1) und vernachlässigt die Nachkommastellen
* `log10($x)`
Berechnet den dekadischen Logarithmus von $x, d.h. den Logarithmus zur Basis 10
* `log2($x)`
Berechnet den Logarithmus von $x zur Basis 2
* `max($x = NULL, $y_ = NULL)`
Ist der erste und einzige Parameter ist ein Array, gibt max() den höchsten Wert dieses Arrays zurück. Sind mindestens zwei Parameter übergeben, gibt max() den größeren dieser Werte zurück
* `min($x = NULL, $y_ = NULL)`
Ist der erste und einzige Parameter ein Array, gibt min() den niedrigsten Wert dieses Arrays zurück. Sind mindestens zwei Parameter übergeben, gibt min() den kleinsten dieser Werte zurück
* `pow($x, $y)`
Berechnet die Potenz von $y zur Basis $x oder kurz $x^$y
* `random()`
Gibt eine Zufalls-Float-Zahl zwischen 0 und 1 zurück
* `randomInt($min, $max)`
Gibt eine Zufalls-Integer-Zahl zwischen $min und $max zurück
* `round($subject, $precision = 0)`
Rundet $subject mathematisch mit der angegebenen Genauigkeit $precision
* `sign($x)`
Gibt -1 zurück, wenn die Zahl $x negativ ist, +1, wenn sie positiv ist und 0, wenn sie 0 ist.
* `sin($x)`
Gibt den Sinus einer Zahl zurück
* `sinh($x)`
Gibt den Sinus-Hyperbolicus einer Zahl zurück
* `sqrt($x)`
Gibt die Quadratwurzel einer Zahl zurück
* `tan($x)`
Gibt den Tangens einer Zahl zurück
* `tanh($x)`
Gibt den Tangens-Hyperbolicus einer Zahl zurück
* `trunc($x)`
Gibt die Zahl ohne Dezimalstellen zurück


**Beispiel(e):**


```

```
