Melhor Envio CSS Style Guide
============================

*Diretrizes de organização e escrita de CSS*


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


### Multiplos seletores

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
