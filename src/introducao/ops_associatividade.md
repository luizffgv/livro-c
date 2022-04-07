# Associatividade de operadores

Quando várias operações têm a mesma precedência, geralmente as agrupamos da
esquerda para a direita, i.e. são associativas-à-esquerda.

## Associatividade à esquerda

Como os operadores binários `+` e `-` possuem a mesma precedência e são
associativos-à-esquerda, ambas as expressões abaixo são equivalentes.

```c
a + b + c - d - e
```

```c
(((a + b) + c) - d) - e
```

Os operadores binários `*`, `/` e `%` possuem a mesma precedência e também
associatividade à esquerda, portanto `a * b / c` é o mesmo que `(a * b) / c`.

Operações são primeiro agrupadas de acordo com a precedência, e depois de acordo
com a associatividade. Por isso `a + b * c / d` é equivalente a
`a + ((b * c) / d)` e não `((a + b) * c) / d`.

## Associatividade à direita

Todos os operadores de atribuição possuem associatividade à direita. Isso
significa que `a = b = c` é equivalente a `a = (b = c)`.

Como os operadores de atribuição possuem a mesma precedência, `a = b *= c += d`
é equivalente a `a = (b *= (c += d))`.
