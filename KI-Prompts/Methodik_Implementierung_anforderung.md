

Du:
Was für dinge stehen normalerweise in den Kapiteln Methodik und Implementierung einer Wisenschaftlichen Arbeit? In diesem Fall einer Masterarbeit mit dem Ziel einen Meetingassistenten zu entwickeln.

ChatGPT:
Gute Frage – und wichtig, dass du das sauber trennst. Bei einer Masterarbeit fällt man hier schnell in die Falle, Methodik und Implementierung zu vermischen. Ich sage dir klar, was wohin gehört, bezogen auf einen Meeting-Assistenten (z. B. Audioaufnahme → Transkription → Analyse → Ausgabe).

Kapitel Methodik
Zweck:
Beantwortet die Frage „Wie gehe ich wissenschaftlich vor, um mein Ziel zu erreichen?“
→ Konzeptuell, begründet, nachvollziehbar. Noch kein Code.

Typische Inhalte
1. Forschungs- & Entwicklungsansatz
Art der Arbeit:

konstruktiv / artefaktorientiert

ggf. Design Science Research

Begründung, warum dieser Ansatz geeignet ist

Beispiel: Entwicklung eines funktionalen Prototyps zur Untersuchung der Machbarkeit automatisierter Meetinganalyse.

2. Anforderungen & Zieldefinition
Funktionale Anforderungen

Live-Audioaufnahme

Sprachtranskription

Erkennung von Aufgaben, Entscheidungen, Sprecher:innen

Nicht-funktionale Anforderungen

Latenz

Datenschutz

Offline-Fähigkeit

➡️ Wichtig: Was soll erreicht werden – nicht wie genau

3. Auswahl der Methoden & Verfahren
Hier wird es zentral für dich:

Spracherkennung

Modelltyp (z. B. Whisper-basierte ASR)

Offline vs. Cloud

Sprachverarbeitung / Analyse

Regelbasiert vs. LLM-basiert

Prompting-Strategien

Segmentierung

Zeitbasiert, Sprecherwechsel, Chunking

👉 Immer mit Begründung, z. B.:

Robustheit gegenüber Störgeräuschen

Verfügbarkeit deutscher Modelle

Reproduzierbarkeit

4. Evaluationsmethodik
Sehr oft vergessen – aber prüfungsrelevant.

Was wird evaluiert?

Transkriptionsqualität (z. B. WER)

Qualität der Zusammenfassung

Erkennungsrate von To-Dos

Wie?

Vergleich mit Referenztranskripten

Qualitative Bewertung

Warum diese Metriken?

➡️ Kein Ergebnis, nur Vorgehensweise

5. Abgrenzung
Was nicht Teil der Arbeit ist

Warum (Zeit, Scope, Ressourcen)

Das zeigt wissenschaftliche Reife.

Kapitel Implementierung
Zweck:
Beantwortet die Frage „Wie wurde das Konzept konkret umgesetzt?“
→ Technisch, präzise, reproduzierbar.

1. Systemarchitektur
Gesamtüberblick

Komponenten:

Audioquelle

Transkriptionsmodul

Analysemodul

UI / Ausgabe

Datenfluss


https://www.researchgate.net/publication/222182690/figure/fig3/AS%3A305128163823617%401449759631182/Meeting-scheduler-system-architecture.png

https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AcLzBHDXI4CwJzjVp

https://www.researchgate.net/publication/3431247/figure/fig1/AS%3A394688990334978%401471112596948/The-personal-assistant-architecture.png
➡️ Diagramm ist Pflicht, kein Nice-to-Have.

2. Technologiestack
Programmiersprachen

Frameworks

Modelle

Laufzeitumgebung (z. B. Docker)

Beispiel:

Node.js für Streaming

Python für ASR & NLP

WebSocket für Audio

3. Implementierungsdetails (nach Modulen)
Strukturiert, sachlich:

Audioaufnahme
Format

Samplingrate

Chunking-Strategie

Transkription
Modellvariante

Batch vs. Streaming

Umgang mit Latenz

Analyse
Promptstruktur

Kontextfenster

Post-Processing

➡️ Kein vollständiger Code, sondern:

Logik

