class: center, middle

# Les IHM et le langage Java
### Henri GARRETA & Cyril PAIN-BARRE & Sébastien NEDJAR (MCF AMU) 
![IUT](logo.png)
---

# À propos
- Sébastien NEDJAR (@nedseb)

![nedseb au travail](chemestrycat.jpg)
---

# À propos
- Sébastien NEDJAR (@nedseb)
    + Maître de conférences au Département Info de l'IUT  d'Aix. Enseignant spécialiste des Bases de données et chercheur en OLAP Mining au LIF.

    + Membre fondateur du Fab Lab Provence et du Laboratoire d'Aixpérimentation et de Bidouille.
    
    + Co-animateur de l'ICSTUG #iutagile.

    + Co-Organisateur des rencontres Beyond Lab.
    
    + Et bien d'autres activités étranges (pour avoir plus de détails faire une psychanalyse d'un étudiant m'ayant subi).
---

class: center, middle

# Cours 1: Java et les objets
---

# Ressources
- [infodoc.iut.univ-aix.fr/~ihm/](http://infodoc.iut.univ-aix.fr/~ihm/) : sujets des TP, pointeurs utiles, polys et transparents, ...

- [www.oracle.com/technetwork/java](http://www.oracle.com/technetwork/java) : logiciels, et documentation, dont :
    + [JRE (Java Runtime Environment)](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) : machine virtuelle java (JVM) + bibliothèques, ce qu'il faut pour exécuter les programmes Java.

    + [JDK (Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) : compilateur et outils de développement en Java - contient le JRE.

    + [docs.oracle.com/javase/8/docs/api](http://docs.oracle.com/javase/8/docs/api/) :  la documentation en ligne des API de la plateforme Java SE.
- Des IDE modernes pour vous faciliter la tache et vous faire gagner du temps : [Eclipse](https://eclipse.org/downloads/), [Netbeans](https://netbeans.org/downloads/), [IntelliJ IDEA](https://www.jetbrains.com/idea/), ...

- [h.garreta.free.fr/](http://h.garreta.free.fr/) : diverses ressources, dont : "[Le langage Java](http://h.garreta.free.fr/polys/PolyJava.pdf)" (Poly très complet écrit par Henri Garreta).
---

# POO, esprit de la chose
- un programme est un ensemble d'objets

- un objet est déterminé par un état et un comportement 

- état : valeurs d'un ensemble de données membres, champs ou **variables d'instance**

- comportement : implémenté par un ensemble de fonctions membres ou **méthodes d'instance**

- une classe est la description d'**objets** de même type, les **instances de la classe**

- il y a aussi des données et des fonctions non attachées aux objets :
    + les données membres `static` ou **variables de classe**

    + les fonctions membres `static` ou **méthodes de classe**
---

# POO, esprit de la chose (suite)
- les objets interagissent en s'envoyant des messages

- un message a toujours un destinataire

- un message dit *quoi* faire, mais non *comment* : il incombe au destinataire du message de savoir les détails que prend chez lui l'exécution du message

- indice : si `p` et `q` représentent des points 
    ```java
    r = distance(p, q)
    ``` 
    s'écrit plutôt 
    ```java
    r = p.distance(q)
    ```
- l'ensemble des messages qu'un objet accepte constitue son interface

- l'interface est la partie publique de l'objet ; elle doit être *simple*, *robuste*, *documentée* et *stable*
---

# Structure générale d'un fichier source
Contrairement à C/C++, en Java, **il n'y a pas** : 
- de directives pour le préprocesseur (lignes commençant par #)
  
   notamment, il n'y a pas besoin de `#include`

- de fichiers de spécification (`.h`) et des fichiers d'implémentation (`.cpp`) séparés


- de variables globales

- de fonctions autonomes

- plusieurs classes publiques dans le même fichier
---

# Structure générale d'un fichier source
Fichier `Liste.java` : 
```java
package mesOutils.mesListes;

import java.outil.Vector;
import java.awt.*;


class Maillon {
    //declaration des membres (variables et fonctions) de la classe Maillon

}


public class Liste {
    //declaration des membres (variables et fonctions) de la classe Liste

}
```

 Le fichier source doit avoir le même nom que la classe publique qu'il contient. 
---

# Package
- Les *Packages* permettent un découpage de l'espace de nommage en plusieurs sous espace de noms (à la manière des `namespace` de C++).

- Comme en C++ ils permettent d'éviter les collisions de nom mais ils permettent aussi une gestion d'accès simpliste.

- Un package est un ensemble cohérent de classes pouvant être importées toutes ensembles comme individuellement.

- Les packages peuvent être structurés de manière hiérarchique (mais cela n'a aucun effet sur les droits d'accès)
---

# Package
- Une classe n'étant pas placée dans un package défini, est placée dans un package spécial, le package par défaut (son utilisation est une mauvaise pratique).

- le nom complet d'une classe (Fully Qualified Class Name ou FQCN) est constituée du nom du package auquel elle appartient suivi de son nom.

   Par exemple, la classe `Liste` située dans le package `mesOutils.mesListes` a pour nom complet : 
   ```java
   mesOutils.mesListes.Liste
   ```
 
- Pour une classe publique, la structure du package et le nom de la classe imposent le chemin du fichier source : 

    Par exemple, la classe `mesOutils.mesListes.Liste` doit se trouver dans le fichier :

    ```sh
    mesOutils/mesListes/Liste.java
    ```
---

# Package : convention
Il existe une convention de nommage pour les packages :

- ceux-ci doivent être écrits entièrement en minuscules

- les caractères autorisés sont alphanumériques (de a à z, de 0 à 9) et peuvent contenir des points (.)

- tout package doit commencer par un TLD : com, edu, gov, mil, net, org ou les deux lettres identifiant un pays (ISO Standard 3166, 1981) ; « fr » correspond à la France, etc.

- aucun mot clé Java ne doit être présent dans le nom, sauf s'il est suivi d'un underscore (" \_ "), comme ceci : 
```java
com.nedjar.package_
```

- pour éviter les collisions de nom avec des bibliothèques externes, la pratique est d'utiliser un nom de domaine que l'on possède comme préfixe de tous les packages d'une application.
---

# Package : exemple
Fichier `Liste.java` : 
```java
package mesOutils.mesListes;

import java.outil.Vector;
import java.awt.*;

class Maillon {
    ...
}

public class Liste {
    ...
}
```

- l'instruction `package` doit être la première du fichier.

- Une classe déclarée publique sera accessible depuis l'extérieur du package.

- Une classe déclarée dont la visibilité ne sera pas spécifiée sera accessible uniquement à l’intérieur du package.
---

# Importation de classes ou de packages
- Une classe Java n'a pas besoin d'inclure quoi que ce soit pour accéder à une autre classe située dans le chemin d'accès aux classes (le **class path**).

- Par exemple **à l’intérieur du package** `mesOutils.mesListes` la déclaration et l'instanciation d'un objet `Liste` se fera comme suit : 
```java
Liste L = new Liste();
```

- Par exemple **à l’extérieur du package** `mesOutils.mesListes` la déclaration et l'instanciation d'un objet `Liste` se fera comme suit : 
```java
mesOutils.mesListes.Liste L = new mesOutils.mesListes.Liste();
```
---

# Importation de classes ou de packages
- Pour simplifier l'utilisation de la classe depuis l’extérieur, on peut l'importer pour ne plus avoir à préfixer.

- l'importation se fait à l'aide du mot clef `import`.

- Dans l'exemple précédent, l'importation marcherait comme suit : 
   ```java
   import mesOutils.mesListes.Liste;

   Liste L = new Liste();
   ```

- Il est possible d'importer l'ensemble des classes d'un package avec un jocker (" \* ")
  
  Par exemple pour importer toutes les classes du package `mesOutils.mesListes` :
  ```java
  import mesOutils.mesListes.*;
  ``` 
---

# Importation de classes ou de packages
- L'importation n'est que du **sucre syntaxique** pour faciliter la vie du développeur. Elle n'a aucun impact sur le code compilé.

- Le compilateur importe les classes du package `java.lang` de manière automatique.

- La JVM charge la classe la première fois où elle est accédée dans le programme.

- Les mécanismes de construction du *class path* et de chargement des classes peuvent être extrêmement complexes et élaborés. Leurs descriptions dépassent le cadre de ce cours.

- Si une classe ne peut pas être trouvée par la JVM, une exception `ClassNotFoundException` sera levée.
---

# Compiler une classe
- Comme C++, Java est un langage compilé.

- Le compilateur Java produit un code intermédiaire appelé **bytecode**.

- Ce bytecode n'est pas directement exécutable par le processeur, il doit être **interprété** par la machine virtuelle Java (JVM).

- C'est grâce à ce procédé, qu'un programme Java peut s'exécuter sur toutes les plateformes sans avoir besoin d'être recompilé ("**write once, run anywhere**"). 
---

# Compiler une classe
L'application la plus simple en Java :
```java
// File : Main.java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

Compilation de cette classe :
```sh
$ javac Main.java
```
Le compilateur produit le fichier Main.class qui contient le bytecode.

---
# Compiler une classe
Affichage du bytecode :
```sh
$ javap -c Main.class
```
Bytecode :
```java
public class Main {
  public Main();
  Code:
    0: aload_0
    1: invokespecial #1 //Method java/lang/Object."<init>":()V
    4: return

  public static void main(java.lang.String[]);
  Code:
    0: getstatic     #2 //Field java/lang/System.out:Ljava/io/PrintStream;
    3: ldc           #3 //String Hello World!
    5: invokevirtual #4 //Method java/io/PrintStream.println:(Ljava/lang/String;)V
    8: return
}
```
---

# Exécuter une classe
- Pour qu'un classe soit **exécutable**, il faut qu'elle possède une **méthode statique** publique appelée `main` prenant un tableau de `String` en paramètre et ne retournant rien.
```java
public static void main(String[] args)
```

- Execution : 
```sh
$java Main
Hello World!
$
```

- Si la classe n'est pas exécutable, on obtient l'erreur suivante :
```sh
$java Liste
Erreur : la méthode principale est introuvable dans la classe Liste, 
définissez la méthode principale comme suit : 
   public static void main(String[] args)
$
```

---

# Java, le langage
Lors de la création du langage Java, il avait été décidé que ce langage devait répondre à cinq objectifs :

1. simple, orienté objet et familier ;
 
2. robuste et sûr ;
 
3. indépendant de la machine employée pour l'exécution ;
 
4. très performant ;
 
5. compilé, multi-tâches et dynamique.

La première caractéristique, fait référence à une méthode de programmation et de conception du langage et le fait qu'un programme écrit en Java ressemble assez fort à un programme écrit en C++.
---

# Java, le langage

- offre toutes les fonctionnalités d’un langage de programmation puissant: même concepts et caractéristiques que tout autre langage orienté objet en supprimant les "erreurs", difficultés majeures des langages plus anciens

- syntaxe familière (proche du C ou du C++)

- gestion automatique de la mémoire (garbage collector) : la libération de la mémoire n’est plus à la charge du programmeur

- nécessite tout de même une certaine expérience avant de tirer au mieux parti de ses possibilités et surtout de son API gigantesque.

- Sauf indication contraire, Java = C : même syntaxe, mêmes concepts de base (Une large partie de la norme ISO/IEC 9899 du langage C est reprise dans Java).

- Avec la surcharge des noms des fonctions, les exceptions, les classes, ..., comme en C++

---

# Java, le langage
- Les mots clef :   
   + Mots clés de déclaration des données ( boolean, float, int, ...)

   + Mots clés de boucle (continue, while, for, ...)

   + Mots clés conditionnels (if, else, switch, ...)

   + Mots clés d’exception (try, throw, catch, ...)

   + Mots clés de classes (class, extends, implements, ...)

   + Mots clés de modification et d’accès (private, public, ...)

   + Mots clés divers (true, false, null, super, this, ... )
---

#Java : différences principales avec le C++
Java ressemble à C++ ... dans sa syntaxe !  mais Java est un **langage robuste et sûr**.

Suppression de ce qui pouvait amener des erreurs graves :
- pas de structures (struct), d'unions (union);

- pas de synonymie de types (typedef);

- pas de préprocesseur (#);

- pas de variables, ni de fonctions en dehors de la classe;

- pas d'héritage multiple de classes;

- pas de surcharge d'opérateurs;

- pas de classes ou méthodes amies (friend);

- pas de pointeurs, seulement des références.
---

# Les types primitifs
- En Java tout est **objet** (les éléments du langage sont des classes) sauf les types primitifs :

| Nom    | Taille en octets | Valeur par défaut |
|:------ | ---------------: | -----------------:|
|boolean |            1 bit |             false |
|byte    |                1 |              0x00 |
|short   |                2 |            0x0000 |
|int     |                4 |                 0 |
|long    |                8 |                0l |
|char    |                2 |           'x0000' |
|float   |                4 |                0f |
|double  |                8 |               0.0 | 


- Tous les entiers sont "avec signe". 

- De plus, les types primitifs obéissent à la sémantique de l’**accès par valeur**.

  Exemple : `x == y` signifie  `x` et `y` ont **même valeur**.
---


# Les types objets
- Hormis les types primitifs, tous les autres types sont des **objets**

  - Tableaux ;

  - Chaîne de caractères (`String` est une classe avec privilèges) ;

  - Les énumérations ;

  - Toutes les autres classes ;

- Les objets obéissent à la sémantique de l'**accès par référence** ;

 Exemple : `x == y` signifie  `x` et `y` ont la **même adresse**.

- La valeur par défaut des types objets est `null`
---

# Notion de référence en Java
En Java, on dit qu'il n'y a plus de pointeur mais comme vous allez le voir, ils sont présents partout mais sont sécurisés 
pour ne pas tomber dans les problèmes liés à l'utilisation directe de la mémoire. 

- "référence" = "pointeur, géré discrètement par la JVM".

- déclaration d'une variable de type objet :
  Exemple (on suppose avoir défini une classe `Point`) :
  ```java
  Point p; //p contiendra une référence sur un objet du type Point
             //Pour l'instant, p contient null
  ```
- instanciation (création) d'un objet :
  ```java
  p = new Point(25, 50); //Maintenant p pointe sur un morceau de mémoire
                           //contenant (au moins) les coordonnées (25,50).
  ```
- on peut aussi associer déclaration et instanciation :
  ```java
  Point q = new Point(100, 200);
  ```
---

# Notion de référence en Java

- désignation des membres (sous réserve que `x` et `distance` soient membres de la classe `Point` et qu'on ait le droit de les mentionner) :
  ```java
  p.x
  p.distance(q)
  ```
  (en C++ cela s’écrirait `Point *p;` puis `p->x` et `p->distance(q)`)
- les références sont modifiables. Par la suite, on pourra écrire :
  ```java
  p = new Point(300, 0); //la précédente valeur de p est "oubliée"
  ```
- quand plus aucune référence ne pointe sur une zone mémoire, la JVM la libérera automatiquement. C'est le principe du ramasse miettes (garbage collector).

- La libération de la mémoire n'étant pas déterministe, on ne peut faire aucune supposition quant à l'occupation mémoire d'un programme Java à un instant *t*.
---

# Tableaux
- Déclaration :
  ```java
  UnType tab[];
  // ou 
  UnType[] tab;
  ```
- Création du tableau :
  ```java
  tab = new UnType[nbElements];
  ```
- Accès au ième élément :
  ```java
  tab[i]
  ```
- Nombre d’éléments du tableau :
  ```java
  tab.length
  ```

---
# Tableaux : exemple
```java
public class Echo {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```

```sh
$javac Echo.java
```

```sh
$java Echo poids 200+30 'au revoir'
poids
200+30
au revoir
$
```
---

# Tableaux : exemple (bis)
```java
public class Echo {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println(arg);
        }
    }
}
```

```sh
$javac Echo.java
```

```sh
$java Echo poids 200+30 'au revoir'
poids
200+30
au revoir
$
```
---

# Chaînes de caractères
Les objets de type `String` représentent des chaînes de caractères immuables
- Notation :
  ```java
  String s = "Bonjour";
  ```
- Concaténation :
  ```java
  s + " à tous !" => "Bonjour à tous !"
  ```

- Propriété remarquable : si seul exp1 est de type `String`
  ```java
  exp1 + exp2 <=> exp1 + conversionEnString(exp2)
  ```
  Exemple : 
  ```java
  int x = 42;
  System.out.println("x = " + x); // Affiche x = 42
  ```
---

# Chaînes de caractères
Comment ça marche ? Deux cas :
1. exp2 est d'un type primitif
  ```java
  exp1 + exp2 <=> exp1 + String.valueOf(exp2)
  ```
2. exp2 est un type objet
  ```java
  exp1 + exp2 <=> exp1 + exp2.toString()
  ```
  En Java, tous les objets ont une méthode `toString()`.
---

# Une classe simple
```java
public class Point {
    int x, y;
    void placer(int a, int b) {
        ...//test de la validité de a et b
        x = a;
        y = b;
    }
    double distance(Point q) {
        int dx = x - q.x;
        int dy = y - q.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
    public String toString() {
        return "(" + x + "," + y + ")";
    }
}
```
Exemple :
```java
Point p;
p = new Point();
p.placer(10, 20);
System.out.println("p : " + p); // Affiche p : (10, 20);
```
---

# Référence `this`

```java
public class Point {
    int x, y;
    void placer(int x, int y) {
        ...//test de la validité de x et y
        this.x = x;
        this.y = y;
    }
    double distance(Point q) {
        int dx = this.x - q.x;
        int dy = this.y - q.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
    public String toString() {
        return "(" + this.x + "," + this.y + ")";
    }
}
```
Exemple :
```java
Point p;
p = new Point();
p.placer(10, 20);
System.out.println("p : " + p); // Affiche p : (10, 20);
```
---

# Constructeurs

```java
public class Point {
    int x, y;
    Point(int x, int y) {
        ...//test de la validité de x et y
        this.x = x;
        this.y = y;
    }
    Point(int x) {
        ...//test de la validité de x et 0
        this.x = x;
        this.y = 0;
    }
    Point() {
        this.x = 0; 
        this.y = 0;
    }
    ... // Mêmes méthodes que précédemment  
}
```
Exemple :
```java
Point p = new Point(10, 20);
Point q = new Point(30);
Point r = new Point();
```
---

# Collaboration entre constructeurs

```java
public class Point {
    int x, y;
    Point(int x, int y) {
        ...//test de la validité de x et y
        this.x = x;
        this.y = y;
    }
    Point(int x) {
        this(x, 0);
    }
    Point() {
        this(0);
    }
    ... // Mêmes méthodes que précédemment  
}
```
Exemple :
```java
Point p = new Point(10, 20);
Point q = new Point(30);
Point r = new Point();
```
---

# Construction par défaut

- **Constructeur par défaut** : si le développeur n'a écrit aucun constructeur, alors le compilateur fournit un constructeur sans argument
qui consiste à initialiser tous les champs avec leur valeur par défaut.
- L'écriture d'un constructeur quelconque suspend ce mécanisme.

- Par exemple : 
  ```java
    public class Point {
        int x, y;
        public String toString() {
            return "(" + this.x + "," + this.y + ")";
        }
    }
  ```
  Un `Point` peut se construire avec le constructeur par défaut :
  ```java
  Point r = new Point();
  System.out.println("p : " + p); // Affiche p : (0, 0);
  ```
---

# Construction par défaut (bytecode)
- **Constructeur par défaut** : si le développeur n'a écrit aucun constructeur, alors le compilateur fournit un constructeur sans argument
qui consiste à initialiser tous les champs avec leur valeur par défaut.
- L'écriture d'un constructeur quelconque suspend ce mécanisme.

- Par exemple :
  ```java
	public class Point {
	  int x;
	  int y;

	  public Point();
	       0: aload_0
	       1: invokespecial #1 // Method java/lang/Object."<init>":()V
	       4: return

	  public java.lang.String toString();
	       0: new           #2 // class java/lang/StringBuilder
           ...
	      39: areturn
	}
  ```
---

# Construction par défaut (bis)

- **Constructeur par défaut** : si le développeur n'a écrit aucun constructeur, alors le compilateur fournit un constructeur sans argument
qui consiste à initialiser tous les champs avec leur valeur par défaut.
- L'écriture d'un constructeur quelconque suspend ce mécanisme.

- Par exemple : 
  ```java
    public class Point {
        int x, y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
        public String toString() {
            return "(" + this.x + "," + this.y + ")";
        }
    }
  ```
  Un `Point` peut se construire avec le constructeur par défaut :
  ```java
  Point r = new Point(0, 0); // Point r = new Point() n'est plus légal
  System.out.println("p : " + p); // Affiche p : (0, 0);
  ```
---

# Construction par défaut (bis bytecode)
- **Constructeur par défaut** : si le développeur n'a écrit aucun constructeur, alors le compilateur fournit un constructeur sans argument
qui consiste à initialiser tous les champs avec leur valeur par défaut.
- L'écriture d'un constructeur quelconque suspend ce mécanisme.

- Par exemple :
  ```java
    public class Point {
      int x;
      int y;
      Point(int, int);
           0: aload_0
           1: invokespecial #1 // Method java/lang/Object."<init>":()V
           4: aload_0
           5: iload_1
           6: putfield      #2 // Field x:I
           9: aload_0
          10: iload_2
          11: putfield      #3 // Field y:I
          14: return
      public java.lang.String toString();
         ...
    }
  ```
---

# Destruction des objets
- **Destruction des objets** : il n'y a rien à faire, la machine Java s'en occupe pour vous. Autrement dit : quand un objet n'est plus utile il suffit de l'« oublier »
  ```java
  Point p = new Point(x1, x1);
  ...
  p = new Point(x2, x2);
  ```
- Le Garbage Collector (ou nettoyeur de mémoire) est responsable de la destruction des objets inutiles. Il se déclenche en temps "presque masqué", lorsque la mémoire manque ou la machine virtuelle est oisive.

- Mécanisme du garbage collector :
  1. marquage des cellules occupées par des objets accessibles

  2. récupération des cellules non marquées : chaînage, parfois regroupement.

- **Attention** : on ne peut plus prévoir quand un objet sera détruit, pour les ressources il ne faut pas compter sur le destructeur leur libération.
---

# Visibilité
En Java, il y a 4 niveaux de visibilité :
 ```java

  public class UneClasse {
  // le membre est accessible dans...

      private int x;        // ...les méthodes de sa classe exclusivement

      int y;                // ...les méthodes de sa classe et celles des 
                            //              autres classes du même paquet

      protected int z;      // ...les méthodes de sa classe, des classes 
                            //        du même paquet et des sous-classes

      public int t;         // ...les méthodes de n'importe quelle classe

      ...
  }
  ```
---

# Visibilité (exemple)
Fichier `Point.java` :
```java
public class Point {
    private int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    // accesseurs (getters)
    public int getX() {
        return x;
    }
    public int getY() {
        return y;
    }

    // mutateurs (setters)
    public void setX(int x) {
        this.x = x;
    }
    public void setY(int y) {
        this.y = y;
    }
}
```

---

# Membres static et final (exemple)

Fichier `Truc.java` :
```java
public class Truc {

    int valeur;// Variable d'instance : chaque instance en a son 
               // propre exemplaire.

    final int rang;// Constante d'instance : chaque instance en a une 
                   // dont on ne peut pas modifier la valeur.

    static int nombreDeTrucs;// Variable de classe : il en existe un seul 
                             // exemplaire accessible par toutes les instances.

    static final int VAL_MAX = 10;// Constante de classe : un seul exemplaire, 
                                  // immuable (proche de #define VAL_MAX 100 en C)

    public Truc(int valeur) {
        this.valeur = valeur;
        rang = nombreDeTrucs;
        nombreDeTrucs++;
    }
}
```

---
# Java Style
Pourquoi avons nous besoin de convention de codage ? 

- 80% de la vie d'une application c'est de la maintenance

- le code ne sera pas maintenu par la même personne pour toute la durée de vie du code.

- les conventions de codage permettent d'améliorer la lisibilité du code et une compréhension plus rapide d'un nouveau code.

En Java, Sun a défini une convention de codage de base que toutes les applications Java suivent :

- [Convention Sun](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)

- [Traduction Française](ftp://ftp-developpez.com/cyberzoide/java/JavaStyle.pdf)

- [Google Java Style ](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html)
---

# Java Style : principes fondamentaux
En plus d'une bonne mise en forme, un programme doit respecter les 4 principes fondamentaux de l'ordre des artisans logiciels :

1. Runs all the tests

2. Contains no duplications

3. Expresses the intent of the programmers

4. Minimizes the number of classes and methods

(Par respect pour la sainte parole, je ne peux me risquer à traduire)
---

# Java Style : mesure de la qualité
.center[![](wtfbyminute.png)]
---

# Java Style : le nommage
> Any fool can write code that a computer can understand. Good programmers write code that humans can understand.

> Martin Fowler, 2008.


- Trouver un *bon identificateur* est une tache complexe. De manière générale, 
il doit être simple à lire, à comprendre et surtout non ambiguë. Les identificateurs courts, les abréviations et 
les sigles sont donc à proscrire.

- L’expressivité est vraiment fondamentale, il faut accepter parfois des identificateurs un peu long si c'est nécessaire.

- Utiliser des mots qui ont du sens

- Ne tronquez pas les mots et n'utilisez pas d'encodage.
---

# Java Style : le nommage

- Nommage des **variables** :
 Pour construire un identificateur en  camelCase, il suffit de mettre chaque première lettre d'un mot en majuscule et de coller les mots les uns aux autres. Petite subtilité, le premier mot ne prend pas de majuscule. 

- Nommage des **classe** :
 Les classes sont nommées selon la méthode camelCase mais commencent par une majuscule. 

- Nommage des **méthodes** : 
Les méthodes sont nommées selon la méthode camelCase et comportent généralement un verbe d'action.

- Nommage des **constantes** :
Les constantes c'est-à-dire les données membres qualifiées `static final` doivent être écrites en majuscules et les mots sont séparés par des "\_". 
---

# Java Style : exemple
```java
public final class Point {
    private final double x;
    private final double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double getX() {
        return x;
    }

    public double getY() {
        return y;
    }

    public double distanceTo(Point that) {
        double deltaX = this.x - that.x;
        double deltaY = this.y - that.y;
        return Math.sqrt(deltaX * deltaX + deltaY * deltaY);
    }

    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}
```
---

# Conclusion
- "Truth can only be found in one place: the code."
 
 Robert C. Martin

- "Codez toujours en pensant que celui qui maintiendra votre code est un psychopathe qui connaît votre adresse."

 Marting Golding

- "[A]nd then it occurred to me that a computer is a stupid machine with the ability to do incredibly smart things, while computer programmers are smart people with the ability to do incredibly stupid things. They are, in short, a perfect match."
 
 Bill Bryson
---
