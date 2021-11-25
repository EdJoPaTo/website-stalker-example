Ich benutze schon seit vielen Jahren Zsh statt Bash in meinen Desktop Setups.
Dabei habe ich dann direkt Oh My Zsh verwendet.
Irgendwann habe ich mal hinterfragt, ob ich Oh My Zsh wirklich brauche und nein, ohne ist das ganze nachvollziehbarer.

Warum Zsh und kein Bash?
==========

Auf meinen Desktop Geräten habe ich mich daran gewöhnt, einige Zsh Features zu nutzen, wie das durchsuchen der history mit Pfeiltasten, und zwar basierend auf der aktuellen Eingabe.
Wenn ich gerade in einem Git Projekt bin und arbeite, sind die letzten Commands alle `git …`.
Wenn ich jetzt mal eben die Musik anpassen will, dann kann ich `mpc` eingeben und einmal Pfeil nach oben drücken.
Jetzt geht es nur noch durch die History Einträge passend zu `mpc`.
Wenn ich das [readme des Zsh plugins](https://github.com/zsh-users/zsh-history-substring-search) richtig deute, ist das ein default Feature des fish Shell, also vielleicht auch mal einen Blick wert.

Die Features die ich von Zsh nutze, sind eher Kleinigkeiten als alle “das große Feature”.
Zum Beispiel kann man mit Bash auch Strg + R drücken und die history durchsuchen.
Das Feature existiert also auch, nur nicht ganz so komfortabel.

Auf Servern / Remote Umgebungen verwende ich aber kein Zsh, sondern die default Konfiguration der Shell, die mit dem OS kommt (also überall Bash).
Ich nutze auf Servern meist eh nur Skripte und dafür brauche ich keine weiteren Features.

Oh My Zsh
==========

Oh My Zsh ist ein Projekt mit dem Ziel, die Konfiguration von Zsh zu vereinfachen.
Das habe ich mal gemacht und Jahre später lief das noch.

Allerdings bringt Oh My Zsh auch so manche Skripte selbst mit, die dann bei jedem Öffnen einer Shell ausgeführt werden.
Und wenn man sich diese genauer anschaut, braucht man das meiste davon eigentlich garnicht.

Das gute ist aber, dass Oh My Zsh komplett mit Zsh arbeitet, sprich alle Skripte (.zsh Dateien) sind nur Scripte, die auch ohne Oh My Zsh von Zsh ausgeführt werden können.
Man kann also selber eine Zsh Konfiguration bauen und dann Oh My Zsh Plugins bei sich herein laden und sie werden funktionieren.

Eigene Konfiguration
==========

Als Basis habe ich [ChrisTitusTech/zsh](https://github.com/ChrisTitusTech/zsh) verwendet, da diese zu Beginn eine kleine Basis hatte, die mir schon mal grundlegend gefiel und von der ich ausgehen konnte.
Basierend darauf habe ich angefangen anzupassen.
Und das ist wohl etwas, das man selber machen muss.
Feststellen was fehlt einem und ergänzen.
Ich habe beispielsweise [meine Konfiguration](https://github.com/EdJoPaTo/LinuxScripts/tree/master/Applications/zsh) auf macOS und Arch Linux am Laufen, weshalb ich einige Sonderfälle abdecken muss.
Andererseits brauche ich einige Plugins nicht, die ChrisTitusTech verwendet.
Ich habe mich auch mehrfach an anderen Konfigurationen inspirieren lassen, die so an mir vorbei kamen, wie beispielsweise die [aliase von leyrer](https://github.com/leyrer/linux-home/blob/master/zshrc).

Meine Konfiguration ist seit einiger Zeit fast unverändert, nur noch die Aliase ändern sich von Zeit zu Zeit, welche wohl noch viel persönlicher sind.
Da versuche ich aber den Weg zu gehen, nicht `git push` zu `gp` zu machen oder solche Art von aliassen, da ich dann anderen Leuten schlechter helfen kann (oder auf meinen Servern plötzlich nachdenken muss, wie etwas geht).
Tippen kann ich schnell genug und da geht `git push` auch fix in eine geübte Handlung über.
Dinge die ich seltener benutze und eh jedes mal nachschauen müsste, packe ich jedoch wieder in einen alias (ffmpeg zum Beispiel).

Fazit
==========

Alles in allem verstehe ich nun mehr, was eigentlich beim Starten einer neuen Shell passiert.
Vieles von Oh My Zsh hat mich nicht weiter gebracht und ich habe ein deutlich simpleres Setup.

Wenn ihr auch eure eigene Konfiguration habt, lasst es mich gern wissen, dann kann ich mich von euch auch inspirieren lassen und meine weiter Optimieren.
