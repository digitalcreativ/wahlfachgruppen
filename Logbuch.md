# Logbuch zum Leistungsnachweis

## Projekt: Digitale Einteilung der Wahlfachgruppen 2. Oberstufe

**Ausbildung:** CAS Bildung im digitalen Wandel – KI-Modul  
**Projektkontext:** Schulen Baar, 2. Oberstufe, Schuljahr 2026/27  
**Verfasserin:** Claudia Bürgisser  
**Projektbeginn:** Anfang Oktober 2026  
**Bearbeitungsstand:** 16. November 2026

> Hinweis: Die früheren Entwicklungsschritte wurden anhand des aktuellen Projektstands und der vorhandenen Dateien rückblickend zusammengefasst. Die späteren Einträge dokumentieren die Anpassungen aus der laufenden Erprobung. Frühere Regeln und Testergebnisse beschreiben den damaligen Stand; die aktuell gültigen Vorgaben sind in Abschnitt 6 zusammengefasst.

## 1. Ausgangslage und Zielsetzung

Die Einteilung der Schülerinnen und Schüler in die Wahlfachgruppen der 2. Oberstufe ist anspruchsvoll. Neben den Fachwünschen müssen Gruppengrössen, Klassen, Schulhäuser sowie die Trennung von Real und Sek berücksichtigt werden. Eine manuelle Einteilung ist zeitaufwendig und fehleranfällig.

Ziel meines Projekts war deshalb die Entwicklung eines einfachen digitalen Werkzeugs, das aus vorhandenen Schülerlisten automatisch einen Vorschlag für die Wahlfachgruppen erstellt. Das Werkzeug sollte ohne Installation und ohne Übertragung personenbezogener Daten an einen externen Server funktionieren. Gleichzeitig war mir wichtig, dass die automatisch erzeugte Lösung von einer Person überprüft und manuell angepasst werden kann.

Als Grundlage dienten die Daten des laufenden Schuljahrs 2026/27. Daraus entwickelte ich einen Prototyp für die 2. Oberstufe, den ich anschliessend mit neu generierten Datensätzen testete. Ziel ist, dass das Werkzeug im Januar 2027 für die Einteilung der künftigen Wahlfachgruppen eingesetzt werden kann.

Wichtig war mir zudem, dass das Werkzeug unabhängig vom Schuljahr funktioniert und nicht jedes Jahr neu programmiert werden muss. Es enthält deshalb keine fest eingetragenen Schuljahre oder Schülerlisten: Klassen und Fachwahlen werden jeweils aus den importierten Daten übernommen, und die Gruppengrössen lassen sich bei Bedarf anpassen.

## 2. Entwicklungsprozess

### Geplantes Vorgehen

Zu Beginn legte ich folgende Arbeitsschritte fest:

- Treffen mit der Stundenplanerin der Schulen Baar
- Fakten austauschen und Materialien sammeln: bestehende Formulare, Listen und Zuteilungen des laufenden Schuljahres
- Prototyp durch Vibe-Coding erstellen, inklusive Anwendung (`index.html`) und Logbuch
- Prototyp mit den Listen des laufenden Schuljahrs 2026/27 testen
- Zwischengespräch mit der Stundenplanerin, um ein erstes Feedback einzuholen
- Prototyp anpassen und verbessern
- Verschiedene Testlisten von der KI erstellen lassen, damit das Werkzeug auch mit anderen Daten geprüft werden kann
- Prototyp fertigstellen, gegebenenfalls das Layout anpassen und den Schulen Baar zur Verfügung stellen
- Eine Forms-Umfrage passend zum Werkzeug erstellen
- Forms-Resultate testen und Testklassen generieren lassen

Die folgenden Phasen dokumentieren, wie diese Schritte umgesetzt wurden und welche Anpassungen sich dabei ergaben.

### Phase 1: Anforderungen klären und Daten verstehen

Zu Beginn traf ich mich mit der Stundenplanerin der Schulen Baar. Wir tauschten die wichtigsten Fakten zur bisherigen Einteilung aus, und ich sammelte die vorhandenen Materialien: bestehende Formulare, Listen und Zuteilungen des laufenden Schuljahres. Auf dieser Grundlage analysierte ich, welche Angaben für die Einteilung notwendig sind. Dazu gehören Name, Klasse, Niveau, Schulhaus, Erst- und Zweitwahl für die Doppellektion sowie das gewählte Fach der Einzellektion.

Ich legte folgende Grundregeln fest:

- Die drei Fachbereiche der Doppellektion sind Bildnerisches Gestalten, Technisches Gestalten und Textiles Gestalten.
- Die Einzellektion umfasst Musik, Deutsch plus und Informatik plus.
- Gruppen sollen wenn möglich klassenintern gebildet werden.
- Reicht dies nicht aus, dürfen Klassen innerhalb desselben Schulhauses gemischt werden.
- Erst danach werden schulhausübergreifende Gruppen geprüft (siehe Hinweis unten).
- Real und Sek bleiben grundsätzlich getrennt. Eine Mischung ist nur als gekennzeichnete Ausnahme bei zu kleinen Gruppen vorgesehen.
- Mindest- und Maximalgrössen müssen einstellbar sein.

> Hinweis: Diese Regeln beschreiben die erste Umsetzung. Sie liess schulhausübergreifende Gruppen noch als letzte Möglichkeit zu, obwohl ich bereits in meinem ersten Prompt verlangt hatte, dass die Schulhäuser getrennt bleiben (siehe Phase 2). Diese Abweichung fiel erst später bei Tests auf. Die Trennung wurde in Phase 17 verbindlich umgesetzt.

Eine besondere Herausforderung waren unterschiedliche CSV-Strukturen. Neben einer Standardliste sollte auch eine Fachmatrix eingelesen werden können. Fehlende oder mehrdeutige Angaben dürfen dabei nicht automatisch erfunden werden, sondern müssen sichtbar bleiben.

### Phase 2: Erster funktionsfähiger Prototyp

Ausgangspunkt war mein erster Prompt an ChatGPT:

> «Kannst du mir bitte helfen ein Tool zu entwickeln, welches wir für die Gruppeneinteilung von Wahlfächern nutzen können?»

Dazu gab ich folgende Informationen und Kriterien an:

- Anzahl SuS und Klassen
- Angebot der Fächer für Doppellektionen (TG, TxG, BG) und Einzellektionen (Informatik, Deutsch, Musik)
- Gruppengrösse in den einzelnen Fächern
- Die Doppellektion wird mit Prioritäten gewählt (1. und 2. Priorität).
- Zuteilungskriterien für die Gruppeneinteilung:
  - innerhalb der eigenen Klasse
  - Real (R) und Sek (S) getrennt, Klassen gemischt
  - Schulhäuser bleiben getrennt (Sennweid: Klassen a–c, Sternmatt 2: Klassen d–f)

Den Prototyp erstellte ich mit ChatGPT durch Vibe-Coding: Ich beschrieb die gewünschten Funktionen und Regeln in eigenen Worten, die KI setzte sie in Programmcode um, und ich prüfte und verfeinerte das Ergebnis im Dialog. So entstand eine eigenständige Browseranwendung in einer HTML-Datei. Sie kann lokal geöffnet werden und verarbeitet alle Daten nur im Arbeitsspeicher des Browser-Tabs. Dadurch ist keine Installation nötig und die Daten bleiben auf dem verwendeten Gerät.

Der erste Prototyp enthielt folgende Funktionen:

- Import einer oder mehrerer CSV-Dateien
- alternativ Einfügen einer Tabelle als Text
- Erkennen und Vereinheitlichen der Fachbezeichnungen
- Prüfen der importierten Daten
- Festlegen der minimalen und maximalen Gruppengrössen
- Berechnen eines Gruppenvorschlags
- Anzeigen der Gruppen nach Doppel- und Einzellektionen
- Kennzeichnen offener Zuteilungen und problematischer Gruppengrössen

### Phase 3: Einteilungslogik verfeinern

Im nächsten Schritt verfeinerte ich die Suchlogik. Der Vorschlag soll zuerst möglichst wenige offene Zuteilungen erzeugen und möglichst viele Erstwünsche erfüllen. Danach werden Klassen- und Schulhausmischungen möglichst klein gehalten. Bei gleichwertigen Lösungen werden unnötige Parallelgruppen und das Aufteilen einzelner Klassen vermieden.

Mir wurde dabei bewusst, dass die Anwendung keinen mathematischen Optimalitätsnachweis liefert. Sie erzeugt einen nachvollziehbaren Vorschlag, der durch eine Fachperson geprüft werden muss. Diese Einschränkung wird in der Anwendung transparent ausgewiesen.

