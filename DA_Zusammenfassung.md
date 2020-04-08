# Algorithmen Zusammenfassung

## Overview

- 0 Einführung
  - Komplexität von Algorithmen
    - O-Notation
  - Weitere Eigenschaften-
- 1 lineare Datenstrukturen
  - Dynamische Mengen
    - Array List
    - Linked List
    - Collections API
    - Map API
    - Stack
    - Queue
    - Deque
- 2 Suchen
  - linear search
  - binäre suche
- 3 Sortieren
  - Insertion-Sort
  - Merge-Sort
  - Quick-Sort
  - Bucket-Sort
- 4 Greedy Algorithmen
  - Aktivitäten Auswahl Problem
  - Komprimierungsproblem
    - Huffman Algorithmus
  - Kürzester Pfad Problem
    - Graphen
    - Dijkstra
- 5 Algorithmen auf Zeichenketten
- 6 Suchen in Bäumen

## Komplexität von Algorithmen

Die Effizienz eines Algorithmus beschreibt wie sparsam dieser mit den Ressourcen
umgeht, die er zur Lösung eines gegebenen Problems beansprucht.
Verschiedene Lösungen des gleichen Probleme können drastische Unterschiede in
ihrer Effizienz haben.

Unter Komplexität eines Algorithmus versteht man seinen maximalen Ressourcenverbrauch,
der in der Regel in Abhängigkeit von der Grösse der Eingabe angegeben wird:

>Komplexität eines Algorithmus = Funktion f(n) der Eingabegrössen

Ressourcen in Anzahl Rechenschritte (Zeitkomplexität) oder Speicherbedarf (anz Variablen -> Platzkomplexität).

Zentrale Frage: Wie ändert sich die Laufzeit, wenn n grösser wird? (Wachstumsrate der Laufzeit)

Komplexität wird immer für den schlechtesten Fall angegeben. Wie lang wird der
Algorithmus maximal brauchen? Schlechtester Fall tritt sehr häufig auf.
Z.B. Suchen eines nicht vorhandenen Wertes.

### O-Notation

Für Laufzeit f:

- **0(1)** f überschreitet einen bestimmten konstanten Wert nicht.
- **O(log n)** f wächst logarithmisch
- **O(sqrt(n))** f wächst wie Wurzelfunktion
- **O(n)** f wächst linear
- **O(n log n)** f wächst log-linear
- **O(n^2)** f wächst quadratisch$
- **O(2^n)** f wächst exponentiell
- **O(n!)** f wächst faktoriell

Kategorisiert heisst das:

- 0(1), O(log n), O(sqrt(n)) wachsen sublinear
- 0(n), O(n log n) wachsen ungefähr linear
- O(n^2) ^3, ^4... polynomielles Wachstum
- exponentiell und faktoriell: selbst kleine Aufgaben kaum lösbar

## Weitere Eigenschaften

- **determiniert** Algorithmus liefert bei jeder Ausführung mit gleichen Eingaben
  die gleiche Ausgabe. Zwischenresultate dürfen sich unterscheiden
- **deterministisch** determinierter Algorithmus, bei dem zu jedem Zeitpunkt der
  nächste Schritt eindeutig definiert ist.
- **Terminiertheit** Algorithmus hält nach Endlich vielen Schritten an
- **Halteproblem** Beweis, dass es keinen Algorithmus gibt, der herausfinden kann
  ob ein Algorithmus terminiert ist. Kann beweisen dass er es ist, aber nicht dass
  er es nicht ist.
- **Korrektheit** Der Algorithmus liefert für jede Eingabe eine Korrekte Ausgabe.
  Testen reicht nicht, ein Beweis muss her.

## Lineare Datenstrukturen (2)

### Dynamische Mengen

Dynamische Mengen passen ihre Grösse der Anzahl Werte and, die sie enthalten.

Eine dynamische Menge die ...

- hinzufügen (add())
- entfernen (remove())
- suchen (contains())

... unterstützt, wird als "Wörterbuch" bezeichnet. Die Operationen heissen Wörterbuchoperationen.

### Arraylist

- Vorteile
  - Schneller Zugriff auf Element in Mitte
