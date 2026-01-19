TP1 - Représentation Graphique avec D3.js
InfoVis 2023 - Dr. Fadloun
Ce projet contient les exercices du TP1 sur la visualisation de données avec D3.js.
Structure du projet
tp1-d3js/
│
├── index.html          # Page d'accueil avec navigation
├── exercice1.html      # Exercice 1 - Formes et animations
├── exercice2.html      # Exercice 2 - Rotations et transitions
└── README.md           # Ce fichier
Installation
Aucune installation n'est nécessaire ! Les bibliothèques sont chargées via CDN :

D3.js v3
Bootstrap 5
jQuery 3.5.0 (pour l'exercice 2)

Utilisation

Ouvrir le projet : Ouvrez simplement index.html dans votre navigateur web
Navigation : Utilisez les boutons pour accéder aux différents exercices
Retour : Cliquez sur "Retour au menu" pour revenir à la page d'accueil

Description des exercices
Exercice 1 : Formes SVG et Animations
Concepts abordés :

Création de formes SVG (cercles, lignes, rectangles)
Variables visuelles (forme, couleur, position, taille)
Interactions utilisateur (mouseover, mouseout)
Transitions et animations D3.js
Utilisation des échelles de couleur

Fonctionnalités :

5 cercles interactifs avec différentes couleurs
Effet de grossissement au survol
Animation de pulsation continue
Changement de couleur de fond progressif
Rectangle et ligne avec interactions

Exercice 2 : Rotations et Transformations
Concepts abordés :

Transformations SVG (translate, rotate, scale)
Transitions multiples et simultanées
Contrôles interactifs (checkboxes, slider)
Rotation d'éléments avec angle variable
Gestion d'événements jQuery et D3.js

Fonctionnalités :

Trois types de transitions sélectionnables :

Déplacement : Translation des formes
Taille : Modification des dimensions
Couleur : Changement de couleurs


Slider de rotation (0-360°) pour le texte
Boutons "Exécuter" et "Réinitialiser"
Interactions au survol sur toutes les formes

Concepts D3.js utilisés
Méthodes principales

d3.select() : Sélectionne un élément du DOM
append() : Ajoute un nouvel élément
attr() : Définit les attributs d'un élément
style() : Définit le style CSS
transition() : Crée une animation
duration() : Définit la durée d'une transition
on() : Gère les événements (mouseover, mouseout, click)

Variables visuelles

Position : x, y, cx, cy
Taille : width, height, r (rayon)
Couleur : fill, stroke
Forme : circle, rect, line, text
Opacité : opacity
Orientation : transform rotate

Échelles de couleur
javascriptvar color = d3.scale.linear()
    .range(["steelblue", "brown"])
    .interpolate(d3.interpolateHcl)
    .domain([0, 200]);
Ressources supplémentaires

D3.js Documentation officielle
Dashing D3.js - SVG Shapes
Tutorialspoint D3.js Tutorial

Auteur
TP réalisé dans le cadre du cours InfoVis 2023 - Dr. Fadloun
Notes techniques

Version D3.js : v3 (utilisée dans le TP original)
Compatibilité : Tous navigateurs modernes
Responsive : Interface adaptée aux différentes tailles d'écran
Framework CSS : Bootstrap 5 pour le design

Améliorations apportées
 - Interface utilisateur moderne et attractive
 - Navigation fluide entre les exercices
 - Design responsive
 - Animations enrichies
 - Code commenté et structuré
 - Gestion d'erreurs (alerts pour l'exercice 2)
 - Console logs pour le debug
Dépannage
Les animations ne fonctionnent pas

Vérifiez que JavaScript est activé dans votre navigateur
Ouvrez la console développeur (F12) pour voir les erreurs éventuelles

Les bibliothèques ne se chargent pas

Vérifiez votre connexion Internet (les bibliothèques sont chargées via CDN)
Essayez de rafraîchir la page (Ctrl+F5)

Les interactions ne répondent pas

Assurez-vous que le fichier est ouvert dans un navigateur web
Ne pas ouvrir le fichier directement, utilisez un serveur local si nécessaire

Bon apprentissage avec D3.js ! 🎨📊