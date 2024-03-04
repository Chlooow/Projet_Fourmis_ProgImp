# Projet Fourmis ProgImp L1

On considère une grille de 20 lignes sur 20 colonnes. Chaque case de la grille peut être vide ou contenir une et une seule des trois choses suivantes : une fourmi, du sucre ou un élément de nid. Une case ne peut pas contenir simultanément deux fourmis, du sucre et une fourmi, ou un élément de nid et une fourmi. Les fourmis doivent donc contourner le sucre et le nid, et se contourner entre elles. Une fourmi peut ramasser du sucre si elle se trouve à côté d'une case contenant du sucre. De même, une fourmi peut déposer du sucre dans le nid si elle porte du sucre et se trouve à côté d'une case contenant un élément de nid.

Au début, les fourmis cherchent du sucre aléatoirement sur la grille. Une fois qu'une fourmi a trouvé du sucre, elle le ramène vers le nid en suivant des "phéromones de nid", qui indiquent le chemin de retour vers le nid. Pendant leur retour du tas de sucre vers le nid, les fourmis marquent leur chemin avec des "phéromones de sucre", qui permettront aux autres fourmis de trouver le sucre plus rapidement. Les phéromones sont des substances émises par la plupart des animaux et certains végétaux, agissant comme des messagers sur des individus de la même espèce. Extrêmement actives, elles agissent en quantités infinitésimales, ce qui leur permet d'être détectées ou transportées sur plusieurs kilomètres.

Pour simplifier, nous supposerons que les "phéromones de nid" sont présentes en permanence et installent un gradient dirigé vers le nid. Cela signifie que l'intensité des phéromones augmente au fur et à mesure que l'on se rapproche du nid. Ainsi, pour se rapprocher du nid, il suffit de se déplacer vers une case de plus forte intensité en phéromones. Les "phéromones de sucre", quant à elles, s'évaporent. Ainsi, les fourmis ne suivront pas un chemin de phéromones de sucre vers un tas de sucre qui a été complètement vidé.

## 1.1 Comportement des fourmis

Pour décrire le comportement des fourmis, nous utiliserons les prédicats (fonctions booléennes) énumérés ci-dessous :

- Prédicats sur une fourmi f :
  - chercheSucre(f) : f ne porte pas de sucre
  - rentreNid(f) : f porte du sucre

- Prédicats sur une place (une case) p :
  - contientSucre(p) : p contient du sucre
  - contientNid(p) : p contient un élément de nid
  - contientFourmi(p) : p contient une fourmi
  - vide(p) : p ne contient ni sucre, ni fourmi, ni élément de nid
  - surUnePiste(p) : l'intensité des phéromones de sucre sur p est non nulle

- Prédicats sur une place p1 et une place voisine p2 :
  - plusProcheNid(p1,p2) : l'intensité des phéromones de nid sur p1 est plus importante que celle sur p2
  - plusLoinNid(p1,p2) : l'intensité des phéromones de nid sur p1 est moins importante que celle sur p2

Pour une place donnée, plusieurs prédicats peuvent être vrais, par exemple : surUnePiste(p) et vide(p).

Le principe général du comportement des fourmis est le suivant : elles cherchent du sucre en bougeant aléatoirement. Quand elles trouvent de la phéromone de sucre, elles s'éloignent le plus vite possible du nid, tout en restant sur la piste tracée par la phéromone de sucre. Quand elles sont à côté du sucre, elles chargent une partie du sucre, puis se rapprochent le plus vite possible du nid tout en posant des phéromones de sucre sur les cases empruntées.

Plus formellement, le comportement d'une fourmi est dicté par les règles énoncées ci-dessous par ordre de priorité décroissante :

___________

# Projet Fourmi

## Les coordonnées

Fonctions utiles (voir TP):

- `Coord(int x, int y);`` qui construit la coordonnée (x,y)
- `EnsCoord voisins(Coord c);`` renvoie l’ensemble des coordonnées des cases voisines de c.

## Les fourmis

Méthode du type `Fourmi`:
- Constructeur `Fourmi(Coord c, int numero, ??? colonie)`
- `Coord coord() const;`  renvoie les coordonnées d’une fourmi
- `int numero() const`
- `bool porteSucre() const;`
- `void prendSucre()`
- `void poseSucre()`
- `???(int) colonie() const`
- `void deplace(Coord c)`
- estVivante, tue .... version avancée

## Les Places

Méthode du type `Place`:
— Constructeur `Place(Coord)`: crée une place dont les coordonnées sont fournies en paramètre, ne contenant
pas de fourmi, ni de sucre, ni d’élément de nid
— Accès :
`Coord Place::coord() const;` renvoie les coordonnées d’une place
`float Place::pheroSucre(??? Colonie) const` renvoie l’intensité en phéromone de sucre sur la place
`float Place::pheroNid() const` renvoie l’intensité en phéromone de nid sur la place
`int Place::numeroFourmi() const` renvoie le numéro de la fourmi sur la place, ou −1 si pas de fourmi
— Prédicats sur une place :
`bool Place::contientSucre() const` renvoie vrai si la place contient du sucre
`bool Place::contientNid() const` renvoie vrai si la place contient un élément de nid
`bool Place::estSurUnePiste() const` renvoie vrai si la place se trouve sur une piste vers du sucre (tracée par la présence de phéromones de sucre)

