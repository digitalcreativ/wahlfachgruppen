# Logbuch zum Leistungsnachweis

## Projekt: Digitale Einteilung der Wahlfachgruppen 2. Oberstufe

**Ausbildung:** CAS Bildung im digitalen Wandel – KI-Modul  
**Projektkontext:** Schulen Baar  
**Verfasserin:** Claudia Bürgisser  
**Bearbeitungsstand:** 4. November 2026

> Hinweis: Die früheren Entwicklungsschritte wurden anhand des aktuellen Projektstands und der vorhandenen Dateien rückblickend zusammengefasst. Der Eintrag vom 3. November 2026 entstand direkt im Anschluss an die Anpassung.

## 1. Ausgangslage und Zielsetzung

Die Einteilung der Schülerinnen und Schüler in die Wahlfachgruppen der 2. Oberstufe ist anspruchsvoll. Neben den Fachwünschen müssen Gruppengrössen, Klassen, Schulhäuser sowie die Trennung von Real und Sek berücksichtigt werden. Eine manuelle Einteilung ist zeitaufwendig und fehleranfällig.

Ziel meines Projekts war deshalb die Entwicklung eines einfachen digitalen Werkzeugs, das aus vorhandenen Schülerlisten automatisch einen Vorschlag für die Wahlfachgruppen erstellt. Das Werkzeug sollte ohne Installation und ohne Übertragung personenbezogener Daten an einen externen Server funktionieren. Gleichzeitig war mir wichtig, dass die automatisch erzeugte Lösung von einer Person überprüft und manuell angepasst werden kann.

## 2. Entwicklungsprozess

### Phase 1: Anforderungen klären und Daten verstehen

Zu Beginn analysierte ich, welche Angaben für die Einteilung notwendig sind. Dazu gehören Name, Klasse, Niveau, Schulhaus, Erst- und Zweitwahl für die Doppellektion sowie das gewählte Fach der Einzellektion.

Ich legte folgende Grundregeln fest:

- Die drei Fachbereiche der Doppellektion sind Bildnerisches Gestalten, Technisches Gestalten und Textiles Gestalten.
- Die Einzellektion umfasst Musik, Deutsch plus und Informatik plus.
- Gruppen sollen wenn möglich klassenintern gebildet werden.
- Reicht dies nicht aus, dürfen Klassen innerhalb desselben Schulhauses gemischt werden.
- Erst danach werden schulhausübergreifende Gruppen geprüft.
- Real und Sek bleiben grundsätzlich getrennt. Eine Mischung ist nur als gekennzeichnete Ausnahme bei zu kleinen Gruppen vorgesehen.
- Mindest- und Maximalgrössen müssen einstellbar sein.

Eine besondere Herausforderung waren unterschiedliche CSV-Strukturen. Neben einer Standardliste sollte auch eine Fachmatrix eingelesen werden können. Fehlende oder mehrdeutige Angaben dürfen dabei nicht automatisch erfunden werden, sondern müssen sichtbar bleiben.

### Phase 2: Erster funktionsfähiger Prototyp

Ich entwickelte eine eigenständige Browseranwendung in einer HTML-Datei. Sie kann lokal geöffnet werden und verarbeitet alle Daten nur im Arbeitsspeicher des Browser-Tabs. Dadurch ist keine Installation nötig und die Daten bleiben auf dem verwendeten Gerät.

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

## 3. Einsatz von künstlicher Intelligenz

Ich setzte KI als Unterstützung bei der Konzeption, Programmierung, Fehlersuche und sprachlichen Überarbeitung ein. Dabei formulierte ich die Anforderungen und prüfte die vorgeschlagenen Lösungen anhand der schulischen Einteilungsregeln. Anpassungen wurden schrittweise vorgenommen und mit den vorhandenen Testdateien beziehungsweise Beispieldaten kontrolliert.

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

Besonders gelungen finde ich die lokale und übersichtliche Lösung: Die Anwendung benötigt keinen Server, kann mit realistischen Testdaten ausprobiert werden und macht offene Fälle transparent. Gleichzeitig sehe ich Grenzen. Raumbelegung, Lehrpersonen, Stundenplanüberschneidungen und weitere organisatorische Bedingungen sind bisher nicht Bestandteil der Berechnung. Auch die gefundene Gruppierung bleibt ein Vorschlag und muss kontrolliert werden.

Für eine Weiterentwicklung würde ich strukturierte Tests mit echten, anonymisierten Planungsfällen durchführen, Rückmeldungen weiterer Anwenderinnen und Anwender einholen und die Regeln für manuelle Ausnahmezuteilungen noch deutlicher in der Oberfläche und in den Exporten dokumentieren.

## 6. Aktueller Stand

Die Anwendung liegt als eigenständige Datei `index.html` vor. Zwei Testdateien für die Schulhäuser Sennweid und Sternmatt stehen zur Verfügung. Der aktuelle Funktionsumfang umfasst Import, Datenprüfung, automatische Gruppenbildung, manuelle Anpassung, offene Zuteilungen, CSV- und PDF-Export sowie das Sichern und Wiederöffnen eines Planungsstands.