- Nachteile
  - Aufwändiges entfernen (Nachrücken)
  - Aufwändiges vergrössern (Alle Elemente kopieren)

```java
public class OwnArrayList {
    private int capacity = 10;
    private int size;
    private Object[] listElements;

    public OwnArrayList() {
        this.size = 0;
        this.listElements = new Object[capacity];
    }

    public int indexOf(Object o) {
        for (int i = 0; i < this.size; i++) {
            if (o.equals(this.listElements[i])
                return i;
        }
        return -1;
    }
    public boolean add(Object o) {
        if (this.size == this.capacity) {
            this.increaseSize();
        }
        this.listElements[size] = o;
        this.size++;
        return true;
    }
    private void increaseSize() {
        this.capacity *= 2;
        Object[] array = new Object[this.capacity];
        for (int i = 0; i < size; i++) {
            array[i] = this.listElements[i];
        }
        this.listElements = array;
    }
    public Object remove(int index) {
        Object removed = this.listElements[index];
        for(int i = index; i < this.size-1; i++) {
            this.listElements[i] = this.listElements[i+1];
        }
        this.listElements[size] = null;
        this.size--;
        return removed;
    }
}
```

### Linked List

- singly liked list: kennt nur das nächste Element
- doubly linked list: kennt letztes und nächstes Element

- Vorteile
  - schnelles Entfernen von Elementen (Zeiger ändern)
  - schnelles hinzufügen in der Mitte der Liste

```java
public class Node<E>{
    private <E> element;
    private Node<E> next;

    public Node(E e) {
        this.element = e;
    }
    public E getElement() {return this.element;}
    public Node<E> getNext() {return this.next;}
    public void setNext(Node<E> node) {this.next = node;}
    public boolean contains(E other) {return this.element.equals(other);}
}
public class LinkedList<E> {
    private Node<E> startNode;

    public LinkedList() {
        this.startNode = null;
    }
    public int indexOf(E e) {
        Node current = this.startNode;
        int index = 0;
        while (current != null) {
            if (current.contains(e)) {
                return index;
            } else{
                index++;
                current = current.getNext();
            }
        }
        return -1;
    }
    public boolean add(E e) {
        Node node = new Node(e);
        if (this.startNode == null) {
            this.startNode = node;
        } else {
            Node<E> current = this.startNode;
            while (current.getNext() != null) {
                current = current.getNext();
            }
            current.setNext(node);
        }
        return true;
    }
    public Node<E> remove(int index) {
        if (index < 0) {
            Node<E> current = this.startNode;
            for (int i = 0; i < index) {
                current = current.getNext();
            }
            Node<E> previous = current;
            Node<E> removed = current.getNext();
            Node<E> next = removed.getNext();

            previous.setNext(next);
            removed.setNext(null);
            return removed;

        } else {
            this.startNode = this.startNode.getNext();
            return this.startNode;
        }
    }
}
```

### Collection API

Vorteile eines Frameworks:

- Reduktion Programmieraufwand durch Bereitstellung v. DA & Alg.
- Leistungsteigerung durch optimale implementation
- Verschiedene Implementierungen einer Schnittstelle sind miteinander austauschbar

- Collection (interface)
  - Set (interface)
    - Sorted Set (interface)
      - TreeSet
    - HashSet
  - List (interface)
    - Vector
      - Stack
    - ArrayList
    - LinkedList (implementiert auch Queue & Dequeue)
  - Queue (interface)
    - Dequeue (interface)
    - Priority Queue

Methoden von Collection:

- boolean add(T t)
- boolean addAll(Collection c)
- void clear()
- boolean contains(T t)
- boolean isEmpty()
- Iterator\<E> iterator()
- boolean remove(T t)
- boolean removeAll(Collection c)
- int size()

Listen sind geordnete Mengen und implementieren zusätzlich die Methoden mit index:

- add(int index, T t)
- set(int index, T t)
- get(int index)
- indexOf(T t), lastIndexOf(T t)
- remove(int index)

LinkedList zusätzliche Methoden:

- addFirst
- addLast
- getFirst
- getLast
- removeFirst
- removeLast

Iteratoren:

- T next()
- boolean getNext()

### Map API

- Map (interface)
  - Hashmap
  - Hashtable
  - SortedMap (interface)
    - Treemap

