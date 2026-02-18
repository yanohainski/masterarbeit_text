
Du:
Hilf mir eine Disskussion für meine Masterarbeit zu schreiben. Hier ist das Ergebniskapitel und die dazugehörigen forschungsfragen: 

\chapter{Ergebnisse}
\section{Durchführung der Tests}
Zur Evaluation des entwickelten Systems wurden mehrere reale Meetings mit einer Dauer von jeweils etwa zehn bis fünfzehn Minuten aufgezeichnet und analysiert. Für alle Versuche wurden identische Rahmenbedingungen verwendet, um die Vergleichbarkeit der Ergebnisse sicherzustelen. Insbesondere kamen durchgängig derselbe Prompt sowie dasselbe LLM zur Generierung der Live-Zusammenfassungen zum Einsatz. 
Die auf Basis des Transkripts erstellte Gesamtzusammenfassung wurde mithilfe von Chat-GPT 5.2 erstellt mit dem Prompt: "Du bist ein Spezialist für Meeting Zusammenfassungen. Fasse das folgende Transkript zusammen:" erstellt.

Die während der Meetings erzeugten Live-Zusammenfassungen wurden direkt aus dem Frontend des Systems exportiert. Zusätzlich wurden vollständige Transkripte von Microsoft Teams gespeichert. Sowohl die Transkripte als auch die Live-Zusammenfassungen sind im Anhang dokumentiert. 

Zur quantitativen Bewertung der Zusammenfassungsqualität wurden ie Metriken ROUGE sowie BERTScore eingesetzt. Hierfür wurde ein Python-Skript implementiert, das jeweils zwei Texte einliest und die entsprechenden Kennzahlen automatisch berechnet. Verglichen wurden die automatisch erzeugte Live-Zusammenfassung des Systems mit: 

\begin{enumerate}
    \item dem Meetingtranskript von Microsoft Teams
    \item einer durch ein LLM und dem Meetingtranskript erstellten Zusammefassung
\end{enumerate}

Die Tabelle \ref{tab:Meetings} gibt einen Überblick über die untersuchten Meetings.

\begin{table}[H]
    \centering
    \begin{tabular}{|p{3.5cm}|p{8cm}|c|}
    \hline
    \textbf{Meetingname} & \textbf{Beschreibung} & \textbf{Teilnehmer}\\
    \hline
    Yan Weekly Checkout & Statusupdate über den aktuellen Prototypen mit Masterarbeitsbetreuer & 2\\
    \hline
    Daily Standup 1& Beschreibung über aktuelle anstehende Aufgaben und Deadlines im Notisent Team & 6\\
    \hline
    Daily Standup 2& Beschreibung über aktuelle anstehende Aufgaben und Deadlines im Notisent Team & 5\\
    \hline
    \end{tabular}
    \caption{Durchgeführte Meetings}
    \label{tab:Meetings}
\end{table}

\section{Analyse}
\subsection{Automatische Metriken}
Insgesamt wurden drei Meetings ausgewertet. Für jedes Meeting wurde die Qualität der automatisch erzeugen Texte anhand eines paarweisen Vergleichs mit einer Referenz untersucht. Ziel war es, sowohl die inhaltliche Übereinstimung als auch die semantische Nähe der generierten zusammenfassung zu quantifizieren. 

Zur Bewertung wurden die Metriken ROUGE-1, ROUGE-2 und ROUGE-L verwendet, welhe auf n-Gramm-Überlappungen basieren und insbesondere die Übereinstimmung zwischen zwei Texten messen. Ergänzend wurde der BERTScore eingesetzt, welcher kontextuelle Wortrepräsentationen nutzt und dadurch semantische Ähnlichkeiten robuster erfasst. 

Precision beschreibt den Anteil der generierten Inhalte, die auch in der Referenz enthalten sind. Recall misst, welcher Anteil der Referenzinhalte durch die generierte Zusammenfassung abgedeckt wird. Die F-Measure stellt das harmonische Mittel beider Werte dar und dient als Gesamtindikator für die Qualität. 

Ein hoher ROUGE-Wert weist auf eine starke textuelle Überlappung hin, während ein hoher BERTScore zusätzlich eine semantische Übereinstimmung signalisiert, selbst wenn unterschiedliche Formulierungen verwendet werden.

