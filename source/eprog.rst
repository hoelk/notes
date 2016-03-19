Java
####

Notes
=======

Aufgabe 4
---------

.. code-block:: java

    import java.util.*;
    import java.io.*;
    public class Stadt implements Comparable<Stadt>
    {
      //Klassenvariablen
      String CountryCode;
      String ASCIIName;
      String CountryName;
      long population;
      double lat;
      double lon;

      //Konstruktor
      Stadt(String CountryCode, String ASCIIName, String CountryName, long Population, double lat, double lon)
      {
        this.CountryCode = CountryCode;
        this.ASCIIName = ASCIIName;
        this.CountryName = CountryName;
        this.population = population;
        this.lat = lat;
        this.lon = lon;

      }

      public int compareTo(Stadt other)
      {
         //andere Stadt ist größer
         if (other.population > this.population) {
           return 1;
         } // end of if
         //andere Stadt ist kleiner
         if (other.population < this.population) {
           return -1;
         } // end of if
         //andere Stadt gleich groß
         else {
           return 0;
         } // end of if-else
        }


      //to String methode
      public String toString()
      {
        String ausgabe = String.format("%15s (L=%10.6f/ B=%10.6f)",ASCIIName,lon,lat);
        String punktpunkt = String.format("%20f", population).replace(" ",".");

        return ausgabe +punktpunkt+"EW.";
      }



    }


    import java.util.*;
    public class Cityfinder
    {

      public static void main (String[]args)
      {
        FileInputStream istream = new FileInputStream("Dateiname");
        InputStreamReader reader = new InputStreamReader (istream);
        BufferedReader input = new BufferedReader (reader);
        String line;

        HashMap<String,LinkedList> cc_stadt = new HashMap<String,LinkedList>(); //verknüpft countrycode mit Stadt

        //Schleife zum Einlesen aller Städte
        while ((line = input.readLine()) != 0 )   //Gibt es ein Land?
        {
          String[] elem = line.split(",");
          LinkedList val = cc_stadt.get(elem[0]);   //Wir kennen das Element, wollen aber dessen Wert (Schlüssel bekannt)
          if (val == 0)
          {
            LinkedList<Stadt> neuesLand = new LinkedList<Stadt>();    //2 Collectionklassen miteinander verbinden
            val = neuesLand;
            cc_stadt.put(elem[0],neuesLand);   //leere Liste anlegen
          }
          //Stadt zu LinkedList hinzufügen
          Stadt x = new Stadt(elem[0],elem[1],elem[2],elem[3],Integer.parseInt(elem[4]),Double.parseDouble(elem[5]),Double.parseDouble(elem[6]),elem[0]); //letztes elem[0] für CountryName platzhalter, elem(4)= Population
          val.add(x);
        }

        FileInputStream istream2 = new FileInputStream("CountryCodes.txt");
        InputStreamReader reader2 = new InputStreamReader (istream2);
        BufferedReader input2 = new BufferedReader (reader2);

        HashMap<String,String> ccc = new HashMap<String,String>();  //ccc = countryCodes and Countries
        while (line2 = input2.readLine()) {
          String[] elem = line2.split(",");
          ccc.add(elem[0],elem[1]);
        } // end of while

        LinkedList<Stadt> steatteDesLandes = cc_stadt.get(args[0]);
        LinkedList<Stadt> sortedCities = Collections.sort(steatteDesLandes);

        //größte Stadt in neue LinkedList speichern
        LinkedList<Stadt> biggestCities = new LinkedList<Stadt>();
        for (int i = 0;i<Integer.parseInt(args[1]) ;i++ ) {
          biggestCities.add(sortedCities.get(i));
        } // end of for

        //Liste mit Städten zum gesuchten Land holen  und sortieren
        //erste n ausgeben  n=(args[1])
        //Namen der Stadt nehmen und schauen, in welchen Ländern es diese Stadt gibt
        Iterator it = biggestCities.iterator();
        while (it.hasNext()) {
          Stadt SuchStadt = it.next();
          String StadtName = SuchStadt.ASCIIName;
          TreeSet<String> CountryCode = new TreeSet<String>();
          Iterator LandIt = cc_stadt.values().iterator();
          while (LandIt.hasNext()) {
            Iterator StadtIt = landIt.next().iterator();
            while (StadtIt.hasNext()) {
              Stadt DS = Stadt.next();
              if (DS.ASCIIName == StadtName) {
                CountryCode.add(DS.CountryCode);
                break;
              } // end of if
            } // end of while
          } // end of while
          //ausgabe
          System.out.println(SuchStadt);
          System.out.println("Andere Länder mit dieser Stadt");
          Iterator CountryIt = CountryCodes.iterator();
          while (CountryIt.hasNext()) {
            System.out.println(ccc.getCountryIt.ext());
          } // end of while
        } // end of while
        //indem wir wir schauen, in welcher Liste so eine Stadt existiert
        //Ländernamen in LinkedList abspeichern
        //sortieren und Länder nach Alphabet (Collection.sort) +ausgeben(Iterator)
        //alles in Methoden
      }


}


Error handling
==============

Pre- and Postconditions
-----------------------

A method accepts arguments and returns a return value

Preconditions: Valid ranges of input arguments (use exceptions)
Postconditions: Valid ranges of output arguments (use assertions)

Asstertions
-----------

* DO: test for situations that *cannot happen* according to programm logic
* DON'T test for invalidüser inputm


.. code-block:: java

    asster gcd > 0: "GCD is positive"

.. code-block:: bash

    java -ea TestAssertion # enable assertions
    java -da TestAssertion # disable assertions (default)


Reference Tables
----------------

.. _primitve-data-types:

Einfache / Primitive Datentypen in Java:
-----------------------------------------

+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| Datentyp   | Größe¹           | Wrapper-Klasse        | Wertebereich                     | Beschreibung                                      |
+============+==================+=======================+==================================+===================================================+
| boolean    | JVM-Spezifisch   | java.lang.Boolean     | true / false                     | Boolescher Wahrheitswert                          |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| char       | 16 bit           | java.lang.Character   | 0 … 65.535 (z. B. ‘A’)           |ünicode-Zeichen (UTF-16)                          |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| byte       | 8 bit            | java.lang.Byte        | -128 … 127                       | Zweierkomplement-Wert                             |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| short      | 16 bit           | java.lang.Short       | -32.768 … 32.767                 | Zweierkomplement-Wert                             |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| int        | 32 bit           | java.lang.Integer     | -2.147.483.648 … 2.147.483.647   | Zweierkomplement-Wert                             |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| long       | 64 bit           | java.lang.Long        | -9.223.372.036.854.775.808 …     | Zweierkomplement-Wert                             |
|            |                  |                       |  9.223.372.036.854.775.807       |                                                   |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| float      | 32 bit           | java.lang.Float       | +/-1,4E-45 … +/-3,4E+38          | Gleitkommazahl (IEEE 754)                         |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| double     | 64 bit           | java.lang.Double      | +/-4,9E-324 … +/-1,7E+308        | Gleitkommazahl doppelter Genauigkeit (IEEE 754)   |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+

