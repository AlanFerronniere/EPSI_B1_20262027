# Sélecteur par nom de balise

Un sélecteur par nom de balise cible tous les éléments d'un type spécifique dans un document HTML. Par exemple, pour sélectionner tous les éléments `<p>` (paragraphes), vous utiliseriez le sélecteur suivant :

```css
p {
		color: blue; /* Change la couleur du texte des paragraphes en bleu */
}
```
Ce sélecteur applique la règle CSS à tous les éléments `<p>` présents dans le document.

# Sélecteur par classe

Un sélecteur par classe cible tous les éléments qui ont une classe spécifique. Les classes sont définies dans le HTML avec l'attribut `class`. Pour sélectionner tous les éléments avec la classe `highlight`, vous utiliseriez le sélecteur suivant :

```css
.highlight {
		background-color: yellow; /* Change la couleur de fond des éléments avec la classe 'highlight' en jaune */
}
```
Ce sélecteur applique la règle CSS à tous les éléments qui ont l'attribut `class="highlight"`.

# Sélecteur par ID
Un sélecteur par ID cible un élément unique dans le document HTML, identifié par son attribut `id`. Les IDs doivent être uniques dans une page. Pour sélectionner un élément avec l'ID `header`, vous utiliseriez le sélecteur suivant :

```css
#header {
		font-size: 24px; /* Change la taille de la police de l'élément avec l'ID 'header' à 24 pixels */
}
```
Ce sélecteur applique la règle CSS uniquement à l'élément qui a l'attribut `id="header"`.

# Sélecteur universel
Le sélecteur universel cible tous les éléments dans le document HTML. Il est représenté par un astérisque (`*`). Pour appliquer une règle à tous les éléments, vous utiliseriez le sélecteur suivant :

```css
* {
		margin: 0; /* Supprime les marges par défaut de tous les éléments */
		padding: 0; /* Supprime les paddings par défaut de tous les éléments */
}
```
Ce sélecteur applique la règle CSS à tous les éléments du document.

# Sélecteur d'attribut
Un sélecteur d'attribut cible les éléments en fonction de la présence ou de la valeur d'un attribut spécifique. Par exemple, pour sélectionner tous les éléments `<a>` (liens) qui ont un attribut `href`, vous utiliseriez le sélecteur suivant :

```css
	a[href] {
		color: green; /* Change la couleur des liens avec un attribut href en vert */
}
```
Ce sélecteur applique la règle CSS à tous les éléments `<a>` qui possèdent un attribut `href`.

# Sélecteurs combinés

Les sélecteurs combinés permettent de cibler des éléments en fonction de leur relation avec d'autres éléments. Voici quelques exemples :
- Sélecteur descendant : cible les éléments qui sont des descendants d'un autre élément.

```css
div p {
		color: red; /* Change la couleur du texte des paragraphes à l'intérieur des div en rouge */
}
```
- Sélecteur enfant : cible les éléments qui sont des enfants directs d'un autre élément.

```css
ul > li {
		font-weight: bold; /* Met en gras les éléments li qui sont des enfants directs d'un ul */
}
```
- Sélecteur adjacent : cible un élément qui suit immédiatement un autre élément.

```css
h1 + p {
		margin-top: 0; /* Supprime la marge supérieure du paragraphe qui suit immédiatement un h1 */
}
```
- Sélecteur général de frères : cible tous les éléments qui suivent un autre élément au même niveau.

```css
h2 ~ p {
		color: gray; /* Change la couleur du texte de tous les paragraphes qui suivent un h2 en gris */
}
```
# Pseudo-classes et pseudo-éléments

Les pseudo-classes et pseudo-éléments permettent de cibler des états spécifiques d'un élément ou des parties spécifiques d'un élément.

- Pseudo-classe : cible un élément en fonction de son état.

```css
a:hover {
		color: orange; /* Change la couleur des liens au survol en orange */
}
```

- Pseudo-élément : cible une partie spécifique d'un élément.

```css
p::first-letter {
		font-size: 200%; /* Agrandit la première lettre des paragraphes */
}
```
Ces sélecteurs CSS sont essentiels pour appliquer des styles de manière précise et efficace dans vos documents HTML. En les combinant, vous pouvez créer des règles de style très spécifiques pour répondre à vos besoins de conception web.

## first-child, last-child, nth-child
Les pseudo-classes `:first-child`, `:last-child` et `:nth-child()` permettent de cibler des éléments en fonction de leur position parmi leurs frères et sœurs.
- `:first-child` : cible le premier enfant d'un parent.

```css
li:first-child {
		font-weight: bold; /* Met en gras le premier élément li dans une liste */
}
```
- `:last-child` : cible le dernier enfant d'un parent.

```css
li:last-child {
		font-style: italic; /* Met en italique le dernier élément li dans une liste */
}
```
- `:nth-child(n)` : cible le nième enfant d'un parent, où n peut être un nombre, une formule ou une expression.

```css
li:nth-child(2) {
		color: blue; /* Change la couleur du texte du deuxième élément li en bleu */
}
li:nth-child(odd) {
		background-color: lightgray; /* Change la couleur de fond des éléments li impairs en gris clair */
}
li:nth-child(even) {
		background-color: white; /* Change la couleur de fond des éléments li pairs en blanc */
}
li:nth
```