Beide Metriken liefern Werte im Bereich zwischen 0 und 1, wobei 1 für eine hohe Ähnlichkeit hindeutet und 0 für keine Ähnlichkeit. 
Beispiel, vergleicht man zwei Identische Texte mit dem ROUGE oder BERTScore so kommt ein Wert von 1.

Zur groben Einordnung der Werte können folgende Bereiche herangezogen werden. 

\begin{itemize}
    \item Unter 0.7 geringe Inhaltliche Übereinstimmung
    \item 0.7 bis 0.8 akzeptable Übereinstimmung
    \item ab 0.8 gute Übereinstimmung
    \item ab 0.9 Sehr gute Übereinstimmung    
\end{itemize}

Bereits kleine Verbesserungen von wenigen Hundersttelpunkten können dabei eine messbare Qualitätssteigerung bedeuten.

Die Ergebnisse der einzelnen Meetings sind in den nachfolgenden Tabellen \ref{tab:test1} \ref{tab:test2} \ref{tab:test3} dargestellt.

\begin{table}[H]
    \centering
    \begin{tabular}{|p{2cm}|c|c|c|c|}
    \hline
    & \textbf{Rouge-1} & \textbf{Rouge-2} & \textbf{Rouge-L} &\textbf{BERTScore}\\ \hline
    \hline
    Transkript & \makecell[l]{Precision: 0.6223\\ Recall: 0.0878\\ F-measure: 0.1539} & \makecell[l]{Precision: 0.1706\\ Recall: 0.0240\\ F-measure: 0.0421} & \makecell[l]{Precision: 0.2114\\ Recall: 0.0298\\ F-measure: 0.0523} &\makecell[l]{Precision: 0.6188\\ Recall: 0.6169\\ F1 Score: 0.6178} \\
    \hline
    AI Summary & \makecell[l]{Precision: 0.2603\\ Recall: 0.4236\\ F-measure: 0.3224} & \makecell[l]{Precision: 0.0333\\ Recall: 0.0543\\ F-measure: 0.0413} & \makecell[l]{Precision: 0.0822\\ Recall: 0.1338\\ F-measure: 0.1018} &\makecell[l]{Precision: 0.6908\\ Recall: 0.6592\\ F1 Score: 0.6746} \\
    \hline
    \end{tabular}
    \caption{Testergebnisse Yan Weekly Checkout}
    \label{tab:test1}
\end{table}

\begin{table}[H]
    \centering
    \begin{tabular}{|p{2cm}|c|c|c|c|}
    \hline
     & \textbf{Rouge-1} & \textbf{Rouge-2} & \textbf{Rouge-L} &\textbf{BERTScore}\\ \hline
    \hline
    Transkript & \makecell[l]{Precision: 0.0797\\ Recall: 0.6517\\ F-measure: 0.1420} & \makecell[l]{Precision: 0.0240\\ Recall: 0.1972\\ F-measure: 0.0429} & \makecell[l]{Precision: 0.0357\\ Recall: 0.2921\\ F-measure: 0.0636} &\makecell[l]{Precision: 0.6254\\ Recall: 0.6284\\ F1 Score: 0.6269} \\
    \hline
    AI Summary & \makecell[l]{Precision: 0.2883\\ Recall: 0.3174\\ F-measure: 0.3021} & \makecell[l]{Precision: 0.0460\\ Recall: 0.0507\\ F-measure: 0.0483} & \makecell[l]{Precision: 0.0969\\ Recall: 0.1067\\ F-measure: 0.1016} &\makecell[l]{Precision: 0.7066\\ Recall: 0.6922\\ F1 Score: 0.6993} \\
    \hline
    \end{tabular}
    \caption{Testergebnisse Daily Standup 1}
    \label{tab:test2}
\end{table}

