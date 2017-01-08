Statistik Austria
#################

ESGVS - Europäische Straßengüterverkehrsstatistik
SGVS  - (Österreichische) Straßengüterverkehrsstatistik

Datenquellen:
*************

ESGVS / SGVS
============

ESGVS: Statistiken der Einzelländer werden geprüft und aggregier
    * Aggregationsebene: Nuts 3 (= Bezirke)
SGVS: Fliest direkt ein mit
    * LKW-Verkehrsaufkommen (Fahrten / Zeit)
    * Transportaufkommen    (Tonnen  / Zeit)
    * Transportleistung     (Tonnenkilometer / Zeit)

ESGVS erfasst tendenziell unter, weil:
    * Ist schwer zu sagen weil es keine direkten vergleichszahlen gibt, aber es
        gibt hinweise aus anderen Datenquellen
    * Stichprobenfehler (Größe der Amtlichen Stichproben sinkt)
    * Fragebögen sind Umfangreich und Komplex, mühsam auszufüllen,
        z.B.: Werden of viele kurze Einzelfahrten zusammengefasst berichtet
    * Leerfahrten oder keine Fahrten prinzipiell weniger arbeit einzutragen
        für Fahrer
    * Fahrzeuge aus Nicht-EU-Staaten werden nicht erfasst
    * Unterschiedliche Erfassungsmethoden
    * Fahrten des kombinierten Verkehrs sind in den jeweiligen
        Verkehrsträgerstatistiken und somit mehrfach erfasst,
        verknüpfung mit nach Verkehrsmittel getrennten Güterdaten
        nicht möglich

Daten für in Österreich gemeldeten Fahrzeuge (Transport- & Verkehrsaufkommen)
unterscheiden sich leicht,
aber nicht statistisch signifikant, zwischen ESGVS und SGVS. Grund
unbekannt.

Unterschiede SGVS / ESGVS
    * Fahrtlängen von in Österreich gemeldeten LKWs deutlich
        kürzer als von ausländischen

CAFT
====

Multinationale Stichtagsbefragung von LKW lenkern an Alpenpässen
und Grenzübergängen, in AT 9 Pässe und 9 Übergänge, ugf 38 Tage im Jahr.
Variablen (Auswahl):
    * Anzahl Achsen
    * Zulassungsland
    * Route
    * Transportierte Warengruppe
    * Ziel
    * Qulle-Ziel in Österreich Gemeindescharf, sonnst in abhängigkeit
        der Entfernung von AT
    * Nur lkw größer 3.5t

    * Große unterschiede zu ESGVS für einzelne Länder, gut übereinstimmung
        für andere


Mautdaten & Automatische Zählstellen
====================================

* Mautbrücken:
    * Fahrzeuge über 3.5t
    * Ladung wird nicht erfasst
    * Achszahl / Emissionsklasse wird erfasst

* Automatische Dauerzählstellen (AZS)
    * Zählt ganzen verkehr
    * Leichte unterschiede in erfassten Fahrzeugkategorien etc...


Verfahren
*********

* Disaggregierung weilo SGVS detailierter als ESGVS
* Matrixkorrekturverfahren
    * Mit VISUM VStromFuzzy
    * Korrektur der Quell-Ziel matrix mittels Zählstellen


Schlussfolgerungen
******************

* ESGSV enthält transitverkehr, der aufgrund Plausibilitätsprüfung nicht
    zum Transitverkehr zählen sollte
* CAFT bräuchte häufigere Stichproben um saisonale Schwankungen zu erfassen
* CAFT kann prinzipiell gut zum Angleichen der ESGSV verwendet werden,
    findet aber leider nur alle 5 Jahre statt
* Ziwschenhalte und Be- und Entladevorgänge fehlen
* Unterfassung in Österreich viel durch mangelnde Beantwortung

* BMVIT will einzelfahrt Daten von statat
* ASFINAG daten nicht im gewünschten umfang um zielß-quell matrix zu verbessern
    * Ableiten der Fahrten funktioniert nicht gut
* Zu intermodalem verkehr kann man nicht viel sagen


Verbesserungsvorschläge
***********************

* Einbeziehung der Datenv on Spediteuren (Frachtbriefe)
* Daten der Wirtschaftskammer
* Daten der Verladeterminals und Eisenbahnunternehmen
* Kontrolle via automatischer Verkehrszählstellen


Notizen - Fragebogen
********************

* N-A um falschmeldungen zu umgehen
