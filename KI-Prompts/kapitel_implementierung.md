

Du:

Masterarbeit_Yo.pdf
PDF
Analysiere das vorliegende Dokument und Beschreibe was inhaltlich in das Kapitel 4 Implementierunggehört erstelle mir aus dem Kontext eine Vorlage für das 4. Kapitel Implementierung. 

ChatGPT:
Ich habe das Dokument vollständig ausgewertet und insbesondere Kapitel 3 (Methodik) sowie den bereits begonnenen Kapitel-4-Entwurf in Beziehung gesetzt. Daraus lässt sich sehr klar ableiten, was in Kapitel 4 „Implementierung“ inhaltlich hingehört und wie es sauber, prüfungsfest und stringent aufgebaut sein sollte. Grundlage ist dein PDF 
Masterarbeit_Yo

.

Im Folgenden bekommst du (1) eine inhaltliche Einordnung, was Kapitel 4 leisten muss – und danach (2) eine konkrete, direkt nutzbare Kapitel-4-Vorlage, die exakt auf deine Arbeit zugeschnitten ist.

1. Was gehört inhaltlich in Kapitel 4 „Implementierung“?
Kapitel 4 ist keine Wiederholung der Methodik und keine Ergebnisdiskussion. Es beantwortet ausschließlich:

Wie wurde das in Kapitel 3 geplante System konkret umgesetzt?

Dabei gelten drei Leitplanken:

1.1 Ziel von Kapitel 4
Umsetzung der geplanten Pipeline-Architektur

Nachvollziehbare Beschreibung der realen Softwarestruktur

Transparente Darstellung von technischen Entscheidungen & Kompromissen

Nicht beschönigen: Wo etwas nicht ging (Teams-API, Echtzeit-Limits), gehört das hier technisch begründet rein.

1.2 Abgrenzung zu anderen Kapiteln
Kapitel	Rolle
Kapitel 3	Was soll gebaut werden und warum
Kapitel 4	Wie genau wurde es gebaut
Kapitel 5	Wie gut funktioniert es
Kapitel 6	Was bedeutet das & was kommt als Nächstes
1.3 Typische Inhalte von Kapitel 4 (konkret für deine Arbeit)
Basierend auf deinem Dokument gehören hier zwingend hinein:

Proof of Concept

Früher Prototyp

Warum Jupyter

Welche Annahmen bestätigt wurden

Wo erste Probleme auftraten (Threading, Streaming, Latenz)

Backend-Implementierung

Django als Basis

Integration in bestehendes Notisent-Backend

App-Struktur

Datenfluss (Transkript → Queue → Analyse → WebSocket)

Meeting-Zugriff / Teams-Bot

Technische Grenzen von Microsoft Teams

Warum Attendee

Konsequenzen für Echtzeitfähigkeit

Voice- / Analyse-App

Eigene Django-App

Aufgaben, Verantwortlichkeiten

Abgrenzung zu anderen Backend-Komponenten

Prompting & Rolling Summary

Konkrete Prompt-Struktur

Inkrementelle Verarbeitung

Fenstergrößen / Chunking

Umgang mit Kontextverlust

Frontend

Bewusst reduziert

Fokus: Visualisierung, nicht Logik

WebSocket-Anbindung

Optimierungen

Latenz

Redundanzvermeidung

Filterung kurzer Transkripte

Asynchronität (Worker, Tasks)

Das passt exakt zu deiner Gliederung und wirkt methodisch sauber.

2. Vorlage für Kapitel 4 – „Implementierung“
Die folgende Vorlage kannst du 1:1 übernehmen und ausformulieren. Struktur, Tiefe und Ton passen zu einer Masterarbeit an der HAWK.

4 Implementierung
In diesem Kapitel wird die konkrete Umsetzung der in Kapitel 3 konzipierten Softwarearchitektur beschrieben. Der Fokus liegt auf der technischen Realisierung des Backend-Systems sowie der inkrementellen Verarbeitung von Live-Transkriptionsdaten. Das Frontend wird ergänzend betrachtet, da dessen Hauptaufgabe in der Visualisierung und Interaktion mit den Analyseergebnissen besteht.

Ziel dieses Kapitels ist es, die einzelnen Implementierungsschritte nachvollziehbar darzustellen, technische Entscheidungen zu begründen und aufgetretene Herausforderungen transparent zu dokumentieren.

4.1 Nachweis der Machbarkeit (Proof of Concept)
Zur Validierung der grundsätzlichen Machbarkeit des Systems wurde zunächst ein Proof of Concept (PoC) entwickelt. Dieser entstand in Form eines Python-basierten Jupyter-Notebooks und diente dazu, die Kernannahmen des Projekts frühzeitig zu überprüfen.