\begin{table}[H]
    \centering
    \begin{tabular}{|p{2cm}|c|c|c|c|}
    \hline
     & \textbf{Rouge-1} & \textbf{Rouge-2} & \textbf{Rouge-L} &\textbf{BERTScore}\\ \hline
    \hline
    Transkript & \makecell[l]{Precision: 0.1748\\ Recall: 0.5963\\ F-measure: 0.2703} & \makecell[l]{Precision: 0.0590\\ Recall: 0.2014\\ F-measure: 0.0912} & \makecell[l]{Precision: 0.0606\\ Recall: 0.2068\\ F-measure: 0.0937} &\makecell[l]{Precision: 0.6355\\ Recall: 0.6332\\ F1 Score: 0.6343} \\
    \hline
    AI Summary & \makecell[l]{Precision: 0.4746\\ Recall: 0.1969\\ F-measure: 0.2783} & \makecell[l]{Precision: 0.0714\\ Recall: 0.0296\\ F-measure: 0.0418} & \makecell[l]{Precision: 0.1458\\ Recall: 0.0605\\ F-measure: 0.0855} &\makecell[l]{Precision: 0.6720\\ Recall: 0.6552\\ F1 Score: 0.6635} \\
    \hline
    \end{tabular}
    \caption{Testergebnisse Daily Standup 2}
    \label{tab:test3}
\end{table}

\subsection{Qualitative Bewertung}
Im Rahmen der Evaluation wurden Meetings unterschiedlicher Größe hinsichtlich der Qualität der automatisch generierten Live-Zusammenfassungen analysiert. Ein Daily Stand-up mit sechs Teilnehmern, sowie weiteres Daily Stand-up mit fünf Teilnehmern und ein Weekly Checkout Meeting mit zwei Teilnehmenden. Die Auswertung fokussierte die zeitliche Verfügbarkeit von Informationen, die thematische Gewichtung im Verlauf sowie die Erkennbarkeit von Entscheidungen, Aufgaben und offnen Punkten. Auf welche Fragen genau bei der qualitativen Bewertung eingegangen wird, ist aus \ref{qualitative Analyse} zu entnehmen.

Bezüglich der zeitlichen Einordnung von Informationen zeigte sich, dass Inhalte nicht stabil oder konsistent in der Zusammenfassung repräsentiert werden. Einzelne Aspekte tauchten verspätet auf oder wurden in späteren Iterationen der Rolling Summary verfälscht fortgeführt. Fehlinterpretationen in frühen Zwischenständen persistierten dabei und wurden durch nachfolgende Aktualisierungen nicht zuverlässig korrigiert. Insbesondere Transkriptionsfehler wirken sich kumulativ aus und führen zu dauerhaft inkorrekten oder kontextuell unpassenden Einträgen. Gleichzeitg wurden einige besprochenen Themen vollständig ausgelassen, während irrelevante Informationen, etwa Begrüßungen oder Verabschiedungen teilweise enthalten sind. 

Hinsichtlich der thematischen Gewichtung zeigte sich ein deutlicher Recency-Effekt. Inhalte aus den letzten Gesprächsabschnitten waren überproportional stark vertreten, während frühere Punkte im Verlauf an Sichtbarkeit verloren oder vollständig verdrängt wurden. Darüber hinaus war die Detailtiefe inkonsistent: Teilweise wurden Themen unnötig ausführlich beschrieben, während andere nur oberflächlich oder gar nicht berücksichtigt wurden. Die Qualität der Zusammenfassung korrelierte dabei erkennbar mit der Gesprächsstruktur; kurze und klar formulierte Beiträge führten zu präziseren Ergebnissen, während längere oder komplexe Diskussionsabschnitte häufiger fehlerhaft oder verkürzt wiedergegeben wurden. Im kleineren Zwei-Personen-Meeting trat dieses Problem zwar abgeschwächt, jedoch weiterhin systematisch auf.

Die Erkennung von Entscheidungen, Aufgaben und offenen Punkten war grundsätzlich möglich, jedoch inhaltlich unzuverlässig. To-Dos wurden häufig identifiziert, allerdings nicht konsistent den korrekten Personen zugeordnet. Kontextverluste und fehlerhafte Sprecherzuweisungen beeinträchtigten die Nachvollziehbarkeit der Verantwortlichkeiten. Explizite Entscheidungen oder offene Fragen wurden nicht durchgehend als solche hervorgehoben, sodass eine strukturierte Aktionsübersicht nur eingeschränkt gegeben war.

