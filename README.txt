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

4) 