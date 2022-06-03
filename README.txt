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
L'index.html contient balise <app-root>, c-à-d la racine de l'app; Angular va remplacer la balise par le 'component' associé 
(ici AppComponent). En fait, c'est app.component.ts qui déclare que app-root intégrera app.component.html
Dans app.component.ts, on peut définir un attribut (dans class AppComponent p.ex. title avec title = 'snapface';)

3) Creer nouveau composant
--------------------------
CLI: > ng generate component face-snap 
Va générer un sous-dossier face-snap correspondant au composant FaceSnapComponent; app.module.ts est mis à jour en déclarant 
le nouveau composant. Similairement à AppComponent, FaceSnapComponent contient un décorateur (@Component) décrivant le comportement.
Ici, une balise (le sélecteur) <app-face-snap></app-face-snap> dans app.component.html intégrera le face-snap.component.html
On peut p.ex. mettre plusieurs fois la balise, ce qui affichera plusieurs fois le contenu de face-snap.component.html

4) Afficher donnees
-------------------
Des attributs sont crees en mettant le nom et type dans la classe; par défaut VSCode marque l'attribut car non initialisé. Pour garantir à
TypeScript qu'on va initialiser, on peut ajouter 'un bang !'
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
On peut simplifier la classe (raccourci TypeScript) en mettant public dans le constructeur ce qui
permet de retirer déclarations/initialisations.
FaceSnapComponent utilise alors l'objet FaceSnap (avec un décorateur @Input) et ne gère plus que l'event
AppComponent utilise directement une ou plusieurs instances de FaceSnap