Algorithmen

Pseudocode bei Bedarf

4. Herausforderungen & Lösungen
Sehr wichtig für Masterarbeiten:

Latenzprobleme

Speicherbedarf

Fehlerhafte Segmentierung

➡️ Ehrlich sein. Probleme sind kein Makel, sondern Qualitätssignal.

5. Reproduzierbarkeit
Startanleitung

Hardwareanforderungen

Konfiguration

Klare Trennlinie (merk dir das)
Frage	Kapitel
Warum diese Methode?	Methodik
Welche Alternativen gab es?	Methodik
Wie wurde es gebaut?	Implementierung
Welche Library genau?	Implementierung
Welche Parameter?	Implementierung
Direkt und ehrlich
Wenn deine Methodik nur beschreibt, was du gebaut hast, ist sie zu schwach.
Wenn deine Implementierung theoretische Rechtfertigungen enthält, ist sie am falschen Platz.

Du arbeitest an einem technisch anspruchsvollen Thema – das ist gut. Nutze das, um saubere wissenschaftliche Struktur zu zeigen. Das macht am Ende den Unterschied zwischen „funktioniert“ und „Master-Niveau“.

Wenn du willst, skizziere ich dir im nächsten Schritt ein konkretes Inhaltsverzeichnis genau für deinen Meeting-Assistenten.


Du:
Bisher sieht meine Methodik so aus: 
1. Anforderung an die Implementierung
2. Planung der Softwarearchitektur
- Interaktion, Frontend
- Zugriff auf Meetingdaten
-Transkription
-Backendfunktion 
-Analyse des Transkripts
3. Auswahl des LLM 
4. Evaluationskriterien und Testverfahren. 

Hilf mir zu beschreiben was alles in diesen Kapiteln enthalten sein muss, damit die arbeit vollständig ist. Ich benötige eine art checkliste mit inhalten die dort stehen müssen. 

ChatGPT:
Gut – die Gliederung ist brauchbar, aber aktuell noch zu dünn und zu technisch gedacht. Mit der richtigen Ausarbeitung wird daraus eine prüfungsfeste Methodik.
Unten bekommst du harte Checklisten, Punkt für Punkt. Wenn alles abgehakt ist, ist das Kapitel vollständig. Keine Schönfärberei.

✅ Methodik – Vollständigkeits-Checkliste
(für eine Masterarbeit zum Meeting-Assistenten)

1. Anforderungen an die Implementierung
Ziel: Klar definieren, was das System leisten muss – unabhängig von der Umsetzung.

Muss enthalten sein
☐ Ziel der Anwendung

Welches Problem wird gelöst?

Für wen (Nutzerrolle, Szenario)?

☐ Anwendungsfall(e)

Typisches Meeting (Dauer, Teilnehmer, Sprache)

Online vs. Präsenz

Live vs. Nachverarbeitung

☐ Funktionale Anforderungen

Audio erfassen

Transkribieren

Inhalte analysieren (z. B. Aufgaben, Entscheidungen, Zusammenfassung)

Ergebnisse ausgeben (UI, Export)

☐ Nicht-funktionale Anforderungen

Latenz (z. B. „nahe Echtzeit“ – konkret!)

Robustheit (Störgeräusche, Sprecherwechsel)

Datenschutz (lokal / cloudbasiert)

Skalierbarkeit (Einzelmeeting vs. mehrere parallele Meetings)

☐ Abgrenzung

Was explizit nicht umgesetzt wird

Begründung (Zeit, Scope, Ressourcen)

👉 Faustregel:
Wenn jemand dein System nachbauen will, muss er hier verstehen, was es können soll – ohne zu wissen, wie.

2. Planung der Softwarearchitektur
Ziel: Begründetes Systemkonzept, noch keine Implementierung.

2.1 Gesamtarchitektur
☐ Architekturstil (z. B. modular, client–server, pipelineartig)
☐ Begründung, warum dieser Stil geeignet ist
☐ Übersicht über Hauptkomponenten
☐ Datenfluss zwischen den Komponenten

