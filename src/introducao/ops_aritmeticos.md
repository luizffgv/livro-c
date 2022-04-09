# Operadores aritméticos básicos

Virtualmente toda a manipulação de dados em C é feita por operadores, que
indicam operações ações a serem realizadas com seus operandos (valores que a
operação recebe).

Na matemática, a soma é uma operação representada pelo operador "+" e se aplica
a dois valores, i.e. uma operação binária. A aridade de uma função/operação é o
número de operandos que ela recebe; uma operação é unária quando tem aridade 1 e
binária quando tem aridade 2.

Em C é possível separar os operadores em grupos de acordo com a aridade de cada
um. Abaixo são apresentados alguns dos operadores aritméticos.

## Binários

A maioria dos operadores binários no C recebem um operando de cada lado com a
seguinte sintaxe:

<div class="syntax">

_operando_[^op-syntax-operand] _op_[^op-syntax-operator] _operando_

</div>

<!-- prettier-ignore -->
[^op-syntax-operand]: Uma expressão que resulta em um valor.

<!-- prettier-ignore -->
[^op-syntax-operator]: Um operador aritmético binário, como `+`, `-` etc.

### `+` binário

O operador binário `+` funciona igual na matemática: o resultado da operação é a
soma dos dois operandos. `5 + 3`, por exemplo, é uma expressão de valor `int`
`8`.

```admonish example "Exemplo"
Aqui está um programa que soma dois números que o usuário digitar
e exibe o resultado:

~~~c
#include <stdio.h>

int main(void)
{
    int a, b;
    printf("Digite dois números: ");
    scanf("%d%d", &a, &b); // "%d %d" é equivalente
    printf("Resultado: %d\n", a + b);

    return 0;
}
~~~
```

### `-` binário

O operador binário `-` funciona de forma parecida ao operador `+` binário, porém
realiza subtração ao invés de adição. `5 - 3`, por exemplo, é uma expressão de
valor `int` `2`.

### `*` binário

O operador binário `*` realiza a multiplicação de seus operandos. O resultado de
`5 * 3` é um `int` `15`.

### `/`

O operador binário `/` realiza a divisão do valor do operando à esquerda pelo
valor do operando à direita. O valor de `5 / 3` é `1`. Como ambos operandos são
`int`s o resultado é um `int` (A parte fracionária é perdida). Se algum dos
operandos fosse de tipo flutuante, e.g. `5 / 3.` (`3.` é um `double`), o
resultado seria a dízima infinita 1,666..., que no caso de `5 / 3.` seria um
`double`.

### `%`

O operador binário `%` resulta no resto da divisão (inteira) do operando à
esquerda pelo operando à direita. O valor de `5 % 3`, e.g., é 2, pois resultado
da divisão inteira é 1 e o resto é 2.

Mais alguns exemplos:

| Operação  | Valor | Explicação                                                             |
| :-------: | :---: | ---------------------------------------------------------------------- |
| `10 % 3`  |   1   | `10 / 3` é igual a `3`, `3 * 3` é igual a `9`, e `10 - 9` é `1`        |
| `10 % 2`  |   0   | `10 / 2` é igual a `5`, `2 * 5` é igual a `10`, e `10 - 10` é `0`      |
| `40 % 7`  |   5   | `40 / 7` é igual a `5`, `7 * 5` é igual a `35` e `40 - 35` é `5`       |
| `-10 % 3` |  -1   | `-10 / 3` é igual a `-3`, `3 * -3` é igual a `-9` e `-10 -(-9)` é `-1` |

## Unários

A maioria dos operadores unários ficam à esquerda do operando, como no seguinte
formato:

<div class="syntax">

_op_ _operando_

</div>

### `+` unário

O operador unário `+` é quase sempre um no-op—uma operação que não faz nada.

Apenas em alguns casos, o operador unário `+` irá converter seu operando para
outro tipo. Esse processo é chamado promoção inteira, que será detalhado bem
depois.

Não se preocupe muito com esse operador, pois é raro encontrar um motivo
legítimo para usá-lo.

### `-` unário

Diferente do `+` unário, esse operador raramente é um no-op. Ele inverte o sinal
de seu operando, transformando `50` em `-50`, `-25` em `25` etc.

Ele pode ser no-op quando seu operando possui valor zero, mas em alguns sistemas
é possível distinguir entre zero positivo e zero negativo. Não se preocupe muito
com isso, pois o sinal do zero raramente altera o comportamento de um programa.

```admonish example "Exemplo"
Aqui está um programa que inverte o número
que o usuário digitar:

~~~c
#include <stdio.h>

int main(void)
{
    int num;

    printf("Digite um número: ");
    scanf("%d", &num);
    printf("%d\n", -num);

    return 0;
}
~~~
```

## Precedência

Assim como na matemática, aqui temos o conceito de precedência de operadores.
Isso significa que algumas operações são agrupadas independentemente da ordem em
que aparecem em uma expressão.

Os operadores `*` e `/` possuem maior precedência que os operadores binários `+`
e `-`, portanto, a expressão `a + b / 2` é o mesmo que `a + (b / 2)`. As versões
unárias de `+` e `-` possuem maior precedência que todos os operadores acima,
portanto `a + b * -c` é o mesmo que `a + (b * (-c))`.

```admonish example "Exemplo"
Aqui estão mais alguns exemplos da precedência desses operadores:

~~~c
int   a = 1 + 2 * 3;   // 7
int   b = 10 + 2 / 2;  // 11
float c = 1 + 3.f / 2; // 2.5f
~~~
```