### Stack

LIFO Prinzip

- push -> hinzufügen
- pop -> oberstes element entfernen
- peek -> auf Objekt zugreifen ohne zu entfernen
- isEmpty -> grösse gleich 0
- int search(T t) -> Distanz bis Spitze des Stapels, o. -1 wenn nicht vorhanden

### Queue

FIFO Prinzip, Enqueue -> hinzufügen, Dequeue -> Entfernen

- offer(T t) -> Element hinzufügen
- peek() -> nächstes Element erfragen
- poll() -> nächstes Element entfernen

### Deque

Wie Queue, kann aber an beiden enden Entnehmen & Hinzufügen

- offerFirst, offerLast
- peekFirst, peekLast
- pollFirst, pollLast

## Suchen (3)

**Eingabe:** Eine Folge von n Elementen, das gesuchte Element x

**Ausgabe:** Der index i an dem sich das Element in der Folge befindet, oder -1 falls es nicht vorhanden ist.

### Sequenzielle Suche

Die Folge wird Element für Element abgesucht, bis das Element gefunden wird.
Sie ist sehr ineffizient, dafür ist die Reihenfolge der Elemente aber egal.
Die Laufzeit ist O(n).

Anwendung: indexOf() von Listen

```java
// linear search
public static int linearSearch(int[] array, int key) {
    int index = 0;
    while (index < array.length) {
        if (array[index] == key) {
            return index;
        } else {
            index++;
        }
    }
    return -1;
}
```

### Binäre Suche

Rekursiver Algorithmus, Logarithmischer Aufwand O(log n).

Bedingungen: sortierte Liste, möglicher Zugriff auf mittlere Elemente (via Index)

Divide-and-conquer (Teilen-Beherrschen-Paradigma)

- Teile Problem in kleinere Teilprobleme
- Beherrsche Teilprobleme rekursiv. Wenn Problem klein genug, löse es direkt
- Vereinige die Lösungen der Teilprobleme zur Lösung des ursprünglichen Problems

```java
public static int binarySearch(int[] array, int key, int low, int high) {
    if (low > high) {
        return -1;
    }
    int middle = (low + high) / 2;
    if (array[middle] == key) {
        return middle;
    } else {
        if (key > array[middle]) {
            return binarySearch(array, key, middle+1, high);
        } else {
            return binarySearch(array, key, low, middle-1);
        }
    }
}
```

### Binäre Suchbäume

Ein binärer Suchbaum hat jeweils eine Wurzel, die sich dann in zwei Richtungen verzweigt.
Jeder Knoten verzweigt sich dann wieder in zei Richtungen. Er ist als der "Vater"
zweier Kinder.

Er ist nur effizient, wenn er verzweigt ist. Es kann zu linear ausbalancierten Bäumen
kommen, dann ist er nicht besser als ein Array.

Es gibt auch nicht binäre Bäume. Die Anzahl Kinder bezeichnet man als den Verzweigungsfaktor (b).

Ein Knoten eines Baumes kann wie folgt aussehen (darin werden Elemente  vom Typ
int gespeichert):

```java
public class TreeNode {
    private int element;
    private TreeNode father, leftChild, rightChild;

    public TreeNode(int element) {
        this.element = element;
        this.father = null;
        this.leftChild = null;
        this.rightChild = null;
    }

    // getters and setters ...
}
```

> Wenn x ein Knoten in einem binären Suchbaum ist, dann sind alle Elemente links
davon kleiner als x. Alle Elemente rechts von x sind grösser.

Die implementation des Suchbaumes:

```java
public class SearchTree {
    private TreeNode root;

    public SearchTree() {
        this.root = null;
    }

    public void add(int element) {
        TreeNode node = new TreeNode(element);
        if (this.root == null) {
            root = node;
        } else {
            TreeNode current = this.root;
            TreeNode father = null;
            boolean right = false;
            while (current != null) {
                father = current;
                if (element >= current.getElement()) {
                    current = current.getRightChild();
                    this.right = true;
                } else {
                    current = current.getLeftChild();
                    right = false;
                }
            }
            node.setFather(father);
            if (right)
                father.setRightChild(node);
            else
                father.setLeftChild(node);
        }
    }
    public TreeNode search(int key) {
        TreeNode current = this.root;
        while (current != null && current.getElement() != key) {
            if (key < current.getElement()) {
                current = current.getLeftChild();
            } else {
                current = current.getRightChild();
            }
        }
        return current;
    }
}
```

