---
title: grid-area
slug: Web/CSS/grid-area
---

{{CSSRef}}

La propriété **`grid-area`** est une propriété raccourcie pour {{cssxref("grid-row-start")}}, {{cssxref("grid-column-start")}}, {{cssxref("grid-row-end")}} et {{cssxref("grid-column-end")}} qui permet de définir la taille d'un objet de la grille et son emplacement via les bords de sa zone de grille.

{{InteractiveExample("CSS Demo: grid-area")}}

```css interactive-example-choice
grid-area: a;
```

```css interactive-example-choice
grid-area: b;
```

```css interactive-example-choice
grid-area: c;
```

```css interactive-example-choice
grid-area: 2 / 1 / 2 / 4;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="example-container">
    <div class="transition-all" id="example-element">Example</div>
  </div>
</section>
```

```css interactive-example
.example-container {
  border: 1px solid #c5c5c5;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: repeat(3, minmax(40px, auto));
  grid-template-areas:
    "a a a"
    "b c c"
    "b c c";
  grid-gap: 10px;
  width: 200px;
}

.example-container > div {
  background-color: rgba(0, 0, 255, 0.2);
  border: 3px solid blue;
}

#example-element {
  background-color: rgba(255, 0, 200, 0.2);
  border: 3px solid rebeccapurple;
}
```

Si quatre valeurs `<grid-line>` sont fournies, la première sera appliquée à `grid-row-start`, la deuxième à `grid-column-start`, la troisième à `grid-row-end` et la quatrième à `grid-column-end`.

Lorsqu'il n'y a pas de valeur pour `grid-column-end`, si `grid-column-start` est un identifiant de zone ({{cssxref("&lt;custom-ident&gt;")}}, `grid-column-end` sera défini avec cet identifiant, sinon il sera défini avec `auto`.

Lorsqu'il n'y a pas de valeur pour `grid-row-end`, si `grid-row-start` est un identifiant de zone, `grid-row-end` sera défini avec cet identifiant, sinon il sera défini avec `auto`.

Lorsqu'il n'y a pas de valeur pour `grid-column-start`, si `grid-row-start` est un identifiant de zone, les quatres propriétés seront définies avec cette valeur. Sinon, elles vaudront `auto`.

La propriété `grid-area` peut également prendre comme valeur un identifiant personnalisé ({{cssxref("&lt;custom-ident&gt;")}}) qui pourra être utilisé comme nom pour une zone de la grille placée grâce à la propriété {{cssxref("grid-template-areas")}}.

## Syntaxe

```css
/* Valeurs avec un mot-clé */
grid-area: auto;
grid-area: auto / auto;
grid-area: auto / auto / auto;
grid-area: auto / auto / auto / auto;

/* Valeurs de type <custom-ident> */
grid-area: une-zone-de-grille;
grid-area: une-zone-de-grille / une-autre-zone;

/* Forme : <integer> && <custom-ident>? */
grid-area: une-zone-de-grille 4;
grid-area: une-zone-de-grille 4 / 2 une-autre-zone;

/* Forme span && [ <integer> || <custom-ident> ] */
grid-area: span 3;
grid-area: span 3 / span une-zone-de-grille;
grid-area: 2 span / une-autre-zone span;

/* Valeurs globales */
grid-area: inherit;
grid-area: initial;
grid-area: unset;
```

### Valeurs

- `auto`
  - : Un mot-clé qui indique que la propriété ne contribue pas au placement de l'élément sur la grille. Cela indique un placement automatique, une taille de fragment (_span_) automatique ou une taille par défaut de `1`.
- `<custom-ident>`
  - : S'il existe une ligne nommée avec '\<custom-ident>-start', la première ligne correspondante contribue au placement de l'élément sur la grille.

    > [!NOTE]
    > Les noms des zones de grille sont générés implicitement. Ainsi, en utilisant `grid-area: foo;` cela sélectionnera le début de la grille nommée correspondante (sauf si une autre ligne `foo-start` a été explicitement déclarée).

    Sinon, la valeur est traitée comme si on avait utilisé `<custom-ident>` et la valeur `1`.

- `<integer> && <custom-ident>?`
  - : La n-ième ligne de la grille contribue au placement de l'élément sur la grille. Si un entier négatif est utilisé, le comptage sera fait depuis la fin de la grille explicite.

    Si un nom est fourni pour \<custom-ident>, seules les lignes ayant ce nom seront comptées. S'il n'y a pas suffisamment de lignes existant avec ce nom, toutes les lignes implicites seront comptées afin de trouver la position.

    Si la valeur entière utilisée est `0`, la règle est invalide.

- `span && [ <integer> || <custom-ident> ]`
  - : Un fragment de grille est utilisé pour le placement de l'élément sur la grille afin que le début de la ligne pour l'élément de la grille soit placé à n lignes du bord de fin.

    Si un nom fourni pour \<custom-ident>, seules les lignes ayant ce nom seront comptées. S'il n'y a pas suffisamment de lignes existantes avec ce nom, tout les lignes implicites du côté de la grille explicite et qui correspondent à la direction de la recherche seront comptées afin de placer ce fragment.

    Si l'entier n'est pas défini, la valeur par défaut qui sera utilisée sera `1`. Les entiers négatifs ou nuls sont invalides.

## Définition formelle

{{CSSInfo}}

## Syntaxe formelle

{{CSSSyntax}}

## Exemples

### CSS

```css
#grid {
  display: grid;
  height: 100px;
  grid-template: repeat(4, 1fr) / 50px 100px;
}

#item1 {
  background-color: lime;
  grid-area: 2 / 2 / auto / span 3;
}

#item2 {
  background-color: yellow;
}

#item3 {
  background-color: blue;
}
```

### HTML

```html
<div id="grid">
  <div id="item1"></div>
  <div id="item2"></div>
  <div id="item3"></div>
</div>
```

### Résultat

{{EmbedLiveSample("Exemples", "100%", "150px")}}

## Spécifications

{{Specifications}}

## Compatibilité des navigateurs

{{Compat}}

## Voir aussi

- {{cssxref("grid-row")}}
- {{cssxref("grid-row-start")}}
- {{cssxref("grid-row-end")}}
- {{cssxref("grid-column")}}
- {{cssxref("grid-column-start")}}
- {{cssxref("grid-column-end")}}
- [Guide : les zones des grilles CSS](/fr/docs/Web/CSS/CSS_grid_layout/Grid_template_areas)
- Tutoriel vidéo : [les zones des grilles CSS (en anglais)](https://gridbyexample.com/video/grid-template-areas/)
