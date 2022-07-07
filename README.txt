Angular 
=========

0) Prérequis:
-------------
Install Node.js (nodejs.org) et npm
Install Angular CLI (shell--> npm i -g @angular/cli)  (i --> install et -g --> global)
Vérif install : ng v 

1) Creation projet Angular avec le CLI
--------------------------------------
Creer dossier pour le projet puis aller dans ce dossier
Creer projet snapface
>ng new snapface --style=scss --skip-tests=true  (styles avec scss; pas de fichiers de tests)
Lancement server dév: >ng serve --> on peut voir le résultat dans un navigateur à l'url localhost:4200

2) Structure
------------
L'index.html contient balise <app-root>, c-à-d la racine de l'app; Angular va remplacer la balise par le 'component'
associé (ici AppComponent). En fait, c'est app.component.ts qui déclare que app-root intégrera app.component.html
Dans app.component.ts, on peut définir un attribut (dans class AppComponent p.ex. title avec title = 'snapface';)

3) Creer nouveau composant
--------------------------
CLI: > ng generate component face-snap 
Va générer un sous-dossier face-snap correspondant au composant FaceSnapComponent; app.module.ts est mis à jour en
déclarant le nouveau composant. Similairement à AppComponent, FaceSnapComponent contient un décorateur (@Component) décrivant le comportement.
Ici, une balise (le sélecteur) <app-face-snap></app-face-snap> dans app.component.html intégrera le face-snap.component.html
On peut p.ex. mettre plusieurs fois la balise, ce qui affichera plusieurs fois le contenu de face-snap.component.html

4) Afficher donnees
-------------------
Des attributs sont crees en mettant le nom et type dans la classe; par défaut VSCode marque l'attribut car non initialisé.
Pour garantir à TypeScript qu'on va initialiser, on peut ajouter 'un bang !'
initialiser dans ngOnInit
Dans le html, on peut faire de la 'string interpolation' avec doubles accolades (p.ex {{title}} )
Autre possibilité: 'attribute binding' utiliser plutôt syntaxe avec []
donc plutôt <img [src]="imageUrl" [alt]="title"> que <img src="{{ imageUrl }}" alt="{{ title }}">
On peut mettre un peu de style (dans fichiers .scss à différents niveaux)

5) Evenements
-------------
creer methode dans le ts pour répondre à un événement et lier la (event binding)

6) Propriétés personnalisées
----------------------------
creer repertoire models dans app puis un fichier .ts dedans => on cree une classe FaceSnap
On peut simplifier la classe (raccourci TypeScript) en mettant public/private dans le constructeur ce qui
permet de retirer déclarations/initialisations.
FaceSnapComponent utilise alors l'objet FaceSnap (avec un décorateur @Input) et ne gère plus que l'event
AppComponent utilise directement une ou plusieurs instances de FaceSnap

7) Structure dynamique
----------------------
Dans TypeScript (TS), on peut avoir des propriétés optionnelles dans la classe (avec un ?)
On peut enlever constructeur pour moins de lourdeur => lors instanciation, il faut une autre syntaxe (sans le new)
Dans le template (html), on met un élément conditionnel avec *ngIf

8) Listes
---------
Dans le template, parcours d'un ensemble avec *ngFor

9) Style dynamique
------------------
Les styles sont définis dans les fichiers .scss; il n'y a pas d'héritage. Un style dans un parent n'est pas vu par l'enfant.
Exception: le fichier de styles principal styles.scss
Dans le template, on peut avoir un style dynamique avec la directive [ngStyle]
On peut ajouter des classes avec [ngClass]

10) Pipes
---------
le caractère pipe | s'applique à un string p.ex. | titlecase pour mettre majuscules à 1ère lettre d'un mot
ou | date pour formater date. On peut préciser le format avec :  --> | date : 'dd/MM/yy'
Les dates apparaissent en anglais car la local par défaut est en-US; pour changer la locale, il faut changer dans
app.module.ts  (providers).
On peut appliquer un pipe de formatage pour les nombres.