### Set

- Jeder Wert darf nur einmal vorkommen.
- ungeordnete Collection
- add gibt false zurück wenn schon vorhanden
- Methoden
  - add
  - addAll
  - remove
  - removeAll
  - size
  - isEmpty
  - contains
  - Keine Index Operationen, da ungeordnet (set, get, indexOf)

### TreeSet

- sortiert
- zwei Iteratoren (iterator, descendingIterator)
- first(), last() -> erstes letztes Element
- higher(T e), lower(T e) -> Nachbar von Element e
- Aufwändiges hinzufügen, schnelles durch iterieren in beide Richtungen, schneller zugriff auf lower und higher

### Suchen mit Hashing

Der Element mit index n, kann in einem Array mit Laufzeit O(1) gefunden werden.
Mit diesem Prinzip kann auch gesucht werden. Wenn wir die Elemente einer Menge
zu einem jeweils eindeutigen int-wert hashen können, wird das Element an Position
mit index der Hashcodes platziert.

"Direkt adressierbare Tabelle"

### Hashtabellen

Wenn die Menge der Elemente gross ist als das Array, frisst die herkömmliche
Suche mit Hashes wahnsinnig viel Speicherplatz.

Die Hashtabelle ist nicht mehr direkt adressierbar, hat aber im Mittleren Fall
immer noch O(1) Laufzeit.

Die Position wird durch das hashen des Schlüsselwertes bestimmt h(k). Array hat
die Grösse m, und hashing-funktion h() gibt integers bis max m zurück.

Es kann aber zu Kollisionen kommen: Zwei Elemente mit gleichem Hash. Zur Konfliktlösung
können alle Elemente mit gleichem Hashwert in einer LinkedList gespeichert werden.

### Hashfunktionen

Soll die *Annahme des einfachen gleichmässigen Hashings* erfüllen: Jeder Schlüssel
wird mit gleicher Wahrscheinlichkeit auf einen der m Slots fallen.

Gut ist, den Schlüssel durch Primzahlen, die nicht zu nah an einer Potenz von 2
liegen. Der Rest der Division gibt den Index (modulo).

Anzahl slots / erwartete Anzahl Element pro Slot: 2000/3 = ungefähr 701

### Hashing in Java

// TODO

## Sortieren (4)

### Insertion Sort

- Nur effizient für kleine Mengen

## Greedy Algorithmen (5)

Lösungen für Optimierungsprobleme.

Besteht aus mehreren Schritten, in jedem Schritt wird eine Entscheidung getroffen.

- Entscheidung, welche Wahl zu diesem Zeitpunkt das beste Ergebnis liefert.
- Eine getroffene Entscheidung wird nicht rückgängig gemacht (daher Greedy)

Greedy Algorithmen sind i.d.R schnell, liefern aber nicht immer die optimale Lösung

### Aktivitäten Auswahl Problem

- Koordination verschiedener Aktivitäten
- Aktivitäten verwenden gemeinsame Ressource
- Ressource kann nur Exklusiv genutzt werden
- Jede Aktivität hat eine Start- und Endzeit
- Die Aktivitäten sind kompatibel, wenn sie sich nicht überschneiden.

- Aktivitäten nach Endzeit sortieren (früheste Endzeit = am meisten Platz für andere)
- Element mit frühester Endzeit ist also Startelement
- Alle Anderen Elemente prüfen: Ist Startzeit später als Endzeit von Startelement (-> kompatibel)
- Das erste Element, dass passt, ist das mit der frühesten Endzeit (sortiert)
- Wird ausgewählt

### Komprimierungsproblem

Huffman Algorithmus: komprimieren von Zeichenketten.
Arbeitet mit einer Tabelle, wie oft jedes Zeichen vorkommt.
Für die Zeichen die Häufig vorkommen wird ein kürzeres Codewort verwendet.
Für seltene, darf das Codewort länger sein.

