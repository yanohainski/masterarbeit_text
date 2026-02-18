

Du:
Gibt es eine Metrik, nach welcher sich KI zusammenfassungen von Texten vergleichen lassen? 18.11.25

ChatGPT:
Ja, es gibt mehrere etablierte Metriken – aber du solltest wissen: Keine davon ist perfekt. Jede misst nur einen Ausschnitt davon, was „gute“ Zusammenfassungen eigentlich ausmacht. Trotzdem geben sie dir eine solide Orientierung, wenn du Modelle vergleichen willst.

🔍 Gängige automatische Metriken
1. ROUGE (1, 2, L, etc.)
Die bekannteste Familie. Sie misst Überlappungen von Wörtern oder Phrasen zwischen Referenzzusammenfassung und Modelloutput.

Vorteil: Schnell, gut vergleichbar.

Nachteil: Bewertet eher Oberflächenform statt echtes Verständnis.

2. BLEU
Eigentlich für Übersetzungen entwickelt, funktioniert aber auch für Summaries – mit ähnlichen Schwächen wie ROUGE.

Vorteil: Standardisiert.

Nachteil: Für Zusammenfassungen oft zu streng und unflexibel.

3. BERTScore
Vergleicht nicht Wörter, sondern deren semantische Einbettungen.

Vorteil: Erfasst Bedeutung besser als ROUGE.

Nachteil: Abhängig vom gewählten Embedding-Modell.

4. MoverScore
Eine Art „semantische Transportdistanz“ zwischen Text und Referenz.

Vorteil: Semantisch sensibler.

Nachteil: Rechenintensiver.

🧠 Moderne LLM-basierte Metriken
Diese funktionieren, indem ein Sprachmodell die Qualität beurteilt.
Beispiele:

GPTScore

G-Eval

LENS

QAF-A / QAF-R

Sie können Aspekte prüfen wie:

Faktentreue

Abdeckung der wichtigsten Punkte

Kohärenz

Stil / Lesbarkeit

Vorteil: Deutlich näher an menschlichen Bewertungen.
Nachteil: Teurer, und abhängig vom bewertenden Modell.

🎯 Was du wirklich vergleichen solltest
Wenn du pragmatisch arbeitest, achte vor allem auf diese Kriterien:

Inhaltsabdeckung: Deckt die Summary die zentralen Ideen ab?

Präzision: Wird nichts Wichtiges hinzu erfunden?

Kürze: Ist sie knapp ohne Informationsverlust?

Lesbarkeit: Klingt sie logisch und verständlich?

Automatische Metriken helfen – aber sie ersetzen nicht die menschliche Bewertung. Nutze sie als Werkzeug, nicht als Wahrheit.

Wenn du magst, kann ich dir auch sagen, welche Metrik für welches Szenario am sinnvollsten ist.


Du:
Ich möchte mein System, welches Live zusammenfassungen per Rolling Summary erzeugt mit nachträglichen Zusammenfassungen über ein Transkript vergleichen um die effektivität des systems messbar zu machen. 

ChatGPT:

Nachgedacht für 22s
Super, das ist ein sehr sinnvolles Ziel – und ja, du kannst dein Rolling-Summary-System ziemlich systematisch messen. Denk in zwei Dimensionen:

Wie gut ist der Inhalt am Ende? (Qualität der finalen Zusammenfassung)

Wie gut ist es unterwegs? (Wie schnell und korrekt tauchen Infos in der Live-Summary auf?)

Ich skizziere dir einen konkreten Evaluations-Plan.

1. Referenz festlegen
Du brauchst pro Aufnahme / Gespräch drei Dinge:

Transkript (vollständig) – das hast du ohnehin.

„Gold“-Zusammenfassung aus dem vollständigen Transkript

Entweder von Menschen geschrieben

Oder von einem starken LLM mit sorgfältigem Prompt, im Zweifel von dir kurz nachbearbeitet.

Rolling Summary deines Systems

Entweder nur der Endzustand

Oder idealerweise Snapshots alle X Sekunden / nach X Tokens.

Die Gold-Summary ist deine Referenz, gegen die du misst.