¹: minimaler Speicherverbrauch

`Quelle <http://de.wikibooks.org/wiki/Java_Standard:_Primitive_Datentypen>`_



Testfragen
===========


2. Semester
-----------

Test 2
------

Schätzen Sie den Aufwand für die rekursive und iterative Berechnung der
Fibonacci-Zahlen ab.

Schreiben Sie eine verbesserte rekursive Funktion zur Berechnung von
Fibonacci-Zahlen, welche bereits berechnete Zahlen in einem Array
speichert und nicht immer wieder neu berechnet.

Schreiben Sie eine effiziente Funktion
public static String reverse(String text);
die den als Parameter übergebenen String umdreht (letztes Zeichen nach
vorne, erstes nach hinten). StringBuilder soll dabei nicht verwendet
werden.

Überprüfen Sie experimentell das Laufzeitverhalten der beiden Funktionen
testString und testSB indem Sie immer wieder die Länge n verdoppeln
und mit der Funktion System.nanoTime() die Laufzeit feststellen.

Sortierverfahren und mittlerer asymptotischer Aufwand

    * Bubblesort     :math:`O(n^2)`
    * Selectionsort  :math:`~N^2/2`
    * Insertionsort  :math:`~N^2/4`
    * Mergesort      :math:`~n \log{n}`
    * Quicksort      :math:`~1.4 n \log{n}`    :math:`O (n^2)`
    * Heapsort


Suchverfahren und asymptitischer aufwand

    * Linear search: O(n)
    * Binary search: O(log n)


Was versteht man unter einem stabilen Sortierverfahren und welche der besprochenen Verfahren gehoeren
zu dieser Kategorie?

    Bei Mehrfacheintraegen bleibt urspruengliche Ordnung erhalten

    * Insertion Sort
    * Merge Sorted
    * Bubblesort
    * Qicksort (nein, aber es gibt varianten die stabil sind)


Was sind Wrapper-Klassen und wozu werden sie benoetigt?

    * Wrappen einen primitiven typ in eine Referenzklasse
    * Haben statische Hilfsfunktionen (z.B MIN_VALUE, MAX_VALUE)
    * Implementieren das Compareable interface
    * Nützlich für Fälle wo direkt keine Primtiven Werte verwendet werden
    können (z.b. in Array lists)


Was versteht man unter Autoboxing bzw. Auto-Unboxing?

    * Beim aufrufen des Konstruktors einer wrapper klasse wird ein primitiver
    Wer "verpackt" (boxing), beim aufrufen der Getter-Methode "entpackt" (unboxing)
    * Das ist umstaendlich zum schreiben deswegen fuegt der Java compiler automatisch
    die Anweisung ein, und man kann es wie eine einfache Zuweisung schreiben:

    .. code-block :: java

        Integer integer = new Integer(17);
        int i = integer.intValue();

        Integer integer = 17;
        int i = integer;


Was ist die Grundidee hinter divide-and-conquer

    * Rekursives reduzieren eines problems of leichter zu lösende
    Teilprobleme


Wie kann man das Problem umgehen, dass die Größe von Arrays nach dem Anlegen nicht mehr
veränderbar ist?

    * Plätze im Array für neue Einträge reservieren. Anzahl der reservierten
    (leeren) Einträge kann dann von zb. den setter und getter methoden überprüft
    und angepasst werden falls mehr/weniger benötigt werden

    * Keine Arrays verwenden sondern die collection Klasse "Array-list"


Geben Sie Unterschiede (Vor- und Nachteile) der Typen String und StringBuilder an.

    * String verhaelt sich wie ein primtiver Datentyp
    * String builder ist veraenderlich und stellt mehr methoden zur verfuegung


Welche Alternativen zu Arrays gibt es, um eine großere Menge von gleichartigen Daten zu organisieren?

    * Array lists (mit Duplikaten)
    * Sets (ohne Duplikate)


Wie unterscheidet sich die Organisation einer Liste von einem Baum?

    * Bei einer Liste folgt auf ein Element immer ein weiteres element
    * Bei einem Baum folgen 2 oder mehr

Was ist die minimale und maximale Hohe eines Binarbaums, welcher 27 Knoten enth ̈ alt?

    * 26 (er entspricht einer Liste)
    * 4

Welche Bedingungen zwischen Knoten mussen bei einem binären Suchbaum erfüllt sein?

    * Knoten müssen geordnet sein
        * Linkes Child kleiner als Parent, rechts Child größer.

Warum sind bin ̈are Suchbaume bei dynamischen Anwendungen vorteilhaft?

    * Einfügen und Löschen von Elementen ist vergleichsweise
    effizient (aber weniger effizient als hastables)

Was versteht man unter einem abstrakten Datentyp?

    Eine Menge von Werten mit dazupassenden Operationen

Was ist der wesentliche Unterschied zwischen Collections und Maps?

    * Collections speichern Einzelelemente und implementieren das Collection
    Interface
    * Maps speichern Element-paare und implementieren das Map interface

Welche Vorteile hat es abstrakte Datentypen zu verwenden statt die entsprechenden Konzepte direkt in
eigene Klassen zu realisieren?

Was versteht man unter einem Iterator?

    * Iteratoren sind verallgemeinerung der idee eines Indexwertes, so dass auch
    über ungeordnete Datentypen (zb Sets) iteriert werden kann
    * Iteratoren verlieren (im allgemeinen) ihre gültigkeit wenn sie am Ende der zu iterierenden
    Collection angekommen sind (Ausname: List iteratoren)
    * Iteratoren verlieren ihre gültigkeit wenn die Collection modifiziert wird
        * Iteratoren bieten selber methoden zum modifizieren von Collections
        die den Iterator nicht entwerten

 Welche Vorteile bieten Listen-Iteratoren gegen ̈ uber einfachen Iteratoren? beide Richtungen, am Ende funktionsfähig

    * Normale iteratoren gehen nur in eine Richtung (zum nächsten element),
    List operatoren können auch zum vorherigen element bewegt werden
    * Normale iteratoren verlieren ihre Gültigkeit wenn sie am ende angekommen
    sind, List iteratoren nicht.


Welche Eigenschaften muss eine gute Hashfunktion haben?

    * Verteilt die Schlüsselwerte gleichmäßig auf den Indexbereich
    der Hastable
    * Eine möglichkeit: Ganzzahldivision des Wertes mit einer
    Primzahl und heranziehen des Rests als hashcode

    .. code-block:: java
        private int hash( Key x )
            { return (x.hashCode() & 0x7fffffff) % M; }


Was versteht man unter einer Kollision in einer Hashtabelle und
welche Möglichkeiten gibt es, das Problem zu lösen?

    Zwei Objekte haben den selben Hashkey
    * Einträge der Hastable bestehen aus linked lists in denen
    alle objekte mit den selben hash codes plaziert werden
    * Objekt wird dem nächsten freien Platz zugeweisen