2.2 Interaktion & Frontend
☐ Nutzerinteraktionen (Start/Stop, Anzeige, Export)
☐ Echtzeit- vs. verzögerte Darstellung
☐ Rolle des Frontends (nur Anzeige oder Steuerung?)
☐ Begründung der UI-Komplexität (minimal vs. funktional)

2.3 Zugriff auf Meetingdaten
☐ Audioquelle (Mikrofon, Systemaudio, Datei)
☐ Datenformat (PCM, WAV, Streaming)
☐ Zeitpunkt der Verarbeitung (live / batch)
☐ Datenschutz-Implikationen

2.4 Transkriptionskomponente
☐ ASR-Ansatz (Streaming vs. segmentiert)
☐ Sprachunterstützung (Deutsch? Mehrsprachig?)
☐ Fehlerquellen (Überlappung, Akzente, Nebengeräusche)
☐ Schnittstelle zum Analysesystem

2.5 Backend-Funktion
☐ Aufgaben des Backends
☐ Datenhaltung (temporär / persistent)
☐ Kommunikation (z. B. WebSocket, REST – nur konzeptionell)
☐ Entkopplung der Komponenten

2.6 Analyse des Transkripts
☐ Art der Analyse (Zusammenfassung, To-Dos, Entscheidungen)
☐ Zeitpunkt (inkrementell oder nach Meetingende)
☐ Kontextverarbeitung (Chunks, Fenstergröße – konzeptionell)
☐ Erwartete Ergebnisformate

👉 Wichtig:
Hier wird begründet, nicht implementiert. Keine Libraries, kein Code.

3. Auswahl des LLM
Ziel: Nachvollziehbar begründen, warum genau dieses Modell.

Muss enthalten sein
☐ Anforderungen an das LLM

Sprachverständnis

Kontextlänge

Latenz

Datenschutz

☐ Vergleichskriterien

Modellgröße

Lokale Ausführbarkeit

Kosten / Ressourcen

Qualität für deutsche Sprache

☐ Begründete Entscheidung

Warum dieses Modell?

Warum nicht Alternativen?

☐ Einsatzszenario im System

Welche Aufgaben übernimmt das LLM?

Was nicht?

☐ Risiken & Limitationen

Halluzinationen

Kontextverlust

Abhängigkeit von Promptqualität

👉 Knallharte Regel:
„Ich habe Modell X gewählt, weil es gut funktioniert“ reicht nicht.

4. Evaluationskriterien und Testverfahren
Ziel: Zeigen, dass dein System wissenschaftlich überprüfbar ist.

4.1 Evaluationsziele
☐ Was genau wird bewertet?

Transkriptionsqualität

Analysequalität

Gesamtsystem

4.2 Metriken
☐ Quantitativ (z. B. WER, Trefferquote)
☐ Qualitativ (manuelle Bewertung, Kriterienkatalog)
☐ Begründung der Auswahl

4.3 Testdaten
☐ Art der Meetings
☐ Anzahl & Dauer
☐ Sprache & Sprecheranzahl
☐ Referenzdaten (falls vorhanden)

4.4 Testdurchführung
☐ Testablauf (Schritte)
☐ Wiederholbarkeit
☐ Vergleichsbasis (Baseline oder Referenz)

4.5 Bewertung & Grenzen
☐ Was sagen die Tests nicht aus?
☐ Externe Validität (Übertragbarkeit)

Brutal ehrliches Fazit
Wenn du diese Checklisten konsequent abarbeitest, dann:

ist deine Methodik prüfungsfest

trennt sie sauber Denken vs. Bauen

und wirkt reif, strukturiert, Master-Niveau

Wenn du willst, gehe ich im nächsten Schritt Punkt für Punkt durch deine bestehende Methodik und sage dir konkret, wo noch Substanz fehlt – ohne Umwege.