— Modifications sur une place :
`void Place::poseSucre(??? quantité)` pose du sucre sur la place
`void Place::enleveSucre()` enlève du sucre sur la place
`void Place::poseNid(??? Colonie)` un élément de nid sur la place
`void Place::poseFourmi(Fourmis)` pose la fourmi donnée en paramètre
`void Place::enleveFourmi()` enlève la fourmi dans la place
`void Place::posePheroNid(float qte)` pose sur la place une phéromone de nid d’intensité donnée
`void Place::posePheroSucre(??? float qte)` pose une phéromone de sucre d’intensité maximale sur la place
`void Place::diminuePheroSucre()` diminue (par évaporation) l’intensité en phéromone de sucre
sur la place
— Modification sur deux places :
`deplaceFourmi` déplace la fourmi donnée en 1er paramètre qui est sur la place donnée en 2e paramètre vers la place donnée en 3e paramètre

`void deplace(Fourmi &, Place p1&, Place p2&)`

```c++
bool Place::estVide() const {
    return p.numeroFourmi() == -1 and (not p.contientNid()) and (not p.contientSucre()); 
}
```


## La grille

Méthode du type `Grille`:
- Constructeur `Grille()`

— Constructeur : initialise une grille vide.
— Accès et modifications (getter et setter):
`Place Grille::chargePlace(Coord)` accède à une place à modifier de la grille, située aux coordonnées indiquées. Renvoie une Copie de la place
`void Grille::rangePlace(Place)` range la place dans la grille après l’avoir modifiée ; si on a rangé les coordonnées de la place dans celle-ci, le paramètre Coord est inutile.
— Méthodes avancées :
`Grille::linearisePheroNid` linéarise l’intensité en phéromones de nid des cases de la grille
(voir plus loin).
`Grille::diminuePheroSucre` diminue suite à l’évaporation les phéromones de sucre sur toute
les cases de la grille.

Placement d'un nid
```c++
Tableau de Coord : contient les coordonnées du nid:
Place le nid dans la grille

void placeNid(Grille &g, vector<Coord> v) {
   for (Coord c : v) {
      Place p = g.chargePlace(c);    // copie de la place
      p.poseNid();
      p.posePheroNid(1);
      g.rangePlace(p);               // range la copie dans la grille
   }
}
```

## Principe linérisation des phéromones de nid

```c++

stable <- Faux
tant que pas stable
    stable <- vrai
    pour toutes les coordonnées c de la grille
    
       p <- chargerPlace(c)
       si p.pheroNid() < 1 faire
           coordVois <- voisins(c)
           maxPhero <- 0
           pour v dans coordVois faire
               voisin <- chargerPlace(v)
               maxPhero <- max(maxPhero, voisin.pheroNid())
           finpour
           maxPhero <- maxPhero - 1. / TAILLE
           si maxPhero > p.pheroNid() faire
               p.posePheroNid(maxPhero)
               rangePlace(p)   // Ne pas oublier de mettre à jour la grille
               stable <- faux
           finsi
        finsi
    finpour
fintantque    
```

Q11 : ATTENTION
Dans la boucle
```
p <- chargerPlace(c)
modification de p
rangePlace(p) // Ne pas oublier de mettre à jour la grille
```

## Analyse Descendante

Programme principal
```c++

initialise la grille
initialise les emplacement (fourmis, nid, sucre)
dessine la grille

tant que pas fini
    mettreAJourEnsFourmis(lagrille, lesFourmis)
    Grille.dessine()
    Grille.diminuerPheroSucre()
fintantque

```

```c++
mettreAJourEnsFourmis(lagrille, lesFourmis)
/* déplace toutes les fourmis en appliquant les règles de leur comportement */
Debut
    pour toute les fourmis f:
        mettreAJourUneFourmi(f, lagrille)
Fin

bool ConditionPeutChargerSucre(Donnée Fourmi f, Donnée Place p1, p2) {
    retourner f.chercheSucre() and p2.contientSucre();
}
void ChargerSucre(Donnée-Résultat Fourmi f, Donnée-Résultat Place p1, p2) {
    f.chargerSucre()
    p1.PoserPheroSucre()
}

void mettreAJourUneFourmi(Fourmi f, Grille g) {
Debut
    cf <- f.coord()
    pf <- g.chargerPlace(cf)
    voiscoord <- voisin(cf)
    pour regle allant de 1 a 6 faire
        pour tout cv de voiscoord faire
            vois = g.chargerPlace(cv)
            si condition_n(regle, f, pf, vois)
               // on peut appliquer la règle regle à la fourmi f
               // et au cases pf et vois
               action_n(regle, f, pf, vois)
               g.rangePlace(pf)
               g.rangePlace(vois)
               return
            finsi
        finpour
    finpour
Fin
}
```

