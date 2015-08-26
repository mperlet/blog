# LaTeX: hilfreiche Einzeiler

Hier ein paar Zeilen LaTeX die ich hin und wieder in meinem Dokumenten verwende.

### Einrückungen nach Absätzen

    \parindent0pt

Im Dokument Header entfernt es die Einrückungen nach Absätzen.

### Abstände zwischen Aufzählungen

    \begin{itemize}
        \itemsep0em
        \item Item 1
        \item Item 2
    \end{itemize}

Verringert die Abstände zwischen Aufzählungen.

### Seitenzahl-Überschift im Inhaltsverzeichnis

    \tableofcontents
    \addtocontents{toc}{~\hfill\textbf{Seite}\par}

Fügt dem Inhaltsverzeichnis eine Seitenzahl Überschrift hinzu.

### Zeilenumbruch nach einem Paragraphen

    \paragraph{Ein Paragraph mit Zeilenumbruch} $\;$ \\


### Zeilenabstand

    \linespread{1.15}

Stellt den Zeilenabstand ein und wird im Dokumenten Header gesetzt.

### Außenabstände

    \usepackage{geometry}
    \geometry{a4paper, top=25mm, left=25mm, right=25mm, bottom=20mm,
    headsep=10mm, footskip=12mm}

Setzt die Außenabstände für Dokumente, wird im Dokumenden Header gesetzt.

### Inhaltsverzeichnis vergrößern / auf eine Seite

    \tableofcontents
    \addtocontents{toc}{\protect\enlargethispage{1cm}}

Vergrößert das Inhaltsverzeichnis um 1cm, hilfreich wenn  eins, zwei Zeilen auf die nächste Seite rutschen.