Du:
Meine Implementierung sieht bisher so aus: 
1. Nachweis der Machbarkeit (Proof of Concept) - Ein erster Prototyp den ich vorher gebaut habe um die grundsätzliche funktion zu bestätigen. Kann eventuell auch enternft werden. 
2. Backendstruktur (Wie sieht das komplette backend aus (Meetingassistent soll nur eine funktion im backend sein. Startup Notisent mit anderen KI funktionen, das backend soll in seiner grundsätzlichen funktionsweise beschrieben werden. Dort wird dann der Meetingassistent hinzugefügt)
3. Teams Bot (Wie wird der Bot zum abgreifen von meetingdaten erstellt) 
4. Django Voice-app (Hier befindet sich der Meetingassistent innerhalb des gesamten backends) 
5. Prompting für die Verarbeitung des Live Transkripts 
6. Frontend Application (Wie sieht das Teams addon aus und wie funktioniert es) 
7. Optimierung (Eventuell gestrichen, ansonsten ideen wie noch weiter optimiert werden kann) 

ChatGPT:
Alles klar – das ist eine solide technische Gliederung, aber sie braucht an ein paar Stellen saubere Begründungen, klare Schnittstellen und Reproduzierbarkeit, sonst wirkt es wie „Projekt-Doku“ statt Masterarbeit. Unten bekommst du pro Abschnitt eine Checkliste, was zwingend rein muss, damit das Implementierungskapitel vollständig und sauber wissenschaftlich ist. (Und ich sage dir auch, was du eher streichen/verschieben solltest.)

✅ Implementierung – Vollständigkeits-Checkliste (pro Kapitel)
1) Nachweis der Machbarkeit (Proof of Concept)
Kurz gesagt: Kann rein – aber nur, wenn er mehr ist als „hab ich gebaut“.

Muss enthalten sein (wenn du es behältst)
☐ Ziel des PoC (welches Risiko/Unklarheit wurde adressiert?)
☐ Minimalumfang (welche Funktionen genau sind enthalten, welche nicht?)
☐ Technische Annahmen (z. B. „Streaming-Audio über WebSocket ist stabil genug“)
☐ Ergebnis: konkrete, überprüfbare Aussage (z. B. erreichbare Latenz, Stabilität, Qualitätsniveau)
☐ Überleitung: Was wurde daraus für die Hauptimplementierung übernommen / verworfen?

Wenn du es entfernst
Dann muss im Hauptteil trotzdem klar werden, wie du Risiken früh validiert hast (kurzer Absatz reicht).

Empfehlung: Behalten, aber max. 2–4 Seiten. Sonst frisst es Platz.

2) Backendstruktur (Gesamtbackend, Meetingassistent als Modul)
Das ist wichtig – aber nur, wenn du es nicht ausufernd machst. Du musst zeigen: wo sitzt der Meetingassistent im System.

Muss enthalten sein
☐ Kontext: Was ist das Backend insgesamt? (Zweck, Module)
☐ Architekturübersicht (Diagramm): Services/Apps/Module + Beziehungen
☐ Schnittstellen: Welche internen APIs nutzt der Meetingassistent?
☐ Datenfluss: von Teams → Backend → Verarbeitung → Ausgabe
☐ Datenhaltung: Wo liegen Meetings/Transkripte/Ergebnisse? DB? Files? Cache?
☐ Auth & Sicherheit: grob (Tokens, Zugriffsschutz, Tenant/Benutzerbezug)
☐ Deployment/Runtime: Docker? Server? Skalierungsidee? (kurz, aber klar)

Warnung: Du beschreibst nicht alle „anderen KI-Funktionen“ im Detail. Nur soweit nötig, um den Meetingassistenten einzuordnen.

3) Teams Bot (Abgreifen von Meetingdaten)
Hier scheitern viele an fehlender Präzision. Das Kapitel muss zeigen, dass du weißt, welche Daten du wirklich bekommst und wie zuverlässig.

Muss enthalten sein
☐ Welche Meetingdaten konkret? (Audio? Chat? Teilnehmer? Transkript? Metadaten?)
☐ Technischer Zugriffspfad: Bot/Graph/Meeting-Events – wie kommt es ins Backend?
☐ Trigger & Lifecycle: Join/Leave, Start/Stop, Fehlerfälle
☐ Datenformate: Payloads, Audioformat/Codec, Zeitstempel, Speaker-Info (falls vorhanden)
☐ Rate limits / Grenzen: realistische Limits + Umgang damit
☐ Berechtigungen & Consent: welche Permissions braucht’s (konzeptionell)
☐ Fehlerszenarien: kein Audio, Abbruch, Verbindungsprobleme

