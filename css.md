Melhor Envio CSS Style Guide
============================

*Diretrizes de organização e escrita de CSS*


## Índice

- [Pré-processador](#pré-processador)
- [Estrutura de pastas](#estrutura-de-pastas)
- [Indentação](#indentação)
- [Sintaxe](#sintaxe)
- [Naming convention](#naming-convention)
	+ [Classes](#classes)
	+ [Variáveis](#variáveis)
- [Regras gerais](#regras-gerais)
	+ [Ordem de importação](#ordem-de-importação)
	+ [Espaçamento](#espaçamento)
	+ [Nesting](#nesting)
	+ [Múltiplos seletores](#múltiplos-seletores)
	+ [Alinhamentos](#alinhamentos)
	+ [@extend primeiro, estilos "regulares" depois](#extend-primeiro-estilos-regulares-depois)
	+ [Pseudo-classes e pseudo-elementos depois](#pseudo-classes-e-pseudo-elementos-depois)
	+ [Modifiers e elements depois](#modifiers-e-elements-depois)
	+ [Nested selectors por último](#nested-selectors-por-último)
	+ [Unidades](#unidades)
	+ [Zero à esquerda](#zero-à-esquerda)
	+ [Separadores de valores](#separadores-de-valores)
	+ [Cores](#cores)
	+ [Border](#border)
	+ [Z-index](#z-index)
	+ [Media queries](#media-queries)
	+ [Vendor prefixes](#vendor-prefixes)
	+ [DRY](#dry)
- [Licença](#licença)


## Pré-processador

O pré-processador utilizado é o [Stylus](https://stylus-lang.com/), escolhido pela sua flexibilidade, rapidez e facilidade.


## Estrutura de pastas

```
css/
├── components/
│   └── *.styl
├── core/
│   ├── config.styl
│   ├── general.styl
│   ├── layout.styl
│   └── mixins.styl
└── style.styl
```


## Indentação

O caracter padrão de indentação utilizado é **tab**, e espaços não devem ser utilizados nem mesmo para alinhamentos.

**Errado**

```styl
.foo
••display block
••margin 0 auto
```

**Errado**

```styl
.foo
••••display block
••••margin 0 auto
```

**Certo**

```styl
.foo
────display block
────margin 0 auto
```


## Sintaxe

O padrão de sintaxe adotado não utiliza *curly braces* `{}`, *colons* `:` e *semicolons* `;`.

**Errado**

```styl
.foo {
	display: block;
	margin: 0 auto;
}
```

**Certo**

```styl
.foo
	display block
	margin 0 auto
```


## Naming convention

### Classes

O padrão de nomeação utilizado é uma combinação de [BEM](http://getbem.com/naming/) com [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/), com nomes sempre em inglês.

Ressaltando que elementos só devem ser estilizados diretamente em casos de extrema necessidade.

**Errado**

```styl
body
	overflow-x hidden

header
	display block
	margin 0 auto

header a
	color $theme-primary

header a.blue
	color $theme-primary-light
```

**Certo**

```styl
body
	overflow-x hidden

.main-header
	display block
	margin 0 auto

	&__link
		color $theme-primary

		&--active
			color $theme-primary-light
```


### Variáveis

Variáveis devem ser nomeadas seguindo o [*kebab-case*](https://en.wiktionary.org/wiki/kebab_case), prefixadas com `$`.

**Errado**

```styl
SizeHuge = 80px
spaceWide = 40px
Theme-Primary = #0550a0
```

**Certo**

```styl
$size-huge = 80px
$space-wide = 40px
$theme-primary = #0550a0
```


## Regras gerais

### Ordem de importação

Vendors primeiro, core depois, componentes depois, partials por último.

**Certo**

```styl
// Vendors
@import 'mantis-toolkit'
@import 'mantis-equalizr'
...

// Core
@import 'core/mixins'
@import 'core/config'
...

// Components
@import 'components/colors'
@import 'components/spacing'
...

// Partials
@import 'partials/home'
@import 'partials/contact'
...
```


### Espaçamento

Deve se manter uma linha (apenas) de espaçamento após um conjunto de variáveis ou regras.

**Errado**

```styl

// Component variables

$foo-top = 10px
$bar-padding = 20px
$baz-margin = 0
// Component foo
.foo
	position absolute
	top $foo-top
	&__bar
		padding $bar-padding
// Component baz
.baz
	margin $baz-margin
```

**Errado**

```styl
// Component variables

$foo-top = 10px

$bar-padding = 20px

$baz-margin = 0


// Component foo

.foo
	position absolute
	top $foo-top


	&__bar
		padding $bar-padding


// Component baz

.baz
	margin $baz-margin
```

**Certo**

```styl
// Component variables
$foo-top = 10px
$bar-padding = 20px
$baz-margin = 0

// Component foo
.foo
	position absolute
	top $foo-top

	&__bar
		padding $bar-padding

// Component baz
.baz
	margin $baz-margin
```


### Nesting

**Errado**

```styl
.foo
	display block

.foo__bar
	display block

	.icon
		margin 0

.foo__bar--baz
	display none
```

**Certo**

```styl
.foo
	display block

	&__bar
		display block

		&--baz
			display none

		.icon
			margin 0
```


### Múltiplos seletores

Cada seletor deve ter sua própria linha, sem necessidade de `,` como separador, para facilitar a legibilidade e debugging.

**Errado**

```styl
.foo, .bar, .baz
	display block
```

**Certo**

```styl
.foo
.bar
.baz
	display block
```


### Alinhamentos

Não usar alinhamentos, de nenhum tipo.

**Errado**

```styl
$size-huge     = 80px
$space-wide    = 40px
$theme-primary = #0550a0

.foo
	position absolute
	top    0
	bottom 0
	right  0
	left   0
```

**Certo**

```styl
$size-huge = 80px
$space-wide = 40px
$theme-primary = #0550a0

.foo
	position absolute
	top 0
	bottom 0
	right 0
	left 0
```


### `@extend` primeiro, estilos "regulares" depois

**Errado**

```styl
.foo
	display block
	@extend .bar
```

**Certo**

```styl
.foo
	@extend .bar
	display block
```


### Pseudo-classes e pseudo-elementos depois

**Errado**

```styl
.foo
	display block

	&:after
		content 'Melhor Envio'

	&:hover
		color $theme-primary
```

**Certo**

```styl
.foo
	&:hover
		color $theme-primary

	&:after
		content 'Melhor Envio'
```


### Modifiers e elements depois

**Errado**

```styl
.block
	&__element
		color $theme-primary

	&--modifier
		display none
```

**Certo**

```styl
.block
	&--modifier
		display none

	&__element
		color $theme-primary
```


### Nested selectors por último

**Errado**

```styl
.block
	.icon
		margin 0

	&__element
		color $theme-primary
```

**Certo**

```styl
.block
	&__element
		color $theme-primary

	.icon
		margin 0
```


### Unidades

Sempre especifique a unidade, a menos que o valor seja `0`.

**Errado**

```styl
.foo
	margin 0%
	line-height 2
```

**Certo**

```styl
.foo
	margin 0
	line-height 2em
```


### Zero à esquerda

Sempre omita os zeros à esquerda.

**Errado**

```styl
.foo
	transform scale(0.5)
	transition-timing-function cubic-bezier(0.5, 4, 0.2, 0.5)
```

**Certo**

```styl
.foo
	transform scale(.5)
	transition-timing-function cubic-bezier(.5, 4, .2, .5)
```


### Separadores de valores

Separadores devem conter 1 espaço somente após a `,`.

**Errado**

```styl
.block
	background rgba( 0 , 0 , 0 , .5 )
	transition-property color , background-color
```

**Certo**

```styl
.block
	background rgba(0, 0, 0, .5)
	transition-property color, background-color
```


### Cores

Use variáveis ao invés de especificar diretamente o hexadecimal.

**Errado**

```styl
.foo
	color #0550a0
```

**Certo**

```styl
.foo
	color $theme-primary
```


### Border

Use `0` ao invés de `none`.

**Errado**

```styl
.foo
	border none
```

**Certo**

```styl
.foo
	border 0
```


### Z-index

Use o [Mantis Layers](https://github.com/acauamontiel/mantis-layers) ao invés de números explícitos, para facilitar o gerenciamento das camadas da aplicação, evitando "números mágicos".

**Errado**

```styl
.foo
	z-index 1

.bar
	z-index 999

	&__baz
		z-index 123
```

**Certo**

```styl
.foo
	z-index foo

.bar
	z-index bar

	&__baz
		z-index bar baz
```


### Media queries

Use o [Mantis Querist](https://github.com/acauamontiel/mantis-querist) ao invés de media queries explicitas, para facilitar o gerenciamento e padronização dos breakpoints.

**Errado**

```styl
.foo
	@media screen and (min-width: 1024px)
		display block
```

**Certo**

```styl
.foo
	@media $from.lg
		display block
```


### Vendor prefixes

Vendor prefixes são adicionados automaticamente pelo plugin [Autoprefixer](https://autoprefixer.github.io/).

**Errado**

```styl
.foo
	-webkit-user-select none
	-moz-user-select none
	-ms-user-select none
	user-select none
```

**Certo**

```styl
.foo
	user-select none
```


### DRY

Não repita códigos desnecessáriamente.

**Errado**

```styl
.color--primary
	color $theme-primary

.color--secondary
	color $theme-secondary

.color--info
	color $theme-info

.color--success
	color $theme-success

.color--danger
	color $theme-danger

.color--warning
	color $theme-warning
```

**Certo**

```styl
.color
	for $theme in $themes
		&--{$theme}
			color lookup('$theme-' + $theme)
```


Evite declarações shorthand desnecessáriamente.

**Errado**

```styl
.foo
	margin 0 0 20px
```

**Certo**

```styl
.foo
	margin-bottom 20px
```


## Licença

(The MIT License)

Copyright 2020 Melhor Envio

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