| Zeichen               |   a |   b |   c |   d |   e |   f |
|:----------------------|:---:|:---:|:---:|:---:|:---:|:---:|
| Häufigkeit            |  45 |  13 |  12 |  16 |   9 |   5 |
| Code fester Länge     | 000 | 001 | 010 | 011 | 100 | 101 |
| Code variabler Länge  |   0 | 101 | 100 | 111 | 1101| 1100|

Um die Codewörter auseinander halten zu können, ist es nicht erlaubt, dass das
Codewort für ein Zeichen das Präfix für ein anderes Zeichen ist.
Sprich, wenn *a=0*, dann darf kein weiteres Codewort mit *0* beginnen.

Code wörter können in einem binären Baum dargestellt werden und sind optimal,
wenn jeder Node genau zwei Kinder hat.

#### Huffman

- Liste sortiert nach Häufigkeiten
- Die kleinsten Häufigkeiten werden zuerst gewählt und wandern somit tiefer in den Baum runter.
- Die kleinsten zwei werden zu einem Knoten zusammen geführt.
- Die Summe ihrer Häufigkeiten ist die Häufigkeit ihres gemeinsamen Knotens
- Der Knoten wird in die Liste eingepflegt (ebenfalls sortiert nach Häufigkeit)
- Wiederholen des Verfahrens, bis sich ein einziger Knoten zu oberst befindet.

![image](img/huffman.png)

### Kürzeste Pfade

#### Graphen

Graphen bestehen aus einer Menge an Objekten und deren Beziehung zu einander.

- Objekte = Knoten
- Beziehungen = Kanten
- Knoten sind adjazent, wenn sie durch eine Kante verbunden sind

Es gibt:

- Gerichtete Graphen (Kante hat eine Richtung)
- Ungerichtete Graphen (Kante geht in beide Richtungen)

Graphen können auf zwei Arten implementiert sein:

- Adjazenzliste
  - Ein Array für jeden Knoten
  - Der Array speichert alle Knoten zu denen diese Knoten eine Verbindung hat
- Adjazentmatrix
  - Besteht aus einem zweidimensionalen Array (Matrix)
  - Anzahl Knoten x Anzahl Knoten
  - Wo ein Knoten eine Verbindung zum Anderen hat wird eine 1 gespeichert
  - Sonst wird eine 0 gespeichert
  - Bei ungerichteten Graphen ist die Matrix symmetisch (Diagonale ist Symmetrieachse)

![image](img/graph.png)

#### Dijkstra Algorithmus

Eine Reihe von Kanten die mehrere Knoten ohne Unterbruch miteinander verbinden
werden als "Pfad" bezeichnet.

- Jede Kante hat eine Distanz
- Alle Distanzen müssen grösser als 0 sein.

Der Dijkstra Algorithmus sucht den kürzesten Weg von einem Knoten zu einem anderen.
Von einem Knoten werden die Kosten und das vorherige Element gespeichert.
Dazu speichert er alle Knoten in einer Priority Queue. -> kleinste Kosten, höchste
Priorität.
Er kennt die Kosten der Knoten noch nicht, Darum speichern wir zu Beginn grosse
Kosten für alle Knoten.

- Läuft so lange, bis keine Knoten mehr in der Priority Queue sind.
- Start beim Anfangsknoten
- Kosten des Startknotens sind 0
- Der Startknoten ist also das erste Element in der Priority Queue und wird als Erstes herausgenommen.
- Für jeden Nachfolger vom Anfangsknoten wird evaluiert ob die Kosten des Nachfolgers kleiner sind als die vom Anfangsknoten plus die Kosten des Pfades zum Nachfolger.
- Wenn das nicht der Fall ist, werden die Kosten des Nachfolger mit den Kosten überschrieben, die wir aufgewendet haben um zu dem Knoten zu gelangen.
- Beim Nachfolger Knoten wird der Vorgänger entsprechend als Vorgänger gespeichert.
- Der Knoten mit den kleinsten Kosten hat nun also Priorität und wird als nächstes raus genommen
- Nun werden alle Nachfolger dieses Knotens evaluiert.
- Sind Ihre Kosten kleiner als der bisherige Pfad zum Knoten, wenn nein -> Kosten mit aktuellem Wert überschreiben
- Wiederholen, bis alle Knoten abgearbeitet.
- Am Schluss bei Zielobjekt starten und jeweils den Vorängern ans Ziel folgen um kürzesten Weg zu erhalten

