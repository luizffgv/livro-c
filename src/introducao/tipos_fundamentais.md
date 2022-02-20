# Tipos fundamentais

Anteriormente vimos que funções, parâmetros e variáveis podem representar
diferentes tipos de dados. Alguns tipos já estão embutidos na linguagem, e serão
chamados de **tipos fundamentais**. Esse grupo inclui os tipos inteiros e os
tipos flutuantes, que podem ser vistos abaixo.

## Tipos inteiros

### Tipo `int`

Representa um número inteiro, como `-30` ou `529`. O menor e maior número
representável em um `int` não está definido no padrão C, mas um `int`
representará, no mínimo, qualquer número inteiro no intervalo \[-32767,32767].

### Tipo `char`

Representa um caractere, como `' '` (espaço em branco), `'s'` (letra "s") ou `?`
(ponto de interrogação). Os caracteres em C devem estar dentro de aspas simples;
`"a"` é uma string.

```c
char foo = 'a'; // Okay

char bar = "a"; // Erro
```

#### Sequências de escape

Alguns caracteres não podem ser simplesmente digitados, portanto são
representados utilizando **sequências de escape**, nesse caso uma barra
invertida `\` seguida de um caractere. Na tabela abaixo estão algumas sequências
de escape.

| Sequência | Descrição                          |
| :-------: | :--------------------------------- |
|   `\a`    | Produz um alerta audível ou visual |
|   `\n`    | Produz uma quebra de linha         |
|   `\'`    | Produz uma aspa simples            |

Tentar armazenar uma aspa simples em um `char` pode ser complicado, pois em
`char ch = ''';` o compilador procura um caractere contido entre o primeiro par
de aspas, porém não há nada dentro. Nesse caso devemos utilizar a sequência de
escape `\'`: `char ch = '\'';`.

```c
char ch = '''; // Erro

char ch = '\''; // Okay
```

#### Conversões para outros tipos inteiros

Valores `char` são internamente representados por valores inteiros, e o valor de
cada caractere depende do sistema. Muitos sistemas utilizam o conjunto de
caracteres ASCII, parcialmente mostrado na tabela abaixo.

| Valor | Caractere | Valor | Caractere | Valor | Caractere |
| ----: | :-------- | ----: | :-------- | ----: | :-------- |
|  `32` | (espaço)  |  `65` | A         |  `97` | a         |
|  `48` | 0         |  `66` | B         |  `98` | b         |
|  `49` | 1         |  `67` | C         |  `99` | c         |
|  `50` | 2         |  `68` | D         | `100` | d         |
|  `51` | 3         |  `69` | E         | `101` | e         |
|  `52` | 4         |  `70` | F         | `102` | f         |
|  `53` | 5         |  `71` | G         | `103` | g         |
|  `54` | 6         |  `72` | H         | `104` | h         |
|  `55` | 7         |  `73` | I         | `105` | i         |
|  `56` | 8         |  `74` | J         | `106` | j         |
|  `57` | 9         |  `75` | K         | `107` | k         |

Quando um valor `char` é convertido para outro tipo inteiro (e.g. `int`), o
resultado é o valor inteiro que representa o caractere no conjunto de caracteres
utilizado. Quando um tipo inteiro é convertido para `char`, o resultado é o
caractere que representa o valor inteiro no conjunto de caracteres utilizado.

```c
char ch = 65; // ch é igual a 'A' se o conjunto de caracteres for ASCII

int i = 'A'; // i é igual a 65 se o conjunto de caracteres for ASCII
```

```admonish warning "<code>'x'</code> é <code>char</code> mesmo?"
Caracteres entre aspas simples, como `'a'`, possuem tipo `int`. Esse detalhe não
costuma ser problemático pois um valor `int` pode ser implicitamente convertido
para `char`.
```

### Tipo `_Bool`

```admonish info "Por que <code>_Bool</code> e não <code>bool</code>?"
Em C, `_Bool` é equivalente ao `bool` de outras linguagens de programação, mas
possui outro nome pois esse tipo foi adicionado no padrão C99 e usar o nome
`bool` poderia quebrar programas antigos.
```

O tipo `_Bool` serve para armazenar um de dois valores: verdadeiro ou falso.
Aqui está um exemplo de duas variáveis `_Bool`, com valores que indicam,
respectivamente, verdade e falsidade:

```c
_Bool verdadeiro = 1;
_Bool falso = 0;
```

Utilizar a palavra-chave `_Bool` pode não ser intuitivo. Por conveniência, é
recomendado incluir o arquivo `<stdbool.h>`, que faz com que `bool` se refira a
`_Bool` e permite utilizar as palavras `true` (verdadeiro) e `false` (falso).
Veja o mesmo código que acima porém utilizando `<stdbool.h>`:

```c
bool verdadeiro = true;
bool falso = false;
```

Sempre que `bool`, `true` ou `false` forem utilizados neste livro, considere que
a diretiva `#include <stdbool.h>` está presente mesmo que em alguns exemplos ela
possa estar omitida por conveniência. É útil lembrar, também, que `true` se
refere ao valor `1` e `false` ao valor `0`.

#### Exemplos de uso

Um exemplo do uso de `bool` são predicados (termo comum para funções que
retornam `true` ou `false`). Suponhamos que a função `Paridade` seja um
predicado que verifica a paridade de um número, retornando `true` caso ele seja
par e `false` caso contrário.

```c
Paridade(1); // false
Paridade(3); // false
Paridade(5); // false

Paridade(2); // true
Paridade(4); // true
Paridade(6); // true
```

## Tipos flutuantes

### Tipo `double`

Representa um número real, como `-30.52` ou `529.0023`. Ao ser convertido para
um inteiro a parte fracionária é descartada, portanto `15.89` se torna `15`. Se
o valor for alto/baixo demais para ser representado por um `int`, o
comportamento é indefinido.

```c
double d = 2.5; // d é igual a 2.5

int i = 2.5; // i é igual a 2
```

### Tipo `float`

Representa um número real assim como `double`, mas os valores representáveis em
um `float` são um subconjunto dos valores representáveis em um `double`. Isso
significa que um `float` pode ter menos precisão e/ou não conseguir representar
valores da mesma magnitude que um `double`.

Um `f` ou `F` após um valor flutuante (e.g. `1.5f`) especifica que o valor é do
tipo `float`.

```c
float f = 2.5f; // f é igual a 2.5
```

### Tipo `long double`

Representa um número real assim como `double`, mas os valores representáveis em
um `long double` são um superconjunto dos valores representáveis em um `double`.
Isso significa que um `long double` pode ter mais precisão e/ou conseguir
representar valores de maior magnitude que um `double`.

Um `l` ou `L` após um valor flutuante (e.g. `1.5l`) especifica que o valor é do
tipo `long double`.

```c
long double ld = 2.5l; // ld é igual a 2.5
```

```admonish warning "Precisão de tipos flutuantes"
Tipos flutuantes podem não representar todos os valores com precisão, mesmo que
estejam entre o valor mínimo e o valor máximo permitidos.

Em geral, quanto mais dígitos um valor possuir, menos precisa será sua
representação. O valor `1.00000001f`, por exemplo, pode se tornar `1.1f` em
algumas implementações.
```