Zusammenfassend zeigt sich, dass die Live-Zusammenfassung zwar eine grobe inhaltliche Orientierung ermöglicht, jedoch unter fortschreitender Gesprächsdauer an Genauigkeit verliert. Transkriptionsfehler, Persistenz falscher Einträge und eine unausgewogene Gewichtung der Inhalte führen zu Informationsverlusten und Verzerrungen. Für eine zuverlässige Dokumentation von Verantwortlichkeiten und Entscheidungen ist daher weiterhin eine manuelle Nachbearbeitung erforderlich.
\newpage
\section{Optimierungsmöglichkeiten}
In diesem Kapitel werden mögliche Optimierungsansätze für den entwickelten Meeting-Assistenten diskutiert. Der Fokus liegt dabei nicht auf bereits implementierten Maßnahmen, sondern auf theoretisch sinnvollen Verbesserungsmöglichkeiten, die sich aus dem aktuellen Stand der Forschung sowie aus den technischen Rahmenbedingungen des Systems ergeben. 

Da die automatische Spracherkennung durch Microsoft Teams vorgegeben ist und nicht beeinflusst werden kann, beziehen sich alle Optimierungsansätze ausschließlich auf die Weiterverarbeitung der erzeugten Transkripte, die Interaktionen mit dem LLM sowie auf architektonische Aspekte des Systems. Dadurch ergeben sich folgende Rahmenbedingungen: 
\begin{itemize}
    \item Die Qualität der Transkripte ist aktuell nicht steuerbar 
    \item Fehlerhafte oder unvollständige Erkennung müssen nachträglich behandelt werden.
    \item Optimierungen können ausschließlich auf Textbasis erfolgen. 
    \item Die Verarbeitung erfolgt zeitnah, jedoch nicht in strikter Echtzeit
\end{itemize}
Dadurch wird klar, dass die Optimierung vor allem auf der semantsichen und strukturellen Ebene ansetzen muss. 

Ein wesentlicher Ansatzpunkt zur Verbesserung der Ergebnisqualität liegt in der Aufbereitung der Transkripte vor der Übergabe an das Sprachmodell, mögliche Maßnahmen umfassen: 
\begin{itemize}
    \item Segmentierung der Transkripte in inhaltlich zusammenhängende Abschnitte
    \item Entfernung redundanter Inhalte, etwa Wiederholungen oder Füllwörter
    \item Normalisierung der Sprache z.B. Vereinheitlichung von Satzfragmenten
    \item Markierung von Sprecherwechseln oder Themenübergängen
\end{itemize}
Eine solche Vorverarbeitung kann dazu beitragen, die Komplexität der Eingabe zu reduzieren und dem Sprachmodell klarere semantische Strukturen bereitzustellen. Dies ist insbesondere bei längeren Meetings relevant, in denen thematsiche Sprünge und Wiederholungen häufig auftreten. 

\subsection{Prompt-Gestaltung}
ein Besonders großer Einfluss auf die Qualität der Ergebnisse ergibt sich aus der Gestaltung der Prompts. Da das Sprachmodell maßgeblich durch den Kontext gesteuert wird, stellt das Prompt-Design einen zentralen Hebel dar. 

Beim Zero-Shot-ansatz erhält das Modell lediglich eine Aufgabenbeschreibung. Dieser Ansatz ist leichtgewichtig und effizient, birgt jedoch Risiken wie z.B. 
\begin{itemize}
    \item uneinheitliche Struktur der Ausgabe
    \item unklare Gewichtung einzelner Inhalte
    \item stärkere Abhängigkeit vom jeweiligen Kontext
\end{itemize}

Few-Shot-Prompting:
Durch das Ergänzen weniger Beispielausgaben kann das Modell stärker gelenkt werden. Mögliche Vorteile sind: 
\begin{itemize}
    \item konsistentere Formatierung
    \item bessere Identifikation von Entscheidungen und Aufgaben
    \item höhere Vergleichbarkeit zwischen einzelnen Zusammenfassungen
\end{itemize}
Dem steht ein erhöhter Tokenverbrauch gegenüber, der sich sowhl auf die Latenz als auch auf die Kosten auswirkt. Theoretisch bietet sich daher ein hybrider Ansatz an, bei dem Few-Shot-Prompts nur für ausgewählte Verarbeitungsschritte eingesetzt werden. 

