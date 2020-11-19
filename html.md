Melhor Envio HTML Style Guide
=============================

*Diretrizes de organização e escrita de HTML*


## Índice

- [Template engine](#template-engine)
- [Estrutura de pastas](#estrutura-de-pastas)
- [Indentação](#indentação)
- [Sintaxe](#sintaxe)


## Template engine

O template engine utilizado é o [Pug](https://pugjs.org).


## Estrutura de pastas

```
html/
├── app/
│   └── **
├── components/
│   └── *.pug
├── functions/
│   └── *.pug
├── includes/
│   └── **
├── layouts/
│   └── *.pug
└── index.pug
```


## Indentação

O caracter padrão de indentação utilizado é **tab**, e espaços não devem ser utilizados nem mesmo para alinhamentos.

**Errado**

```pug
.foo
••.bar(
••••foo='foo',
••••bar='bar',
••••baz='baz'
••)
••••.baz
```

**Errado**

```pug
.foo
••••.bar
••••••••foo='foo',
••••••••bar='bar',
••••••••baz='baz'
••••)
••••••••.baz
```

**Certo**

```pug
.foo
────.bar
────────foo='foo',
────────bar='bar',
────────baz='baz'
────)
────────.baz
```


## Sintaxe

**Errado**

```pug
.foo(bar="bar")
```

**Certo**

```pug
.foo(bar='bar')
```


**Errado**

```pug
Input(Type='text')
```

**Certo**

```pug
input(type='text')
```


**Errado**

```pug
a(href='https://' + link) Link
```

**Certo**

```pug
a(href=`https://${link}`) Link
```


**Errado**

```pug
nav
	a(href=link) link
	a(href=link) link
	a(href=link) link
ul
	li
		p lorem ipsum
	li
		p lorem ipsum
```

**Errado**

```pug
nav

	a(href=link) link

	a(href=link) link

	a(href=link) link


ul

	li

		p lorem ipsum

	li

		p lorem ipsum
```

**Certo**

```pug
nav
	a(href=link) link
	a(href=link) link
	a(href=link) link

ul
	li
		p lorem ipsum

	li
		p lorem ipsum
```


**Errado**

```pug
.foo(bar='bar' baz='baz')
```

**Certo**

```pug
.foo(bar='bar', baz='baz')
```


**Errado**

```pug
form( method='post', action=url )
	input( type='text', name='name', value='value' )
	button( type='submit' )
```

**Errado**

```pug
form(method='post', action=url)
	input(type='text', name='name', value='value')
	button(type='submit')
```

**Certo**

```pug
form(method='post', action=url)
	input(
		type='text',
		name='name',
		value='value'
	)
	button(type='submit')
```


**Errado**

```pug
table: tr: td text
```

**Certo**

```pug
table
	tr
		td text
```


**Errado**

```pug
div(class='foo')
```


**Errado**

```pug
div.foo
```

**Certo**

```pug
.foo
```


**Errado**


```pug
span(id='foo')
```

**Certo**

```pug
span#foo
```

**Errado**

```pug
span(class='foo')
```

**Certo**

```pug
span.foo
```


**Errado**

```pug
div(id='foo')
```

**Certo**

```pug
#foo
```


**Errado**

```pug
input(type='text').foo
```

**Certo**

```pug
input.foo(type='text')
```


**Errado**

```pug
input.foo#bar(type='text')
```

**Errado**

```pug
input.foo(type='text')#bar
```

**Certo**

```pug
input#bar.foo(type='text')
```


**Errado**

```pug
- var a = 'This is code'

p= 'This code is <escaped>'
p!=  'This code is <strong>not</strong> escaped'
```

**Certo**

```pug
-var a = 'This is code'

p='This code is <escaped>'
p!='This code is <strong>not</strong> escaped'
```


**Errado**

```pug
if true == false
if true != false
```

**Certo**

```pug
if true === false
if true !== false
```


**Errado**

```pug
h1= `${title}`
```

**Certo**

```pug
h1= title
```


## Licença

(The MIT License)

Copyright 2020 Melhor Envio

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