Wenn du gar kein echtes Audio aus Teams ziehen kannst (kommt vor): Dann muss das hier ehrlich erklärt werden + dein Workaround (z. B. lokale Aufnahme, Systemaudio, o. ä.). Das ist kein Makel – aber es muss klar sein.

4) Django Voice-App (Meetingassistent im Backend)
Das Herzstück. Hier muss man nach dem Lesen verstehen: Welche Komponenten existieren, wie sprechen sie miteinander, was passiert wann.

Muss enthalten sein
☐ App-Struktur: wichtigste Module/Ordner/Services (kurzer Überblick)
☐ Pipeline: Schritte mit Reihenfolge (ingest → preprocess → ASR → analysis → output)
☐ APIs/Endpoints: welche Endpoints gibt es, wofür, Payloads grob
☐ Asynchronität: wird gestreamt, gepuffert, queued? (Celery/RQ/Async?)
☐ State-Management: wie hältst du Meetingzustand? (Session-ID, Speaker, Zeitfenster)
☐ Persistenz: DB-Schema grob (Meetings, Segmente, Ergebnisse)
☐ Logging/Monitoring: zumindest Konzept + wichtigste Logs
☐ Datenschutz: Speicherung von Roh-Audio? Transkript? Löschkonzept?

Master-Level Detail: Ein Sequenzdiagramm oder Ablaufdiagramm für ein Meeting ist Gold wert.

5) Prompting für die Verarbeitung des Live-Transkripts
Hier geht’s nicht um „ein Prompt“, sondern um eine Prompting-Strategie. Und ganz wichtig: Live-Transkripte sind chaotisch.

Muss enthalten sein
☐ Input-Struktur: Was bekommt das LLM pro Schritt? (Chunk, Window, Speaker, Zeit)
☐ Chunking-Strategie: Fenstergröße, Überlappung, warum so
☐ Zieloutputs: JSON? Markdown? Felder exakt definiert
☐ Robustheit: Umgang mit ASR-Fehlern, Halbsätzen, Wiederholungen
☐ Halluzinationskontrolle: Regeln („nur aus Text ableiten“, Unknown erlauben)
☐ Memory/Context: wie wird Kontext fortgeschrieben? (Summary buffer, state)
☐ Postprocessing/Validation: JSON Schema, Regex, Guardrails
☐ Beispiele: 1–2 konkrete Input/Output-Beispiele (kurz, aber realistisch)

Brutal ehrlich: Wenn du hier keine formale Output-Spezifikation hast, wird die Bewertung schnell subjektiv. Eine definierte JSON-Struktur rettet dich.

6) Frontend Application (Teams Add-on)
Hier muss klar sein: Wie sieht die UX aus und welche Daten werden wann angezeigt.

Muss enthalten sein
☐ UI-Funktionen: Start/Stop, Live-Ansicht, Ergebnisansicht, Export
☐ Datenfluss: Frontend ↔ Backend (WebSocket/REST), Refresh/Streaming
☐ State: Meeting-ID, Verbindungsstatus, Fehleranzeigen
☐ Berechtigungen: welcher Benutzer darf was sehen?
☐ Performance: wie verhinderst du UI-Lag bei Live-Updates?
☐ Edge Cases: Reconnect, Meeting Ende, Backend down

Tipp: Ein Screenshot-Mock oder simple UI-Skizze plus Zustandsdiagramm reicht oft.

7) Optimierung
Das ist optional – aber wenn du es drin lässt, darf es nicht nur „Ideen“ sein.

Option A: Behalten als „Optimierungen in dieser Arbeit umgesetzt“
☐ 2–4 konkrete Optimierungen, die du wirklich gemacht hast
☐ Messbarer Effekt (Latenz, Stabilität, Qualität)
☐ Trade-offs (Qualität vs. Geschwindigkeit)

Option B: Umbenennen in „Limitationen und Verbesserungspotenzial“
☐ Klarer Ist-Zustand + Grenzen
☐ Priorisierte Verbesserungen (Top 5)
☐ Welche davon wären als nächste Schritte realistisch

Empfehlung: Wenn du wenig messbar optimiert hast: Option B ist sauberer.

