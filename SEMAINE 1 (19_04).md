Projet Chloé et Chéïma:

# SEMAINE 1 (19/04)

# Ce qui a été fait:
***chloe :***
*  la mise en page du TP, et finis la partie 1
*  la classe EnsCoord
*  Le constructeur partie 2
*  L’operateur (Mais peut être faux à verifier) partie 2
*  Je ne peux pas continuer Voisines sans la methode d'ajout je crois

**26/04 :**
*  corps des méthodes du moins des idées je n'ai pas compilé
*  je pense qu'il manque un getter pour faire ces questions comme on a fait pour lig et col
*  je n'ai pas la syntaxe de getter pour un vector
*  je me suis arrêter a ieme(exclus)
*  pour la partie 4 je crois il me manque la méthode ajoute pour le faire (pas sur)

**28/04 :**
*  j'ai reglé position, contient et ses tests
*  j'ai modifié ajouté et tester ca marche mais il y a un truc louche (cf erreurs)
 
**05/05 :** 
* je me suis arreté a pose sucre j'ai commenté mes fonctions
* car je ne suis pas sur mais normalement ca devrait être ca

**08/05 :** 
* J'ai fait la mise en page de Place.cpp et Place.hpp (je n'ai pas modifié le makefile puisque qu'on est sur fourmis
* pour eviter trop des erreurs inutiles)
* je n'ai pas avancé sur fourmis, mais je compte faire demain et demander de l'aide

**12/05 :** 
* j'ai tout réglé cf fourmis.cpp et hpp j'essaye de faire des test mais ca ne marche pas du coup tu peux essayer aussi
* en tout cas on est bien on garde le rythme :) 

**14/05 :** 
* Fourmis fini
* Place : constructeur fait, test ok
* Proposition des attributs (voir juste en dessous)


**15/05 :** 
* Voisines finis
* fini place

**16/05 :** 
* grille presque finis il manque linearisation et les tests

### Attributs Place:
```
 private:
 
 Coord CoordP; //Coordonnee de la place
 int pheroS;   //intensite de pheromones de sucre
 int pheroN;   //intensite de pheromones de nid
 int numbF;    //numero de la fourmi se trouvant dessus -1 sinon
  ```

# STATUT :
Chloe :Tout compile bien (mais est-ce bon ? a vérifier) + 2 Warnings
les tests écrits passent tous
**25/04 :** ok
**26/04 :** Chloe - je n'ai pas compilé mais j'ai submit
**28/04 :**  chloe - j'ai compilé tout marche mais ieme ne fonctionne pas ./test : est partiellement ok.
**30/04 :** chloe - j'ai finis les tests présent, il manque juste le test de ieme j'essaye de faire voisines
**05/05 :** tout compile correctement
**08/05 :** tout compile bien 
**12/05 :** Erreur du aux test Porte, Prend, & poseSucre
**14/05 :** 
**15/05 :** ca compile
**16/05 | 17/05  :** ca compile

# Erreurs/warnings

Cheima : j'ai reglé le probleme des warnings.

Chloe : 
~~coord.cpp:61:TEST CASE:  Inegalité
coord.cpp:73: ERROR: CHECK( c != d ) is NOT correct!
  values: CHECK( (0, 0) != (1, 0))~~


~~CHECK(contient(d) == false);~~

probleme :
ens.pop_back();
SAUF QUE: on veut pas enlever le dernier élement on veut un element en particulier!!
solution : 
ens.pop_back() (car pop_back enleve le dernier element du tab)

~~probleme : 
il ajoute bien l'élément mais a l'affichage il n'apparait pas~~
          
### erreur ensCoord:
j'ai ça pour contient quand j'ai voulu faire des tests pour contient (voir mon coord.cpp)
```
error: 'class std::vector<Coord>' has no member named 'contient'

```
(reglé)

probleme : 
coord.cpp: In member function 'int EnsCoord::ieme(int)':
coord.cpp:226:17: error: cannot convert '__gnu_cxx::__alloc_traits<std::allocator<Coord>, Coord>::value_type' {aka 'Coord'} to'int' in return
  226 |     return ens[n];
      |                 ^
 ### NOUVEAU PROBLEME POUR CHEIMA:
~~(regarde mon cpp): j'essay de faire en sorte que mes tests passent et tout j'ai refait spprime et j'ai deux petites erreurs:
    JE T ENVOIE LE SCREEN DE MON TERMINAL SUR WHATSAPP~~
    
~~reponse : ~~
    ~~ton operateur ne marche pas , je te propose de regarder mon operateur~~ 