![image](img/djikstra.png)

## Algorithmen auf Zeichenketten (6)

Oft müssen Zeichenketten auf Ähnlichkeit mit anderen Zeichenketten untersucht werden,
oder es soll ermittelt werden ob eine Zeichenkette in einer grösseren vorkommt.
Je grösser der String, desto schwieriger wird die Aufgabe.

- Ein Alphabet ist die Menge aller erlaubter Zeichen
- Ein Wort ist eine Folge von Zeichen
- Präfixe sind Zeichen am Anfang eines Wortes
- Suffixe sind Zeichen am Ende eines Wortes
- Teilwörter (substring) entstehen durch Entfernung Präfixen und/oder Suffixen
- Teilfolge entstehen aus durch Entfernung beliebiger Zeichen (Alle Teilfolgen sind auch Teilwörter, aber nicht umgekehrt)

### Editierdistanz von Zeichenketten

Wie ähnlich sind sich zwei Zeichenketten? Dafür gibt es etliche Möglichkeiten, zwei davon sind:

1. Was ist die maximale Teilfolge? Je länger die Folge, desto ähnlicher sie Strings
2. Zwei Strings sind sich ähnlich, wenn die Anzahl Änderungen, die notwendig sind um x in y zu verwandeln klein ist.

Die drei Typischen Editier-Operationen sind:

- Ersetzen eines Symboles
- Einfügen eines Symboles
- Löschen eines Symboles

Die **Einheitskosten** dieser Operationen sind jeweils 1. Das einzige das "gratis" ist,
ist, ein Zeichen durch sich selbst zu ersetzen, sprich, es nicht zu verändern.

**Schreibmaschinenkosten** berechnen die Kosten einer Ersetzung aus der Entfernung
zweier Zeichen auf einer Tastatur. Für Löschen und Einfügen werden konstante Kosten
verwendet. Diese Form wird bei Korrekturvorschlägen verwendet.

Die **Editierdistanz** ist die Folge von Editieroperationen x in y zu überführen,
mit minimalen Kosten. Auch "Levenstein-Distanz" genannt.

Editieroptionen sollten:

- grösser als null sein
- identische substitutionen kosten 0 (a durch a ersetzen)
- die gleiche Operation mit weniger Schritten, soll weniger oder gleich viel kosten
- Symmetrie: Kosten a durch b ersetzen sind gleich wie b durch a ersetzen.

### Berechnung Editierdistanz

Laufzeit O(nm) -> n = Länge String 1; m = Länge String 2

- Für die beiden Strings wird eine Matrix von 1+n Länge und 1+m Höhe erstellt.
- Position (0,0) wird mit 0 initialisiert
- Die erste Spalte wird mit den Kosten für das Löschen der Buchstaben gefüllt
  - 1x Löschen gleich Kosten: 1
  - Den ersten Buchstaben löschen: 1 Kosten
  - Den zweiten Buchstaben löschen: Kosten von 1 = 1 plus Kosten des löschens = 1; 1+1 = 2
  - Dritter: Kosten von 2 = 2, Kosten diesen Buchstaben löschen: 1; 2+1 = 3
  - Für alle Zeichen weitermachen
- Die erste Zeile wird mit den Kosten aller Einfügungen gefüllt
  - System analog zu Löschen
- Für alle Elemente der Matrix:
  - In das aktuelle Feld wird das Minimum folgender Möglichkeiten eingetragen:
    - Kosten Substitution: Wert von diagonal oben links stehendem Feld addieren mit Kosten der Substitution. (m[i] = n[j] = 0 | m[i] =/= m[j] = 1)
    - Kosten Löschen: Feld oben + Kosten Löschen
    - Kosten Einfügen: Feld links mit Kosten Einfügen addieren

Das letzte Feld der Matrix (rechts unten) hält nach diesem Algorithmus die Editierdistanz.