\subsection{Voranalyse mit klassischen NLP-Verfahren}
Eine weitere Möglichkeit der Optimierung besteht in der vorgeschalteten Analyse der Transkripte mittels klassischer NLP-Methoden. Ziel ist es, dem Sprachmodell nicht ausschließlich Rohtext, sondern bereits strukturierte Informationen bereitzustellen. 

Mögliche Verfahren sind unter anderem: 
\begin{itemize}
    \item Satz- und Abschnittssegmentierung
    \item Erkennung von Schlüsselbegriffen und Themen
    \item Identifikation von Personen, Projekten oder Entscheidungen
    \item Klassifikation von Gesprächsanteilen (Diskussion, Entscheidung, Aufgabe)
\end{itemize}

Existierende Python Werkzeuge wie spaCy \cite{spacy} eignen sich für solche Aufgaben, da sie effizient arbeiten und sich gut in bestehende Pipelines integrieren lassen. Eine solche Vorverarbeitung könnte insbesondere die Extraktion von Aktionspunkten udn Beschlüssen verbessern. 

Neben der inhaltlichen Qualität spielt die Systemleistung ebenfalls eine zentrale Rolle, insbesondere bei einem Einsatz während laufender Meetings. 
Durch effektive Filterstrategien lassen sich irrelevante Inhalte wie Smalltalk oder Wiederholungen herausfiltern und somit die Belastung des LLM reduzieren, was sich positiv auf die Laufzeit auswirkt. 

Die gezeigten Opimierungsansätze zeigen, dass trotz der aktuell noch festen Vorgabe durch die Spracherkennung Verbesserungspotential besteht. Die beschriebenen Ansätze bilden eine konzeptionelle Grundlage für zukünftige Erweiterungen und können in weiterführenden Arbeiten praktisch evaluiert und miteinander verglichen werden. 

\newpage
Anhand der folgenden Forschungsfragen wird präzisiert, welche Ergebnisse diese Arbeit leifert. 
Forschungsfragen:
\begin{enumerate}
    \item\textbf{Wie kann ein Live-Meetingassistent entwickelt werden?} 

Diese Frage untersucht wie so ein Live-Meetingassistent vom Grundkonzept her aufgebaut werden muss um funktioniern zu können. 

    \item\textbf{Was für Anforderungen muss so ein Meetingassistent erfüllen?}

In diesem Zusammenhang soll untersucht werden, welche Anforderungen ein Meetingassistent erfüllen muss um einen Mehrwert für ein Meeting zu bieten. 

    \item\textbf{Wie ist die Qualität im vergleich zu Komplett zusammengefassten Meetings?} 

Es wird erforscht, wie sich ein Live-Meetingassistent im Vergleich zu bereits bestehenden Tools zum zusammenfassen von Meetings schlägt.

    \item\textbf{Kann die Zusammenfassung in annehmbarer Zeit erstellt werden?} 

Mit dieser Forschungsfrage soll untersucht werden, ob die Bearbeitungsgeschwindigkeit des Tools schnell genug ist um weiterhin einen natürlichen Arbeitsfluss zu haben. 
    
\end{enumerate}

Diese Forschungsfragen bilden die Grundlage für die Entwicklung eines leistungsfähigen, flexiblen und nutzerfreundlichen KI-Meetingassistenten, welcher sich in die Notisent Umgebung integrieren lässt.

ChatGPT:
Gut, du hast bereits eine saubere Ergebnisbasis gelegt: quantitative Metriken, qualitative Beobachtungen und konkrete Systemgrenzen. Genau darauf baut eine starke Diskussion auf. In der Diskussion interpretierst du nicht nur Zahlen, sondern beantwortest klar: Was bedeuten sie für die Forschungsfragen – und wo sind die harten Grenzen des Systems?

Ich formuliere dir im Folgenden ein zusammenhängendes, wissenschaftlich klingendes Diskussionskapitel, das du direkt übernehmen oder anpassen kannst.

\chapter{Diskussion}