### Erreur
    
    no match for 'operator<<' operand types are 'std::ostream' {aka 'std'
std::cout << voisines(A); 
    
    
# Questions:

```
**Rand et srand =  #include <cstdlib>
> #include <ctime>**
```
 ça apparait où ça ??
 Chloe : C'est pour une des question je met ca la comme ca on oublit pas

 le "unsigned int" sert à quoi ?et le ens correspond à quoi ?
 **reponse :** ```unsigned int``` je t'avous je ne sais pas je me suis inspiré du code sur discord, tu peux essayer de mettre un int normal pour voir ?
 je vais tester
 
 ```ens``` si tu regarde bien dans le fichier Coord.hpp, c'est le nom du tableau dans EnsCoord
okkkk

```ens.push_back(e[i]);```

Chloe : faut-il un getter et setter (pas besoin de setter) pour ```vector<Coord> ens;``` ? 
reponse partielle : Oui
syntaxe : 
```
// getter 
    //Coord set.ens() const { return ens; }
    //const vector<Coord> get_ens() {return ens.size();}
    
    //setter
    //set<vector<Coord> > ens { return ens.size();}
  ```  

    
explique-moi poseFourmi    
   ```
    poseFourmi
void Place::poseFourmi(Fourmi f) { // ou veux-tu poser la fourmis ?
    if(get_numeroFourmi() != -1) {
        throw invalid_argument("il y a déja une fourmi a cette place");
    }
    set_numeroFourmi(f.get_nb());
}

```

     
    
  
### ERREUR TEST : 
    
    
    

### Question pour les methodes privées:

est-ce qu'il y a des choses qu'il faut ecrire ou faire en plus lorsque l'on utilise une methode privée plutot qu'une methode publique?
chloe : pas vraiment de réponse car on a regler le problème on ne peut tester position mais position est bien ecrite !
  
  
Tkt tous ce que j'ai enlevé je l'ai mis dans un truc word au cas ou ;) 
On a bientot finis fourmis il nous reste place et Grille et je pense qu'on sera deja bien Si on fait pas le main
C'est pas grave on pourra juste dire que si on l'avais fait on utiliserais tatatata, et tititi...etc.
    
    
### correction
    
### Proposition
    
si ce que ta fais s'avère être faux, je pense que c'est faux parce qu'après il te demande de poser une pheromone
donc si tu pose une pheromone, tu ne peux pas poser un sucre de 255 je ne sais pas si tu vois :(
    
    
```//setter
    int sucre; //attribut
    void set_sugar(int s) { sucre = s; }
   //getter
    int get_sugar() const { return sucre; }
    
bool Place::contientSucre(Coord p) {
    if ((get_sugar() == true) and (get_pheroS() == 255)) {
        return true;
    }else{
        return false;
    }
}
```
    
```//setter
    int nid; //attribut (deja présent)
   //getter
    int get_nid() { return nid; } 
    
bool Place::contientNid(Coord p) {
    if ((get_nid() == true) and (get_pheroS() == 255)) {
        return true;
    }else{
        return false;
    }
}
```    
    
```
    pose sucre
    
void Place::poseSucre(Coord p) {
    if(contientSucre(p) == true) {
        throw invalid_argument("il y a deja du sucre sur cette place");
    }else{
        set_sugar(1);
    }
}
```
```
    enleveSucre
void Place::enleveSucre(Coord p) {
    if(not contientSucre(p)) {
        throw invalid_argument("il n'y avait pas de sucre sur la place");
    }else{
        set_sugar(0);
    }
}
```

```
    poseNid
    void Place::poseNid(Coord p) {
    if(contientNid(p)) {
        cout << "on ne peux poser de nid" << endl;
    }else{
        set_nid(1);
    }
}
```

```
    posePheroNid
void posePheroNid(float p_Nid) {
    if (il y a deja des pheromones de cette intensité){
    throw invalid_argument("il y a deja des pheromones de cette intensité");
    }
    if(p_Nid > 0 and p_Nid <= 1){
           set_pheroN(p_Nid);
    }else{
        throw invalid_argument("les pheromones que vous voulez ajouter sont en dehors de la limite autorisé");                
    }
}
```
                                
```                               
 posePheroSucre
void posePheroSucre(int p_Sucre) {
    if (il y a deja des pheromones de cette intensité){
    throw invalid_argument("il y a deja des pheromones de cette intensité");
    }
    if(p_Sucre > 0 and p_Sucre <= 255){
           set_pheroS(p_Sucre);
    }else{
        throw invalid_argument("les pheromones que vous voulez ajouter sont en dehors de la limite autorisé");                
    }    
}
```
```  
    diminuePheroSucre
void posePheroSucre(){
    if(get_PheroS() < 0){
       throw invalid_argument("il n'y a pas de pheromones");
    }else{
    pheromones--;
    }
}
```  
    
```
    deplaceFourmi
void deplaceFourmi(int fourmi, Coord x, Coord y){
    
}  
```
    
estVide
```bool estVide(Place p) {
    if((p n'a pas de sucre) and (p n'a pas d'element de nid) and (p ne contient pas de fourmis) {
    return true;
    }else{
    return false;
    }
}
```
    
```
    estPlusProcheNid
bool estPlusProcheNid(Place a, Place b){
    
}
    
    etre plus proche d'un nid ca veux dire qu'il faut tester
    si la Place a des pheromones de nid plus élevé que ceux de la Place b. Si c'est plus élevé alors return true, sinon false
    
    ou
    
    compter le nombre de voisins qui contient un nid
    si le nombre de voisin contenant un nid de Place a est plus élevée que ceux de la place b, alors renvois true, false sinon
```
  PoseFourmi: 
```    
void Place::poseFourmi(Fourmi f) {
    if(get_numeroFourmi() != -1) {
        throw invalid_argument("il y a déja une fourmi a cette place");
    }
    set_numeroFourmi(f.get_nb());
}    
 ```  
En clair on sait que si le numero de fourmi de la place = -1 ça veut dire qu'il n'y en a pas donc j'ai juste fais en sorte que quand tu rajoute une fourmi on recupere son numero (f.get_nb())  et on le met dans numeroFourmi de la place voila voila   
    
a ok ! 