### Phase 4: Kontrolle und manuelle Bearbeitung

Die Importkontrolle wurde erweitert, damit Schulhaus und Fachwahlen vor der Berechnung überprüft beziehungsweise ergänzt werden können. Zusätzlich lassen sich Schülerinnen und Schüler nach der Berechnung manuell zwischen passenden Gruppen verschieben. Die Anwendung kontrolliert dabei weiterhin die maximale Gruppengrösse und weist auf Verletzungen der Mindestgrösse hin.

Offene Fälle bleiben ausdrücklich sichtbar. Damit wird vermieden, dass unvollständige Daten oder nicht passende Gruppenkonstellationen unbemerkt zu einer falschen Zuteilung führen.

### Phase 5: Sichern und Exportieren

Für die praktische Verwendung ergänzte ich verschiedene Ausgabemöglichkeiten:

- CSV-Export für die Weiterbearbeitung in Excel
- PDF-Gruppenlisten zum Herunterladen oder Drucken
- Speichern des gesamten Planungsstands als JSON-Datei
- späteres Wiederöffnen eines gespeicherten Plans

Manuelle Änderungen werden in den Export übernommen. Ausserdem enthält die Oberfläche Hinweise für den Fall, dass ein Browser einen automatischen Download blockiert.

### Zwischengespräch mit der Stundenplanerin – 30. Oktober 2026

Nach den ersten Tests mit den Listen des laufenden Schuljahres stellte ich der Stundenplanerin der Schulen Baar den Prototyp vor und holte ein erstes Feedback ein. Wir besprachen vor allem organisatorische Details:

- die zulässigen Gruppengrössen der einzelnen Fächer,
- welche Klassen miteinander gemischt werden dürfen,
- dass die Schulhäuser bei der Einteilung immer getrennt bleiben müssen,
- dass die Fachwahlen künftig allenfalls über eine Forms-Umfrage erhoben werden.

Diese Rückmeldungen bildeten die Grundlage für mehrere der folgenden Anpassungen: die fachbezogenen und nach Real und Sek getrennten Gruppengrössen (Phasen 7, 8 und 15), die Regeln zur Mischung von Klassen in festen Klassenblöcken (Phasen 14 und 25), die verbindliche Schulhaustrennung (Phase 17) sowie das Forms-Formular mit dem passenden Import (Phase 20). Das Gespräch zeigte mir, wie wichtig der Austausch mit der Person ist, die den Prozess in der Praxis verantwortet: Viele dieser Regeln waren aus den vorhandenen Listen allein nicht ersichtlich.

### Phase 6: Offene Fachzuteilungen erweitern – 3. November 2026

Beim praktischen Prüfen zeigte sich, dass offene Doppellektions-Zuteilungen zu stark eingeschränkt waren. Im Auswahlmenü erschienen nur Gruppen aus der Erst- oder Zweitwahl der betreffenden Person. Dadurch konnte in einem offenen Ausnahmefall der dritte Fachbereich nicht manuell gewählt werden.

Ich passte deshalb die Auswahl bei den offenen Fachzuteilungen an. Für eine noch offene Doppellektion stehen nun alle drei Fachbereiche zur Verfügung:

- Bildnerisches Gestalten
- Technisches Gestalten
- Textiles Gestalten

Die bisherigen Schutzmechanismen bleiben bestehen: Es werden nur Gruppen des passenden Typs und Niveaus angeboten, und die maximale Gruppengrösse darf nicht überschritten werden. Bereits regulär zugeteilte Schülerinnen und Schüler können weiterhin nur innerhalb ihrer vorgesehenen Fachwahlen verschoben werden. Die Öffnung betrifft gezielt die noch ungelösten Fälle.

### Phase 7: Individuelle Gruppengrössen pro Fach – 3. November 2026

Die Gruppengrenzen waren zunächst teilweise zusammengefasst: Technisches und Textiles Gestalten verwendeten dieselben Werte, ebenso alle Fächer der Einzellektion. Für die konkrete Planung ist es jedoch sinnvoll, die Kapazitäten jedes Fachs einzeln festzulegen.

Ich erweiterte den Bereich «Gruppengrössen» deshalb auf sechs separate Zeilen. Minimum und Maximum können nun für Bildnerisches Gestalten, Technisches Gestalten, Textiles Gestalten, Musik, Deutsch plus und Informatik plus unabhängig eingegeben werden. Die Berechnung, die Prüfung manueller Verschiebungen und die Warnungen zu Gruppengrössen verwenden jeweils die fachbezogenen Werte. Ältere gespeicherte Pläne mit den früheren gemeinsamen Grenzwerten können weiterhin geöffnet werden; ihre bisherigen Werte werden dabei auf die entsprechenden Einzelfächer übertragen.

### Phase 8: Offizielle Gruppengrössen für Real und Sek – 3. November 2026

Da für Real und Sek unterschiedliche offizielle Maximalgrössen gelten, trennte ich die Einstellungen zusätzlich nach Niveau. Für die 2. Real gelten nun die Maximalwerte BG 16, Textiles Gestalten 10, Technisches Gestalten 10, Musik 18, Deutsch plus 16 und Informatik plus 16. Für die 2. Sek gelten BG 18, Textiles Gestalten 10, Technisches Gestalten 10, Musik 18, Deutsch plus 18 und Informatik plus 18. Die bisherigen Mindestgrössen bleiben bei 6 für Doppellektionen und 8 für Einzellektionen, können aber weiterhin individuell angepasst werden. Bei ausnahmsweise gemischten Real-/Sek-Gruppen wird die strengere der beiden Maximalgrössen angewendet.

### Phase 9: Gestaltung und Orientierung überarbeiten – 4. November 2026

Ich überarbeitete die Kopfgestaltung und die typografische Hierarchie der Anwendung. Die zusätzliche oberste Kopfzeile mit dem «w.»-Symbol und der wiederholten Bezeichnung «Wahlfächer 2. Oberstufe» wurde entfernt. Dadurch beginnt die Seite direkter mit dem eigentlichen Titel und wirkt ruhiger.

Die Reihenfolge der Gruppenbildung wird oben rechts nun verständlicher beschrieben: zuerst klassenintern, danach klassenübergreifend bei weiterhin getrennten Niveaus Real und Sek und schliesslich bei Bedarf schulhausübergreifend. Die mögliche Ausnahme bei zu kleinen Gruppen bleibt separat ausgewiesen.

Ausserdem vereinheitlichte ich die Schrift der Überschriften mit der Schrift des Untertitels «Schulen Baar». Der zentrale Button «Gruppen berechnen» behält zur besseren Erkennbarkeit eine etwas kräftigere, eigenständige Schriftgestaltung.

### Phase 10: Farbkonzept, Veröffentlichung und inklusive Sprache – 5. November 2026

Mit Unterstützung von ChatGPT passte ich das Erscheinungsbild an das Farbkonzept der Schulen Baar an. Blau dient nun als Hauptfarbe, Orange beziehungsweise Gelb als Akzentfarbe. Weisse und hellgraue Flächen sowie eine dunkle, neutrale Schrift sorgen für Übersichtlichkeit. Tabellenköpfe, aktive Filter, Schaltflächen und Hinweise wurden farblich aufeinander abgestimmt.

Anschliessend richtete ich für das Projekt ein GitHub-Repository ein und veröffentlichte die Anwendung mit GitHub Pages. Damit kann das Werkzeug über einen Weblink direkt im Browser aufgerufen werden. Eine `.nojekyll`-Datei kennzeichnet das Projekt als statische Webseite und unterstützt die automatische Bereitstellung nach jedem Push auf den Hauptbranch.

Beim Einrichten der Veröffentlichung achtete ich besonders auf den Datenschutz. Die beiden lokalen CSV-Testdateien wurden aus dem veröffentlichten Git-Verlauf entfernt. Eine `.gitignore`-Regel verhindert, dass CSV-Dateien künftig versehentlich zu GitHub hochgeladen werden. Die Testdateien bleiben lokal für die Erprobung der Anwendung verfügbar.

Zum Abschluss überprüfte ich die Sprache der Benutzeroberfläche. Die Überschrift «Schülerdaten» bei Schritt 1 wurde durch die kurze und inklusive Bezeichnung «SuS-Daten» ersetzt. Für Mengen- und Grenzwerte wird weiterhin der sachliche Begriff «Gruppengrössen» verwendet.

Die veröffentlichte Anwendung ist erreichbar unter: `https://digitalcreativ.github.io/wahlfachgruppen/`