2. Qualität der finalen Zusammenfassung messen
Hier behandelst du dein Live-System wie ein „normales“ Summarisierungsmodell.

2.1 Automatische Overlap-Metriken
Vergleiche finale Rolling-Summary vs. Gold-Summary mit z. B.:

ROUGE-1 / ROUGE-2 / ROUGE-L

BERTScore (semantischer Overlap)

Damit bekommst du z. B. für jede Aufnahme Werte wie:

ROUGE-1: 0.47

ROUGE-L: 0.41

BERTScore F1: 0.86

Diese kannst du mitteln über viele Gespräche und mit einem „Offline“-System vergleichen, das die Zusammenfassung nur nachträglich aus dem Transkript erzeugt.

👉 Interpretation:

Offline-Summary = „Upper bound“

Rolling-Summary sollte im Idealfall „nah dran“ liegen (z. B. 90–95 % des Scores).

2.2 LLM-/Human-Judgements
Overlap-Metriken sagen nicht alles. Sinnvoll ist zusätzlich:

Kriterien:

Abdeckung: Deckt die Summary die wichtigsten Punkte des Transkripts ab? (0–5)

Korrektheit / Faktentreue: Erfindet sie Dinge oder verzerrt sie Inhalte? (0–5)

Klarheit & Struktur: Verständlich, gut lesbar? (0–5)

Du kannst z. B. pro Gespräch folgendes machen:

Offline-Summary = Referenz

Rolling-Summary = zu bewertende Summary

Entweder Menschen oder ein LLM bewerten nach oben genannten Kriterien.

So bekommst du z. B.:

System	Abdeckung	Korrektheit	Klarheit
Offline (Transkript-basiert)	4.6	4.8	4.5
Rolling (Live)	4.2	4.5	4.3
Damit wird ziemlich klar, wie „weit drunter“ dein Live-System liegt.

3. Streaming-spezifische Metriken (der spannende Teil)
Ein Rolling-System soll nicht nur gut sein, sondern früh gut sein.
Dafür brauchst du Zeitbezug.

3.1 Key-Point-Recall über die Zeit
Extrahiere aus dem Transkript Key Points (manuell oder mit LLM), z. B.:

Beschluss A

Aufgabe B

Info C

Für jeden Key Point bestimmst du:

Zeitpunkt, wann er im Transkript gesagt wird: t_speech

Dann schaust du in deinen Rolling-Summary-Snapshots:

Erster Snapshot, in dem dieser Key Point inhaltlich korrekt auftaucht: t_summary

Nun kannst du pro Key Point berechnen:

Erfassungs-Latenz: t_summary - t_speech

Recall(t): „Wie viel Prozent der Key Points sind nach X Minuten bereits in der Summary enthalten?“

Beispiel:

Nach 5 Minuten: 60 % aller späteren Key Points sind schon erwähnt

Nach 10 Minuten: 80 %

Am Ende: 95 %

Das zeigt sehr anschaulich, wie „reaktiv“ dein System ist.

3.2 „Drift“ vs. finale Offline-Summary
Du kannst zusätzlich messen, wie stark sich die Rolling-Summary während des Gesprächs der finalen Offline-Summary annähert.

Vorgehen:

Erzeuge Offline-Gold-Summary S_gold.

Erzeuge Rolling-Snapshots S_t zu Zeitpunkten t = 1min, 2min, ....

Für jeden Snapshot berechne Overlap (ROUGE/BERTScore) zwischen S_t und S_gold.

Dann bekommst du eine Kurve:

t=2min: ROUGE-L = 0.20

t=5min: 0.35

t=10min: 0.45

t=Ende: 0.52

Das zeigt, wie „schnell“ deine Live-Zusammenfassung auf ein Niveau kommt, das nah an der bestmöglichen (Offline-)Zusammenfassung liegt.

4. Konkreter Vergleich: Rolling vs. Offline-System
Am Ende kannst du z. B. so auswerten:

Endqualität:

ROUGE/BERTScore Rolling vs. Gold

ROUGE/BERTScore Offline vs. Gold

→ Verhältnis Rolling / Offline in %

Zeitverhalten:

Durchschnittliche Erfassungs-Latenz pro Key Point

Recall der Key Points nach X Minuten

