Statistische Mustererkennung
############################


Skalen... (siehe statistik) (ordinal, kardinal, etc..)


* Klassifikation - Systematik, zb Taxonomie der Tiere anlegen
* Klassierung - Wenn man auf basis einer Klasifikation
    ein Objekt zuweist
* Klassifizierung - Trainieren eines Klassifizierers


Lineare Sepparierbarkeit
========================

* eventuell kann ich meine features so transformieren
    dass ich sie linear sepparieren kann,
    beispiel  punkte in einem kreis, quadrate
    der features verwenden

    ::

        xxxxxxxxx
      x           x
      x   yyyy    x
      x   yyyy    x
      x           x
        xxxxxxxxx


Perceptron Konvergenz-Theorem
=============================

* Margin eines Punktes = sein Abstand zur Hyperebene
    (negative margin = falsch klassiert)

* Margin der Hypereben = Minimale margin aller punkte
    (je größer desto besser)

* Wenn problem nicht linear sepparierbar, rennt
    perzeptron für immer


Grundbegriffe Wahrscheinlichkeitstheorie
========================================

Merkmal (Mustererkennung) = Elementar Ereigniss (Wahrscheinlichkeitstheorie)

Ereigniss = Menge an Elementarereignissen, zb Normale Körpergöße
1,50 - 1,70

* P(Omega) = wahrscheinlichkeit des gesammten stichprobenraums
* Disjunkt = Mengen haben leeren durchschnitt

*53*

Distales merkmal = gesichtslandschaft einer person
Proxales = ergebniss der messung des gesichtes

*52*

Px = Qualifizierendes merkmal auf dem bild
P = Qualifizierendes merkmal auf dem urbild

*56*

Summe der p(i) = 1, nicht summe der i


wahrscheinlichkeitsfunktion/ mass function p(X=1), pi
verteilungsfunktion F(i) = summe(pi)

beides sind Wahrscheinlicheiten (im diskreten fall)


*86*

h = 1 enstpricht mittelwert

*92*

* wahrer parameter = skalar (nicht bekannt)
* schäzer - zufallsvariable
* schätzwert - skalar für aktuelle stichrpobe

*93*

* index i wird nicht gebraucht wenn variablen unabhängig
Prüfungsrelevant

*94*

nimm jenes theta dass die stichprobe (xi.... xn) am warscheinlichsten macht

Maximum likelyhood auf normalvertelung kommt zu least squares


* 99 *

formel eigentlich eine schätung, aber wir ersetzen di ekleinen xi durch grosse XI
(zufallsvariablen),.. dann haben wir einen schätzer


frequentistische statistik: punktschätzung des mittelwertes
Bayes statistik resultat is verteilung des richtigen wertes, ausgegangen von
meinem wissen (stichprobe)

* 117

P(B|A)... bedingte warscheinlichkeit = P(B wenn A)
P(B,A)... Verbundwarscheinlichkeit = P (B und A)

users-producers-accuracy nachschlagen