### Phase 11: Testdaten anonymisieren – 5. November 2026

Für Demonstrationen gegenüber Kolleginnen und Kollegen anonymisierte ich die beiden lokalen CSV-Testdateien vollständig. Sämtliche Vor- und Nachnamen wurden durch 159 eindeutige Kennungen von `SuS-1` bis `SuS-159` ersetzt. Klassen, Niveau, Geschlecht und Fachwahlen blieben erhalten, damit die Dateien weiterhin realistische Berechnungen ermöglichen. Die Klassen a–c gehören dabei zu Schulhaus 1 und die Klassen d–f zu Schulhaus 2; `R` bezeichnet Real und `S` Sek.

Der Import wurde so erweitert, dass anonymisierte Fachmatrizen mit einer einzelnen `SuS-*`-Kennung ohne zweites Namensfeld verarbeitet werden können. Eine abschliessende Prüfung bestätigte, dass keine ursprünglichen Namen oder Namensangaben in Bemerkungsfeldern mehr vorhanden sind. Die CSV-Dateien bleiben weiterhin durch `.gitignore` vom öffentlichen GitHub-Repository ausgeschlossen und können bei Bedarf separat weitergegeben werden.

### Phase 12: Gruppen besser füllen und Beispieldaten präzisieren – 6. November 2026

Beim Ausprobieren mit den 160 fiktiven Schülerinnen und Schülern fiel mir auf, dass viele kleine Gruppen entstanden. Die bisherige Gewichtung bevorzugte klassenreine Gruppen zu stark. Ich liess die Einteilungslogik deshalb so anpassen, dass innerhalb der organisatorischen Vorgaben weniger und besser gefüllte Gruppen entstehen. Ein erster Vergleich mit den bisherigen Beispieldaten ergab 28 statt 37 Gruppen bei vollständig erfüllten Erstwünschen und ohne offene Zuteilungen.

Anschliessend präzisierte ich die Vorgaben für die Beispieldaten: höchstens zwei Schulhäuser und 14 Klassen sowie eindeutige Klassenbezeichnungen mit R für Real und S für Sek. Der überarbeitete Beispielgenerator erzeugt 160 fiktive SuS in zwölf Klassen, R1a–R1f und S1a–S1f. Die Klassen R1a–R1c und S1a–S1c gehören zu Schulhaus 1, R1d–R1f und S1d–S1f zu Schulhaus 2. Auch die CSV-Vorlage verwendet nun entsprechende Klassen- und Schulhausbezeichnungen.

Besonders wichtig war mir, dass eine bessere Auslastung nicht zu unnötiger Schulhausmischung führt. Die Suche priorisiert bei getrennter Einteilung nun möglichst wenige offene Zuteilungen, möglichst wenige Zweitwahlen, möglichst wenig Schulhausmischung und danach möglichst wenige Gruppen. Innerhalb gleichwertiger Lösungen werden Klassen möglichst zusammengehalten. Real und Sek bleiben grundsätzlich getrennt; die gekennzeichnete Ausnahme bei zu kleinen Gruppen bleibt bestehen.

Mit den überarbeiteten Beispieldaten ergab die Prüfung 32 Gruppen, alle 160 Erstwünsche erfüllt, keine offenen Zuteilungen und keine schulhausübergreifenden Gruppen. Zusätzlich wurden die Zuordnung von Klassen zu Schulhäusern, die Mindest- und Maximalgrössen sowie die vollständige und eindeutige Zuteilung pro SuS und Lektionstyp geprüft. Die höhere Gruppenzahl gegenüber dem ersten Vergleich erklärt sich durch die geänderten Beispieldaten und den Vorrang der Schulhaustrennung. Die Ergebnisse sind Testfälle und kein Nachweis einer global optimalen Einteilung.

### Phase 13: Klasseninterne Gruppen wieder vorrangig behandeln – 6. November 2026

Bei einer weiteren Prüfung präzisierte ich die Prioritäten: Wenn innerhalb einer Klasse im betreffenden Fach eine Gruppe mit gültiger Mindest- und Maximalgrösse möglich ist, soll diese gegenüber einer Verteilung auf gemischte Gruppen bevorzugt werden. Als Beispiel nannte ich S1e im Technischen Gestalten. Die bessere Gruppenauslastung darf diese Priorität nicht verdrängen.

Die Gewichtung wurde sowohl bei der Suche nach Fachzuteilungen als auch bei der anschliessenden Gruppenbildung angepasst. Nach möglichst wenigen offenen Zuteilungen, möglichst vielen Erstwünschen und möglichst wenig Schulhausmischung werden nun klasseninterne Gruppen bevorzugt. Erst danach folgt die möglichst geringe Gruppenzahl. Diese Präzisierung ersetzt die entsprechende Reihenfolge aus Phase 12. Die Erklärung in der Anwendung wurde ebenfalls aktualisiert.

Ein konstruierter Prüffall mit sechs SuS aus S1e sowie je sieben aus S1d und S1f im Technischen Gestalten bestätigte, dass alle drei Klassen eigene Gruppen erhalten und S1e zusammenbleibt. Ein weiterer Prüffall mit drei Klassen zu je sechs SuS bestätigte den Vorrang dreier klasseninterner Gruppen gegenüber zwei gemischten Gruppen. Mit den 160 Beispieldaten entstehen weiterhin 32 Gruppen ohne offene Zuteilungen oder Schulhausmischung; alle Erstwünsche werden erfüllt. Die Gruppengrenzen und die eindeutige Zuteilung wurden ebenfalls geprüft. Die Suche bleibt eine Heuristik und garantiert keine global optimale Lösung.

### Phase 14: Real und Sek verbindlich trennen und Klassenpaare bilden – 10. November 2026

Bei der weiteren Erprobung präzisierte ich die organisatorischen Regeln. Real und Sek müssen in allen Fächern immer getrennt bleiben, auch bei zu kleinen Gruppen. Die bisherige Ausnahme für niveaugemischte Gruppen wurde deshalb entfernt. Wenn keine gültige Gruppe gebildet werden kann, bleibt die Fachzuteilung sichtbar offen.

BG, Technisches Gestalten und Textiles Gestalten finden innerhalb einer Klasse gleichzeitig statt. Deshalb dürfen Klassen nicht für jedes dieser Fächer unabhängig miteinander kombiniert werden. Ich liess feste, voneinander unabhängige Klassenblöcke mit höchstens zwei Klassen einführen. Innerhalb eines solchen Blocks können sowohl gemischte als auch klassenreine Gruppen entstehen. Beispielsweise sind S2a + S2c in TG und TxG sowie separate BG-Gruppen für S2a und S2c möglich.

Anschliessend erweiterte ich dieselbe Paarregel auf Musik, Deutsch plus und Informatik plus. Eine Klasse darf damit über alle sechs Fächer hinweg nur mit derselben Partnerklasse gemischt werden. Die Paarbildung berücksichtigt die Fachwahlen beider Lektionstypen gemeinsam. Die Klassenblöcke werden bei den Gruppen angezeigt und begrenzen die manuellen Verschiebungen. Gespeicherte Einteilungen mit unzulässigen Mischungen müssen nach Übernahme der Daten und Einstellungen neu berechnet werden.

### Phase 15: Gruppengrössen und Darstellung anpassen – 10. November 2026

Ich passte die Gruppengrenzen schrittweise an die konkreten Planungsvorgaben an. Zunächst wurden für beide Niveaus die Maximalgrössen auf 18 für BG, 12 für TG und TxG sowie 18 für die drei Einzelfächer gesetzt. Danach erhöhte ich in der Sek die Maximalgrössen für Musik, Deutsch plus und Informatik plus auf 20. Zuletzt senkte ich die Mindestgrösse in allen drei Gestaltungsfächern bei Real und Sek von 6 auf 5. Die Mindestgrösse der Einzelfächer bleibt 8. Alle Grenzen sind weiterhin individuell einstellbar.

Für eine bessere Orientierung tauschte ich die Schriftgrössen der Gruppeninformationen: «Klassenrein» beziehungsweise die Mischungsbezeichnung erscheint grösser, die ergänzende Angabe «Klassenblock» kleiner.

### Phase 16: Offene Zuteilungen für beide Lektionstypen bearbeiten – 10. November 2026

SuS ohne vollständige Fachwahl benötigen für die Doppel- und die Einzellektion jeweils eine eigene Zuteilung. Ich liess die offenen Fälle deshalb getrennt unter «Doppellektion · BG / TG / TxG» und «Einzellektion · Musik / Deutsch plus / Informatik plus» aufführen. Fehlen beide Wahlen, erscheint die betreffende Person in beiden Bereichen.