Geben Sie fur die folgende Zahlenreihe an, wie sich die Reihe schrittweise verandert, wenn sie mit Hilfe
von Quicksort, Selectionsort, Insertionsort oder Mergesort sortiert wird und des erste Element das
Pivot-Element ist: 5,1,3,2,7,4,6


Unterschied Comperator und Comparable

    Comparable
    * Sortierlogik in selber klasse wie zu sortierende Objekte
    * Definiert die Natürliche ordnung von Objekten
    * Zu sortierende klassen müssen das interface implementieren

    Compareable
    * Sortierlogik in sepparater klasse; sortieren nach unterschiedlichen
    Werten möglich
    *






Test 1
-------

Welchen Zweck haben Packages in Java?

    Organisationseinheit für zusammenhängende Klassen.
    Hilft auch beim verhindern von Namenskonflikten. Mehre Klassen mit
    selbem Namen innerhalb eines Packages sind nicht möglich, allerdings
    können verschiedene Packages Klassen des selben Namens haben.

Wie können Packages von der JVM gefunden werden?

    Dieümgebungsvariable CLASSPATH legt fest wo Java nach Packages sucht.
    Alle Bytecodedatein eines Packages müssen in einem Verzeichnis liegen.
    Die Datein etwaiger Subpackages liegen inünterverzeichnissen.

Wieviele Verzeichnisse kann dieümgebungsvariable CLASSPATH enthalten?

    Belibeig viele

Gibt es Klassen im JDK, die auch ohne import-Klausel zur verfügung stehen?

    * Man kann statt zu importieren den ganzen Pfad der Klasse angeben
    * Java.lang wird automatisch importiert

Was versteht manünter einem qualifizierten Namen?

    Eindeutiger name einer klasse/methode/variable/etc.. incl. dem
    package name

Was ist derünterschied zwischen importünd static import?

    import static importiert felderünd methoden die als public static
    definiert sind. Sonnst muss man den qualifizierten namen verwenden
    (Zb Math.PI mit import, PI mit import static)

Was besagt eine sogenannte package-Klausel?

    * Teilt einer Quelltextdatei mit zu welchem package sie gehört

Was passiert, wenn in einer Quelltextdatei keine package-Klausel existiert?

    * Dann gehört sie zum default-packageünd kann von anderen packages
    nicht importiert werdne

Wie können Namenskonflikte im Zusammnhang mit Packages aufgelöst werden?

    * Angabe des qualifizierten names

Kann ein Java-Archiv (jar-file) mehrere Packages enthalten?

    * Nein, allerdings kann sie sub-packages enthalten.

Kann ein Java-Archiv neben class-Dateien noch andere Dateien enthalten?

    * Es gibt noch die MAINFEST.MF metainformations datei.

Gibt es Dateien, die in jedem jar-file vorhanden sein müssen?

    * Manifest.MF

Was ist der Vorteil von jar-files?

    * Ganzes Package in einer Datei
    * Weniger platzbedarf (komprimierung)
    * Digitale Signierung möglich (zb bei Android)

Wie können Sie sich Zugang zu einem jar-Archiv verschaffen, wenn Sie das Programm jar nicht zur
Verfügung haben?

    * Kann mit jedem zipünpacker entpackt werden

Wozu dienen Interfaces?

    * Trennen schnittstelleünd Implementierung
    * Schnittstelleöffentlich, implementierung nicht

Kann ein Interface Methoden enthalten?

    * Nein (Bzw nur deren Köpfe)

Kann ein Interface Daten enthalten?

    * Ja (im sinne von konstanten)

Was versteht manünter dem Begriff Design by Contract?

    * Definition von pre-ünd postconditions für eine methode

Kann ein Interface private Methoden enthalten?

    * Nein
    * Kann köpfe von public methoden enthalten, aber nicht private

Wieviele Interfaces kann eine Klasse implementieren?

    * Beliebig viele

Können von einem Interface Variablen definiert werden?

    * Ja, nur lokale variablen

Wie kann man ein Interface-Objekt erzeugen?

    * Garnicht, müssen einer klasse zugweisen werden

Was versteht manünter dynamischem Binden?

    * Richtige methode wird vom aktuell zugewiesen Objekt festgelegt
    * Methodenwahl also erst zur Laufzeit möglich

Beschreiben Sie denünterschied zwischen statischemünd dynamischem Typ.

    * Variable ist bei komplierung mit einem fixen typ definiert
    * Der Variable wird erst zur laufzeit ein Objekt eines bestimten
    types zugwiesen

Muss eine Klasse auch nicht benötigte Methoden eines Interfaces implementieren?

    * Ja, alle

Gibt es einenünterschied, ob eine Variable vom Interface-Typ ist
oder vom konkreten Typ?

    * Ja, bei einem interface typ kann es sein dass mehr Methoden
    existieren


Welchen Vorteil hat es, wenn der Copy-Konstruktor einer Klasse einen Interface-Typ-Parameter hat?

    * Sie sind flexibler anwendbar
    * Jede beliebige immplementierende klasse kann übergeben werden

.. code-block:: java

        class Name implements Interface {
          Name (Interface Variable) {
            a = Variable.a
         }  }


Was versteht manünter einer Superklasse?

    * Überklasse, von welcher eine andere Klasse abgeleitet ist

Welche Arten der Vererbung kennen Sie und was ist derünterschied?

    * Interfaces: Fixieren gemeinsame eigenschaften mehrer
    Klassen

    * Vererbung konkreter Klassen: Eine Klasse wird von
    einer anderen Abgeleitet, dh sie hat alle Eigenschaften
    der Basisklasse, kann aber noch erweitert werden.

Welche Abhilfe gibt es, wenn eine Methode unbrauchbar
für die abgeleitete Klasse ist?

    * Ererbte Methoden können redefiniert werden
    * Einschraenkung:
        * Name und Parameterliste müssen übereinstimmen.
        * Zugriffsschutz: darf gelockert werden aber nicht eingeschränkt.
        * Ergebnistyp: Statt der Basisklasse darf die abgeleitete Klasse verwendet werden.
        Für den Methodenrumpf gelten keine Einschränkungen.

Was bedeutet der Zugriffsschutz-Modifier protected?

    * Zugriff nur für abgeleitete Klassen (und die Klasse selbst) erlaubt

Kann eine Klasse in Java von mehreren Basisklassen abgeleitet sein?

    * Nein

Kann eine Klasse in Java mehrere Interfaces Implementieren?

    * Ja

Nennen Sie eine Methode, die immer geerbt ist?

    * Erbt immer vom der Objekt klase: toString, equals(Object x), getClass

Was hat es mit der Klasse Object auf sich?

    * s.o.

Wie kann ein Konstruktor einer Basisklasse in der abgeleiteten
Klasse verwendet werden?

    * mit super()

Wie können Programmabstürze verhindert werden?

    * Auffangen von Exceptions

Was können Ausnahmezustände sein?

    * Zugriff auf nicht vorhandene Datei, Zugriff auf nicht vorhandenes
    array element, etc..

