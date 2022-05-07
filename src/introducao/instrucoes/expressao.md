# Instruções de expressão

Instruções de expressão são instruções compostas por expressões completas.

Vejamos um código de exemplo:

```c
int main(void)
{
    // Instrução de expressão, pois chamadas de funções são expressões.
    printf("Digite um número inteiro: ");

    // Declaração, não é uma instrução
    int num;

    // Instrução de expressão, pois chamadas de funções são expressões.
    scanf("%d", &num);

    // Instrução de expressão. Contém a expressão completa num = num * 2
    num = num * 2;

    // Instrução de expressão, pois chamadas de funções são expressões.
    printf("O dobro do número digitado é %d.\n", num);

    // Instrução return
    return 0;
}
```

```admonish info "Expressões completas"
Uma expressão completa é uma expressão que não está contida em outra.

~~~c
a = 2 * 8 / 3;
~~~

No trecho acima a expressão `a = 2 * 8 / 3` é completa, enquanto as demais não.
A expressão `2` não é completa pois está contida em `2 * 8`, a expressão `2 * 8`
não é completa pois está contida em `2 * 8 / 3`, e a expressão `2 * 8 / 3` não é
completa pois está contida em `a = 2 * 8 / 3`.

O diagrama a seguir demonstra visualmente a composição da mesma expressão:

~~~mermaid
flowchart LR
    exp0[a]-----exp6["a = 2 * 8 / 3"]
    exp1[2]---exp4[2 * 8]
    exp2[8]---exp4
    exp4---exp5
    exp3[3]----exp5[2 * 8 / 3]
    exp5---exp6
~~~

Para saber qual expressão está contida em qual, utilizamos as regras de
precedência e associatividade de operadores: `a = 2 * 8 / 3` é o mesmo que
`((a) = (((2) * (8)) / (3)))`, e a partir disso basta notar quais parênteses estão
contidos entre outros parênteses.
```