Bei einer offenen Doppellektion können alle drei Gestaltungsfächer angeboten werden. Bei einer fehlenden Einzelfachwahl sind die drei Einzelfächer möglich. Eine vorhandene feste Einzelfachwahl bleibt berücksichtigt. Die Auswahl führt zu bestehenden Gruppen; neue Gruppen werden dadurch nicht automatisch angelegt. Die maximale Gruppengrösse wird beim Verschieben kontrolliert.

Eine weitere praktische Prüfung zeigte, dass die Zugehörigkeit zum selben Klassenblock allein noch nicht ausreicht: SuS aus S2a sollen beispielsweise nicht in die klassenreine BG-Gruppe der S2c gelangen. Ich schränkte die Auswahl für offene Zuteilungen deshalb zusätzlich ein. Es erscheinen nur Gruppen, in denen bereits SuS derselben Klasse sind. Das gilt für beide Lektionstypen und wird auch unmittelbar beim Verschieben geprüft.

### Phase 17: Schulhausgrenzen auch für Klassenblöcke absichern – 10. November 2026

Bei einer Prüfung fiel ein Klassenblock S2a + S2e auf. Die sichtbare Informatikgruppe war zwar klassenrein, der hinterlegte Block verband jedoch zwei Schulhäuser. Eine blosse Bevorzugung schulhausinterner Lösungen genügte somit nicht.

Ich liess die Schulhaustrennung verbindlich in die Paarbildung aufnehmen. Gruppen und Klassenblöcke dürfen nur innerhalb desselben Niveaus und Schulhauses entstehen. Zusätzlich gilt für die Klassenbezeichnungen mit R oder S und den Buchstaben a bis f: a/b/c gehören zu Schulhaus 1, d/e/f zu Schulhaus 2. Diese Klassengruppen dürfen auch dann nicht kombiniert werden, wenn im Import versehentlich dieselbe Schulhausbezeichnung steht. Die Schutzregel gilt ebenso bei manuellen Verschiebungen und bei der Prüfung gespeicherter Pläne.

Damit entfällt auch die in früheren Phasen beschriebene Möglichkeit einer schulhausübergreifenden Zuteilung. Zu kleine Gruppen bleiben gegebenenfalls offen.

### Phase 18: Klassenpaar S2a + S2c festlegen und aktuellen Stand prüfen – 10. November 2026

Anhand der vorhandenen anonymisierten Schülerlisten prüfte ich die konkrete Situation von S2a, S2b und S2c. S2a hat 15 BG-, 5 TG- und 1 TxG-Wahl sowie eine fehlende Gestaltungswahl. S2c hat 9 BG-, 7 TG- und 5 TxG-Wahlen sowie ebenfalls eine fehlende Gestaltungswahl. Das Paar S2a + S2c ermöglicht damit zwei klassenreine BG-Gruppen sowie eine gemeinsame TG-Gruppe mit 12 und eine gemeinsame TxG-Gruppe mit 6 SuS.

Ich legte dieses Klassenpaar für die aktuelle Planung ausdrücklich fest. Es wird bei der Berechnung verwendet, sofern beide Klassen innerhalb desselben zulässigen Schulhausbereichs vorhanden sind. S2b bleibt in der vorliegenden Konstellation klassenintern. Die Vorgabe gilt wie die übrigen Klassenpaare über alle sechs Fächer hinweg.

Die Senkung der gestalterischen Mindestgrösse auf 5 löst nicht jeden offenen Fall: In S2b bleiben die 4 TxG-Wahlen unter dem Minimum. Auch die kleinen Musik- und Deutsch-plus-Gruppen werden dadurch nicht automatisch möglich. Fehlende Wahlen müssen weiterhin nachgefragt und organisatorische Ausnahmen bewusst entschieden werden.

Die wiederholbaren Prüfungen in `verify.cjs` kontrollieren unter anderem die JavaScript-Syntax, die Gruppengrenzen, die vollständige und eindeutige Zuordnung pro SuS und Lektionstyp, die Trennung von Real und Sek sowie die gemeinsamen Klassenpaare über alle sechs Fächer. Zusätzlich werden die Schulhausgrenzen bei gleichen importierten Schulhausbezeichnungen, das vorgegebene Paar S2a + S2c und die Auswahl offener Zuteilungen nur bei tatsächlichen Mitschülerinnen und Mitschülern geprüft. Auch der direkte Versuch, eine offene S2a-Zuteilung in die klassenreine BG-Gruppe der S2c zu verschieben, wird abgewiesen.

Mit dem aktuellen Stand ergeben die 160 fiktiven Beispieldaten 34 Gruppen und 53 offene Fachzuteilungen. Die Prüfung der Sennweider Testdatei bestätigt S2a + S2c und klasseninterne Gruppen der S2b. Bei den Doppellektionen bleiben dort die zwei fehlenden Wahlen aus S2a und S2c sowie die vier TxG-Zuteilungen der S2b offen. Frühere Testergebnisse ohne offene Zuteilungen beziehen sich auf die damaligen, weniger strengen Regeln. Die Suche bleibt eine Heuristik und liefert keinen Nachweis einer global optimalen Einteilung.

### Phase 19: Klassen- und Fachübersicht aus den vorhandenen Importen – 10. November 2026

Ich ergänzte einen aufklappbaren Bereich «Klassen & Fächer · Übersicht und Hinweise» oberhalb der Gruppenübersicht. Die beiden bestehenden CSV-Dateien können weiterhin gemeinsam hochgeladen werden. Die neue Übersicht entsteht ausschliesslich aus den geladenen Schülerlisten und der aktuellen Einteilung; eine zusätzliche Zusammenstellungsdatei ist nicht erforderlich.

Ein Klassenfilter begrenzt die Anzeige bei Bedarf auf eine einzelne Klasse. Pro Klasse und Fach werden die Erst- beziehungsweise festen Wahlen, separat die Zweitwahlen, die zugeordneten SuS und die offenen Fälle mit vorhandener Fachwahl angezeigt. Die Gruppenangaben zeigen jeweils den Anteil der Klasse sowie die gesamte Belegung im Verhältnis zum Maximum. Vor der Berechnung erscheinen bereits die Wahlzahlen; die Zuteilungsspalten bleiben bis zur Berechnung offen.

Hinweise machen fehlende Fachwahlen, Importhinweise, fehlende Schulhausangaben und offene Zuteilungen sichtbar. Liegt die Zahl der Wahlen klassenintern unter dem Minimum, wird auf die Prüfung einer Mischung innerhalb des festen Klassenpaars hingewiesen. Dies ist kein automatischer Nachweis, dass eine gemeinsame Gruppe unmöglich ist. Volle Gruppen und verletzte Gruppengrenzen werden zusätzlich aufgeführt. Ein Vergleich mit den importierten Wahlen macht Abweichungen durch Zweitwahlen oder manuelle Änderungen sichtbar. Fehlende Fachwahlen werden nicht einem beliebigen Fach zugeschrieben und erscheinen deshalb gesondert bei den Hinweisen.

Die Übersicht aktualisiert sich bei einer neuen Berechnung, bei Änderungen der Importangaben und bei manuellen Verschiebungen. Auch doppelte oder unvollständige Zuordnungen pro SuS und Lektionstyp werden geprüft. Die bestehenden Regeln für Niveau, Schulhaus, Klassenpaare und manuelle Zuteilungen bleiben bestehen.

Die automatisierten Prüfungen wurden mit beiden ursprünglichen CSV-Testdateien zusammen durchgeführt (159 SuS). Geprüft wurden Wahl- und Zuordnungszahlen, die Anzeige vor und nach der Berechnung, fehlende Wahlen, Engpässe, volle Gruppen, die Aktualisierung nach manueller Zuteilung, die Erkennung doppelter Zuordnungen, der Klassenfilter und die HTML-Ausgabe der Übersicht. Der Upload mehrerer Dateien bleibt vorhanden. Eine visuelle Browserprüfung wurde in dieser Umgebung nicht durchgeführt.

### Phase 20: Microsoft-Forms-Antworten direkt importieren – 12. November 2026

