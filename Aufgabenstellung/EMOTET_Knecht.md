# Emotet

Eine Zusammenfassung zur Malware Emotet am Beispiel der Heise Mediengruppe von [Pascal Knecht](pascal.knecht@juventus.schule) für das Fach Hacking Exposed.


## Überblick

[Emotet](https://en.wikipedia.org/wiki/Emotet) ist eine Schadsoftware, die sich im Moment wohl primär per Mail und Word-Dokumente mit Makros verbreitet.

Durch gezieltes [Spear Phishing](https://en.wikipedia.org/wiki/Phishing#Spear_phishing) werden existierende Email-Kommunikationsverläufe aufgegriffen, um dadurch die Chance zu erhöhen, ein neues Opfer zu infizieren. Neue Opfer bringen dann wiederum neue Emailverläufe, sodass sich Emotet effektiv von Unternehmen zu Unternehmen durchhangeln kann.

Emotet selbst fungiert als sogenannter [Dropper](https://en.wikipedia.org/wiki/Dropper_(malware)) und lädt weitere Schadsoftware wie TrickBot respektive die [Ransomware](https://de.wikipedia.org/wiki/Ransomware) Ryuk nach erfolgreicher Infektion nach.


## Emotet am Beispiel der Heise Mediengruppe

Mitte 2019 wurde Heise mit der Schadsoftware Emotet infiziert. Konkret war zwar nicht die Heise Onlineredaktion oder die c't betroffen aber deren Schwester- und Mutterunternehmen, die Heise Medien Gruppe. Wie bei Emotet üblich, wurde eine Email mit einem Word-Dokument von extern an einen internen Mitarbeiter gesendet. Das Email kam von einem Hotel, welches eine Geschäftsbeziehung mit der Heise Mediengruppe hat, und bezog sich auf eine Übernachtung eines Heise-Mitarbeitenden. Durch diesen Spear-Phishing-Ansatz erschien das Email für das Opfer sehr glaubwürdig.

Im Word-Dokumentanhang befand sich ein eingebettetes Makro. Der Mitarbeiter aktivierte Makros, wodurch weitere Schadsoftware aus dem Internet nachgeladen und sein Computer mit Emotet infiziert wurde. Das war der erste Fehler.

Von diesem Rechner verbreitet sich Emotet dann weiter im gesamten Netzwerk und befall circa 100 Rechner. Diese Ausbreitung war unter anderem dadurch möglich, dass Emotet mit den User Credentials eines Domänen-Administrators arbeiten konnte. Wie genau Emotet im Falle Heises an das Passwort gekommen ist, ist nicht eindeutig geklärt. Vermutet wird, dass der entsprechende Admin dem User helfen wollte und sich lokal mit dem Domänen-Admin Passwort angemeldet hat. Das ist der zweite schwerwiegende Fehler.

Da sich die infizierten Rechner zu einem [Command-and-Control-Server](https://de.wikipedia.org/wiki/Botnet#Command-and-Control-Technik) im Internet verbanden, fiel den Administratoren bald auf, dass etwas im Netzwerk nicht stimmte. Sie reagierten schnell, wodurch der grosse Schaden ausblieb. Zwei Tage nach der Infektion wurde die Sachlage richtig eingeschätzt und der Lock-Down des gesamten Heise Netzwerkes verordnet. Ab diesem Zeitpunkt gab es kein Internet mehr für alle Mitarbeiter und die gesamte Infrastruktur wurde in einem neu eingerichteten, separaten Netzwerk neu aufgebaut. Rechner um Rechner mussten geprüft und ins neue Netz gezügelt werden.

Eine grössere Infizierung oder Lösegeldforderung blieb damit aus. Heise ging von Anfang an sehr transparent mit dem Problem um, was in der Nachbetrachtung den Reputationsschaden sicherlich schmälert.


## Abwehrmassnahmen

-   Word-Dokumente mit inkludierten Makros sollten grundsätzlich nicht verschickt werden, da sie immer wieder als Dropper für Erstinfektionen eingesetzt werden. Einige Mailsecurity Gateways erlauben es, Office-Dokumente mit Makros zu erkennen und beispielsweise in eine Quarantäne zu verschieben. Durch diese technische Massnahme kommen potentielle Dateianhänge mit aktiven Inhalten gar nicht erst in das eigene Netzwerk hinein.

-   Eingehende Emails können von einem Mailsecurity Gateway auch im Subject durch ein Tag für intern und extern ergänzt werden. Dadurch kann der empfangende Mitarbeiter sofort sehen, ob ein Mail eines Kollegen von intern oder aus dem Internet über einen gekaperten Mailserver verschickt wurde.

-   Schulung aller Mitarbeitenden wie mit Office-Dokumenten aus nicht vertrauenswürdiger Quelle umzugehen ist. Es muss allen Mitarbeitenden bewusst sein, dass es keine absolute Sicherheit gibt und Sicherheit eher als Prozess zu verstehen ist, an welchem jeder Einzelne mit beteiligt ist.

-   Restriktive Firewall-Policy die ein- und ausgehend nur benötigte Verbindungen zulässt und das Netzwerk in unterschiedliche Zonen aufteilt. Durch eine Segmentierung des Netzwerks werden Zugriffe aus verschiedenen Teilnetzen untereinander erschwert, was eine mögliche Ausbreitung erschweren kann.

-   Lokale Administratorenrechte sollen nicht erlaubt sein, alle User arbeiten mit eingeschränkten Rechten, auch Administratoren. Erweiterte Rechte sind nur einigen wenigen Personen erlaubt, die erweiterte Informatikkenntnisse insbesondere auch im Bereich IT-Security aufweisen. Dadurch wird es einer Schadsoftware möglichst erschwert, sich weiter im Netzwerk auszubreiten.

-   Offline Backups sind in diesem Fall sinnvoll, weil Emotet online Backups gezielt sucht und löscht, damit die Chance einer erfolgreichen Lösegeldforderung steigt.


## Quellen

-   [Heise c't: Trojaner-Befall: Emotet bei Heise](https://www.heise.de/ct/artikel/Trojaner-Befall-Emotet-bei-Heise-4437807.html=)
-   [Logbuch Netzpolitik: LNP321 Verluste durch außergewöhnliche Schadensfälle](https://logbuch-netzpolitik.de/lnp321-verluste-durch-aussergewoehnliche-schadensfaelle)