Kurve „ROUGE vs. Gold über die Zeit“

Subjektive Qualität (LLM/Human):

Durchschnittspunkte pro Kriterium (Abdeckung, Faktentreue, Klarheit)

Damit kannst du sehr klar sagen:

„Unser Live-System erreicht 92 % der inhaltlichen Qualität des Offline-Systems, erfasst 80 % der Schlüsselpunkte innerhalb von 2 Minuten und hat im Schnitt eine Latenz von 30 Sekunden pro Key Point.“

Das ist dann wirklich messbar und kommunizierbar.

Wenn du willst, kann ich dir im nächsten Schritt ganz konkret:

ein kleines Schema / JSON-Format für deine Evaluationsdaten vorschlagen

oder Pseudocode (Python) skizzieren, wie du die Metriken berechnest.


Du:
Gib mir wissenschaftliche Paper für deine Infos, besonders zu den verschiedenen benchmarks

ChatGPT:
Gerne. Hier sind einige wissenschaftliche Arbeiten, die sich mit Metriken zur Bewertung von Textzusammenfassungen befassen — sie liefern eine solide Grundlage für deine Evaluation und helfen dir, die Limitationen zu verstehen.

Wichtige Paper und Studien
BERTScore: Evaluating Text Generation with BERT — Zhang et al. (2019)
Beschreibt die Metrik BERTScore, welche kontextuelle Einbettungen nutzt zur Bewertung von generierten Texten. 

Nutzbar zur Bewertung von Zusammenfassungen — besserer semantischer Vergleich als klassische N-gram-Metriken.

Understanding the Extent to which Summarization Evaluation Metrics Measure the Information Quality of Summaries — Deutsch & Roth (2020)
Untersucht kritisch, inwiefern Metriken wie ROUGE und BERTScore wirklich „Informationsüberlappung“ messen. 

Wichtiger Hinweis: Auch semantische Metriken messen nicht perfekt, was du eigentlich willst (z. B. Faktentreue, Abdeckung).

A Benchmark of metrics for text summarization — Gorceix & Keusch (~2022)
Vergleich verschiedener Metriken (ROUGE, BLEU, BERTScore etc.) auf System- und Zusammenfassungs-Level für Zusammenfassungsaufgaben. 

Wichtig: Zeigt sehr schwache bis moderate Korrelationen zwischen automatischen Metriken und menschlichen Bewertungen.

Re‑Evaluating Evaluation for Multilingual Summarization — Forde et al. (2024)
Untersucht, wie gut gängige Metriken in mehrsprachigen Umgebungen funktionieren (nicht nur Englisch). 

Hinweis: Deine Anwendung (z. B. deutschsprachiger Text) profitiert davon, da Limitationen auf anderen Sprachen gezeigt werden.

EVA‑Score: Evaluating Abstractive Long‑form Summarization on Informativeness through Extraction and Validation — Fan et al. (2024)
Neue Metrik (EVA-Score) speziell für lange Zusammenfassungen, mit Fokus auf Informationsgehalt statt nur Überlappung. 

Besonders relevant, wenn dein System lange Texte oder Live-Streams zusammenfasst.

Empfehlungen für deine Anwendung
Nutze mindestens eine klassische Metrik wie ROUGE (L/N) zur Basis.

Ergänze mit semantischer Metrik wie BERTScore.

Da du Live & später per Transkript vergleichst: Achte auf Zeit- bzw. Verlaufsmetriken (nicht immer in diesen Papers ausgeführt).

Beachte: Viele Arbeiten berichten, dass Autometric Scores nur begrenzt mit menschlicher Bewertung korrelieren. Beispiel: Gorceix fand auf „Sum-Up-Level“ niedrige Korrelationen. 

Wenn du deutschsprachige oder lange Texte hast, nutze Studien wie Forde et al. (2024) bzw. Fan et al. (2024) — zeigt, dass Standardmetriken dort schwächer sein können.

Wenn du möchtest, kann ich eine komplette Literaturliste mit ~10–15 Papers zusammenstellen (inklusive Links) speziell für Zusammenfassungsmetriken und Evaluation von Streaming- bzw. Rolling-Zusammenfassungen. Möchtest du das?