Für die künftige Erfassung der Fachwahlen erstellte ich mit Unterstützung von ChatGPT ein Microsoft-Forms-Formular. Die SuS wählen ihre Klasse, eine erste und eine andere zweite Priorität in den Gestaltungsfächern sowie ein festes Einzelfach. Über Verzweigungen gelangt jede Erstwahl zu einer passenden Zweitwahl-Frage. Für die namentliche Zuordnung wird die Einstellung «Namen aufzeichnen» verwendet; die Antworten werden auf eine Antwort pro Person beschränkt. Die Einrichtung im schulischen Microsoft-365-Konto erfolgt durch mich; die KI hat das Formular nicht direkt im Konto angelegt.

Anhand eines bereinigten Excel-Testexports ergänzte ich den Import in der bestehenden Anwendung. Die Dateiauswahl akzeptiert nun neben den bisherigen CSV-Dateien auch Forms-Antworten im XLSX-Format. Eine zusätzliche Installation oder externe Bibliothek ist nicht nötig. Die Verarbeitung erfolgt weiterhin lokal im Browser. Die beiden bisherigen CSV-Testdateien bleiben einzeln und gemeinsam importierbar; auch das Forms-Format wird als CSV erkannt.

Der Import berücksichtigt die tatsächlichen Spalten des Formulars: Name, Klassenfrage, Erstwahl, die drei verzweigten Zweitwahl-Spalten und das zusätzliche Einzelfach. Pro Antwort wird nur der zur Erstwahl passende Zweitwahl-Zweig übernommen. Enthalten andere Zweige noch Werte, werden diese nicht als zusätzliche Wahl interpretiert; stattdessen erscheint ein Importhinweis. Erst- und Zweitwahl müssen verschieden sein. Fehlende Angaben bleiben sichtbar, nicht erkannte Fach- oder Klassenangaben führen zu einer verständlichen Fehlermeldung.

Klassenbezeichnungen wie «Sek 2a» werden als «S2a» übernommen. Real/Sek und der Schulhausbereich werden daraus abgeleitet; a/b/c gehören zu Schulhaus 1 und d/e/f zu Schulhaus 2. Der eingereichte Testexport enthielt «Sek 1a» und wurde entsprechend als «S1a» eingelesen. Die Jahrgangszahl wird nicht stillschweigend geändert. Für die reale Anmeldung der 2. Oberstufe müssen die Klassenoptionen im Formular daher passend eingerichtet sein.

Der direkte XLSX-Import liest die erste Tabelle und benötigt einen aktuellen Browser mit Unterstützung der verwendeten Dekomprimierung. Andernfalls kann dieselbe Antwortdatei aus Excel als CSV UTF-8 gespeichert und eingelesen werden. Die Verarbeitung übernimmt Zellwerte; Formeln und externe Verknüpfungen werden nicht ausgeführt. Umfangreiche, beschädigte oder kennwortgeschützte Dateien werden abgewiesen.

Die eingereichte Testdatei wurde erfolgreich mit einer Antwort eingelesen: Technisches Gestalten als Erstwahl, Textiles Gestalten als Zweitwahl und Musik als Einzelfach. Zusätzliche synthetische Prüfungen in `verify-forms.cjs` decken alle drei Zweitwahl-Zweige, veraltete Werte in anderen Zweigen, fehlende Namen und Wahlen, Klassen- und Niveauzuordnung, doppelte Antwort-IDs, Forms-CSV sowie unterschiedliche XLSX-Speicherformen ab. Die bestehenden Prüfungen in `verify.cjs` bleiben erfolgreich. Eine visuelle Prüfung des Uploads im Browser wurde nicht durchgeführt. Eine direkte Verbindung zum schulischen SharePoint ist damit noch nicht eingerichtet: Die Forms-Antwortdatei wird weiterhin heruntergeladen und anschliessend in das Einteilungstool importiert.

Damit der Forms-Import nicht nur mit einer einzelnen Antwort, sondern unter realistischen Bedingungen geprüft werden konnte, liess ich mit KI eine Testliste im Format der Forms-Antworten erstellen. Sie enthält 160 anonyme, fiktive SuS mit Klasse, Erstwahl, passender Zweitwahl und Einzelfach (`Forms-Testdaten_160_SuS.xlsx`). Echte Namen oder Daten aus der Umfrage wurden dafür nicht verwendet. Diese Testliste diente in den folgenden Phasen als wichtigste Grundlage für die Überprüfung der Einteilungsregeln.

### Phase 21: Passende klassenreine Gruppen zusammenführen – 12. November 2026

Beim Testen zeigte sich, dass zwei klassenreine Gruppen teilweise getrennt blieben, obwohl ihre gemeinsame Grösse innerhalb der erlaubten Gruppengrenzen lag. Ich präzisierte deshalb die Priorität: Innerhalb desselben festen Klassenpaars werden solche Gruppen desselben Fachs zusammengeführt, wenn die Summe das jeweilige Maximum nicht überschreitet. Die Regel gilt für alle sechs Fächer und beide Niveaus. Sie ersetzt in diesem Fall den bisherigen Vorrang klassenreiner Gruppen.

Die Prüfung berücksichtigt auch kleinere Teilgruppen, wenn eine Klasse aufgrund ihrer Grösse bereits mehrere Gruppen benötigt. Klassenpaare, Schulhausgrenzen und die Trennung von Real und Sek bleiben verbindlich. Gruppen oberhalb des Maximums werden nicht zusammengeführt. Die Änderung greift bei einer neuen Berechnung; vorhandene gespeicherte Einteilungen müssen dafür neu berechnet werden.

Die Prüfungen bestätigten die Zusammenführung bei allen sechs Fächern, bei Real und Sek, genau am Maximum sowie bei passenden Teilgruppen. Ein Gegenbeispiel mit insgesamt 20 BG-Wahlen bei einem Maximum von 18 bleibt auf zwei Gruppen verteilt. Mit der Forms-Testdatei mit 160 fiktiven SuS entstehen neu 24 statt 40 Gruppen, ohne offene Zuteilungen und mit vollständig erfüllten Erstwünschen. Die 160 integrierten Beispieldaten ergeben unter den aktuellen Regeln 32 Gruppen und 53 offene Fachzuteilungen. Auch die bisherigen Import- und Einteilungsprüfungen bleiben erfolgreich.

### Phase 22: Forms-Testdatei an zehn Klassen ohne c-Klassen anpassen – 12. November 2026

Für die kommende Klassenkonstellation passte ich die Forms-Testdatei auf S1a, S1b, S1d, S1e, S1f und die entsprechenden fünf Realklassen an. Sie enthält weiterhin 160 fiktive SuS, nun je 16 pro Klasse. C-Klassen sind nicht mehr enthalten. Alle Personen haben unterschiedliche Erst- und Zweitwahlen sowie eine feste Einzelfachwahl. Der Import behält die ausdrücklich gewünschten Klassenbezeichnungen des ersten Jahrgangs bei.

Die Prüfung bestätigt zehn Klassen, 80 Real- und 80 Sek-SuS sowie 64 Personen in Schulhaus 1 und 96 in Schulhaus 2. Mit den aktuellen Standardgrenzen entstehen 32 Gruppen; alle 160 Erstwahlen werden erfüllt. Bei den Einzellektionen bleiben 16 Zuteilungen offen: Bei je drei Klassen pro Niveau in Schulhaus 2 bleibt innerhalb fester Zweierpaare eine Klasse allein; ihre vier Musik- und vier Deutsch-plus-Wahlen unterschreiten jeweils das Minimum von acht. Die neuen offenen Fälle sind somit eine Folge der veränderten Testkonstellation. Die Einteilungsregeln und die bisherigen Testdateien wurden dafür nicht geändert.

### Präzisierung der Testklassengrössen – 12. November 2026

Die anschliessend präzisierten Klassengrenzen betragen höchstens 14 SuS in Real und 20 in Sek. Ich passte deshalb ausschliesslich die Forms-Testdaten auf fünf Realklassen mit je 12 SuS und fünf Sekklassen mit je 20 SuS an. Damit bleiben zehn Klassen und insgesamt 160 Personen erhalten: 60 Real- und 100 Sek-SuS. Die Klassenbuchstaben a/b/d/e/f und die Schulhauszuordnung bleiben bestehen. Dies ersetzt die zuvor gleichmässige Verteilung von 16 Personen pro Klasse.

Import und vollständige, eindeutige Fachzuordnung wurden erneut geprüft. Die neue Verteilung der Fachwahlen führt bei unveränderten Fachgruppengrenzen und festen Klassenpaaren zu 25 Gruppen und 52 offenen Fachzuteilungen. Die Testdaten enthalten dabei vollständige Erst-, Zweit- und Einzelfachwahlen; offene Zuteilungen entstehen aufgrund der organisatorischen Gruppengrenzen. Die Klassengrenzen wurden nicht als neue Fachgruppengrenzen übernommen.