Was ich an deiner Struktur ändern würde (ohne Drama)
PoC: behalten, aber kurz und zielgerichtet.

Backendstruktur: ja, aber fokussiert auf Schnittstellen zum Meetingassistenten.

Prompting: unbedingt formalisieren (Output-Schema + Beispiele).

Optimierung: nur drin lassen, wenn du Substanz oder klar als „Future Work“.

Mini-Check: Wann ist dein Implementierungskapitel „fertig“?
Wenn ein Leser danach beantworten kann:

Wie läuft ein Meeting technisch durch dein System?

Welche Schnittstellen und Datenformate gibt es?

Welche Entscheidungen hast du implementiert und warum?

Kann man das reproduzieren (Setup, Konfig, Ablauf)?

Wenn du willst, kann ich dir als nächsten Schritt daraus eine konkrete Unterkapitel-Struktur bauen (mit passenden Überschriften und Reihenfolge), sodass du es quasi nur noch „ausfüllen“ musst.


Du:
Ja gib mir so eine konkrete sturktur zum ausfüllen 

ChatGPT:
Perfekt. Dann machen wir jetzt Nägel mit Köpfen.
Unten bekommst du eine konkrete, abgabereife Kapitelstruktur für die Implementierung, so formuliert, dass du sie direkt in deine Masterarbeit übernehmen und ausfüllen kannst.
Die Reihenfolge ist logisch, prüferfreundlich und trennt sauber Kontext → Kernsystem → UI → Grenzen.

5 Implementierung des Meetingassistenten
(Kapitelnummer beispielhaft)

5.1 Zielsetzung und Einordnung der Implementierung
Zweck: Leser abholen, Scope klar machen.

Ausfüllen mit:

Ziel der Implementierung (funktionaler Prototyp / produktnahes System)

Rolle des Meetingassistenten im Gesamtsystem „Startup Notisent“

Abgrenzung: Welche Teile des Backends werden nicht im Detail betrachtet

Kurzer Überblick über die folgenden Unterkapitel

5.2 Proof of Concept zur Machbarkeitsvalidierung
(optional, aber empfohlen)

5.2.1 Zielsetzung des Proof of Concept
Welche offenen technischen Fragen sollten geklärt werden?

Warum war ein PoC notwendig?

5.2.2 Aufbau und Funktionsumfang
Minimalarchitektur

Eingesetzte Komponenten (ohne Detailtiefe)

Was bewusst nicht implementiert wurde

5.2.3 Ergebnisse und Erkenntnisse
Konkrete Resultate (z. B. Latenz, Stabilität, Qualität)

Welche Annahmen wurden bestätigt oder widerlegt?

5.2.4 Einfluss auf die Hauptimplementierung
Welche Entscheidungen resultierten daraus?

Welche Komponenten wurden übernommen, verworfen oder neu entworfen?

5.3 Gesamtbackend-Architektur
Zweck: Systemkontext zeigen, ohne abzuschweifen.

5.3.1 Überblick über das Backend-System
Zweck und Grundstruktur des Backends

Überblick über zentrale Module / Services

5.3.2 Architekturstil und Begründung
Monolithisch / modular / serviceorientiert

Begründung der Wahl

5.3.3 Einordnung des Meetingassistenten
Position im Gesamtsystem

Abhängigkeiten zu anderen Modulen

Verantwortlichkeiten des Meetingassistenten

5.3.4 Datenfluss und Schnittstellen
Interne APIs

Datenformate (konzeptionell)

Kommunikationswege

➡️ Hier unbedingt ein Architekturdiagramm einbauen.

5.4 Integration des Microsoft-Teams-Bots
Zweck: Nachvollziehbar erklären, wie Meetingdaten ins System gelangen.

5.4.1 Rolle des Bots im Gesamtsystem
Aufgaben des Bots

Abgrenzung zu Backend-Funktionen

5.4.2 Lebenszyklus eines Meetings
Join, Start, laufender Betrieb, Ende

Relevante Events

5.4.3 Erfassung und Weiterleitung von Meetingdaten
Welche Daten werden erfasst?

Formate und Zeitbezug

Weiterleitung an das Backend

