# Operadores de atribuição

Anteriormente vimos como modificar um objeto com os operadores `++` e `--`,
porém esses operadores só incrementam ou decrementam por 1. Para modificar um
objeto de forma mais complexa, é necessário utilizar operadores de atribuição.
Assim como o nome sugere, operadores de atribuição atribuem um novo valor a um
objeto.

## Atribuição simples

O operador `=` (atribuição simples) atribui ao operando à esquerda o valor da
expressão à direita.

```admonish example "Exemplo"
~~~c
int x = -3;
printf("%d\n", x);

x = 5; // x agora vale 5
printf("%d\n", x);

x = x + x; // x agora vale 10 (5 + 5)
printf("%d\n", x);
~~~

> -3<br>5<br>10
```

## Atribuição composta

Os operadores de atribuição composta existem para simplificar atribuições do
formato `x = x op expr` tal que `expr` seja uma expressão e `op` seja um dos
operadores binários `*`, `/`, `%`, `+`, `-`, `<<`, `>>`, `&`, `^` ou `|`. Com
atribuição composta `x = x op expr` pode ser reescrito como `x op= expr`.

Isso quer dizer que a expressão `a = a + b` pode ser reescrita como `a += b`, e
`x = x * (25 + y)` como `x *= 25 + y`.

```admonish example "Exemplo"
~~~c
int x = -3;
printf("%d\n", x);

x += 8; // x agora vale 5 (-3 + 8)
printf("%d\n", x);

x *= 2; // x agora vale 10 (5 * 2)
printf("%d\n", x);
~~~

> -3<br>5<br>10
```

Os operadores de atribuição possuem precedência menor que todos os outros
operadores vistos até agora, portanto `a + b = c - d` é equivalente a
`(a + b) = (c - d)`.