Wie kann auf einen Ausnahmezustand im Programm reagiert werden?

    * Mit try-catch-finally konstrukten

Wie kann ein Fehlerzustand an die aufrufende Einheit einer Methode
weitergeleitet werden?

    * Via throws klausel im methodenkopf

Was versteht man unter Auffangen einer Exception?

    * Behandeln einer exception mittels catch(eception). Hier kann
    festgelegt werden wie mit so einen Ausnahmezustand umgegangen werden
    soll

Was passiert, wenn im try-Block eines Programms eine Exception auftritt?

    * Try block wird abgebrochen, das dazugehörige catch wird ausgefuert

Was passiert, wenn eine Exception in einer Methode nicht behandelt wird?

    * Muss weitergegeben werden an die aufrufenden methode, sonnst
    kompiliert nicht

Wie kann ein Programmierer erkennen, ob in einer Funktion Exceptions
auftreten können?

    * Durch Exceptionsignatur nach dem Methodenkopf
    (returntyp methodenname (parameterliste) throws exceptiontyp1…)
    und Dokumentation @throw exceptiontyp Text

Was versteht manünter einer Exception-Signatur?

    * returntyp methodenname (parameterliste) *throws exceptiontyp1…*

Was versteht manünter einer Methdoden-Signatur?

    * Methodenname + Übergabeparameter (methodenname(Parameter))

Was ist derünterschied zwischen überladen und überschreiben (redefinieren) einer Methode?

    * Überladene Methoden: mehrere Methoden mit gleichen Namen aber unterschiedlichen Parametern
    * Redefinieren: neue implementierung einer geerbten Methode,

Was bedeuten die reservierten Wörter final und finally in Java?

    * Final: schlussendliche Wert einer Variable, kann nicht mehr verändert werden
    * finally: Block, nach den try- und catchBlöcken, der am Ende des Programms noch immer ausgeführt wird, egal ob Exception oder nicht.

Ist es in Java möglich eigene Exceptions zu definieren?

    * Ja

    .. code-block:: java

        class Exceptionname extends Exception {
            Exceptionname () {  }
            Exceptionname (String message) {  super(message) ;  }
        }

Was versteht manünter Exception-Chaining?

    * Methode fängt Exception auf und gibt stattdessen eine andere Exception weiter.

Zeichnen Sie ein einfaches Beispiel für ein Klassendiagramm in UML auf.
Wie wird eine Vererbungsbeziehung im Klassendiagramm dargestellt?
Wie kann man in einem Klassendiagramm den Zugriffsschutz erkennen?
Erklären Sie direkteünd indirekte Rekursion.

    * Direkte Rekursion: Methode ruft sich selbst immer wieder auf
    * indirekte Rekursion: Methoden rufen sich wechselseitig immer wieder auf

Was ist der entscheidende Punkt bei einer rekursiven Methode, damit es nicht zu einerünendlichen
Aufruffolge kommt?

    * Das problem muss immer kleiner werden und irgendwann ohne rekursion
    loesbar sein

Kann es in einem funktionierenden Programm zu einem Stack-Uberlauf kommen?

    * Das programm muss immer kleiner werden, nicht immmer groesser

Was wird auf dem Programm-Stack abgelegt?

    * Parameter und lokale Variablen (Last in, First out)


1. Semester
-----------

Test 1
^^^^^^

In welcher Datei steht der Bytecode der Klasse „Motorfahrzeug“?

  Motorfahrzeug.class

Was ist Voraussetzungüm einer Variablen Werte eines anderen Datentyps zuweisen zu können?

  Typenkonversation
  * Implizit: Wird automatisch gemacht
  * Explizit: Muss angegeben werden, bsp: ``(double)(int) 1``

Welche der folgenden Datentypen sind primitive Datentypen in Java

  Bool, bool, integer, Integer, int, Int, Real, real, Float, float,
  Double, double, Rational, rational, Complex, complex, String, string

  **Antwort :**  int, float, double

  **Anmerkungen**

  * String is eine Klasse, kein einfacher Datentyp
  * Primitive Datentypen haben immer kleine Anfangsbuchstaben
  * Siehe :ref:`primitve-data-types`.

Was ist Polymorphie?

  Eine Methode ist polymorph wenn sieünterschiedliche Datentypen annimmt.

  * Beispiel: Der ``+`` Opperator ist akzeptiert ``int``ünd ``double`` Werte.

Hat eine Anweisung einen Typ?

  Nein, eine Anweisung kann aber einem Ausdruck einen Wert zuweisen

Was macht ein Typecastünd wie ist die Syntax?

  Konvertiert einen Ausdruck von einem Datentyp in einem anderen.

  * Z.b (int) (double)
  * `Mehr Details <http://www.java-tutorial.org/typecasting.html>`_

Wie ruft man den Java-Compiler auf der Kommandozeile auf?

  ``javac Klassenname.java``

Was ist derünterschied zwischen intünd double?

  * int: ganze Zahlen
  * double: Gleitkommazahlen

Mit welchen Operationen können Sie aus einer 7-stelligen Matrikelnummer das Inskriptionsjahr extrahieren?

  * 0499999 / 100000 = 04
  * 04 + 2000 = 2004

Kommt die folgende Schleife zu einem Ende? Begründung?

  ``for(int j=1; j!=0; j++) ;``

  Ja, wegen wrap around. Sobald der der Wert für j den maximalen integer wert
  ``231 - 1`` übersteigt fängt er von ganzünten an ``-231``.

  Anmerkung: ``double`` überlauf wrapt nicht sonder liefert +/-ünendlich.

Wie startet man ein Java-Programm?


  ``java Klassenname`` in der Kommandozeile eingeben.

Welche Dateiendung muss eine Java-Quelltextdatei haben?


  ``.java``

Wie heißt die Datei, in welcher der Quelltext der Klasse „Motorfahrzeug“ steht?

  ``Motorfahrzeug.java``

Was wird benötigt,üm auf einem beliebigen Rechner ein Java-Programm ausführen zu können?

  Ein JRE (Java Runtime Envirnment)ünd das Programm (.class Datei).

Was brauchen Sieüm Java-Quellcode zu erstellen?

  Einen text editor.

Wie erzeugt man ausgehend von der Datei „Test.java“ die Datei „Test.class“?

  Kompilieren. ``javac Test.java``

Was versteht manünter einem Syntaxfehler?

  Angabe entspricht nicht der formalen Gramatik oder Rechtschreibung von Java

Welche Art von Fehlern kann ein Compiler feststellen?

  Syntaxfehler

Ein Programm läßt sich fehlerfrei übersetzen, liefert aber falsche Ergebnisse.
Wie nennt man einen solchen Fehler?

  Semantikfehler

Ein Programm beendet sich nicht wie vorgesehen, sondern „stürzt ab“.
Wie nennt man einen solchen Fehler?

  Laufzeitfehler (runtime error)

Muss jede Variable einen Datentyp haben?

  Ja

