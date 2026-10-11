# Transitions et Animations CSS

## 1. Introduction

En CSS, il est possible de donner vie à une page web en animant les éléments. Cela améliore l'expérience utilisateur en fournissant des retours visuels (feedback) lors des interactions.

Il existe deux manières principales d'animer en CSS :
1. **Les Transitions** : Pour passer de manière fluide d'un état A à un état B lors d'une interaction (par exemple au survol de la souris avec `:hover`).
2. **Les Animations (`@keyframes`)** : Pour créer des mouvements autonomes, complexes ou qui se répètent en boucle (comme un spinner de chargement).

---

## 2. Les Transitions CSS

Une transition permet d'adoucir le passage d'une valeur CSS à une autre au lieu d'avoir un changement instantané et brutal.

### La syntaxe

On déclare la transition **sur l'état initial** de l'élément (pas sur le `:hover`).

```css
.bouton {
    background-color: #3b82f6; /* État initial */
    /* Propriété raccourcie : transition: [propriété] [durée] [effet]; */
    transition: background-color 0.3s ease;
}

.bouton:hover {
    background-color: #1d4ed8; /* Nouvel état au survol */
}
```

### Les 4 propriétés d'une transition

| Propriété | Description | Exemple |
| :--- | :--- | :--- |
| `transition-property` | La propriété CSS à animer (ou `all`) | `background-color`, `transform`, `all` |
| `transition-duration` | La durée de l'effet en secondes (`s`) ou millisecondes (`ms`) | `0.3s`, `300ms` |
| `transition-timing-function` | La courbe d'accélération | `ease` (défaut), `linear`, `ease-in-out` |
| `transition-delay` | Le délai avant de démarrer l'effet (optionnel) | `0.1s` |

> **Astuce pratique :** La plupart du temps, on utilise la syntaxe raccourcie :  
> `transition: all 0.3s ease;` (anime toutes les propriétés modifiées en 0.3 seconde).

---

## 3. Exemples de base : Transitions

### Exemple 1 : Bouton avec changement de couleur fluide

**HTML :**
```html
<button class="mon-bouton">Cliquez-moi</button>
```

**CSS :**
```css
.mon-bouton {
    background-color: #0ea5e9;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    /* Transition fluide sur la couleur de fond */
    transition: background-color 0.3s ease;
}

.mon-bouton:hover {
    background-color: #0284c7;
}
```

---

### Exemple 2 : Carte interactive (zoom et élévation au survol)
L'utilisation conjointe de `transform: translateY()` et d'une ombre `box-shadow` donne un effet de soulèvement très moderne.

**HTML :**
```html
<div class="carte">
    <h3>Article intéressant</h3>
    <p>Survolez cette carte pour voir l'effet de soulèvement.</p>
</div>
```

**CSS :**
```css
.carte {
    background-color: #ffffff;
    border: 1px solid #e2e8f0;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
    /* Transition sur la position et l'ombre */
    transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.carte:hover {
    transform: translateY(-6px); /* Remonte de 6 pixels */
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12); /* Ombre plus diffuse */
}
```

---

## 4. Les Animations CSS (`@keyframes`)

Les animations permettent d'animer des éléments sans attendre d'action de l'utilisateur (dès le chargement) et peuvent tourner en boucle à l'infini.

### Le principe en 2 étapes :

1. **Définir les étapes clés avec `@keyframes`** : On donne un nom à l'animation et on décrit ce qui change (de `from` à `to`, ou avec des pourcentages `0%`, `50%`, `100%`).
2. **Appliquer l'animation à l'élément** : On utilise la propriété `animation`.

```css
/* Étape 1 : Définir l'animation */
@keyframes apparition {
    from {
        opacity: 0; /* Totalement transparent au début */
    }
    to {
        opacity: 1; /* Complètement visible à la fin */
    }
}

/* Étape 2 : L'appliquer */
.titre {
    /* animation: [nom] [durée] [répétition]; */
    animation: apparition 1s ease-in;
}
```

### Les propriétés clés d'une animation

- `animation-name` : Le nom défini dans `@keyframes`.
- `animation-duration` : Temps pour réaliser un cycle (ex: `2s`).
- `animation-iteration-count` : Nombre de répétitions (ex: `1`, `3`, ou `infinite` pour une boucle perpétuelle).
- `animation-timing-function` : Accélération (`linear`, `ease`, etc.).

---

## 5. Exemples de base : Animations

### Exemple 3 : Un loader / spinner qui tourne à l'infini

**HTML :**
```html
<div class="spinner"></div>
```

**CSS :**
```css
/* 1. Définition de la rotation de 0 à 360 degrés */
@keyframes rotation {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

/* 2. Le cercle de chargement */
.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #e2e8f0;
    border-top: 4px solid #3b82f6; /* Couleur de la pointe */
    border-radius: 50%; /* Rend la boîte ronde */
    /* Tourne en 1 seconde, vitesse constante (linear), à l'infini */
    animation: rotation 1s linear infinite;
}
```

---

### Exemple 4 : Un badge qui palpite ("pulsing")

**HTML :**
```html
<span class="badge-live">EN DIRECT</span>
```

**CSS :**
```css
/* 1. Définition du battement avec des pourcentages */
@keyframes pulsation {
    0% {
        transform: scale(1);
        opacity: 1;
    }
    50% {
        transform: scale(1.1); /* S'agrandit légèrement */
        opacity: 0.7;          /* Devient un peu plus transparent */
    }
    100% {
        transform: scale(1);   /* Revient à la taille normale */
        opacity: 1;
    }
}

/* 2. Style du badge */
.badge-live {
    display: inline-block;
    background-color: #ef4444;
    color: white;
    font-weight: bold;
    padding: 6px 14px;
    border-radius: 20px;
    font-size: 0.8rem;
    /* Battement continu toutes les 1.5 secondes */
    animation: pulsation 1.5s ease-in-out infinite;
}
```

---

## 6. Bonnes pratiques simples

1. **Restez sobre :** Une animation doit servir l'expérience utilisateur (indiquer qu'un bouton est cliquable, qu'un contenu charge). Trop d'animations fatiguent le regard.
2. **Durées recommandées pour les interactions :**
   - Survol / clic : entre `0.2s` et `0.3s` (200ms à 300ms). Au-delà, l'interface semble lente et peu réactive.
3. **Performances :** Privilégiez toujours les propriétés `transform` (déplacement, rotation, taille) et `opacity`. Elles sont directement calculées par la carte graphique (GPU) et ne ralentissent pas le navigateur.