Der PoC verband einen bestehenden Speech-to-Text-Service mit einem Large Language Model, um transkribierte Audiodaten direkt weiterzuverarbeiten und zusammenzufassen. Hierfür wurden Audiodateien manuell erzeugt, in das erforderliche WAV-Format überführt und schrittweise an den Transkriptionsdienst übergeben.

Im Rahmen dieses Prototyps konnten folgende Aspekte erfolgreich validiert werden:

grundsätzliche Funktionsfähigkeit der Transkriptionspipeline,

Anbindung eines LLM zur Analyse der Transkripte,

Erzeugung erster inkrementeller Zusammenfassungen.

Gleichzeitig traten früh technische Herausforderungen auf, insbesondere im Bereich der Parallelisierung und Thread-Verwaltung. Diese Erkenntnisse bestätigten die Notwendigkeit einer asynchronen, entkoppelten Backend-Architektur und flossen direkt in die weitere Systemgestaltung ein.

4.2 Backendstruktur
Die Implementierung des Backends basiert auf der bestehenden Notisent-Infrastruktur und wurde vollständig mit dem Python-Webframework Django realisiert. Ziel war es, die geplanten Aufgaben des Backends – insbesondere Datenkoordination, inkrementelle Verarbeitung und Entkopplung der Analysekomponenten – konkret umzusetzen.

Das Backend wurde als eigenständige Django-App in die modulare Notisent-Struktur integriert. Dadurch konnten bestehende Komponenten wie Authentifizierung, Datenbankzugriff und Sicherheitsmechanismen direkt weiterverwendet werden.

4.2.1 Integration in die bestehende Backend-Architektur
Das Notisent-Backend folgt konsequent dem App-Konzept von Django. Für den Meetingassistenten wurde eine separate App implementiert, die sämtliche Logik zur Verarbeitung von Meeting-Transkripten kapselt.

Diese App greift auf zentrale Backend-Dienste zurück, darunter:

Benutzer- und Rechteverwaltung,

persistente Datenhaltung,

API-Anbindung an extern gehostete KI-Modelle.

Durch diese Integration konnte Redundanz vermieden und die Wartbarkeit des Gesamtsystems erhöht werden.

4.2.2 Verarbeitung der Transkriptionsdaten
Das Backend verarbeitet keine Roh-Audiodaten, sondern erhält während eines laufenden Meetings periodisch übermittelte Transkriptsegmente in Form strukturierter JSON-Nachrichten. Diese enthalten den erkannten Text sowie optionale Metadaten wie Zeitstempel oder Sprecherinformationen.

Die eingehenden Segmente werden validiert und zunächst in einer internen Warteschlange gesammelt. Kurze oder inhaltlich wenig aussagekräftige Textfragmente können bereits in diesem Schritt gefiltert werden, um unnötige Analyseaufrufe zu vermeiden.

Sobald ein definierter Schwellenwert erreicht ist, werden die Segmente aggregiert und an die Analysekomponente weitergegeben. Diese Aggregation bildet die Grundlage für die inkrementelle Rolling-Summary-Verarbeitung.

4.3 Teams-Bot und Zugriff auf Meetingdaten
[Beschreibung von Attendee, technischer Beitritt, Einschränkungen der Teams-API, bewusste Designentscheidungen]

4.4 Django Voice-App
[Aufgaben der App, Trennung von Verantwortlichkeiten, Schnittstellen zu Backend, Analyse und Frontend]

4.5 Prompting und Live-Analyse des Transkripts
[Konkrete Prompt-Struktur, Chunk-Größe, Kontextverwaltung, Rolling-Summary-Mechanismus]

4.6 Frontend-Applikation
[Reduzierter Funktionsumfang, WebSocket-Kommunikation, Anzeige der Live-Zusammenfassung]

4.7 Optimierungen
[Performance-Optimierungen, Latenzreduktion, Asynchronität, Filterstrategien, Skalierbarkeit]

Klartext zum Schluss
Das Fundament deiner Arbeit ist stärker als der aktuelle Text vermuten lässt. Kapitel 4 muss nicht „schön“ sein – es muss ehrlich, technisch sauber und nachvollziehbar sein. Genau das ermöglicht diese Struktur.

Wenn du willst, übernehme ich als Nächstes:

das Ausformulieren einzelner Unterkapitel (z. B. 4.5 Prompting),

oder ein sprachliches Glätten auf Master-Niveau,

