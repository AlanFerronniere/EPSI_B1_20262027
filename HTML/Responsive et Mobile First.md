# Le Responsive Design et l'approche Mobile First

## 1. Qu'est-ce que le Responsive Web Design ?

Le **Responsive Web Design** (ou design réactif/adaptatif) est une méthode de conception web permettant à une page de s'adapter automatiquement à la taille de l'écran de l'utilisateur :
- Smartphone (petit écran tactile vertical)
- Tablette (écran moyen, orientation portrait ou paysage)
- Ordinateur portable ou fixe (grand écran horizontal)

L'objectif principal est d'offrir une expérience de lecture et de navigation optimale **sans jamais faire apparaître de barre de défilement horizontal** (scroll horizontal) et sans forcer l'utilisateur à zoomer.

---

## 2. La balise indispensable : le Viewport

Pour qu'un navigateur mobile comprenne qu'une page est responsive, il faut obligatoirement inclure la balise `<meta name="viewport">` dans la section `<head>` du document HTML.

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <!-- Balise viewport obligatoire pour le responsive -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon site responsive</title>
</head>
<body>
    ...
</body>
</html>
```

### Que fait cette balise ?
- `width=device-width` : indique au navigateur que la largeur de la page doit correspondre à la largeur réelle de l'écran de l'appareil (et non à une simulation d'écran d'ordinateur à 980px).
- `initial-scale=1.0` : définit le niveau de zoom initial à 100% lors du chargement de la page.

> **Règle :** Sans cette balise, vos Media Queries ne fonctionneront pas correctement sur les smartphones !

---

## 3. Le principe du "Mobile First"

### C'est quoi ?
L'approche **Mobile First** consiste à penser et coder le design d'abord pour les petits écrans (smartphones), puis à enrichir progressivement la mise en page pour les écrans plus grands (tablettes, ordinateurs).

### Pourquoi concevoir en Mobile First ?
1. **Usage réel :** Plus de 60% du trafic internet mondial se fait sur mobile.
2. **Simplicité du code :** Sur mobile, le flux naturel du HTML (les blocs `<div>`, `<section>`, `<article>` s'empilent verticalement) est déjà idéal. On écrit donc un CSS de base très léger et épuré.
3. **Performance :** Les appareils mobiles, souvent limités en bande passante ou puissance, ne chargent pas de code inutile ou surchargé.

### Mobile First vs Desktop First

| Approche | Philosophie | Media Queries utilisées |
| :--- | :--- | :--- |
| **Mobile First** *(Recommandé)* | On code d'abord pour mobile, on agrandit ensuite | `@media (min-width: ...)` |
| **Desktop First** *(Ancienne méthode)* | On code d'abord pour PC, on réduit ensuite | `@media (max-width: ...)` |

En Mobile First, on utilise **`min-width`** : *« applique cette règle dès que l'écran fait AU MOINS cette largeur »*.

---

## 4. Les Media Queries (`@media`)

Une **Media Query** permet d'appliquer des règles CSS spécifiques uniquement si certaines conditions d'affichage sont remplies (notamment la largeur de l'écran).

### Syntaxe générale en Mobile First

```css
/* 1. STYLES PAR DÉFAUT (Mobile First) */
/* Ces règles s'appliquent à tous les écrans, en commençant par les téléphones */
body {
    font-size: 16px;
}

/* 2. TABLETTE : à partir de 768px de large */
@media (min-width: 768px) {
    body {
        font-size: 18px;
    }
}

/* 3. ORDINATEUR : à partir de 1024px de large */
@media (min-width: 1024px) {
    body {
        font-size: 20px;
    }
}
```

### Les points de rupture (Breakpoints) courants

Les points de rupture sont les largeurs d'écran clés où la disposition change :
- `< 768px` : Smartphones (styles de base sans Media Query)
- `768px` : Tablettes (iPad, tablettes Android)
- `1024px` : Ordinateurs portables et petits écrans
- `1200px` ou `1440px` : Grands écrans d'ordinateur

---

## 5. Les règles d'or pour un design fluide

### 1. Rendre les images toujours fluides
Par défaut, une image conserve sa taille en pixels. Si une image fait 1200px de large, elle dépassera de l'écran d'un smartphone. Pour l'adapter automatiquement :

```css
img {
    max-width: 100%;
    height: auto;
    display: block;
}
```
- `max-width: 100%` : L'image ne dépassera jamais la largeur de son conteneur parent.
- `height: auto` : La hauteur s'adapte proportionnellement pour éviter toute déformation.

### 2. Éviter les largeurs fixes en pixels (`px`)
- À éviter : `width: 900px;` (débordera sur un smartphone de 390px).
- À privilégier : `width: 100%; max-width: 1100px; margin: 0 auto;` (s'adapte au mobile tout en restant contenu sur grand écran).

---

## 6. Petits exemples pratiques de base

### Exemple 1 : Changer la couleur d'un bloc selon la taille d'écran
Un exemple minimaliste pour comprendre comment réagit une Media Query `min-width`.

**HTML :**
```html
<div class="boite">Redimensionnez votre fenêtre !</div>
```

**CSS (Mobile First) :**
```css
/* Par défaut sur mobile : fond orange */
.boite {
    background-color: #f97316;
    color: white;
    padding: 20px;
    text-align: center;
    border-radius: 8px;
}

