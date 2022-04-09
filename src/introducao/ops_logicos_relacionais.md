# Operadores de igualdade, lógicos, e relacionais

<!-- Precisamos de uma vírgula de Oxford pra tirar ambiguidade no título -->

## Operadores de igualdade

Os operadores de igualdade verificam a equivalência entre os valores de dois
objetos.

### Operadores `==` e `!=`

O operador `==` ("igual a") produz o valor `1` (`true`) quando seus operandos
possuem valores equivalentes. A expressão `5 == 5` tem valor `1`, enquanto a
expressão `5 == 6` tem valor `0` (`false`).

O operador `!=` ("não igual a") é o oposto de `==`. Quando ambos os operandos
possuem valores equivalentes a expressão tem valor `0`, caso contrário `1`.
`7 != 9` resulta em `1`, e `7 != 7` resulta em `0`.

```admonish example "Exemplos"
Imaginemos a expressão `A <op> B`, sendo `<op>` um dos operadores `==` ou
`!=`.

|   A | op  | B   | Resultado |
| --: | :-: | :-- | :-------: |
|  10 | ==  | 10  |  `true`   |
|  10 | !=  | 10  |  `false`  |
|  10 | ==  | 25  |  `false`  |
|  10 | !=  | 25  |  `true`   |
```

Se `A == B` for `true`, `A != B` é necessariamente `false`.

## Operadores relacionais

### Operadores `<` e `>`

O operador `<` ("menor que") produz o valor `1` quando o valor do operando à
esquerda for **menor** que o valor à direita, e o operador `>` ("maior que")
produz o valor `1` quando o valor do operando à esquerda for **maior** que o
valor à direita. Nos demais casos, o resultado é `0`.

```admonish example "Exemplos"
Imaginemos a expressão `A <op> B`, sendo `<op>` um dos operadores `<` ou
`>`.

|   A |  op  | B   | Resultado |
| --: | :--: | :-- | :-------: |
|   0 | &lt; | 15  |  `true`   |
|   0 | &gt; | 15  |  `false`  |
|  15 | &lt; | 15  |  `false`  |
|  15 | &gt; | 15  |  `false`  |
|  15 | &lt; | 0   |  `false`  |
|  15 | &gt; | 0   |  `true`   |
```

Se ambos `A > B` e `A < B` forem `false`, então `A == B` é `true` e vice-versa.

```admonish warning "Comparando NaNs"
A afirmação anterior não se aplica caso pelo menos uma das expressões `isnan(A)`
e `isnan(B)` (de `<math.h>`) for diferente de `false`.  Um objeto de tipo
flutuante pode possuir um valor NaN, que representa um número indefinido ou
irrepresentável.
```

### Operadores `<=` e `>=`

Os operadores `<=` ("menor que ou igual a") e `>=` ("maior que ou igual a") são
similares aos operadores acima. `A <= B` é `true` quando `A` for **menor** ou
igual a `B`, e `A >= B` é `true` quando `A` for **maior** ou igual a `B`.

É possível que tanto `A <= B` quanto `A >= B` sejam `true`, nesse caso `A` e `B`
possuem valores equivalentes.

## Operadores lógicos

Para todos os fins relacionados aos operadores lógicos, qualquer valor diferente
de `0` (`false`) é considerado `true`.

### Operador `!`

O operador `!` ("NÃO lógico") inverte o valor lógico de uma expressão—`true` se
torna `false` e `false` se torna `true`.

Se a expressão `<expr>` for `true`, a expressão `!(<expr>)` é necessariamente
`false`. `!` tem precedência maior que todos os operadores apresentados nessa
página.

### Operadores `&&` e `||`

Os operadores `&&` ("E lógico") e `||` ("OU lógico") são simples. O resultado da
aplicação de `&&` é `true` quando ambos os operandos possuem valor `true`,
enquanto `||` produz `true` quando pelo menos **um** de seus operandos possuir
valor `true`.

```admonish example "Exemplos"
|       A |  op  | B       | Resultado |
| ------: | :--: | :------ | :-------: |
| `false` | \|\| | `false` |  `false`  |
| `false` |  &&  | `false` |  `false`  |
|  `true` | \|\| | `false` |  `true`   |
|  `true` |  &&  | `false` |  `false`  |
|  `true` | \|\| | `true`  |  `true`   |
|  `true` |  &&  | `true`  |  `true`   |
```

Assim, podemos utilizar várias expressões para produzir um valor lógico. Por
exemplo: `a < b && b < c` só é `true` se `a`, `b` e `c` cada um possuir um valor
maior que o anterior. A precedência dos operadores lógicos E e OU é menor do que
a dos operadores relacionais, portanto a expressão anterior é equivalente a
`(a < b) && (b < c)`.

A precedência do operador `||` é menor do que a de `&&`, portanto
`a || b || c && d || e` é equivalente a `a || b || (c && d) || e`.

```admonish example "Exemplo de utilização"
Vamos utilizar os operadores que vimos para fazer uma função que verifica se
vários números estão ordenados—cada número na sequência é maior ou equivalente
ao anterior.

~~~c
bool Ordenados(int a, int b, int c, int d, int e)
{
    return a <= b && b <= c && c <= d && d <= e;
}
~~~

A função `Ordenados` retorna `true` com os argumentos `1, 2, 3, 4, 5`, mas
retorna `false` com os argumentos `1, 2, 3, 4, 3`. Vamos utilizá-la em um
programa interativo:

~~~c
int main(void)
{
    int a, b, c, d, e;

    printf("Digite 5 inteiros separados por vírgula: ");
    scanf("%d ,%d ,%d ,%d ,%d",
           &a, &b, &c, &d, &e);

    // Isso exibirá "1" (true) ou "0" (false)
    printf("Os números estão ordenados? %d\n",
           Ordenados(a, b, c, d, e));
}
~~~

O posicionamento das vírgulas no `scanf` acima pode ser contraintuitivo, mas
lembre-se de um detalhe que vimos sobre a string de formato: um espaço em branco
faz o `scanf` pular **zero ou mais** caracteres white-space na leitura, portanto
ele funciona corretamente até se a vírgula estiver logo após o número. A
especificação `%d` também pula caracteres white-space caso existam, assim até a
entrada `1 , 2,3, 4,   5` funcionaria corretamente.

Valores `bool` se tornam `int` ao serem passados para `printf`, por isso a
especificação `%d` funciona corretamente.
```

### Associatividade

Os operadores de igualdade, lógicos, e relacionais são associativos-à-esquerda,
exceto o operador `!`.
