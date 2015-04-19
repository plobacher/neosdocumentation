# Import einer Site

Zunächste einmal kopiert man die Site in das Verzeichnis `Site`:

```
cd /path/to/Neos/directory
cp /path/to/site/Inspiring.WorkshopPage Packages/Sites/.
```

Anschließend importiert man diese Site über die Kommandozeile und löscht den Cache:

```
./flow site:import --package-key Inspiring.WorkshopPage

./flow flow:cache:flush --force
```

Eine Anzeige alles Site erhält man über `./flow site:list`