Kann man einer Variablen Werte von einem anderen Datentyp zuweisen?

  Nein. Man kann aberünterümständen Datentypen konvertierten (typecasten). Dies
  kann auch autamtisch passieren.
  Z.b. Wenn man versucht einer ``double`` Variablen einen ``integer`` wert
  zuzuweisen, wird dieser automatisch nach ``double`` konvertiert.

Wenn man einen Datentyp A einer Variablen von einem anderen Datentyp B zuweisen kann,
dann sagt man „A ist . . . . . . . . . zu B“.

  kompatibel (implizite Typenkonversation wird durchgeführt)
  (``integer`` ist kompatibel zu ``double``, aber nichtümgekehrt!)

Was ist derünterschied zwischen floatünd double?

    * Beides sind datentypen für Gleitkommawerte
    * ``double`` stellt mehr Speicherplatz zur Verfügung, daher:
        * höhere Genauigkeit (``double`` steht für *Doppelte Genauigkeit*)
        * höheres Maxünd tieferes Min als ``float``
    * Siehe :ref:`primitve-data-types`


Welche der folgenden Namen sind gültige Bezeichner in Java?

  3fach, null, jahr2000, 8ung, after_sun, just-in-time, class, classic,
  r2d2, a1a1a1a1a, 12345abcde, holzWeg

  jahr2000, after_sun, classic, r2d2, a1a1a1a1a, holzWeg

  Regeln:
      * Der Name darf nicht mit einer Ziffer beginnen
      * Sonderzeichen wie : * ; + - / sind nicht nicht erlaubt
      * Reservierte Wörteründ Schlüsselwörter sind nicht erlaubt

Was ist derünterschied zwischen =ünd == ?

    * ``=``  ist eine Zuweisung (``a = 1`` weist der Variablen ``a`` den Wert ``1`` zu)
    * ``==`` ist ein Vergleich  (``1 == 1`` gibt aus ``true``)

Welche Modifier kennen Sieünd was ist Ihre Bedeutung?

  Access Control Modifiers:

  Java provides a number of access modifiers to set access levels for classes, variables, methods and constructors. The four access levels are:

      * Visible to the package, the default. No modifiers are needed.
      * ``private`` :  Visible to the class only .
      * ``public``:    Visible to the world .
      * ``protected``: Visible to the package and all subclasses ().

  Non Access Modifiers:

  Java provides a number of non-access modifiers to achieve many other functionality.

      * ``static`` for creating class methods and variables
      * '``final`` modifier for finalizing the implementations of classes, methods, and variables. (können nicht mehr geändert werden)
      * ``abstract`` modifier for creating abstract classes and methods.
      * ``synchronized`` and volatile modifiers, which areüsed for threads.

Was ist derünterscheid zwischen Ausdruckünd Anweisung?

  Ein Ausdruck hat einen bestimmten Typ, er kann als Teil von anderen Ausdrucken
  verwendet werden.
  Eine Anweisung hat keinen Typ, sie bewirkt irgend etwas.

Welche Operationen sind mit ganzen Zahlen möglich?


    * Arithmethische opperationen:
        * ``+ - * / % ++`` (increment) ``--`` (decrement)
    * Vergleichsopperationen:
        * ``== != > < >= <=``
    * Bitweise Operationen (haben wir nicht durchgemacht)

Was macht der Operator % ?


  Rest einer Ganzzahldivision


Welche Arten von Anweisungen sind in einem Schleifenrumpf erlaubt?

  Alle

Was ist ein Block? Welche Auswirkungen sind damit verbunden?

  Variablen die innerhalb eines Blocks initialisiert werden, gelten nur
  in diesem.

Welche besonderen Werte kann eine double-Variable annehmen?

    * ``Double.Min_value``, ``Double.Max_Value`` : Maximal/Minimalwert
    * ``NaN`` : Not a Number
    * ``positive_infinity``, ``negative_infinity``

Wann benötigt man einen Typecast?

    * Implizite Typenkonversation geht nur, wenn ein niederwertiger Datentyp in einen höher wertigen Datentypenümgewandelt wird (``int`` -> ``double``)
    * explizite Typenkonversation mittels typecast funktioniert auch anders herum

Kann man in Java eigene Typen definieren?

    * Ja, allerdings nur Referenztypenünd keine primitiven typen.

Was versteht manünter Initialisierung?

    * Wertzuweisung, erfolgt nach der Dekleration (Spezifizierung des Datentyps)
    * Dekleration ``int i;``
    * Initialisierung ``i = 1;``

Kann der Wert 10(−20) in einer double-Variable gespeichert werden?

    Ja

Was ist der Vorteil einer IDE?

    Z.b.:

    * Syntaxhighlighting,
    * Code completion,
    * Debugger,
    * (teil)automatisiertes kompilieren
    * integration von version managment
    * refactoring tools, etc..

Wie errechnet sich die Größe von Math.MAX_VALUE?

    Gibt's nicht


Test 2
^^^^^^

In welchen zweiünterschiedlichen Situationen kommt in Java das reservierte Wort this zum Einsatz?

  * Zum Zugriff auf eine Objektvariable, wenn sie durch einen gleichnamigen Parameter oder eine gleichnamige lokale Variable verdeckt wird.
  * Bei der Konstruktorverkettung zum Aufruf eines anderen Konstruktors.


Was bedeutet overloadingünd worauf ist dabei zu achten?

  Overloading bezeichnet die Möglichkeit,
  dass eine Klasse mehrere Methoden mit gleichem Namen
  haben kann. Diese Methoden müssen
  sich aber anhand der Parameterlisteünterscheiden lassen,
  entweder durchünterschiedliche Anzahl von Parametern oder durchünterschiedliche Datentypen der
  Parameter.


Wozu dient ein Konstruktor?

    Ein Konstruktor dient zur korrekten Initialisierung eines neu erzeugten Objekts einer Klasse.


Wieviele Konstruktoren kann eine Klasse minimalünd maximal haben?

    Jede Klasse hat mindestens einen Konstruktoründ kann beliebig viele davon haben. Wenn in einer
    Klasse kein Konstruktor definiert wird, dann erzeugt der Compiler automatisch einen
    Default-Konstruktor.


Wie funktioniert die Initialisierung von Objekten im Gegensatz zu primitiven Variablen?

    Im Gegensatz zu primitiven Variablen, die explizit initialisiert werden müssen,
    sind Objekte nach dem
    Anlegen automatisch initialisiert. Falls Objektvariablen nicht durch den Konstruktor initialisiert werden,
    bekommen Sie typabhängig
    passende Default-Werte.


Was sind die Vor-ünd Nachteile einerünveranderlichen Klasse

    Vorteil:ünveränderliche Klassen können fast wie primitive Variablen verwendet werden.
    Nachteil: Methoden zur Veränderung eines Objekts müssen jeweils ein neues Objekt erzeugen.


In Java gibt es keine Moglichkeit, für Klassen Operatoren zu definieren. Wie kann man sich ersatzweise behlfen?

    Man kann Methoden definieren, welche die entsprechenden Operationen durchführen.