```c++
condition_n(r, f, p1, p2)
switch(r) {
   case 1: return condition1(r, f, p1, p2)
   case 2: return condition2(r, f, p1, p2)
   ...
}
```
# Structuration et compilation séparée

Relire le cours et les exemples.

- fichier .hpp contient les déclarations
```c++
#ifndef NOMFICHIER_HPP
#define NOMFICHIER_HPP

#include <...>
#include "..."


const int blabla = 4;
// pas de variable dans le .hpp

...

#endif
```

Fichier .cpp contient les définitions
```c++
#include <iostream...>

#include "fichier.hpp"

...
```

Rêgle:
1 - tout ce qu'on utilise (variable, constante, classe, enum...) doit être défini. Pour ceci, on inclus le fichier correspondant.
2 - Ce qui est utilisé doit être défini dans un .cpp une fois et une seule.

En particulier, chaque cpp ne doit être compilé qu'une fois => JAMAIS #include "fichier.cpp"

Makefile:

Compilation du fichier fich.o:
```
fich.o: fich.cpp f1.hpp f2.hpp # (tous les fichiers inclus)
        g++ -Wall -std=c++11 -c fich.cpp
```        
Creation (édition des liens) de l'executable exec 
```
exec: exec.o autre.o # (tous les fichiers qui contienent les définitions)
        g++ -Wall -std=c++11 -o exec exec.o autre.o

# rêgle pour le lancement d'exec
run: exec
        ./exec
```
Le fichier s'appelle `Makefile`
faire `make run`


# Questions

## Include classique

```c++
#include <iostream>    # cin cout, ostrean
#include <sstream>     # ostringstream
#include <iomanip>     # setw setprecision
#include <string>
#include <vector>
#include <array>
#include <stdexcept>   # exception
#include <cmath>       # sin, cos, sqrt, ...
#include <ctime>       # time
#include <cstdlib>     # rand srand
```

## Question 1 : écrire ma question ici

- La méthode `ajouter` de la classe EnsCoord ne lève pas d'exception si les coordonnées sont déjà présentes, est-ce que c'est voulu ?

  Oui ! 

- Pourquoi ne peut on pas ~~déclarer~~ définir l'opérateur << dans un header ? Mauvaise pratique d'utiliser le keyword `inline` ?

  On peut le faire.

- Rajouter des opérateurs et des fonctions pour tester le code de EnsCoord, pertinent ou non ?

  Oui ! Attention à ne pas briser l'encapsulation en révélant la structure interne (l'utilisateur ne doit pas savoir qu'il y a un vecteur dedans)...

- Les onliners dans les fichiers d'en-tête, bonne ou mauvaise pratique ?

  Bon si code très court.

- Comment se déroule la soutenance, il faut un document ?

     * 5 min de présenation de votre code
     * question de l'examinateur

- est-ce que c'est mieux de mettre les constructeur dans le hpp?

  * déclaration dans le hpp
  * définition si code court (une ou deux lignes)

- comment on saute un test case?
  
  voir la doc sur https://github.com/onqtam/doctest
  
  dans le fichier source
  ```
  TEST_CASE("name"*doctest::skip(true))
  ```
  
  lors de l´appel

Pour avoir la liste des testcases:
```
./tests -ltc
[doctest] listing all test case names
===============================================================================
Constructeur
Operateur <<
Constructeur
Operator==
Operateur <<
Constructor
Constructeur
Méthode ajoute
Méthode supprime
Méthode estVide
Méthode choixHasard
taille
Méthode ieme
Fonction voisines
===============================================================================
[doctest] unskipped test cases passing the current filters: 14
```
Lance les tests sans supprime:
```
./tests --test-case-exclude='Méthode supprime'
```
on peut aussi utiliser un motif:
```
./tests --test-case-exclude='*supprime'
```


## Règles :
1. Si chercheSucre(f) et contientSucre(p2), alors f charge du sucre et pose une phéromone de sucre sur p1.
2. Si rentreNid(f) et contientNid(p2), alors f pose son sucre.
3. Si rentreNid(f) et vide(p2) et plusProcheNid(p2, p1), alors f se déplace sur p2 et pose une phéromone de sucre sur p2.
4. Si chercheSucre(f) et surUnePiste(p1) et vide(p2) et plusLoinNid(p2, p1) et surUnePiste(p2), alors f se déplace sur p2.
5. Si chercheSucre(f) et surUnePiste(p2) et vide(p2), alors f se déplace sur p2.
6. Si chercheSucre(f) et vide(p2), alors f se déplace sur p2.