### Testklassengrössen und Fachwahlen variieren – 12. November 2026

Für realistischere Testläufe verteilte ich die 160 fiktiven SuS neu: R1a 12, R1b 14, R1d 11, R1e 13, R1f 14 sowie S1a 20, S1b 18, S1d 19, S1e 20 und S1f 19. Damit enthält die Forms-Testdatei 64 Real- und 96 Sek-SuS. Die Maximalgrössen von 14 beziehungsweise 20 werden eingehalten; c-Klassen bleiben ausgeschlossen. Auch die Verteilung der Gestaltungs- und Einzelfachwahlen variiert zwischen den Klassen. Alle Erst- und Zweitwahlen sind vollständig und verschieden.

Die erneute Import- und Einteilungsprüfung bestätigt 160 eindeutige Personen in zehn Klassen und gültige Gruppengrenzen. Mit dieser Testverteilung entstehen 29 Gruppen und 31 offene Fachzuteilungen. Dies ersetzt die unmittelbar zuvor beschriebene gleichmässige Verteilung je Niveau. Die Anwendung selbst wurde hierfür nicht geändert.

### Phase 23: Alle Einzellektionen manuell verschieben – 12. November 2026

Beim Testen zeigte sich, dass die manuelle Auswahl bei den Einzellektionen noch auf das ursprünglich gewählte Fach beschränkt war. Ich öffnete deshalb die Auswahl für Musik, Deutsch plus und Informatik plus. Bereits zugeteilte SuS können nun zwischen bestehenden passenden Gruppen aller drei Einzelfächer verschoben werden. Auch offene Zuteilungen mit vorhandener Einzelfachwahl dürfen manuell einem anderen Einzelfach zugeteilt werden.

Die Schutzregeln bleiben bestehen: Niveau, Schulhausbereich, festes Klassenpaar und maximale Gruppengrösse müssen passen. Für offene Zuteilungen werden weiterhin nur Gruppen angeboten, in denen bereits SuS derselben Klasse sind. Fällt die Quellgruppe durch das Verschieben unter die Mindestgrösse, erscheint eine Warnung. Die automatische Berechnung verwendet weiterhin die ursprüngliche feste Einzelfachwahl; manuelle Fachänderungen werden nicht als neue Wahl zurückgeschrieben.

Die ursprüngliche Wahl bleibt im Plan zur Kontrolle erhalten. Abweichende Einzelfachzuteilungen werden im CSV-Export als «Manuell zugeteilt» ausgewiesen. Auch die Planprüfung beim Wiederöffnen wurde angepasst, damit eine gültige manuelle Fachänderung erhalten bleibt. Die Klassen-/Fachübersicht aktualisiert die tatsächliche Zuordnung und weist auf Abweichungen von der ursprünglichen Wahl hin.

Die Prüfungen decken alle sechs möglichen Wechsel zwischen den drei Einzelfächern ab. Die Auswahl, das tatsächliche Verschieben, die unveränderte ursprüngliche Wahl, die Warnung bei unterschrittenem Minimum und das Wiederöffnen einer gespeicherten manuellen Fachänderung wurden erfolgreich geprüft. Die bisherigen Import-, Einteilungs- und Schutzregelprüfungen bleiben erfolgreich.

### Phase 24: Zweitwahlen auf begründete Notfälle beschränken – 12. November 2026

Bei der Erprobung stellte ich fest, dass zu viele Zweitwahlen verwendet wurden. Die bisherige Suche priorisierte möglichst wenige offene Fachzuteilungen vor möglichst wenigen Zweitwahlen. Da die Klassenpaare über alle sechs Fächer gemeinsam bestimmt werden, konnte eine Änderung der Gestaltungswahl dabei auch indirekt eine bessere Einzelfachkonstellation ermöglichen. Dies entsprach nicht dem gewünschten starken Vorrang der Erstwahl.

Ich liess die Suche in zwei Schritte trennen. Zuerst wird ausschliesslich mit Erstwahlen gerechnet. Die dabei gewählten Klassenblöcke bleiben für den anschliessenden Einsatz von Zweitwahlen fest. Innerhalb dieser Blöcke werden Zweitwahlen nur zur Lösung konkreter offener Gestaltungszuteilungen geprüft: zum Schliessen einer Lücke von einer oder zwei Personen, zum Abbau einer kleinen Überzahl oder zur Zuteilung aus einem Fach, dessen gesamte Wahlzahl im Block unter der Mindestgrösse liegt.

Aus einem Fach, das nach seinen ursprünglichen Wahlzahlen grundsätzlich eine Gruppe bilden kann, werden höchstens zwei Personen pro Block auf ihre Zweitwahl umgeteilt. Bei einem vollständig unterbesetzten Fach kann dagegen eine grössere Anzahl seiner Wahlen auf die jeweilige Zweitwahl wechseln, wenn dies die offenen Fälle reduziert. Reparaturen mit zwei Personen werden gemeinsam geprüft, damit eine Mindestzahl auch dann erreicht werden kann, wenn ein einzelner Wechsel noch nicht genügt. Offene Gestaltungszuteilungen dürfen in keinem anderen Fach zunehmen. Zweitwahlen dienen damit weder der blossen Verringerung der Gruppenzahl noch der Verbesserung der Einzelfachzuteilungen. Wenn keine solche Reparatur möglich ist, bleiben Fälle bewusst offen.

Die automatisierten Prüfungen bestätigen Reparaturen mit einer und zwei Personen, die Zuteilung aus einem nicht zustande kommenden kleinen Fach, den Ausgleich einer kleinen Überzahl bei individuell gesetzten Gruppengrenzen sowie den Schutz bereits möglicher Gruppen. Ein Test mit offenen Einzelfächern und vollständig möglichen Gestaltungs-Erstwahlen bestätigt, dass hierfür keine Zweitwahlen eingesetzt und keine Klassenpaare nachträglich verändert werden.

Mit der aktuellen Forms-Testdatei mit 160 fiktiven SuS werden vier Zweitwahlen verwendet; alle Gestaltungszuteilungen sind gelöst. Es entstehen 30 Gruppen und 28 offene Einzelfachzuteilungen. Die eingebauten 160 Beispieldaten ergeben 32 Gruppen und 54 offene Fachzuteilungen. Die übrigen Import-, Verschiebe- und Schutzregelprüfungen bleiben erfolgreich. Die Suche bleibt begrenzt und heuristisch; offene Fälle sind weiterhin fachlich zu prüfen.

### Phase 25: Klassenblöcke mit bis zu drei Klassen zulassen – 12. November 2026

Die organisatorischen Vorgaben wurden erweitert: Innerhalb eines Schulhauses dürfen Gruppen SuS aus bis zu drei Klassen desselben Niveaus enthalten. In der aktuellen Konstellation sind somit R1a + R1b und R1d + R1e + R1f sowie entsprechend S1a + S1b und S1d + S1e + S1f möglich. Klassenreine Gruppen und kleinere Kombinationen bleiben ebenfalls zulässig. Die Trennung von Real und Sek und zwischen den beiden Schulhausbereichen bleibt verbindlich.

Ich erweiterte die gemeinsame Blocksuche über alle sechs Fächer auf Einzel-, Zweier- und Dreierblöcke. Die frühere standardmässig festgelegte Paarung S2a + S2c entfällt. Dadurch kann auch eine dritte Klasse zur Mindestgrösse eines Fachs beitragen. Die Maximalgrössen bleiben unverändert. Passende Gruppen innerhalb eines Blocks werden weiterhin zusammengeführt, wenn die gemeinsame Grösse das Maximum nicht überschreitet.

Die erste Berechnung erfolgt weiterhin nur mit Erstwahlen. Die daraus gebildeten Klassenblöcke bleiben bei anschliessenden Notfallkorrekturen durch Zweitwahlen fest. Auch die manuellen Schutzregeln gelten weiter; bei offenen Zuteilungen werden nur Gruppen mit tatsächlichen Mitschülerinnen und Mitschülern derselben Klasse angeboten. Die Prüfung und Wiederherstellung gespeicherter Pläne berücksichtigt nun auch Dreierblöcke und erhält deren Zugehörigkeit über alle Fächer hinweg.

Geprüft wurden Gruppen aus drei Klassen in allen sechs Fächern und bei beiden Niveaus, die Gruppengrenzen, der Ausschluss schulhaus- oder niveauübergreifender Gruppen, das Verbot von Blöcken aus mehr als drei Klassen und das Wiederöffnen eines gespeicherten Dreierblocks. Die bisherigen Prüfungen zu Erstwahlvorrang, Notfall-Zweitwahlen, Import und manuellen Verschiebungen bleiben erfolgreich.