Was fällt Ihnen zu folgender Anweisung in einem Java-Programm ein?

  .. code-block:: java

	  if (punkt==null)
	  {
	  // ...
	  }

  Es wird hier geprüft, ob die Variable `punkt` ein Objekt referenziert.


Was sind die wesentlichenünterschiede zwischen den Java-Typen Stringünd StringBuilder?

  StringBuilder ist einer normale veränderliche
  Klasse.
  String istünveränderlich
 ünd hat ein paar Besonderheiten: kein new notwendig, +-Operator zur
  Verkettung,


Der Vergleich von Referenztypen mit den Operatoren == bzw. != ist zwar moglich, aber meistens nicht besonders sinnvoll. Warum ist das so?

  Weil die beiden Operatoren nur die Objektreferenzen vergleichen, aber nicht den Inhalt der Objekte. Der
  Vergleich von zwei Referenzvariablen liefert also nur dann true, wenn die beiden Variablen auf dasselbe
  Objekt verweisen.


Wie kann man die Länge eines Strings zur Laufzeit ermitteln?

  variablenname.length()


Wie kann man die Länge eines Arrays zur Laufzeit bekommen?

  Über die Objektvariable length.
  array.length

Ist die Operation "1"+ 2 zulässig? Falls ja: Welchen Typ hat das Ergebnis?

  Ja, String


Ist die Operation '1'+ 2 zulässig? Falls ja: Welchen Typ hat das Ergebnis?

  Ja, Int


Definieren Sie ein arrayünd initialisieren Sie es mit folgenden Werten; 14, 2, 17, 71, 100.0

  .. code-block:: java

    double[] x = new double[] {14, 2, 17, 71, 100.0};


Welche Methoden bezeichnet man auch als Funktionen?

  Methoden mit einem Rückgabewert


Was bedeutet das reservierte Wort private in Java?

  Ein Zugriff auf diese Elemente von außen ist nicht mäglich.


Was ist ein Copy-Konstruktor?

  Erzeugt eine Kopie eines Objekts.


Welche Wert hat eine boolean-Objektvariable nach der Erzeugung, falls die Klasse keinen explizit definierten Konstruktor hat?

  false


Zählen Sie alle Ihnen bekannte Werttypen in Java auf.

  char, byte, short, int, long, boolean, float, double


Wie werden neue Objekte erzeugt?

  Mit dem reservierten Wort new wird ein Konstruktor aufgerufen.


Wie werden Klassenvariablen definiert?

  Mit dem Modifier static


Geben Sie ein einfaches Beispiel fär die Definition einer Methodeünd deren Aufruf an.

  .. code-block:: java

    // Definition:
       double kubik(double x) { return x*x*x; }

    // Aufruf:
       double y=myobj.kubik(2);


Wodurchünterscheiden sich die Zeichensätze ASCII, ISO-Latin1ündünicode?

  Anzahl der Zeichen, verschiedene Zeichen mit Zeichencodes gräßer 12


Was ist die Gemeinsamkeit bei den Zeichensätzen ASCII, ISO-Latin1ündünicode?

  Die ersten 128 Zeichen sind gleich.





Wie viele Elemente enthält das folgende Array: int [][][] = new int [2][4][3]; ?

  2 · 4 · 3 = 24 Elemente


Welche besonderen Werte kann eine double-Variable annehmen?

  Double.NaN, Double,POSITIVE INFINITY, Double.NEGATIVE INFINITY


Was bedeutet das reservierte Wort public in Java?

  Auf das entsprechende Element ist ein Zugriff von außen möglich.


Was ist die Aufgabe eines Konstruktors?

  Objekt erzeugenünd Anfangszustand herstellen.


Welchen Wert hat eine lokale int-Variable, der kein Wert zugewiesen wurde?

  Der Wert istündefiniert.


Wieviele Referenztypen kann es in einem Java-Programm geben?

  beliebig viele


Wie kann ein Ojekt in Java wieder zerstört werden?

  Das geschieht automatisch.


Was ist das Besondere an Klassenvariablen?

  Klassenvariablen sind nur einmal pro Klasse vorhanden.


Wie ist ein Methodenkopf aufgebaut?

  Typ Name ( Parameterliste )



2. Semester
-----------



Codebeispiele:
==============

Zahlentrippel
-------------

.. code-block:: java

    public class Tripple {
	private int a;
	private int b;
	private int c;

	Tripple(int a,int b,int c){
	    this.a = a;
	    this.b = b;
	    this.c = c;

	}

	public boolean equals (Tripple trip) {
	    if (a == trip.a && b == trip.b && c == trip.c) return true;
	    if (a == trip.a && b == trip.c && c == trip.b) return true;
	    if (a == trip.b && b == trip.a && c == trip.c) return true;
	    if (a == trip.b && b == trip.c && c == trip.a) return true;
	    if (a == trip.c && b == trip.b && c == trip.a) return true;
	    if (a == trip.c && b == trip.a && c == trip.b) return true;

	    return false;
	}

	public static void main(String[] args) {
	    Tripple t1 = new Tripple(1, 9 ,8);
	    Tripple t2 = new Tripple(9, 1 ,8);
	    Tripple t3 = new Tripple(8, 1 ,9);
	    Tripple t4 = new Tripple(8, 1 ,99);

	    System.out.println(t1.equals(t1) + " " + t1.equals(t2) + " " + t1.equals(t3) + " " + t1.equals(t4) );

	}
    }


Polynomial
----------

.. code-block:: java

    public class Tripple {
	private int a;
	private int b;
	private int c;

	Tripple(int a,int b,int c){
	    this.a = a;
	    this.b = b;
	    this.c = c;

	}

	public boolean equals (Tripple trip) {
	    if (a == trip.a && b == trip.b && c == trip.c) return true;
	    if (a == trip.a && b == trip.c && c == trip.b) return true;
	    if (a == trip.b && b == trip.a && c == trip.c) return true;
	    if (a == trip.b && b == trip.c && c == trip.a) return true;
	    if (a == trip.c && b == trip.b && c == trip.a) return true;
	    if (a == trip.c && b == trip.a && c == trip.b) return true;

	    return false;
	}

	public static void main(String[] args) {
	    Tripple t1 = new Tripple(1, 9 ,8);
	    Tripple t2 = new Tripple(9, 1 ,8);
	    Tripple t3 = new Tripple(8, 1 ,9);
	    Tripple t4 = new Tripple(8, 1 ,99);

	    System.out.println(t1.equals(t1) + " " + t1.equals(t2) + " " + t1.equals(t3) + " " + t1.equals(t4) );

	}
    }



Übungsaufgaben
--------------