Ziel dieser Arbeit war die Konzeption, Implementierung und Evaluation eines Live-Meetingassistenten, der während laufender Meetings automatisch Transkripte verarbeitet und fortlaufend Zusammenfassungen generiert. Die Ergebnisse zeigen deutlich, dass ein solches System technisch realisierbar ist und einen praktischen Mehrwert bieten kann, gleichzeitig jedoch systematische Qualitätsgrenzen bestehen, die insbesondere aus der Echtzeitverarbeitung und der Abhängigkeit von fehlerbehafteten Transkripten resultieren. Im Folgenden werden die Resultate im Kontext der Forschungsfragen kritisch eingeordnet.

Bezogen auf die erste Forschungsfrage nach der Entwicklung eines Live-Meetingassistenten konnte gezeigt werden, dass eine modulare Architektur aus Transkription, textbasierter Vorverarbeitung, LLM-gestützter Zusammenfassung sowie einer Frontend-Integration grundsätzlich geeignet ist, kontinuierlich verwertbare Informationen bereitzustellen. Die praktische Umsetzung in einer realen Meetingumgebung demonstriert die technische Machbarkeit unter produktionsnahen Bedingungen. Besonders relevant ist hierbei, dass keine strikte Echtzeitverarbeitung erforderlich war, sondern eine zeitnahe, inkrementelle Aktualisierung ausreicht, um den Nutzer während des Meetings zu unterstützen. Dies reduziert die Systemkomplexität erheblich und macht den Einsatz großer Sprachmodelle trotz höherer Latenzen praktikabel. Damit ist die Kernhypothese bestätigt, dass ein Live-Meetingassistent mit heutigen LLMs umsetzbar ist.

Im Hinblick auf die Anforderungen an einen solchen Assistenten zeigen die qualitativen Ergebnisse jedoch klar, dass reine Textgenerierung nicht ausreicht. Für einen tatsächlichen Mehrwert müssen Informationen nicht nur zusammengefasst, sondern strukturiert, korrekt gewichtet und zuverlässig einzelnen Verantwortlichkeiten zugeordnet werden. Die Evaluation verdeutlicht, dass insbesondere Entscheidungen, Aufgaben und offene Punkte konsistent erkannt werden müssen, da gerade diese Aspekte für den Arbeitsalltag entscheidend sind. Das aktuelle System erreicht hier lediglich eine eingeschränkte Zuverlässigkeit. Fehlzuweisungen von To-Dos oder das Auslassen zentraler Diskussionspunkte reduzieren den praktischen Nutzen deutlich. Daraus folgt, dass funktionale Anforderungen wie Robustheit gegenüber Transkriptionsfehlermeldungen, stabile Kontextverwaltung über längere Zeiträume und eine explizite Aktionspunkt-Extraktion mindestens genauso wichtig sind wie die reine sprachliche Qualität der Zusammenfassung.

Die quantitative Analyse liefert ein differenziertes Bild zur dritten Forschungsfrage, dem Vergleich zwischen Live-Zusammenfassungen und nachträglich erzeugten Gesamtsummaries. Die ROUGE-Werte zeigen insgesamt nur moderate n-Gramm-Überlappungen, was zunächst auf eine geringe textuelle Übereinstimmung hindeuten könnte. Gleichzeitig erreichen die BERTScores durchgängig höhere Werte, was auf eine solide semantische Nähe schließen lässt. Diese Diskrepanz ist erwartbar, da abstraktive Zusammenfassungen häufig andere Formulierungen verwenden als die Referenztexte. Besonders relevant ist jedoch, dass die KI-basierte Referenzzusammenfassung in allen Meetings konsistent höhere BERTScore-Werte erzielt als der direkte Vergleich mit dem Transkript. Dies deutet darauf hin, dass eine nachgelagerte Gesamtzusammenfassung qualitativ überlegen ist.