Mit der aktuellen Forms-Testdatei entstehen 28 Gruppen und nur noch sieben offene Fachzuteilungen statt zuvor 28. Die Gestaltungs-Erstwahlen können vollständig erfüllt werden. Die integrierten 160 Beispieldaten ergeben 32 Gruppen ohne offene Fachzuteilungen. Die früheren Ergebnisse und Beschränkungen auf feste Zweierpaare beschreiben historische Zwischenstände.

### Schrift und Bedienelemente vereinheitlichen – 13. November 2026

Nach den inhaltlichen Erweiterungen überarbeitete ich mit ChatGPT die Gestaltung der Anwendung. Ziel waren eine einheitliche Schrift, gut lesbare Bedienelemente und eine klare Gewichtung der Schaltflächen.

- Bisher waren zwei Schriftarten gemischt (DM Sans und Manrope). Nun verwendet die gesamte Anwendung einheitlich Arial, auch in Eingabefeldern, Auswahllisten und Schaltflächen.
- Die Grundschrift wurde von 14 auf 16 Pixel vergrössert. Sehr kleine Texte von 10 bis 12 Pixeln, etwa in Gruppenlisten, Hinweisen, Tabellen und Auswahlmenüs, wurden auf 12 bis 14 Pixel angehoben. Die Zahlenfelder der Gruppengrössen sind grösser und dadurch leichter zu bedienen.
- Die Schaltflächen wurden nach ihrer Wichtigkeit gestaltet: «Gruppen berechnen» ist als Hauptaktion farbig hervorgehoben, die Exportfunktionen (PDF, CSV, Plan sichern) erscheinen zurückhaltender als weisse Schaltflächen mit blauem Rand.
- Bei der Bedienung mit der Tastatur zeigt eine deutliche blaue Umrandung, welches Element gerade ausgewählt ist.
- Die Darstellung auf mittleren und kleinen Bildschirmen wurde angepasst, damit Kennzahlen, Filter und Schaltflächen auch auf schmalen Geräten übersichtlich umbrechen.

Die Einteilungslogik blieb dabei unverändert.

### Phase 26: Bedienoberfläche überprüfen und vereinfachen – 16. November 2026

Nach den vielen inhaltlichen Erweiterungen fiel mir auf, dass der linke Navigationsbereich sehr lang geworden war. Ich liess die Oberfläche deshalb mit Claude Code überprüfen. Dabei zeigte sich, dass die zentrale Schaltfläche «Gruppen berechnen» erst nach zwölf Eingabefeldern für die Gruppengrössen folgte und «Plan öffnen» ganz unten stand, obwohl man diese Funktion oft zu Beginn braucht. Zudem war der Erklärtext «So wird zugeteilt» über viele Entwicklungsphasen gewachsen. Er enthielt Wiederholungen, überholte Hinweise wie die entfallene Vorgabe S2a + S2c und teilweise widersprüchliche Begriffe wie «Paar» statt «Klassenblock».

Vor der Überarbeitung erstellte ich eine Sicherheitskopie der Anwendung, um bei Bedarf zum bisherigen Stand zurückkehren zu können. Anschliessend liess ich den linken Bereich neu ordnen:

- Unter «SuS-Daten» stehen nun der Datei-Import, «Gespeicherten Plan öffnen» und die Beispieldaten direkt untereinander. Das selten benötigte Einfügen einer Tabelle als Text ist eingeklappt.
- Die Gruppengrössen sind standardmässig eingeklappt. Aufgeklappt erscheinen Real und Sek in einer kompakten Tabelle nebeneinander, gegliedert nach Doppel- und Einzellektion. Eine kleine Statusanzeige zeigt, ob die Standardwerte gelten, Werte angepasst wurden oder ungültige Werte vorliegen, etwa ein Minimum über dem Maximum. Bei ungültigen Werten klappt der Bereich vor der Berechnung automatisch auf.
- Dadurch ist «Gruppen berechnen» ohne Scrollen sichtbar. «Plan sichern» steht mit einem kurzen Datenschutzhinweis am Ende der Spalte.

Den Erklärtext «So wird zugeteilt» verschob ich unter die Gruppenübersicht und liess ihn auf den aktuellen Stand kürzen: fünf nummerierte Regeln (Erstwahlen zuerst, klassenrein oder im Klassenblock, feste Blöcke mit höchstens drei Klassen, Zweitwahlen nur im Notfall, lieber offen als regelwidrig) sowie kurze Hinweise zu den strikten Trennungen, zum manuellen Anpassen, zum Import, zu den Grenzen des Werkzeugs und zum Datenschutz. Auch die Kurzfassung oben rechts wurde an diese Regeln angepasst.

Zusätzlich wurden kleinere Punkte bereinigt. Die Anwendung verwendet nun durchgehend die Du-Form; zuvor standen «deine Planung» und «eure Wahlfachgruppen» nebeneinander. Die Seitenbeschreibung enthält kein veraltetes Datum mehr. Neu erscheint beim Schliessen oder Neuladen des Browser-Tabs eine Rückfrage, wenn seit dem letzten Sichern Daten importiert, Gruppen berechnet oder manuelle Änderungen vorgenommen wurden. Da die Daten bewusst nur im Arbeitsspeicher des Tabs liegen, schützt dies vor versehentlichem Datenverlust.

Die Einteilungslogik selbst wurde nicht verändert; alle Eingabefelder und Schaltflächen behielten ihre bisherigen technischen Bezeichnungen. Die Darstellung wurde mit Bildschirmaufnahmen in breiter und schmaler Ansicht geprüft. Die automatisierten Prüfungen in `verify.cjs` und `verify-forms.cjs` konnten auf dem verwendeten Gerät nicht ausgeführt werden, da Node.js nicht installiert ist. Die Funktionen Laden, Berechnen, Sichern, Wiederöffnen sowie die Rückfrage beim Schliessen sind daher noch von Hand im Browser zu testen.

Diese Phase zeigt mir, dass ein Werkzeug durch schrittweise Erweiterungen funktional besser, in der Bedienung aber unübersichtlicher werden kann. Eine bewusste Überprüfung der Oberfläche aus Sicht der Anwenderinnen und Anwender ist deshalb ebenso wichtig wie die Weiterentwicklung der Einteilungsregeln.

## 3. Einsatz von künstlicher Intelligenz

Ich setzte KI als Unterstützung bei der Konzeption, Programmierung, Fehlersuche und sprachlichen Überarbeitung ein. Dabei arbeitete ich mit zwei Werkzeugen:

- **ChatGPT** war bis kurz vor Projektende mein einziges KI-Werkzeug. Damit entstanden alle Phasen von der ersten Version des Tools über die Einteilungsregeln, das Farbkonzept und Layout der Schulen Baar bis zur Forms-Umfrage und dem passenden Import (Phasen 1–25).
- **Claude Code** zog ich erst gegen Ende des Projekts hinzu, als mir bewusst wurde, dass ein zweites Werkzeug sinnvoll sein könnte. Claude Code arbeitet direkt in den Projektdateien auf meinem Computer. Damit liess ich am 16. November 2026 die Oberfläche überprüfen und vereinfachen (Phase 26) sowie dieses Logbuch ergänzen und eine Zusammenfassung für den Leistungsnachweis entwerfen.

Der zusätzliche Blick eines zweiten Werkzeugs war hilfreich: Claude Code fand in der bestehenden Anwendung Punkte, die im Verlauf der vielen Erweiterungen untergegangen waren, etwa den veralteten Erklärtext und die fehlende Warnung vor Datenverlust.

In beide Werkzeuge gab ich keine echten Schülerdaten ein, sondern arbeitete mit anonymisierten beziehungsweise fiktiven Testdaten. Dabei formulierte ich die Anforderungen und prüfte die vorgeschlagenen Lösungen anhand der schulischen Einteilungsregeln. Anpassungen wurden schrittweise vorgenommen und mit den vorhandenen Testdateien beziehungsweise Beispieldaten kontrolliert.

Die KI übernahm nicht die pädagogische oder organisatorische Entscheidung. Insbesondere Gruppengrössen, Ausnahmen sowie die Zulässigkeit von Mischgruppen müssen weiterhin durch die verantwortliche Person beurteilt werden. Für mich war die KI vor allem ein Werkzeug, um Ideen schneller in einen funktionsfähigen Prototyp zu übersetzen und technische Probleme gezielt zu bearbeiten.

