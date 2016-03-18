# Google-Docs Diagramme verlustfrei exportieren

Mich hat es schon lange stört das man bei Google-Docs Diagramme nur als .png exportieren kann. Mit diesem Umweg ist es möglich die Diagramme als .pdf zu speichern.
Der Vorteil ist, dass hier keine Rasterung vorgenommen wird, die Grafiken sind also verlustfrei!

### Schritt 1

Tabelle mit Diagramm in Google-Docs öffnen und die Developer Console öffnen (STRG+SHIFT+I). Dann unter *Elements* das `<svg>`-Tag suchen und markieren. Das Kästchen links oben kann bei der suche helfen.
![](https://dl.dropboxusercontent.com/content_link/ENSN4sZervgnadb9fXIXVXggq7VaeEeAo7nw57TWbVCryQYbaHWAky9PJu2uxboJ/file)

Das markierte Tag in die Zwischenablage kopieren (STRG+C) und in einen beliebigen Editor einfügen. 

### Schritt 2

Die Datei als `chart.svg` speichern und danach mit

```
inkscape -A chart.pdf chart.svg
```

konvertieren. Inkscape ist eine von vielen Möglichkeiten, ich habe es benutzt da es in den Fedora Repos enthalten ist.
