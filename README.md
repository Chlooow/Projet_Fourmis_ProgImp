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

## Règles :
1. Si chercheSucre(f) et contientSucre(p2), alors f charge du sucre et pose une phéromone de sucre sur p1.
2. Si rentreNid(f) et contientNid(p2), alors f pose son sucre.
3. Si rentreNid(f) et vide(p2) et plusProcheNid(p2, p1), alors f se déplace sur p2 et pose une phéromone de sucre sur p2.
4. Si chercheSucre(f) et surUnePiste(p1) et vide(p2) et plusLoinNid(p2, p1) et surUnePiste(p2), alors f se déplace sur p2.
5. Si chercheSucre(f) et surUnePiste(p2) et vide(p2), alors f se déplace sur p2.
6. Si chercheSucre(f) et vide(p2), alors f se déplace sur p2.