.. code-block:: java

  public class Rehersal_exercises {

      public static void main(String[] args) {
	  int a = Integer.parseInt(args[0]);
	  int b = Integer.parseInt(args[1]);
	  int c = Integer.parseInt(args[2]);

	  // 1. Test

	  // MEDIAN von 3 Zahlen
	  int med = a;

	  if ((a >= c & c >= b) | (b >= c & c >= a)) med = c;
	  if ((a >= b & b >= c) | (c >= b & b >= a)) med = b;
	  if ((b >= a & a >= c) | (c >= a & a >= b)) med = a;

	  System.out.println("----- Median -----");
	  System.out.println("Input:  a = " + a + ", b = " + b + ", c = " + c);
	  System.out.println("Median: " + med + "\n");


	  // Dreieck
	  double seiteA = a;
	  double seiteB = b;
	  double gamma = Math.toRadians(c);
	  double Area = (1d / 2d) * seiteA * seiteB * Math.sin(gamma);

	  System.out.println("----- Dreiecks Berechnung ----- ");
	  System.out.printf("Input: a = %.0f, b = %.0f, Winkel Gamma (rad / degree) = %.2f / %d%n", seiteA, seiteB, gamma, c);
	  System.out.printf("Output: Fläche = %.02f Sin Gamma %f %n%n", Area, Math.sin(gamma));


	  // Parallelschaltung von Widerständen
	  double R1 = a;
	  double R2 = b;
	  double Rp = (R1 * R2) / (R1 + R2);

	  System.out.println("----- Wiederstand ----- ");
	  System.out.printf("R1: %.3f, R2: %.3f, Rp: %.3f%n%n", R1, R2, Rp);


	  // Kreissektoründ -abschnitt
	  double r = Math.toRadians(a);
	  double alpha = c;
	  double SectorArea = (alpha * r * r) / 2d;
	  double SegmentLength = r * r / 2d * (alpha - Math.sin(alpha));

	  System.out.println("----- Kreissektoründ Kreissegment ----- ");
	  System.out.printf("Input:  Radius: %.0f, alpha (rad / deg): %.02f / %.02f%n", r, alpha, Math.toDegrees(alpha));
	  System.out.printf("Output: Kreissektor Fläche: %.03f, Kreissegment Länge: %.03f%n%n", SectorArea, SegmentLength);

	  // Tetraederberechnung
	  double TetraderVol = (seiteA * seiteA * seiteA * Math.sqrt(2)) / 12;
	  double TetraderArea = seiteA * seiteA * Math.sqrt(3);

	  System.out.println("----- Tetrader Berechnung ----- ");
	  System.out.printf("Input:  Seite: %.0f%n", seiteA);
	  System.out.printf("Output: Tetraeder Volumen: %.03f, Tetraeder Oberfläche: %.03f%n%n", TetraderVol, TetraderArea);

	  // Freier Fall
	  double hoehe = a;
	  double g = 9.80665; // m / s²
	  double impactVelocity = Math.sqrt(2 * g * hoehe);
	  double fallTime = impactVelocity / hoehe;

	  System.out.println("----- Freier Fall ----- ");
	  System.out.printf("Input:  Fallhöhe: %.0f%n", hoehe);
	  System.out.printf("Output: Aufprallgeschwindigkeit: %.03f (m/s²), Fallzeit: %.03f (s)%n%n", impactVelocity, fallTime);

	  // Fabonacci Nummern
	  int n = a;
	  long f0 = 0;
	  long f1 = 1;

	  System.out.println("----- Fabonacci nummern ----- ");
	  System.out.println("Input: , n = " + n);
	  System.out.print("Fabonacci nummern: ");
	  if (n >= 1) System.out.print(f0 + ", ");
	  if (n >= 2) System.out.print(f1 + ", ");
	  if (n >= 3) {
	      for (int i = 3; i <= n; i++) {
		  long fp = f0 + f1;
		  System.out.print(fp + ", ");
		  f0 = f1;
		  f1 = fp;
	      }
	  }
	  System.out.print("\n");

	  // Zweierpotenzen
	  int x = a;
	  int i = 0;
	  double result = 0;

	  while (result < x) {
	      result = Math.pow(2, i);
	      i++;
	  }

	  System.out.println("----- Zweierpotenzen ----- ");
	  System.out.println("Input: x = " + x);
	  System.out.println("Zweierpotenzen :" + i + " " + result + "\n");

	  // römische Zahl in Dezimalzahl
	  int inputArab = (a + 10 * b + 100 * c) * a * b * c;
	  int arab1000 = inputArab / 1000;
	  int arab100 = inputArab / 100 % 10;
	  int arab10 = inputArab / 10 % 10;
	  int arab1 = inputArab % 10;
	  String Rom1 = "Fehler";
	  String Rom10 = "Fehler";
	  String Rom100 = "Fehler";
	  String Rom1000 = new String(new char[arab1000]).replace("\0", "M");

	  switch (arab1) {
	      case 1:
		  Rom1 = "I";
		  break;
	      case 2:
		  Rom1 = "II";
		  break;
	      case 3:
		  Rom1 = "III";
		  break;
	      case 4:
		  Rom1 = "IV";
		  break;
	      case 5:
		  Rom1 = "V";
		  break;
	      case 6:
		  Rom1 = "VI";
		  break;
	      case 7:
		  Rom1 = "VII";
		  break;
	      case 8:
		  Rom1 = "VIII";
		  break;
	      case 9:
		  Rom1 = "IX";
		  break;
	      case 0:
		  Rom1 = "";
		  break;
	  }

	  switch (arab10) {
	      case 1:
		  Rom10 = "X";
		  break;
	      case 2:
		  Rom10 = "XX";
		  break;
	      case 3:
		  Rom10 = "XXX";
		  break;
	      case 4:
		  Rom10 = "XL";
		  break;
	      case 5:
		  Rom10 = "L";
		  break;
	      case 6:
		  Rom10 = "LX";
		  break;
	      case 7:
		  Rom10 = "LXX";
		  break;
	      case 8:
		  Rom10 = "LXXX";
		  break;
	      case 9:
		  Rom10 = "XC";
		  break;
	      case 0:
		  Rom10 = "";
		  break;
	  }

	  switch (arab100) {
	      case 1:
		  Rom100 = "C";
		  break;
	      case 2:
		  Rom100 = "CC";
		  break;
	      case 3:
		  Rom100 = "CCC";
		  break;
	      case 4:
		  Rom100 = "CD";
		  break;
	      case 5:
		  Rom100 = "D";
		  break;
	      case 6:
		  Rom100 = "DC";
		  break;
	      case 7:
		  Rom100 = "DCC";
		  break;
	      case 8:
		  Rom100 = "DCCC";
		  break;
	      case 9:
		  Rom100 = "CM";
		  break;
	      case 0:
		  Rom100 = "";
		  break;
	  }

	  System.out.println("----- Römische Zahlen ----- ");
	  System.out.println("Input arabisch : " + arab1000 + " + " + arab100 + " + " + arab10 + " + " + arab1 + " = " + inputArab);
	  System.out.println("Output römisch :" + Rom1000 + Rom100 + Rom10 + Rom1);
	  System.out.println("");


	  // 2. Test

	  /*
	  Schreiben Sie eine Java-Funktion, welche einen String als Parameter entgegennimmtünd die Länge
	  der längstenünunterbrochenen Folge von Ziffern als Ergebnis zurückgibt. (ohne Regex)
	  */

	  System.out.println("----- String Manipulation ----- ");
	  String text = ("A-Ä-Ö-Ü a-e-ö-ü hallo 12 hnjkj54 n324 ä 2n5ö Ä Üöä23 3252l 5 235 jjnljh 5t252p 12345678 ");
	  System.out.println(text);


	  int sequenceLength = 0;
	  int maxSequenceLength = 0;

	  for (int j = 0; j < text.length(); j++) {
	      if (text.charAt(j) >= '0' & text.charAt(j) <= '9') {
		  sequenceLength++;
	      } else {
		  maxSequenceLength = Math.max(maxSequenceLength, sequenceLength);
		  sequenceLength = 0;
	      }
	  }

	  System.out.println("Länge längste zusammenhängende Ziffernfolge: " + maxSequenceLength);

	  /*
	 ümlaute ersetzen
	  Schreiben Sie eine Java-Funktion, welche einen String als Parameter entgegennimmtünd alle
	 ümlaute durch "AE", "OE", "UE", "ae", "ou", "ue" ersetzt.
	  */

	  StringBuilder textUl = new StringBuilder(text);

	  for (int k = 0; k < textUl.length(); k++) {
	      if (textUl.charAt(k) == 'ä') textUl.replace(k, k + 1, "ae");
	      if (textUl.charAt(k) == 'Ä') textUl.replace(k, k + 1, "Ae");
	      if (textUl.charAt(k) == 'ö') textUl.replace(k, k + 1, "oe");
	      if (textUl.charAt(k) == 'Ö') textUl.replace(k, k + 1, "Oe");
	      if (textUl.charAt(k) == 'ü') textUl.replace(k, k + 1, "ue");
	      if (textUl.charAt(k) == 'Ü') textUl.replace(k, k + 1, "Ue");
	  }

	  System.out.println("Umlaute ersetzt: " + textUl.toString());

	  /*
	  Differenzen
	  Schreiben Sie ein Java-Programm, welches eine beliebige Anzahl von ganzen Zahlen als
	  Kommandozeilenparameter entgegennimmtünd folgende Aufgabe löst:
	  Das Programm soll alle möglichen Differenzen bilden (nur Absolutwerte)ünd aufsteigend
	  sortiert ausgeben.
	  Verbesserung: Jede auftretende Differenz soll nur ein Mal ausgegeben werden.
	  */

	  System.out.println("----- Differenzen ----- "); //todo
	  double[] inputNumbers = {33, 2, 9, 34, 34, 5, 32, 2, 3, 5, 6, 3, 77};
	  double[] differences = new double[(inputNumbers.length) * 4];

	  System.out.println("----- Emtpy Array ----- " + inputNumbers.length);

	  for (double element : differences) {
	      System.out.println(element);
	  }
	  System.out.println("----- ----- ");

	  intünique_elements_count = 0;

	  for (intü = 0;ü < inputNumbers.length;ü++) {
	      for (int v =ü + 1; v < inputNumbers.length; v++) {
		  double diffValue = Math.abs(inputNumbers[u] - inputNumbers[v]);

		  boolean firstOccurence = true;

		  for (double element : differences) {
		      if (element == diffValue) {
			  firstOccurence = false;
		      }
		  }

		  if (firstOccurence) {
		      differences[unique_elements_count] = diffValue;
		     ünique_elements_count++;
		      System.out.println("Value: " + diffValue + " Position: " +ünique_elements_count);
		  }
	      }
	  }

	  System.out.println("----- Filled Array ----- ");

	  for (double element : differences) {
	      System.out.println(element);
	  }
	  System.out.println("----- ----- ");

	  for (i = 0; i <ünique_elements_count; i++) {
	      int l = i + 1;
	      while ((l > 0) && (differences[l] < differences[l - 1]) && (l <ünique_elements_count)) {
		  double tmp_element = differences[l];
		  differences[l] = differences[l - 1];
		  differences[l - 1] = tmp_element;
		  l--;
	      }
	  }

	  System.out.println("----- Sorted Array ----- ");

	  for (i = 0; i <ünique_elements_count; i++) {
	      System.out.println(differences[i]);
	  }
	  System.out.println("----- ----- ");

	  /*
	  Geben Sie eine Methode an, welche einen String als Parameter entgegennimmtünd als Ergebnis true liefert,
	  wenn folgende Bedingungen erfüllt sind, sonst false.
	  Bedingungen:
	      1. Im String dürfen nur Ziffern enthalten sein.
	      2. Jede enthaltene Ziffer darf nur ein Mal vorkommen.
	  */

	  System.out.println(Ziffernstring("01a"));
	  System.out.println(('1' + 2));
	  System.out.println(("1" + 2));

	  /*
	  Schreiben Sie eine statische Methode zurümwandlung von römischen Zahlen in Dezimalzahlen.
	  Die Methode soll einen String-Parameter mit der römischen Zahl erhaltenünd als Ergebnis die
	  äquivalente arabische Zahl zurückgeben.
	  */

	  String roman = ("MCMLXXXIV");

	  System.out.println("----- Römische Zahlen -> Dezimalzahlen ----- ");
	  System.out.println("Input römisch : " + roman);
	  System.out.println("Output arabisch :" + romanToArabic(roman));
	  System.out.println("");

      }

      public static boolean Ziffernstring(String text) {
	  boolean[] Ziffern = new boolean[10];

	  for (int i = 0; i < text.length(); i++) {
	      char character = text.charAt(i);

	      if (character < '0' || character > '9') {
		  return false;
	      } else {
		  int x = character - '0';
		  System.out.println(x + " " + character);
		  if (Ziffern[x] == true) {
		      return false;
		  } else {
		      Ziffern[x] = true;
		  }
	      }
	  }
	  return true;
      }

      public static int romanToArabic(String roman) {
	  int decimalValue = 0;

	  for (int i = 0; i < roman.length(); i++) {
	      char currentDigit = roman.charAt(i);
	      char nextDigit;
	      int sign = 1;

	      if (i + 1 < roman.length()) {
		  nextDigit = roman.charAt(i + 1);
	      } else {
		  nextDigit = currentDigit;  // a bitügly but works
	      }

	      if (romanDigitValue(currentDigit) < romanDigitValue(nextDigit)) {
		  sign = -1;
	      }

	      decimalValue += romanDigitValue(currentDigit) * sign;
	  }
	  return decimalValue;
      }

      public static int romanDigitValue(char romanDigit) {
	  int digitValue = 0;

	  if (romanDigit == 'I') digitValue += 1;
	  if (romanDigit == 'V') digitValue += 5;
	  if (romanDigit == 'X') digitValue += 10;
	  if (romanDigit == 'L') digitValue += 50;
	  if (romanDigit == 'C') digitValue += 100;
	  if (romanDigit == 'D') digitValue += 500;
	  if (romanDigit == 'M') digitValue += 1000;

	  return (digitValue);
      }

  }