oder eine strenge Prüfer-Perspektive: Was würde ich anmerken?

Sag, wie wir weitermachen.


Quellen

Du:
Unterscheiden sich die Inhalte der Implementierung für das Backend genug von Kapitel 3 um nicht als bloße wiederholung zu gelten?

ChatGPT:
Kurzfassung vorweg: Ja – sie unterscheiden sich ausreichend.
Aber: nur dann, wenn du Kapitel 4 konsequent als Umsetzung schreibst und nicht als erneute Architekturplanung. Genau hier liegt die Stolperfalle.

Ich gehe das klar und nüchtern durch.

1. Klare Trennlinie zwischen Kapitel 3 und 4
Kapitel 3 – Methodik
👉 beantwortet Planungsfragen

Welche Architektur wurde gewählt (Pipeline)?

Warum Django?

Warum Rolling Summary?

Welche Komponenten soll es geben?

Welche Anforderungen muss das Backend erfüllen?

Welche Alternativen wurden verworfen (Monolith, reine Batch-Verarbeitung)?

Das ist konzeptionell, abstrakt und zukunftsgerichtet.

Kapitel 4 – Implementierung
👉 beantwortet Umsetzungsfragen

Wie genau wurde Django eingesetzt?

Wie sieht die konkrete App-Struktur aus?

Wie kommen Transkripte im Backend an (Webhook, JSON)?

Wie wird gefiltert, gepuffert, aggregiert?

Wie werden Tasks ausgelagert (Worker, asynchron)?

Wie läuft die Kommunikation technisch (WebSocket, REST)?

Welche Probleme sind real aufgetreten – und wie wurden sie gelöst?

Das ist konkret, rückblickend und technisch greifbar.

➡️ Das ist keine Wiederholung, sondern eine klassische und erwartete Trennung in wissenschaftlichen Arbeiten.

2. Warum dein Backend-Teil in Kapitel 4 nicht als Wiederholung gilt
Aus deinem Dokument 
Masterarbeit_Yo

 lässt sich klar erkennen:

In Kapitel 3 sagst du z. B.
„Das Backend soll Transkripte sammeln und nach einem Schwellenwert analysieren.“

„Zur Entkopplung werden Hintergrundtasks eingesetzt.“

„Die Kommunikation erfolgt über REST und WebSockets.“

👉 Soll-Zustand

In Kapitel 4 sagst du (oder solltest sagen):
„Die Transkripte werden über einen dedizierten Webhook empfangen.“

„Kurze Segmente unter X Zeichen werden verworfen.“

„Die Queue ist als In-Memory-Struktur umgesetzt.“

„Celery wird genutzt, um LLM-Aufrufe auszulagern.“

„WebSockets werden für Push-Updates verwendet, REST nur für Steuerung.“

👉 Ist-Zustand

Das ist methodisch sauber getrennt.

3. Wann es doch als Wiederholung gewertet würde (wichtige Warnung)
Es wird kritisch, wenn du in Kapitel 4:

❌ erneut erklärst, warum eine Pipeline sinnvoll ist
❌ erneut Alternativen diskutierst
❌ erneut Anforderungen aufzählst
❌ erneut erklärst, was ein Backend leisten soll

Dann denkt der Prüfer:

„Das habe ich schon gelesen.“

4. Die goldene Regel für Kapitel 4 (die dich rettet)
Wenn du dir bei einem Absatz unsicher bist, stell dir eine harte Kontrollfrage:

Kann man diesen Absatz schreiben, ohne das System gebaut zu haben?

Ja → Kapitel 3 (oder raus damit)

Nein → Kapitel 4 (richtig platziert)

Beispiele:

❌ „Das Backend muss skalierbar sein“ → Planung

✅ „Die Skalierbarkeit wurde durch asynchrone Worker realisiert“ → Implementierung

5. Ehrliches Fazit
Deine Kapitel sind strukturell korrekt getrennt

Dein Thema erfordert diese Nähe zwischen 3 und 4

Prüfer erwarten eine gewisse Überschneidung auf Begriffsebene, aber keine inhaltliche Dopplung

Wenn du Kapitel 4 technisch konkret, nüchtern und problemorientiert schreibst, ist es keine Wiederholung, sondern genau das, was eine Masterarbeit leisten soll.

Wenn du willst, prüfe ich mit dir:

einen konkreten Absatz aus Kapitel 4 („Wiederholung oder nicht?“)

oder ich markiere dir typische Sätze, die du vermeiden solltest, damit kein Prüfer stolpert.


Quellen