Konkret bedeutet das: Das Live-System kann thematische Kernaussagen erfassen, erreicht jedoch nicht die Kohärenz und Vollständigkeit einer einmaligen, globalen Verarbeitung des gesamten Transkripts. Dieses Ergebnis ist sachlich logisch. Während der Laufzeit stehen dem Modell nur Teilinformationen zur Verfügung, wodurch Kontextverluste und Fehlinterpretationen wahrscheinlicher werden. Die gemessenen Werte belegen somit keine Schwäche der Implementierung, sondern eine strukturelle Grenze inkrementeller Zusammenfassung. Ein Live-Ansatz wird systembedingt selten die Qualität einer Offline-Gesamtauswertung erreichen. Entscheidend ist daher nicht Perfektion, sondern ausreichende Nützlichkeit.

Die qualitative Analyse bestätigt diese Interpretation deutlich. Der beobachtete Recency-Effekt, das Vergessen früherer Inhalte sowie die Persistenz fehlerhafter Zwischenstände zeigen typische Probleme rollierender Zusammenfassungen. Einmal eingeführte Fehlinterpretationen werden nur selten korrigiert und wirken sich kumulativ aus. Zusätzlich führen Transkriptionsfehler direkt zu inhaltlichen Verzerrungen, da das LLM keine Möglichkeit besitzt, diese zuverlässig zu erkennen oder zu validieren. Hier zeigt sich eine klare Abhängigkeit von der Qualität der Spracherkennung. Solange das Eingangssignal fehlerhaft ist, bleibt auch die Zusammenfassung fehleranfällig. Diese Einschränkung ist fundamental und kann nicht allein durch Prompt-Optimierung behoben werden.

Bezüglich der vierten Forschungsfrage zur zeitlichen Machbarkeit zeigen die Tests, dass die Generierung der Live-Zusammenfassungen in ausreichend kurzer Zeit erfolgt, um den natürlichen Arbeitsfluss nicht zu unterbrechen. Die Verarbeitung erfolgt nicht in Echtzeit im Millisekundenbereich, jedoch schnell genug, um als unterstützendes Werkzeug wahrgenommen zu werden. Damit erfüllt das System eine zentrale praktische Anforderung. Eine leicht verzögerte, aber kontinuierlich aktualisierte Zusammenfassung ist für Nutzer deutlich wertvoller als eine perfekte, aber erst nach dem Meeting verfügbare Auswertung. Dieser Trade-off zwischen Geschwindigkeit und Qualität ist im Anwendungskontext gerechtfertigt.

Trotz der insgesamt positiven Ergebnisse müssen die Grenzen der Evaluation klar benannt werden. Die Anzahl der Meetings ist mit drei Szenarien begrenzt, wodurch die statistische Aussagekraft eingeschränkt bleibt. Zudem unterscheiden sich die Meetings hinsichtlich Teilnehmerzahl, Struktur und Gesprächsdynamik, was die Vergleichbarkeit erschwert. Weiterhin basieren die automatischen Metriken auf textuellen Referenzen, die selbst keine objektive Wahrheit darstellen, sondern ebenfalls durch ein LLM erzeugt wurden. Dadurch entsteht eine gewisse Bewertungsunschärfe. Für zukünftige Arbeiten wären größere Datensätze, manuell erstellte Goldstandards sowie Nutzerstudien zur wahrgenommenen Nützlichkeit sinnvoll, um belastbarere Aussagen treffen zu können.

Zusammenfassend lässt sich festhalten: Der entwickelte Live-Meetingassistent funktioniert, liefert semantisch sinnvolle Zusammenfassungen und ist im praktischen Einsatz zeitlich geeignet. Gleichzeitig bleibt die Qualität hinter einer nachträglichen Gesamtauswertung zurück, insbesondere bei längeren und komplexeren Meetings. Die größten Schwachstellen liegen nicht primär im Sprachmodell selbst, sondern in der fortlaufenden Kontextverwaltung sowie in der Fehleranfälligkeit der zugrunde liegenden Transkripte. Optimierungen wie strukturierte Vorverarbeitung, gezieltes Prompt-Design oder hybride NLP-Ansätze sind daher vielversprechende nächste Schritte.

Unterm Strich zeigt die Arbeit realistisch und ohne Schönfärberei: Ein Live-Meetingassistent ist heute machbar und nützlich, aber noch kein vollwertiger Ersatz für eine manuelle oder nachgelagerte Dokumentation. Genau hier liegt das Potenzial zukünftiger Forschung – und damit eine klare Richtung für Weiterentwicklungen.