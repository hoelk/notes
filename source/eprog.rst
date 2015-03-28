Einführung in das Programmieren (Java)
######################################


Notizen
=======

.. _primitve-data-types:

Einfache / Primitive Datentypen in Java:
-----------------------------------------

+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| Datentyp   | Größe¹           | Wrapper-Klasse        | Wertebereich                     | Beschreibung                                      |
+============+==================+=======================+==================================+===================================================+
| boolean    | JVM-Spezifisch   | java.lang.Boolean     | true / false                     | Boolescher Wahrheitswert                          |
+------------+------------------+-----------------------+----------------------------------+---------------------------------------------------+
| char       | 16 bit           | java.lang.Character   | 0 … 65.535 (z. B. ‘A’)           | Unicode-Zeichen (UTF-16)                          |
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

1. Semester
-----------

Test 1
^^^^^^

In welcher Datei steht der Bytecode der Klasse „Motorfahrzeug“?

  Motorfahrzeug.class

Was ist Voraussetzung um einer Variablen Werte eines anderen Datentyps zuweisen zu können?

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

  Eine Methode ist polymorph wenn sie unterschiedliche Datentypen annimmt.

  * Beispiel: Der ``+`` Opperator ist akzeptiert ``int`` und ``double`` Werte.

Hat eine Anweisung einen Typ?

  Nein, eine Anweisung kann aber einem Ausdruck einen Wert zuweisen

Was macht ein Typecast und wie ist die Syntax?

  Konvertiert einen Ausdruck von einem Datentyp in einem anderen.

  * Z.b (int) (double)
  * `Mehr Details <http://www.java-tutorial.org/typecasting.html>`_

Wie ruft man den Java-Compiler auf der Kommandozeile auf?

  ``javac Klassenname.java``

Was ist der Unterschied zwischen int und double?

  * int: ganze Zahlen
  * double: Gleitkommazahlen

Mit welchen Operationen können Sie aus einer 7-stelligen Matrikelnummer das Inskriptionsjahr extrahieren?

  * 0499999 / 100000 = 04
  * 04 + 2000 = 2004

Kommt die folgende Schleife zu einem Ende? Begründung?

  ``for(int j=1; j!=0; j++) ;``

  Ja, wegen wrap around. Sobald der der Wert für j den maximalen integer wert
  ``231 - 1`` übersteigt fängt er von ganz unten an ``-231``.

  Anmerkung: ``double`` überlauf wrapt nicht sonder liefert +/- Unendlich.

Wie startet man ein Java-Programm?


  ``java Klassenname`` in der Kommandozeile eingeben.

Welche Dateiendung muss eine Java-Quelltextdatei haben?


  ``.java``

Wie heißt die Datei, in welcher der Quelltext der Klasse „Motorfahrzeug“ steht?

  ``Motorfahrzeug.java``

Was wird benötigt, um auf einem beliebigen Rechner ein Java-Programm ausführen zu können?

  Ein JRE (Java Runtime Envirnment) und das Programm (.class Datei).

Was brauchen Sie um Java-Quellcode zu erstellen?

  Einen text editor.

Wie erzeugt man ausgehend von der Datei „Test.java“ die Datei „Test.class“?

  Kompilieren. ``javac Test.java``

Was versteht man unter einem Syntaxfehler?

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

  Nein. Man kann aber unter umständen Datentypen konvertierten (typecasten). Dies
  kann auch autamtisch passieren.
  Z.b. Wenn man versucht einer ``double`` Variablen einen ``integer`` wert
  zuzuweisen, wird dieser automatisch nach ``double`` konvertiert.

Wenn man einen Datentyp A einer Variablen von einem anderen Datentyp B zuweisen kann,
dann sagt man „A ist . . . . . . . . . zu B“.

  kompatibel (implizite Typenkonversation wird durchgeführt)
  (``integer`` ist kompatibel zu ``double``, aber nicht umgekehrt!)

Was ist der Unterschied zwischen float und double?

    * Beides sind datentypen für Gleitkommawerte
    * ``double`` stellt mehr Speicherplatz zur Verfügung, daher:
        * höhere Genauigkeit (``double`` steht für *Doppelte Genauigkeit*)
        * höheres Max und tieferes Min als ``float``
    * Siehe :ref:`primitve-data-types`