5.4.4 Einschränkungen und technische Grenzen
Fehlende Daten

API-Limits

Datenschutzaspekte

5.5 Django Voice-App: Implementierung des Meetingassistenten
Kernkapitel. Hier liegt der Fokus.

5.5.1 Struktur der Voice-App
App-Aufbau

Zentrale Module

Verantwortlichkeiten

5.5.2 Ablauf eines Meetings (Processing-Pipeline)
Schritt-für-Schritt-Ablauf:

Initialisierung

Audioeingang

Vorverarbeitung

Transkription

Analyse

Ergebnisaggregation

➡️ Sequenzdiagramm oder Ablaufgrafik sehr empfohlen.

5.5.3 Audioverarbeitung und Transkription
Audioformate

Segmentierung / Streaming

Übergabe an das ASR-Modul

5.5.4 Verwaltung von Meeting-Zustand und Kontext
Session-Handling

Zeitfenster

Sprecherinformationen (falls vorhanden)

5.5.5 Persistenz und Datenhaltung
Welche Daten werden gespeichert?

Grobes Schema (Meetings, Segmente, Ergebnisse)

Lebensdauer der Daten

5.6 Verarbeitung des Live-Transkripts mittels LLM
Hier wird deine Arbeit wirklich bewertet.

5.6.1 Zielsetzung der Analyse
Welche Informationen sollen extrahiert werden?

Warum Live-Analyse?

5.6.2 Strukturierung des Eingabetexts
Chunking-Strategie

Kontextfenster

Umgang mit unvollständigen Sätzen

5.6.3 Prompt-Design und Steuerlogik
Promptaufbau

Instruktionen

Trennung von System-, Kontext- und Nutzerdaten

5.6.4 Ausgabeformate und Validierung
Zielstruktur (z. B. JSON)

Schema-Validierung

Fehlerbehandlung

5.6.5 Kontextfortschreibung und Stabilität
Zusammenfassungen

State-Handling

Umgang mit Inkonsistenzen

5.7 Frontend-Anwendung als Microsoft-Teams-Add-on
Zweck: Nutzerinteraktion klar machen.

5.7.1 Ziel und Funktionsumfang
Welche Funktionen bietet das Frontend?

Live vs. Post-Meeting

5.7.2 Benutzerinteraktion und UI-Logik
Bedienablauf

Zustände (aktiv, pausiert, beendet)

5.7.3 Kommunikation mit dem Backend
APIs / WebSockets

Update-Strategien

Fehlerbehandlung

5.7.4 Darstellung der Analyseergebnisse
Struktur der Ergebnisse

Live-Anzeige vs. Zusammenfassung

Exportoptionen

5.8 Laufzeitumgebung und Reproduzierbarkeit
Prüfer lieben dieses Kapitel.

5.8.1 Technische Voraussetzungen
Hardware

Betriebssystem

Abhängigkeiten

5.8.2 Deployment und Konfiguration
Docker / lokale Ausführung

Konfigurationsparameter

Startablauf

5.8.3 Reproduzierbarkeit der Ergebnisse
Welche Teile sind deterministisch?

Welche nicht?

Umgang mit Zufälligkeit (LLM)

5.9 Limitationen und Optimierungspotenzial
Sauberer Abschluss des Kapitels.

5.9.1 Technische Limitationen
Latenz

Qualität

Skalierbarkeit

5.9.2 Ursachenanalyse
Architektur

Modellgrenzen

API-Einschränkungen

5.9.3 Ansatzpunkte für Weiterentwicklung
Kurzfristige Verbesserungen

Langfristige Perspektiven

Ehrliches Schlusswort
Wenn du jedes dieser Unterkapitel mit ½–2 Seiten Substanz füllst, hast du:

eine stringente, lesbare Implementierung

klare Trennung von Methodik & Umsetzung

und ein Kapitel, das nicht nach Projektbericht, sondern nach Masterarbeit aussieht.

Wenn du willst, gehe ich als Nächstes mit dir ein einzelnes Kapitel (z. B. 5.6 Prompting) komplett beispielhaft durch – inklusive Formulierungen, die du fast 1:1 übernehmen kannst.