## 4. Herausforderungen und Erkenntnisse

Eine zentrale Herausforderung war die Übersetzung organisatorischer Regeln in eindeutige Programmlogik. Begriffe wie „möglichst klassenintern“ oder „nur wenn nötig mischen“ benötigen im Programm eine klare Reihenfolge und Gewichtung.

Weitere wichtige Erkenntnisse waren:

- Datenqualität ist entscheidend. Fehlende oder uneinheitliche Angaben müssen vor der Berechnung sichtbar gemacht werden.
- Eine automatische Lösung braucht immer eine manuelle Korrekturmöglichkeit.
- Ausnahmen dürfen nicht versteckt werden, sondern müssen klar gekennzeichnet sein.
- Datenschutz kann durch eine vollständig lokale Verarbeitung gestärkt werden.
- Export und Sicherung sind für den realen Einsatz ebenso wichtig wie die Berechnung selbst.
- Kleine Praxistests zeigen Bedienprobleme, die bei der reinen Entwicklung leicht übersehen werden. Die Öffnung aller drei Fachbereiche bei offenen Doppellektionen ist ein Beispiel dafür.

## 5. Reflexion

Das Projekt zeigt mir, dass KI die Entwicklung eines auf einen konkreten Schulprozess zugeschnittenen Werkzeugs stark beschleunigen kann. Ohne genaue Kenntnis des schulischen Ablaufs wäre jedoch keine brauchbare Lösung entstanden. Entscheidend war das Zusammenspiel zwischen meinem Fachwissen, dem schrittweisen Testen und der technischen Unterstützung durch KI.

Rückblickend fällt mir beim Vergleich mit meinem ersten Prompt auf, dass die wichtigsten Grundregeln von Anfang an formuliert waren, etwa die Trennung der Schulhäuser. Die KI setzte diese Vorgabe zunächst jedoch nur als Bevorzugung um. Erst meine Tests zeigten, dass ein Klassenblock trotzdem zwei Schulhäuser verbinden konnte (Phase 17). Andere Kriterien wie «Klassen gemischt» oder die Prioritäten der Doppellektion mussten im Verlauf deutlich genauer gefasst werden: Daraus wurden feste Klassenblöcke mit höchstens drei Klassen und Zweitwahlen, die nur im Notfall eingesetzt werden. Eine klare Vorgabe im Prompt garantiert also noch nicht, dass die KI sie auch verbindlich umsetzt. Die Kontrolle der Ergebnisse bleibt unverzichtbar.

Besonders gelungen finde ich die lokale und übersichtliche Lösung: Die Anwendung benötigt keinen Server, kann mit realistischen Testdaten ausprobiert werden und macht offene Fälle transparent. Gleichzeitig sehe ich Grenzen. Die gemeinsamen Klassenblöcke mit bis zu drei Klassen berücksichtigen die organisatorische Verbindung der Fächer; konkrete Raumbelegung, Lehrpersonen und weitere Stundenplanüberschneidungen werden jedoch noch nicht berechnet. Auch die gefundene Gruppierung bleibt ein Vorschlag und muss kontrolliert werden.

Für eine Weiterentwicklung würde ich strukturierte Tests mit echten, anonymisierten Planungsfällen durchführen, Rückmeldungen weiterer Anwenderinnen und Anwender einholen und die Regeln für manuelle Ausnahmezuteilungen noch deutlicher in der Oberfläche und in den Exporten dokumentieren.

In einem weiteren Schritt kann ich mir vorstellen, ein entsprechendes Werkzeug auch für die deutlich komplexere 3. Oberstufe zu entwickeln und weitere digitale Hilfsmittel für die Stundenplanung zu erstellen. Dieser Umfang würde jedoch über den vorliegenden Leistungsnachweis hinausgehen und wäre eher als Thema einer CAS-Abschlussarbeit geeignet.

## 6. Aktueller Stand

Die Anwendung liegt als eigenständige Datei `index.html` vor. Zwei anonymisierte Testdateien für die Schulhäuser Sennweid und Sternmatt stehen zur Verfügung. Der Funktionsumfang umfasst Import, Datenprüfung, automatische Gruppenbildung, manuelle Anpassung, getrennt dargestellte offene Doppel- und Einzelfachzuteilungen, CSV- und PDF-Export sowie das Sichern und Wiederöffnen eines Planungsstands. Die wiederholbaren Prüfungen sind in `verify.cjs` und für den Forms-Import in `verify-forms.cjs` dokumentiert. Zusätzlich zu den bisherigen CSV-Listen werden heruntergeladene Microsoft-Forms-Antworten als XLSX oder CSV unterstützt. Eine direkte SharePoint-Verbindung besteht nicht. Die Anwendung ist schuljahrunabhängig: Sie enthält keine fest eingetragenen Schuljahre, und Klassen sowie Fachwahlen stammen jeweils aus dem Import. Für jedes neue Schuljahr müssen lediglich die Klassenoptionen im Forms-Formular aktualisiert werden. Zudem muss die Zuordnung der Klassenbuchstaben a/b/c zu Schulhaus 1 und d/e/f zu Schulhaus 2 weiterhin gelten. Die Bedienoberfläche ist seit Phase 26 kompakter: Gruppengrössen und Texteingabe sind einklappbar, die Regeln stehen gekürzt unter der Gruppenübersicht, und vor dem Schliessen eines Tabs mit ungesicherten Änderungen erscheint eine Rückfrage.

Aktuell gelten folgende Standardgrenzen:

| Fach | Real: Minimum–Maximum | Sek: Minimum–Maximum |
|---|---:|---:|
| Bildnerisches Gestalten | 5–18 | 5–18 |
| Technisches Gestalten | 5–12 | 5–12 |
| Textiles Gestalten | 5–12 | 5–12 |
| Musik | 8–18 | 8–20 |
| Deutsch plus | 8–18 | 8–20 |
| Informatik plus | 8–18 | 8–20 |

Zusätzlich zeigt der aufklappbare Bereich «Klassen & Fächer» aus den vorhandenen Importdaten eine filterbare Klassen-/Fachübersicht mit Wahlen, Zuteilungen, offenen Fällen und Gruppenbelegung. Hinweise zu fehlenden Angaben und Engpässen aktualisieren sich mit der Einteilung. Die beiden bisherigen CSV-Dateien können weiterhin gemeinsam importiert werden; eine weitere Datei ist nicht nötig.

Die Grenzwerte sind einstellbar. Beim Öffnen eines gespeicherten Plans werden dessen Einstellungen übernommen; die aktuellen Standardwerte ersetzen bestehende gespeicherte Werte nicht automatisch.

Real und Sek sowie die beiden Schulhausbereiche bleiben strikt getrennt. Für alle sechs Fächer gelten gemeinsame disjunkte Klassenblöcke mit höchstens drei Klassen desselben Schulhauses und Niveaus. Klassenreine Gruppen innerhalb eines Blocks bleiben möglich. Passende Gruppen desselben Fachs im selben Klassenblock werden jedoch zusammengeführt, wenn ihre gemeinsame Grösse das Maximum nicht überschreitet. Dies gilt auch für passende Teilgruppen. Die frühere feste Vorgabe S2a + S2c entfällt. In der aktuellen Konstellation sind a/b sowie d/e/f innerhalb desselben Niveaus und Schulhauses kombinierbar. Offene Zuteilungen können nur in bestehende passende Gruppen mit tatsächlichen Mitschülerinnen und Mitschülern derselben Klasse verschoben werden; die maximale Gruppengrösse bleibt verbindlich.

Bei den Einzellektionen sind manuelle Wechsel zwischen passenden bestehenden Gruppen von Musik, Deutsch plus und Informatik plus möglich, unabhängig von der ursprünglichen festen Wahl. Diese bleibt für die automatische Berechnung und Kontrolle erhalten; manuelle Änderungen werden gespeichert und exportiert.

Die automatische Suche bildet zunächst Klassenblöcke ausschliesslich nach Erstwahlen. Zweitwahlen werden anschliessend nur für gezielte Notfallkorrekturen innerhalb derselben Blöcke eingesetzt: bei kleinen Unter- oder Überzahlen oder bei nicht zustande kommenden kleinen Gestaltungsfächern. Bereits mögliche Fachgruppen dürfen dabei nicht durch neue offene Fälle beeinträchtigt werden.

Nicht lösbare Fälle werden ausdrücklich offen ausgewiesen. Die Anwendung ist ein Planungswerkzeug; die pädagogische und organisatorische Prüfung bleibt bei der verantwortlichen Person.