Welche der folgenden Namen sind gültige Bezeichner in Java?

  3fach, null, jahr2000, 8ung, after_sun, just-in-time, class, classic,
  r2d2, a1a1a1a1a, 12345abcde, holzWeg

  jahr2000, after_sun, classic, r2d2, a1a1a1a1a, holzWeg

  Regeln:
      * Der Name darf nicht mit einer Ziffer beginnen
      * Sonderzeichen wie : * ; + - / sind nicht nicht erlaubt
      * Reservierte Wörter und Schlüsselwörter sind nicht erlaubt

Was ist der Unterschied zwischen = und == ?

    * ``=``  ist eine Zuweisung (``a = 1`` weist der Variablen ``a`` den Wert ``1`` zu)
    * ``==`` ist ein Vergleich  (``1 == 1`` gibt aus ``true``)

Welche Modifier kennen Sie und was ist Ihre Bedeutung?

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
      * ``synchronized`` and volatile modifiers, which are used for threads.

Was ist der Unterscheid zwischen Ausdruck und Anweisung?

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

    * Implizite Typenkonversation geht nur, wenn ein niederwertiger Datentyp in einen höher wertigen Datentypen umgewandelt wird (``int`` -> ``double``)
    * explizite Typenkonversation mittels typecast funktioniert auch anders herum

Kann man in Java eigene Typen definieren?

    * Ja, allerdings nur Referenztypen und keine primitiven typen.

Was versteht man unter Initialisierung?

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

In welchen zwei unterschiedlichen Situationen kommt in Java das reservierte Wort this zum Einsatz?

  * Zum Zugriff auf eine Objektvariable, wenn sie durch einen gleichnamigen Parameter oder eine gleichnamige lokale Variable verdeckt wird.
  * Bei der Konstruktorverkettung zum Aufruf eines anderen Konstruktors.


Was bedeutet overloading und worauf ist dabei zu achten?

  Overloading bezeichnet die Möglichkeit,
  dass eine Klasse mehrere Methoden mit gleichem Namen
  haben kann. Diese Methoden müssen
  sich aber anhand der Parameterliste unterscheiden lassen,
  entweder durch unterschiedliche Anzahl von Parametern oder durch unterschiedliche Datentypen der
  Parameter.


Wozu dient ein Konstruktor?

    Ein Konstruktor dient zur korrekten Initialisierung eines neu erzeugten Objekts einer Klasse.


Wieviele Konstruktoren kann eine Klasse minimal und maximal haben?

    Jede Klasse hat mindestens einen Konstruktor und kann beliebig viele davon haben. Wenn in einer
    Klasse kein Konstruktor definiert wird, dann erzeugt der Compiler automatisch einen
    Default-Konstruktor.


Wie funktioniert die Initialisierung von Objekten im Gegensatz zu primitiven Variablen?

    Im Gegensatz zu primitiven Variablen, die explizit initialisiert werden müssen,
    sind Objekte nach dem
    Anlegen automatisch initialisiert. Falls Objektvariablen nicht durch den Konstruktor initialisiert werden,
    bekommen Sie typabhängig
    passende Default-Werte.


Was sind die Vor- und Nachteile einer unveranderlichen Klasse

    Vorteil: Unveränderliche Klassen können fast wie primitive Variablen verwendet werden.
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


Was sind die wesentlichen Unterschiede zwischen den Java-Typen String und StringBuilder?

  StringBuilder ist einer normale veränderliche
  Klasse.
  String ist unveränderlich
  und hat ein paar Besonderheiten: kein new notwendig, +-Operator zur
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


Definieren Sie ein array und initialisieren Sie es mit folgenden Werten; 14, 2, 17, 71, 100.0

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


Geben Sie ein einfaches Beispiel fär die Definition einer Methode und deren Aufruf an.

  .. code-block:: java

    // Definition:
       double kubik(double x) { return x*x*x; }

    // Aufruf:
       double y=myobj.kubik(2);


Wodurch unterscheiden sich die Zeichensätze ASCII, ISO-Latin1 und Unicode?

  Anzahl der Zeichen, verschiedene Zeichen mit Zeichencodes gräßer 12


Was ist die Gemeinsamkeit bei den Zeichensätzen ASCII, ISO-Latin1 und Unicode?

  Die ersten 128 Zeichen sind gleich.





Wie viele Elemente enthält das folgende Array: int [][][] = new int [2][4][3]; ?

  2 · 4 · 3 = 24 Elemente


Welche besonderen Werte kann eine double-Variable annehmen?

  Double.NaN, Double,POSITIVE INFINITY, Double.NEGATIVE INFINITY