/* Dès 768px (tablette) : fond vert */
@media (min-width: 768px) {
    .boite {
        background-color: #10b981;
    }
}

/* Dès 1024px (ordinateur) : fond bleu */
@media (min-width: 1024px) {
    .boite {
        background-color: #3b82f6;
    }
}
```

---

### Exemple 2 : Passer de 1 colonne (mobile) à 2 colonnes (ordinateur)
Sur smartphone, on empile les sections les unes sous les autres. Sur grand écran, on les place côte à côte avec Flexbox.

**HTML :**
```html
<div class="layout">
    <main class="contenu">Contenu principal</main>
    <aside class="sidebar">Barre latérale</aside>
</div>
```

**CSS (Mobile First) :**
```css
/* Sur mobile : affichage vertical naturel */
.layout {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.contenu, .sidebar {
    background-color: #f1f5f9;
    padding: 20px;
    border-radius: 6px;
}

/* À partir de 768px : affichage en 2 colonnes */
@media (min-width: 768px) {
    .layout {
        flex-direction: row; /* Côte à côte */
    }

    .contenu {
        flex: 3; /* Prend 3/4 de la largeur */
    }

    .sidebar {
        flex: 1; /* Prend 1/4 de la largeur */
    }
}
```

---

### Exemple 3 : Grille de cartes adaptative
Afficher 1 carte par ligne sur smartphone, 2 sur tablette, et 3 sur ordinateur.

**HTML :**
```html
<div class="grille">
    <article class="carte">Carte 1</article>
    <article class="carte">Carte 2</article>
    <article class="carte">Carte 3</article>
</div>
```

**CSS (Mobile First) :**
```css
.grille {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

/* Mobile : 1 carte par ligne (pleine largeur) */
.carte {
    background: #ffffff;
    border: 1px solid #e2e8f0;
    padding: 20px;
    border-radius: 8px;
    flex: 1 1 100%; /* Occupe 100% de la largeur */
}

/* Tablette (>= 768px) : 2 cartes par ligne */
@media (min-width: 768px) {
    .carte {
        flex: 1 1 calc(50% - 20px);
    }
}

/* Ordinateur (>= 1024px) : 3 cartes par ligne */
@media (min-width: 1024px) {
    .carte {
        flex: 1 1 calc(33.333% - 20px);
    }
}
```

---

### Exemple 4 : Menu de navigation responsive
Un menu dont les liens sont empilés verticalement sur smartphone, puis alignés horizontalement sur grand écran.

**HTML :**
```html
<header class="navbar">
    <div class="logo">MonSite</div>
    <nav>
        <ul class="nav-links">
            <li><a href="#">Accueil</a></li>
            <li><a href="#">Articles</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
</header>
```

**CSS (Mobile First) :**
```css
/* Mobile : en-tête empilé */
.navbar {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    padding: 16px;
    background-color: #1e293b;
}

.logo {
    color: #ffffff;
    font-weight: bold;
    font-size: 1.25rem;
}

.nav-links {
    list-style: none;
    display: flex;
    flex-direction: column; /* Liens empilés */
    gap: 8px;
    text-align: center;
    padding: 0;
    margin: 0;
}

.nav-links a {
    color: #cbd5e1;
    text-decoration: none;
}

/* Ordinateur (>= 768px) : barre horizontale classique */
@media (min-width: 768px) {
    .navbar {
        flex-direction: row; /* Logo à gauche, liens à droite */
        justify-content: space-between;
    }

    .nav-links {
        flex-direction: row; /* Liens alignés horizontalement */
        gap: 20px;
    }
}
```

---

## 7. Comment tester son affichage responsive ?

Pour tester le comportement de votre page sans avoir besoin de 10 appareils différents :
1. Ouvrez votre page dans votre navigateur (Chrome, Firefox, Edge).
2. Ouvrez les **Outils de développement** (touche `F12` ou clic droit -> **Inspecter**).
3. Cliquez sur l'icône **Mode appareil** (raccourci `Ctrl + Shift + M` sous Windows ou `Cmd + Option + M` sous Mac).
4. Vous pouvez maintenant redimensionner librement la fenêtre en faisant glisser les bordures, ou sélectionner des modèles de téléphones et tablettes (iPhone SE, iPad Air, etc.) pour vérifier votre mise en page !