```java
private static final double DEL = 1, INS = 1, SUB = 3;
private static double[][] D;
private static String[][] P; // einfügen "-"; ersetzen "\"; löschen "|"

private static double computeSED(String x, String y) {
    int n = x.length();
    int m = y.length();
    D = new double[n+1][m+1];
    P = new String[n+1][m+1];
    D[0][0] = 0;
    P[0][0] = "*";
    for (int i = 1; i <= n; i++) {
       D[i][0] = D[i-1][0] + DEL;
        P[i][0] = "|";
    }
    for (int i = 1; i <= m; i++) {
        D[0][i] = D[0][i-1] + INS;
        P[0][i] = "-";
    }
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++){
            double m1 = D[i-1][j-1] + cost(x.charAt(i-1), y.charAt(j-1));
            double m2 = D[i-1][j] + DEL;
            double m3 = D[i][j-1] + INS;
            if (m1 <= m2 && m1 <= m3) {
                D[i][j] = m1;
                P[i][j] = "\\";
            } else {
                if (m1 < m3) {
                    D[i][j] = m2;
                    P[i][j] = "|";
                } else {
                    D[i][j] = m3;
                    P[i][j] = "-";
                }
            }
        }
    }
    return D[n][m];
}
private static double cost(char a, char b) {
    return a == b ? 0 : SUB;
}
```

### Längste gemeinsame Teilfolge

Wenn die Teilfolge *z* sowohl Teil von *x* als auch *y* ist gilt:

```0 ≤ |lcs(x,y)| ≤ min(|x|,|y|)```

Es könne folgende Ähnlichkeitsmasse bestimmt werden:

- L1: ```|lcs(x,y)| / min(|x|,|y|)```
  - 0 bedeutet kein gemeinsames Symbol
  - 1 bedeutet, dass x Teilfolge von y ist, oder umgekehrt
- L2: ```2 * lcs(x,y)| / (|x| + |y|)```
  - 0 bedeutet kein gemeinsames Symbol
  - 1 bedeutet x=y

### Suchen in Zeichenketten

String-Matching-Algorithmen finden Textsegmente in einer Zeichenkette.

Die einfachste is das naive String matching.

```java
// naive string matching
public static boolean search(String pattern, String T) {
    for (int i = 0; i < T.length() - pattern.length(); i++) {
        int j = 0;
        while (j < pattern.length() && pattern.charAt(j) == T.charAt(i+j)) {
            j++;
        }
        if (j == pattern.length()) {
            return true;
        }
    }
    return false;
}
```

### Boyer-Moore Algorithmus

Baut auf dem naiven algorithmus auf. Das Suchfenster wird aber nicht nur um eine
Position verschoben und er läuft von rechts nach links.

Sobald ein Mismatch auftaucht, wird ermittelt um wie viele Positionen das Suchfenster
nach links anhand von zwei Heuristiken verschoben werden soll.
Die beiden Heuristiken können unterschiedlich viel Schritte vorwärts machen wollen.
Der Algorithmus entscheidet sich für den höheren.

- Bad Character Heuristik
  - Das Suchwort der letzte Buchstabe des Suchwortes wird mit dem Buchstaben an gleicher Position im String verglichen
  - Wenn sie nicht übereinstimmen:
    - Der falsche Buchstabe wird zum Bad Character.
    - Das Suchwort wird nach vorne verschoben, so dass das erste aufkommen des Bad Characters im Wort an gleicher stelle ist wie der BAd character
    - Letzter Buchstabe wird wieder verglichen
    - Wenn der Bad Character im Wort nicht vorkommt, dann wird das Suchwort direkt nach dem Bad Character vorgerückt
  - Wenn sie übereinstimmen, dann zweit-, drittletzten, ... Buchstaben vergleichen
- Good-Suffix-Heuristik
  - Nicht prüfungsrelevant

### Rabin-Karp Algorithmus

Sucht mit Hash-Funktionen. Gleiche Strings = gleiche Hashwerte, aber gleiche Hashwerte
können von verschiedenen Strings stammen.

Lohnt sich nur, wenn Hashwerte schnell berechnen lassen.

### Weitere Algorithmen

- Knuth-Morris-Prat ähnlich wie Boyer-Moore
- Suffix-baum

## Suchen in Bäumen (7)