Was bedeutet das reservierte Wort public in Java?

  Auf das entsprechende Element ist ein Zugriff von außen möglich.


Was ist die Aufgabe eines Konstruktors?

  Objekt erzeugen und Anfangszustand herstellen.


Welchen Wert hat eine lokale int-Variable, der kein Wert zugewiesen wurde?

  Der Wert ist undefiniert.


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


	  // Kreissektor und -abschnitt
	  double r = Math.toRadians(a);
	  double alpha = c;
	  double SectorArea = (alpha * r * r) / 2d;
	  double SegmentLength = r * r / 2d * (alpha - Math.sin(alpha));

	  System.out.println("----- Kreissektor und Kreissegment ----- ");
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
	  Schreiben Sie eine Java-Funktion, welche einen String als Parameter entgegennimmt und die Länge
	  der längsten ununterbrochenen Folge von Ziffern als Ergebnis zurückgibt. (ohne Regex)
	  */

	  System.out.println("----- String Manipulation ----- ");
	  String text = ("A-Ä-Ö-Ü a-e-ö-ü hallo 12 hnjkj54 n324 ä 2n5 ö Ä Üöä23 3252l 5 235 jjnljh 5t252p 12345678 ");
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
	  Umlaute ersetzen
	  Schreiben Sie eine Java-Funktion, welche einen String als Parameter entgegennimmt und alle
	  Umlaute durch "AE", "OE", "UE", "ae", "ou", "ue" ersetzt.
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
	  Kommandozeilenparameter entgegennimmt und folgende Aufgabe löst:
	  • Das Programm soll alle möglichen Differenzen bilden (nur Absolutwerte) und aufsteigend
	  sortiert ausgeben.
	  • Verbesserung: Jede auftretende Differenz soll nur ein Mal ausgegeben werden.
	  */

	  System.out.println("----- Differenzen ----- "); //todo
	  double[] inputNumbers = {33, 2, 9, 34, 34, 5, 32, 2, 3, 5, 6, 3, 77};
	  double[] differences = new double[(inputNumbers.length) * 4];

	  System.out.println("----- Emtpy Array ----- " + inputNumbers.length);

	  for (double element : differences) {
	      System.out.println(element);
	  }
	  System.out.println("----- ----- ");

	  int unique_elements_count = 0;

	  for (int u = 0; u < inputNumbers.length; u++) {
	      for (int v = u + 1; v < inputNumbers.length; v++) {
		  double diffValue = Math.abs(inputNumbers[u] - inputNumbers[v]);

		  boolean firstOccurence = true;

		  for (double element : differences) {
		      if (element == diffValue) {
			  firstOccurence = false;
		      }
		  }

		  if (firstOccurence) {
		      differences[unique_elements_count] = diffValue;
		      unique_elements_count++;
		      System.out.println("Value: " + diffValue + " Position: " + unique_elements_count);
		  }
	      }
	  }

	  System.out.println("----- Filled Array ----- ");

	  for (double element : differences) {
	      System.out.println(element);
	  }
	  System.out.println("----- ----- ");

	  for (i = 0; i < unique_elements_count; i++) {
	      int l = i + 1;
	      while ((l > 0) && (differences[l] < differences[l - 1]) && (l < unique_elements_count)) {
		  double tmp_element = differences[l];
		  differences[l] = differences[l - 1];
		  differences[l - 1] = tmp_element;
		  l--;
	      }
	  }

	  System.out.println("----- Sorted Array ----- ");

	  for (i = 0; i < unique_elements_count; i++) {
	      System.out.println(differences[i]);
	  }
	  System.out.println("----- ----- ");

	  /*
	  Geben Sie eine Methode an, welche einen String als Parameter entgegennimmt und als Ergebnis true liefert,
	  wenn folgende Bedingungen erfüllt sind, sonst false.
	  Bedingungen:
	      1. Im String dürfen nur Ziffern enthalten sein.
	      2. Jede enthaltene Ziffer darf nur ein Mal vorkommen.
	  */

	  System.out.println(Ziffernstring("01a"));
	  System.out.println(('1' + 2));
	  System.out.println(("1" + 2));

	  /*
	  Schreiben Sie eine statische Methode zur Umwandlung von römischen Zahlen in Dezimalzahlen.
	  Die Methode soll einen String-Parameter mit der römischen Zahl erhalten und als Ergebnis die
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
		  nextDigit = currentDigit;  // a bit ugly but works
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
