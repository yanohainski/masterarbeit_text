

Du:
Ein weiteres Schlüsselmerkmal aktueller LLMs ist ihre Fähigkeit zu In-Context Learning. Das Modell nutzt dabei allein auf Basis der im Prompt bereitgestellten Beispiele oder Instruktionen neue Aufgabenstrukturen, ohne dass Parameteränderungen notwendig sind. Damit entsteht eine bemerkenswerte Flexibilität: Das Modell kann Aufgaben lösen, für die es nie explizit trainiert wurde, sofern die Aufgabenbeschreibung im Kontext ausreichend präzise ist.
%warum geht das? 02.02.26

ChatGPT:
Das funktioniert nicht „magisch“, sondern ist eine direkte Konsequenz dessen, wie moderne LLMs trainiert sind und was sie intern repräsentieren.

Der Kernpunkt: Ein LLM lernt beim Pretraining keine Aufgaben im klassischen Sinn, sondern eine extrem generalisierte Abbildung
„gegeben ein Kontext → wie geht der Text sinnvoll weiter“.
Dieser scheinbar einfache Lernauftrag zwingt das Modell, Strukturen, Muster und Relationen in Sprache zu internalisieren – inklusive Instruktionen, Beispiele, formaler Regeln und Problemlöseschritte.

Warum In-Context Learning dadurch möglich wird:

Erstens: Implizite Meta-Lernfähigkeit durch Training auf Vielfalt.
Während des Trainings sieht das Modell Milliarden von Texten, darunter Anleitungen, Q&A-Formate, Code, mathematische Herleitungen, Erklärungen mit Beispielen, Korrekturen usw. Viele dieser Texte haben die Form: Beschreibung einer Aufgabe → mehrere Beispiele → Lösung.
Das Modell lernt dabei nicht explizit „so lernt man neue Aufgaben“, aber es internalisiert statistisch genau dieses Muster. In-Context Learning ist daher kein zusätzliches Modul, sondern ein emergentes Verhalten.

Zweitens: Der Prompt fungiert als temporärer „Arbeitsraum“.
Die Parameter bleiben unverändert, aber der Kontext selbst wirkt wie ein flüchtiger Speicher. Beispiele im Prompt legen eine Aufgabenstruktur fest, und das Modell passt seine Vorhersagen dynamisch an diese Struktur an.
Man kann das als funktionale Anpassung ohne Gewichtsänderung verstehen: Das Modell konditioniert sein Verhalten vollständig auf den Kontext.

Drittens: Interne Repräsentationen sind auf Abstraktion ausgelegt.
LLMs bilden nicht nur Wörter ab, sondern hochdimensionale Repräsentationen von Konzepten, Relationen und Transformationen.
Wenn du im Prompt mehrere Beispiele gibst, erkennt das Modell die gemeinsame Transformation zwischen Eingabe und Ausgabe – selbst wenn die konkrete Aufgabe neu ist. Entscheidend ist nicht die Aufgabe, sondern die Regel, die sich aus dem Kontext rekonstruieren lässt.

Viertens: Attention ersetzt explizites Umschalten von Modulen.
Durch Self-Attention kann das Modell relevante Teile des Prompts gezielt heranziehen. Es „entscheidet“ nicht symbolisch, welche Aufgabe vorliegt, sondern gewichtet kontextuelle Hinweise probabilistisch.
Je präziser und konsistenter der Prompt, desto stabiler diese Gewichtung – daher die enorme Bedeutung von Prompt-Qualität.

Die unbequeme Wahrheit:
In-Context Learning ist keine Garantie, sondern ein statistisches Phänomen. Es funktioniert hervorragend, solange die Aufgabenbeschreibung klar ist und in den Raum dessen fällt, was das Modell strukturell abstrahieren kann. Sobald der Kontext widersprüchlich, zu lang oder konzeptionell neuartig wird, bricht das Verhalten sichtbar ein.

Kurz gesagt:
LLMs können In-Context Learning, weil sie beim Training gelernt haben, Instruktionen als Daten zu behandeln – und Daten als etwas, aus dem sich Regeln ableiten lassen. Das ist beeindruckend, aber nicht grenzenlos.


Du:
beschreibe das ganze in zwei bis drei sätzen um den text zu erweitern um das zu beschreiben

ChatGPT:
Das ist möglich, weil große Sprachmodelle beim Pretraining nicht auf feste Aufgaben, sondern auf das Erkennen und Fortführen von Mustern in sehr unterschiedlichen Kontexten optimiert werden. Beispiele und Instruktionen im Prompt fungieren dabei als temporäre Aufgabenbeschreibung, aus der das Modell die zugrunde liegende Regel abstrahiert, ohne seine Parameter anzupassen. In-Context Learning ist somit ein emergentes Verhalten, das aus der Kombination von vielfältigen Trainingsdaten, abstrakten internen Repräsentationen und kontextsensitiver Attention entsteht.




