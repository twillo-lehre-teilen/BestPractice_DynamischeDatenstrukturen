<!--
author:   Lennart Rosseburg für twillo

email:    support.twillo@tib.eu

comment:  Eine Selbstlerneinheit [...] Diese Seite ist lizenziert unter der [Lizenz CC-BY-SA (3.0)](https://creativecommons.org/licenses/by-sa/3.0/legalcode).

language: de

mode:     Textbook

version:  0.0.1

date:     19/05/2022

logo:     docs/thumbnail.JPG

icon:     docs/twillo_logo.svg

link:     https://cdn.jsdelivr.net/gh/TorroRosso46/Suchprobleme/custom.css

import:   
-->

# Dynamische Datenstrukturen

> # Lizenzhinweis
>
> Der Kurs *Dynamische Datenstrukturen*, von Lennart Rosseburg für twillo, ist lizenziert unter der [Lizenz CC-BY-SA (3.0)](https://creativecommons.org/licenses/by-sa/3.0/legalcode).
>
> #### Unter Nutzung von
>
> - Dem [Kapitel "Dynamische Datenstrukturen"](https://de.wikiversity.org/wiki/Kurs:Algorithmen_und_Datenstrukturen/Vorlesung/Dynamische_Datenstrukturen) aus dem [Kurs "Algorithmen und Datenstrukturen"](https://de.wikiversity.org/wiki/Kurs:Algorithmen_und_Datenstrukturen), von Wikiversity unter der Beteiligung folgender [Autor:innen](https://de.wikiversity.org/w/index.php?title=Kurs:Algorithmen_und_Datenstrukturen/Vorlesung/Dynamische_Datenstrukturen&action=history), unter der [Lizenz CC-BY-SA (3.0)](https://creativecommons.org/licenses/by-sa/3.0/legalcode).

<!-- style="background-color:transparent;" -->
> Diese Selbstlerneinheit konzentriert sich auf die Funktionsweise verschiedener Dynamischer Datenstrukturen und enthält interaktive Aufgaben um das Gelernte zu überprüfen und zu verinnerlichen.

<!--  style="background-color:#A6D492;" -->
> #### Ziel des Kurses:
>
> Am Ende dieser Selbstlerneinheit sollten Sie die vorgestellten Dynamischen Datenstrukturen kennen, unterscheiden und selbst anwenden können.

## Einleitung

Unter [dynamischen Datenstrukturen](https://de.wikipedia.org/wiki/Datenstruktur) verstehen wir Datenstrukturen bei denen man Elemente löschen und hinzufügen kann, eine interne Ordnung (z.B. Sortierung) vorliegt und diese Ordnung unter Änderungen aufrecht erhalten bleibt. Ein Beispiel sind Lineare Datenstrukturen und Sortierung. Bei einer **unsortierten** Liste sind Änderungen einfach, aber der Zugriff aufwändig. Bei einer **sortierten** Liste sind die Änderungen schwierig, aber dafür der Zugriff einfach. Für diesen Trade-of ist eine “intelligente Datenstruktur” gesucht, die Änderungen **und** Zugriffe einfach, sprich effizient, hält. Viele dynamische Datenstrukturen nutzen Bäume als Repräsentation.

## Grundlagen

Bevor wir die einzelnen dynamischen Datenstrukturen vorstellen, ein kurzer Abschnitt zu den benötigten Grundlagen.

### Bäume

In diesem Kapitel werden [Bäume](https://de.wikipedia.org/wiki/Baum_%28Graphentheorie%29) als kurzen Einschub behandelt. Ein Baumelement $e$ ist ein Tupel $e=(v,\lbrace e_{1},...,e_{n}\rbrace )$ mit $v$ vom Wert $e$ und $\lbrace e_{1},...,e_{n}\rbrace$ sind die Nachfolger, bzw. Kinder von $e$. Ein Baum $T$ ist ein Tupel $T=(r,\lbrace e_{1},...,e_{n}\rbrace )$ mit $r$ als Wurzelknoten (ein Baumelement) und $\lbrace e_{1},...,e_{n}\rbrace$ als Knoten (Baumelemente) des Baumes mit $r\in \lbrace e_{1},...,e_{n}\rbrace$ und für alle $e_{i}=(v_{i},K_{i})$ und $e_{j}=(v_{j},K_{j})\in \lbrace e_{1},...,e_{n}\rbrace$ gilt $K_{i}\bigcap K_{j}=\emptyset$

Man spricht von einem geordneten Baum, wenn die Reihenfolge der Kinder $\lbrace e_{1},..,e_{n}\rbrace$ eines jeden Elements $e=(v,\lbrace e_{1},...,e_{n}\rbrace )$ festgelegt ist (schreibe dann $(e_{1},...,e_{n})$ statt $\lbrace e_{1},...,e_{n}\rbrace )$.

---

<lia-keep><h4>Beispiel:<h4></lia-keep>

<div style="width:80%;margin:auto;">
<img src="docs/Beispiel_Graph_1.svg" style="float:right;"/>
<p>
$T=(v_{4},\lbrace v_{1},v_{2},v_{3},v_{4},v_{5}\rbrace )$

- $v_{1}=(1,\lbrace \rbrace )$
- $v_{2}=(2,\lbrace v_{1},v_{3}\rbrace )$
- $v_{3}=(3,\lbrace \rbrace )$
- $v_{4}=(4,\lbrace v_{2},v_{5}\rbrace )$
- $v_{5}=(5,\lbrace \rbrace )$
</p>
</div>

<div style="clear:both;width:80%;margin:auto;padding-top:10px;">
<img src="docs/Beispiel_Graph_2.svg" style="float:right;"/>
<p>
$T'=(v_{4},\lbrace v_{2},v_{5}\rbrace )$

- $v_{2}=(2,\lbrace v_{5}\rbrace )$
- $v_{4}=(4,\lbrace v_{2},v_{5}\rbrace )$
- $v_{5}=(5,\lbrace \rbrace )$
</p>
<p style="clear:both;">
$T'$ ist **kein** Baum, da $v_{4}$ und $v_{2}$ ein gemeinsames Kind haben.
</p>
</div>

<div style="clear:both;"></div>

---

<lia-keep><h4>Begriffe:<h4></lia-keep>

<center>
![BinärBaum Beschriftung](docs/BinärBaum_Beschriftung.svg)
</center>

Ein **Pfad** folgt über **Kanten** zu verbundenen **Knoten**, dabei existiert zu jedem Knoten genau ein Pfad von der **Wurzel**. Ein Baum ist immer *zusammenhängend* und *zyklenfrei*.

<br><br>

<center>
![BinärBaum Niveau](docs/BinärBaum_Niveau.svg)
</center>

Das **Niveau** der jeweiligen Ebene entspricht immer der jeweiligen **Länge des Pfades**. Die Höhe eines Baumes entspricht dem größten Niveau + 1.

---

<lia-keep><h4>Anwendungen:<h4></lia-keep>

Man benutzt Bäume beispielsweise zur Darstellung von Hierarchien, wie Taxonomien, oder für Entscheidungsbäume. Bäume werden oft genutzt um sortierte, dynamische oder lineare Datenstrukturen zu repräsentieren, da Einfüge- und Löschoperationen leicht so definiert werden können, dass die Sortierung beibehalten wird. Ein Baum kann auch als Datenindex genutzt werden und stellt so eine Alternative zu Listen und Arrays dar.

<center>
![Suchbaum](docs/Suchbaum.svg)
</center>

Hier wird beispielsweise nach der 5 gesucht und der Baum wird als *Suchbaum* genutzt.

Man kann auch einen Baum aus *Termen* bilden. Der Term $(3+4) * 5 + 2 * 3$ ergibt folgenden Baum:

<center>
![Termbaum](docs/Termbaum.svg)
</center>

---

<lia-keep><h4>Atomare Operationen auf Bäumen:<h4></lia-keep>

Zu den Operationen zählen **lesen** mit

- $root()$: Wurzelknoten eines Baums
- $get(e)$: Wert eines Baumelements $e$
- $children(e)$: Kinderknoten eines Elements $e$
- $parent(e)$: Elternknoten eines Elements $e$

und **schreiben** mit

- $set(e,v)$: Wert des Elements $e$ auf $v$ setzen
- $addChild(e,e’)$: Füge Element $e’$ als Kind von $e$ ein (falls geordneter Baum nutze $addChild(e,e’,i)$ für Index $i$)
- $del(e)$: Lösche Element $e$ (nur wenn $e$ keine Kinder hat)

---

<lia-keep><h4>Spezialfall: Binärer Baum als Datentyp:<h4></lia-keep>

``` Java

  class TreeNode<K extends Comparable<K>>{

    K key;
    TreeNode<K> left = null;
    TreeNode<K> right = null;

    public TreeNode(K e) {key = e; }
    public TreeNode<K> getLeft() {return left; }
    public TreeNode<K> getRight()  {return right; }
    public K getKey() {return key; }

    public void setLeft(TreeNode<K> n) {left = n;}
    public void setRight(TreeNode<K> n) {right = n;}

    ...

    }

```
<lia-keep><h5>Beispiel:</h5></lia-keep>

``` Java
  TreeNode<Character> root = new TreeNode<Character>(‘A‘);
  TreeNode<Character> node1 = new TreeNode<Character>(‘B‘);
  TreeNode<Character> node2 = new TreeNode<Character>(‘C‘);
  TreeNode<Character> node3 = new TreeNode<Character>(‘D‘);

  root.setLeft(node1);
  root.setRight(node2);
  node2.setLeft(node3);
```

<center>
![Beispiel_Graph_3](docs/Beispiel_Graph_3.svg)
</center>

---

#### Traversierung

## Bäume

### Binäre Suchbäume

### AVL-Bäume

### 2-3-4-Bäume

### Rot-Schwarz-Bäume

## Heaps

## Hashtabellen
