# Logo und Footer realisieren

## Logo richten

Um das Logo zu richten, können wir dieses wie folgt abändern:

```
<img src="../../../Public/Images/logo-01.svg" alt="">
```

Schöner wäre es aber, wenn der Alt-Text entsprechend gefüllt ist. Fügen wir hierzu im TypoScript das Site-Objekt ein:

```
...
body {
	...
	homepage = ${site}
	...
```

Nun können wir darauf aus dem Template zugreifen:

```
<img src="../../../Public/Images/logo-01.svg" alt="{homepage.properties.title}">
```

Nun müssen wir uns um die Verlinkung kümmern - dafür ersetzen wir den `<a>` durch einen ViewHelper:

```
<neos:link.node node="{homepage}" class="navbar-brand">
    <img src="../../../Public/Images/logo-01.svg" alt="{homepage.properties.title}">
</neos:link.node>
```

Allerdings kann dieser ViewHelper nicht ohne Weiteres aufgerufen werden, da per Default nur der Namespace `f:` registriert ist. Daher muss ganz oben ins Template noch eine weitere Namespace-Deklaration:

```
<!DOCTYPE html>
{namespace neos=TYPO3\Neos\ViewHelpers}
...
```

## Copyright ausgeben

Ganz unten links wollen wir das aktuelle Jahr als Copyright ausgeben. Dafür könnten wir das natürlich direkt ins Template schreiben. Unter Berücksichtigung, dass wir ein leistungsfähiges CMS haben, welches die Seite ausliefert, ist das natürlich keine besonders gute Idee.

Daher verlagern wir das Copyright prinzipiell ins Template in den Schlüssen `body`:

```
	...
	footer {
		copyright = '(c) 2014'
	}
	...
```

Die Ausgabe machen wir im Template wie folgt:

```
<footer class="brown-bg">
	<div class="container">
		<div class="row">
			<div class="col-sm-3">
				<p>{footer.copyright -> f:format.raw()}</p>
			</div>
			...
```

Tatsächlich ist dies aber immer noch nicht wirklich dynamisch - daher verwenden wir nun im TypoScript Eel und FlowQuery:

```
	copyright = ${'&copy; ' + Date.year(Date.now()) + ' by Little Bean Roastery'}
```


## Social Media Icons verlinken

Um die Social Media Icons zu verlinken, machen wir es uns zunutze, das Neos sich einer zentralen Konfigurationsdatei bedient. Dabei wird im Verzeichnis `Package/Site/Schulung.Website/Configuration/` nach einer Datei 'Settings.yaml' gesucht.

Legen wir daher diese Datei `Settings.yaml` mit dem nachfolgenden Inhalt an:

```
Schulung:
  Website:
    Sociallinks:
      Facebook: 'https://www.facebook.com/patrick.lobacher'
      Twitter: 'https://twitter.com/PatrickLobacher'
      Google: 'http://plus.google.com/105500420878314068694'
      Xing: 'http://www.xing.com/profile/Patrick_Lobacher
```

Achten Sie darauf, dass alle Einrückungen mit je zwei Leerzeichen gemacht werden.

Im TypoScript können wir nun diese Datei auslesen:

```
...
footer {
	...
	social {
        facebook = ${Configuration.setting('Schulung.Website.Sociallinks.Facebook')}
        twitter = ${Configuration.setting('Schulung.Website.Sociallinks.Twitter')}
        google = ${Configuration.setting('Schulung.Website.Sociallinks.Google')}
        xing = ${Configuration.setting('Schulung.Website.Sociallinks.Xing')}
    }
    ...
}

```

Nun können wir im Template darauf zugreifen:

```
...
<ul class="social">
	<li><a href="{footer.social.facebook}" class="icon-facebook"><span>Facebook</span></a></li>
	<li><a href="{footer.social.twitter}" class="icon-twitter"><span>Twitter</span></a></li>
	<li><a href="{footer.social.google}" class="icon-google-plus"><span>G+</span></a></li>
	<li><a href="{footer.social.xing}" class="icon-xing"><span>Xing</span></a></li>
</ul>
...
```


Eine weitere Möglichkeit ist, nur den Pfad zu den SocialMedia_Profilen anzugeben:

```
footer {
	social ${Configuration.setting('Schulung.Website.Sociallinks')}
}
```

Anschließend kann man wie folgt darauf zugreifen:

```
<ul class="social">
	<li><a href="{footer.social.Facebook}" class="icon-facebook"><span>Facebook</span></a></li>
  ...
</ul>
```
