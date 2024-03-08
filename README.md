# INTRODUCTION 

Ceci est un sujet ou l'on vas créer un petit jeu 2048 en JS. Nous allons utiliser la librairie p5.js pour le faire.

Ce tutoriel est divisé en plusieurs étapes qui représentent les différentes étapes de création du jeu. Il est conseillé de suivre les étapes dans l'ordre. Il manque volontairement des informations dans les étapes pour vous laisser chercher par vous même et pour vous laisser réfléchir par vous même.

# INSTALLATION

Vous n'avez pas besoin d'installer quoi que ce soit, vous n'avez qu'à aller sur [le site editor.p5.js](https://editor.p5js.org/).

# STEP 1: LES BASES

La librairie p5.js est basée sur le principe de fonction. Chaque fonction est appelée à un moment précis. Nous allons voir les principales fonctions de la librairie.

## La fonction setup()

La fonction setup() est appelée une seule fois au début du programme. Elle est utilisée pour initialiser les variables et les objets.

## La fonction draw()

La fonction draw() est appelée à chaque frame. Elle est utilisée pour mettre à jour l'affichage.

## La fonction keyPressed()

La fonction keyPressed() est appelée à chaque fois qu'une touche du clavier est appuyée. Elle est utilisée pour récupérer les entrées clavier.

## La fonction keyReleased()

La fonction keyReleased() est appelée à chaque fois qu'une touche du clavier est relâchée. Elle est utilisée pour récupérer les entrées clavier.

## La fonction mousePressed()

La fonction mousePressed() est appelée à chaque fois qu'un bouton de la souris est appuyé. Elle est utilisée pour récupérer les entrées souris.

## La fonction mouseReleased()

La fonction mouseReleased() est appelée à chaque fois qu'un bouton de la souris est relâché. Elle est utilisée pour récupérer les entrées souris.

## Et bien d'autres...

Il existe de nombreuses autres fonctions dans la librairie p5.js. Vous pouvez les retrouver sur le site officiel de la librairie : https://p5js.org/reference/

---

Posons les bases de notre jeu. Qu'est ce qu'un 2048 ? C'est un jeu ou il y a une grille de 4x4 cases. Chaque case contient un nombre et chaque nombre a une couleur. On peux donc créer les premières variables de notre jeu :

```js
const SIZE = 4; // La taille de la grille
const BLOCK_SIZE = 100; // La taille d'une case en pixel

// Les couleurs des cases en fonction de leur valeur, ce sont des tableaux de 3 valeurs (R, G, B) entre 0 et 255
const BLOCK_COLORS = {
    0: [255, 255, 255],
    2: [255, 0, 0],
    4: [0, 255, 0],
    8: [0, 0, 255],
    16: [255, 255, 0],
    32: [255, 0, 255],
    64: [0, 255, 255],
    128: [255, 255, 255],
    256: [255, 0, 0],
    512: [0, 255, 0],
    1024: [0, 0, 255],
    2048: [255, 255, 0],
}

// La grille du jeu
let blocks = [
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0]
];
```

# STEP 2: ON DESSINE

Avant de pouvoir dessiner, il nous faut créer un `Canvas`. Un `Canvas` est une zone sur laquelle on peut dessiner. Pour créer un `Canvas` il faut utiliser la fonction `createCanvas()` dans la fonction `setup()`.

```js
function setup() {
    createCanvas(SIZEX, SIZEY); // Il faut remplacer SIZEX et SIZEY par la taille du Canvas en pixel
}
```

Maintenant que nous avons les bases de notre jeu, nous allons pouvoir dessiner la grille. Pour cela nous allons utiliser la fonction draw().

```js
function draw() {
    // On dessine la grille
    // A vous de jouer
}
```

Pour cela vous allez avoir besoin de la fonction rect() qui permet de dessiner un rectangle. Cette fonction prend 4 paramètres : x, y, width, height. x et y sont les coordonnées du coin supérieur gauche du rectangle et width et height sont la largeur et la hauteur du rectangle.

```js
rect(0, 0, 100, 100); // Dessine un carré de 100x100 en (0, 0)
```
Mais aussi la fonction fill() qui permet de remplir le rectangle avec une couleur. Cette fonction prend 3 paramètres : r, g, b. r, g et b sont les valeurs de rouge, vert et bleu de la couleur.

```js
fill(255, 0, 0); // Rempli le rectangle avec la couleur rouge
```

A vous de compléter la fonction draw() pour dessiner la grille.
Vous pouvez vérifier que votre code fonctionne en modifiant la valeur d'une case de la grille. La couleur de la case correspondante doit changer.

# STEP 3: LES VALEURS DES BLOCKS

C'est bien beau d'avoir des cases mais il faut aussi pouvoir noter des valeurs dedans. Pour cela il faut utiliser la fonction de p5.js: `text()`. Cette fonction prend 3 paramètres : text, x, y. x et y sont les coordonnées du coin supérieur gauche du texte et text est le texte à afficher.
Il y a aussi la fonction `textSize()` qui permet de changer la taille du texte. Cette fonction prend 1 paramètre : size. size est la taille du texte en pixel.

```js
write_text(0, 0, "Hello World"); // Affiche "Hello World" en (0, 0)
```

A vous de compléter la fonction draw() pour afficher les valeurs des cases de la grille.
Vous devez normalement avoir la valeur des cases de la grille et la couleur correspondante. 

# STEP 4: FAUT TOUT FAIRE BOUGER

On rentre dans la grosse partie du projet. Faire bouger les cases.

Maintenant que nous avons les bases de notre jeu, nous allons pouvoir faire bouger les cases. Pour cela nous allons utiliser la fonction `keyPressed()`.

```js
function keyPressed() {
    // On fait bouger les cases
    // A vous de jouer
}
```

Pour cela vous allez avoir besoin de la variable `keyCode` qui contient le code de la touche du clavier qui a été appuyée. Vous pouvez trouver la liste des codes des touches du clavier sur le site officiel de la librairie : https://p5js.org/reference/#/p5/keyCode

```js
if (keyCode === LEFT_ARROW) {
    // La touche flèche gauche a été appuyée
}
```
Un conseil: faites une fonction `move_all` qui vas faire bouger toutes les cases dans une direction. Vous pourrez ensuite appeler cette fonction dans la fonction `keyPressed()`.

Il faut aussi créer une fonction `add_block` qui va ajouter une case de valeur 2 ou 4 dans une case vide de la grille. Cette fonction ne prend pas de paramètre.
Voici un code qui peux vous aider :

```js
let random_y = Math.floor(Math.random() * SIZE);
let random_x = Math.floor(Math.random() * SIZE);
let random_value = Math.random() < 0.5 ? 2 : 4;

while (blocks[random_y][random_x] !== 0) {
    random_y = Math.floor(Math.random() * SIZE);
    random_x = Math.floor(Math.random() * SIZE);
}
```

# STEP 5: LES FUSIONS

Maintenant que les cases bougent, il faut qu'elles fusionnent. Je vais rien dire et vous laisse faire. Bon courage.

# STEP 6: LE JEU EST FINI

Maintenant que le jeu est fini, a vous de jouer. Vous pouvez ajouter des fonctionnalités comme un menu, un score, un meilleur score, un bouton pour recommencer, etc...
