# Eigene, neue Blog-Engine

## Problemstellung

Frei nach dem Motto lieber selber machen wenn es nichts fertiges, passendes gibt.
Bisher hatte ich Blogger von Google benutzt. Habe aber nach einer Lösung gesucht welche
nicht von externen Providern abhängig ist. Meine Anforderungen waren:

* Static-Sites, keine Abhängigkeiten serverseitigen Engines, Datenbanken
* Providerunabhängigkeit
* schnelles schreiben von Einträgen
* keine Clientseitige Software zum Rendern, es soll also möglich sein von überall her Artikel zu schreiben
* Einen Feed ala RSS

Blogsoftware, Anbieter und Static-Site-Generatoren gibt es wie Sand am Meer,
das was ich aber eigentlich gesucht habe, fand ich nicht also überlegte ich mir
ein eigenes kleines Konzept.

## Umsetzung

### Static-Sites

Ein Artikel besteht nur aus einem Markdown-File, so wie es auch bei den meisten SSG-Frameworks
der Fall ist. Da ich keine serverseitige Software zum Rendern verwenden will, muss ein
Markdown-Parser in Javascript her. Nach 10 Sekunden auf Github habe ich mich für
[markdown-js](https://github.com/evilstreak/markdown-js) entschieden.

### Providerunabhängigkeit

Momentan wird der Blog über Github-Pages serviert. Ein Umzug stellt aber kein Problem dar,
da nur ein einfacher, im Internet verfügbarer Webserver benötigt wird. Und wenn es im Notfall
der heimische Raspberry Pi mit einem `python -m SimpleHTTPServer` ist.

### Einträge, Blogartikel schreiben

Jeder neuer Post wird in einer extra Datei im `/articles`-Ordner gespeichert.
Die Metadaten wie `Autor`, `Datum`, `Titel` werden in einer `manifest.js` Datei im Root
Verzeichnis gehalten.

Ein Beispiel sieht wie folgt aus:


    [mathias@/blog]% tree
    .
    ├── article
    │   ├── latex_einzeiler.md
    │   └── neuer_blog.md
    ├── index.html
    └── manifest.js

    1 directory, 4 files

Die `index.html` liefert die gerenderten Artikel aus und ist der Einstiegspunkt
für den Browser. Ein Out-of-the-Box-Webserver sollte auch immer diese Datei standardmäßig
ausliefern. Die `manifest.js` Datei beschreibt alle Artikel und dient der `index.html`
zum aggregieren der Posts und kann auch zum einbinden in externe Webseiten genutzt werden.
Als Technologie wird hier `JsonP` verwendet, auf der anderen Seite muss nur die Funktion
`blogManifestResponse(response)` implementiert werden. Wobei die `response` ein Array von Blogartikeln ist.

Beispiel der `manifest.js`:


    [mathias@/blog]% cat manifest.js
    blogManifestResponse(
        [
            {
                "title": "LaTeX: hilfreiche Einzeiler",
                "filename": "article/latex_einzeiler.md",
                "hash": "latex_einzeiler",
                "author": "Mathias Perlet",
                "published": "26.06.2014"
            },
            {
                "title": "Neue Blog Software",
                "filename": "article/neuer_blog.md",
                "hash": "neuer_blog",
                "author": "Mathias Perlet",
                "published": "25.08.2015"
            },
        ]
    );


* `titel` wird in der Blogübersicht angezeigt
* `filename` zeigt auf die Markdown-Datei
* `hash` dient zur Addressierung für den Browser, wird in der URI angezeigt
* `author` falls mal einen Gastartikel gibt
* `published` sollte im Format DD.MM.YYYY sein, dient zur Sortierung der Artikel nach Erscheinungsdatum

### Wie geht es weiter?

Momentan ist das ganze noch sehr Alpha, funktionert aber bisher schon ganz gut.
Ich werde die `index.html` noch anpassen und auch die `manifest.js` etwas erweitern.
Und ja, aus mehr Dateien besteht dieses Projekt auch nicht :).

Diesen Blogartikel werde ich wohl auch noch ein paar mal überarbeiten und erweitern, wie ich Lust und Zeit habe.
Aber prinzipiell sollte schon mal ein kleiner Eindruck der Idee entstanden sein.

Bei Fragen und Anregungen findet ihr genug Kontaktmöglichkeiten auf
[mperlet.de](http://mperlet.de)




