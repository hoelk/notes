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
