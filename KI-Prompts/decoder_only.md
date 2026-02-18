

Du:
Wie funktioniert ein Decoder Only Transformer modell? 18.11.25

ChatGPT:
Ein Decoder-Only-Transformer ist im Kern ein großes Vorhersage-Modell: Er sagt Wort für Wort (bzw. Token für Token) voraus, was als Nächstes kommt. Kein Hokuspokus – nur konsequente Musteranalyse im großen Stil.

Hier ist die Funktionsweise klar und ohne unnötige Schnörkel:

1. Eingabe rein → Tokens
Text wird in Tokens zerlegt. Jedes Token wird in einen Vektor eingebettet. Zusätzlich bekommt jedes Token eine Positionsinformation, damit das Modell weiß, in welcher Reihenfolge es steht.

2. Mehrere Decoder-Layer
Jeder Layer besteht aus zwei zentralen Bausteinen:

Masked Self-Attention

Feed-Forward-Netzwerk

Und genau dieses Masking macht den Unterschied zu Encoder-Decoder-Modellen:
Das Modell darf beim Vorhersagen immer nur nach links schauen – also nur auf frühere Tokens. So bleibt es bei einer echten autoregressiven Vorhersage.

3. Masked Self-Attention
Das Modell berechnet, welche früheren Tokens für das nächste Token wichtig sind.
Das läuft über die bekannten Q (Query), K (Key) und V (Value) Matrizen.
Die Maske sorgt dafür, dass das Modell nicht in die Zukunft spicken kann.

Ergebnis: Das Modell erzeugt eine gewichtete Zusammenfassung des Kontexts – dynamisch und abhängig von dem, was bisher gesagt wurde.

4. Feed-Forward
Auf jedes Token wird ein kleines neuronales Netzwerk angewendet. Es arbeitet unabhängig für jedes Token und transformiert die Repräsentationen weiter.

5. Layer stapeln
Davon gibt es meist Dutzende. Jeder Layer baut auf den vorherigen auf.
So entsteht Schritt für Schritt ein tiefes Verständnis des bisherigen Texts.

6. Logits → Wahrscheinlichkeiten
Am Ende kommt ein großer Vektor heraus, der für jedes mögliche nächste Token eine Wahrscheinlichkeit repräsentiert.

7. Generieren
Jetzt wird entschieden:

Top-k?

Temperatur?

Greedy?

Sampling?

Egal wie du wählst – das nächste Token wird erzeugt. Danach wird es wieder eingespeist und der Kreislauf startet erneut.

Wenn du möchtest, kann ich das Ganze auch grafisch, in Pseudocode, anhand eines Mini-Beispiels oder am Architekturvergleich (Encoder vs. Decoder vs. Encoder-Decoder) durchgehen.


Du:
Stelle das ganze grafisch dar

ChatGPT:

Bild erstellt
Generiertes Bild
Generiertes Bild
Generiertes Bild



Weitergeben



