# Gnome 3 und .Xmodmap-Autostart

Neuer Laptop, neue Probleme... 
Während bei meinem alten Lenovo X220i neben den Pfeiltasten die *Prev* und *Next*-Tasten liegen,
sind bei meinem neuen Lenovo T460s an der selben Stelle die *Bild*-Up/Down Tasten. Das nervt beim browsen im Web und im Filemanager.

Das Tool `xmodmap` bietet hier eine schnelle, einfache Lösung um die Tasten "umzumappen".
Dafür muss nur eine .Xmodmap-Datei angelegt werden. Die passenden Key-Codes kann man sich mit dem Tool `xev` anzeigen lassen.


    [mathias@mathias-t460s ~]% echo """
    keycode 112 = XF86Back
    keycode 117 = XF86Forward
    """ >> .Xmodmap


Leider wird die Datei nicht mehr automatisch geladen. Ein Autostart-Script muss also her.


	[mathias@mathias-t460s ~]% echo """
	sleep 5
	xmodmap /home/mathias/.Xmodmap
	""" > .loadXmodMap.sh
	[mathias@mathias-t460s ~]% chmod +x .loadXmodMap.sh



Als letzten Schritt muss man Gnome noch sagen das es dieses Script starten soll.


    [mathias@mathias-t460s ~]% echo """
    [Desktop Entry]
    Name=loadXmodMap
    GenericName=loadXmodMap
    Comment=Loads the .Xmodmap File
    Exec=/home/mathias/.loadXmodMap.sh
    Terminal=false
    Type=Application
    X-GNOME-Autostart-enabled=true
    """ > .config/autostart/loadXmodMap.desktop


Ziemlich frickelig, hoffentlich gibt es zukünftig eine schönere Lösung. Habe im Netz leider noch keine bessere Lösung gefunden. 