11) Services
------------
Réorg de l'app (component face-snap-list) puis creer dossiers services (dans app) puis fichier face-snaps.service.ts dedans.
Un service est une classe que l'on va 'décorer' avec @Injectable(). Il n'y a pas de ngOnInit() dans un service.
Dans le service, on peut ajouter constructeur avec argument avec modificateur d'accès, ce qui crée la propriété.
Le modificateur doit être public ou plutôt private (pour empêcher accès direct)
Une méthode peut prendre (comme paramètre) un 'literal type' pour éviter de pouvoir utiliser n'importe quelle string
(en fait pas limité aux string)

12) Single Page Applications (SPA) et routing
---------------------------------------------
Dans le dossier app, creer fichier app-routing.module.ts et declarer classe pour routing (voir code). Cette classe
doit également être importée dans app.module.ts; de plus dans template d'AppComponent, changer <app-face-snap-list> par
<router-outlet>
Creation composant landing-page qui correspondra à la route 'vide'; utiliser routerLink pour aller sur une route enregistrée.
Ajouter menu de navigation dans HeaderComponent
Transformer lien sur landing page en bouton
Creer nouveau composant SingleFaceSnapComponent ainsi qu'une route d'un snap spécifique

13) Observables - RxJS
----------------------
Dans app.component.ts, utiliser la méthode interval (de rxjs) qui crée un Observable qui émet des nombres croissants.
On peut appliquer des opérateurs à un Observable (avec pipe). L'opérateur map transforme les émissions (p.ex.
multiplication par 10). Comme autres opérateurs 'bas-niveau', il y a filter, tap.
Il y a aussi des opérateurs 'haut-niveau': xxxMap (p.ex. switchMap). Un Observable haut-niveau est un observable
qui souscrit à d'autres Observables. L'Observable qui souscrit est appelé Observable extérieur et ceux qui sont souscrits
sont les Observables intérieurs.

14) Fuites de mémoires Observables
----------------------------------
voir code
On peut éviter fuites si p.ex. on sait combien d'émissions d'observable on veut avec take
==> 3 émissions : take(3)
On peut aussi détruire avec ngOnDestroy qui sera appelé à la destruction du composant.
Creer un Subject (un Observable que l'on peut faire émettre à la demande)

15) Formulaires
---------------
En Angular, il y a 2 méthodes pour creer formulaires: 'template' ou 'réactive'
Formulaire template: ajouter FormsModule aux imports de AppModule
Formulaire réactif: sont générés en TypeScript; ajouter ReactiveFormsModule (à AppModule). Creer nouveau composant new-face-snap.
Ajouter une route pour ce composant. Creer un bouton dans HeaderComponent pour creer ces nouveaux snaps. Le NewFaceSnapComponent
contiendra le formulaire FormGroup (et non pas NgForm - form template-). Injecter un FormBuilder pour simplifier la
génération de formulaires. Dans ngOnInit(), utiliser le FormBuilder avec la méthode group. Dans le template, lier formulaire
(formGroup) au snapForm.
Pour avoir aperçu du côté 'réactif', afficher en temps réel le FaceSnap => creer Observable

16) Validation
--------------
voir code

17) Requêtes serveur
--------------------
Clonez un backend (angular-intermediate-backend). Une fois cloné, dans le dossier du backend, faites  npm install  ,
puis  npm run start  . Vous devriez voir quelque chose comme : 'Loading db.json'; le backend de développement tourne
sur http://localhost:3000 !
Pour vérifier que le backend fonctionne, vous pouvez visiter http://localhost:3000/facesnaps –
vous devriez voir le JSON des FaceSnaps retournés par le backend.
Importer HttpClientModule depuis AppModule.
Injectez HttpClient dans FaceSnapsService en y créant un constructor, comme pour les components.
Dans FaceSnapListComponent, modifier pour utiliser un Observable qui émet le tableau de FaceSnap.
Modifier le service (getAllFaceSnaps) pour retourner non pas un tableau de FaceSnap mais un Observable<FaceSnap[]>
en utilisant le get de HttpClient.
Modifier SingleFaceSnapComponent en ajoutant un Observable de FaceSnap.

18) Requêtes composées
----------------------
Il faut modifier onSnap() dans SingleFaceSnapComponent.
Modif pour creer nouveaux FaceSnap. Modifier onSubmitForm() de NewFaceSnapComponent.


