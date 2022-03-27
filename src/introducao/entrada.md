# Entrada básica

As funções de entrada do C permitem ao programa interagir com o usuário lendo
informações. A função principal que usaremos pra isso é a `scanf` de
`<stdio.h>`.

## Função `scanf`

Assim como `printf`, a função `scanf` recebe uma string de formato; a diferença
é que nesse caso a string determina não o que será exibido, mas o que será lido.

Os modificadores de comprimento e especificadores de conversão na string de
formato determinam o tipo do valor que será lido. Vejamos algumas especificações
(todas devem iniciar com `%`):

| Modificador | Especificador | Significado                                          |
| ----------: | :------------ | ---------------------------------------------------- |
|             | `c`           | Um caractere, será armazenado em um `char`           |
|         `h` | `d`           | Um número inteiro, será armazenado em um `short`     |
|             | `d`           | Um número inteiro, será armazenado em um `int`       |
|         `l` | `d`           | Um número inteiro, será armazenado em um `long`      |
|        `ll` | `d`           | Um número inteiro, será armazenado em um `long long` |
|             | `f`           | Um número real, será armazenado em um `float`        |
|         `l` | `f`           | Um número real, será armazenado em um `double`       |
|         `L` | `f`           | Um número real, será armazenado em um `long double`  |

Diferente de `printf`, perceba que `scanf` utiliza a especificação `%f` para
`float` e `%lf` para `double`. Você não deve utilizar `%f` no lugar de `%lf` ou
`%d` lugar de `%hd` e vice-versa.

Para armazenar um valor lido com uma especificação de conversão, precisamos
especificar seu alvo (a localização de um objeto na memória).

```admonish example "Exemplo"
Neste caso, utilizaremos o operador `&` unário (_address-of_, ou endereço-de)
para obter o endereço do objeto representado pela variável `n`:

~~~c
int n;
scanf("%d", &n);
~~~
```

A chamada de função no exemplo acima lê um número inteiro da entrada e armazena
seu valor em `n` por meio de seu endereço na memória. A especificação `%d`
descarta quaisquer caracteres white-space da entrada até encontrar outro tipo de
caractere, portanto essa `scanf` funciona com qualquer número de caracteres
white-space precedendo o número na entrada.

Antes de continuar é importante definir o que é um caractere white-space. Essa
expressão se refere a qualquer caractere da lista abaixo.

- `' '` (espaço)
- `'\t'` (tabulação horizontal)
- `'\v'` (tabulação vertical)
- `'\n'` (quebra de linha)
- `'\f'` (quebra de página)

```admonish example "Um programa com entrada/saída"
Retomando nosso foco, já podemos fazer um simples programa com entrada e saída:

~~~c
#include <stdio.h>

int main(void)
{
    printf("Digite um número inteiro: ");
    int num;
    scanf("%d", &num);

    printf("O número digitado foi %d.\n", num);

    return 0;
}
~~~
```

Execute o exemplo acima e tente fazê-lo produzir um resultado incorreto. A
leitura do número pode dar errado de várias formas, incluindo:

- A entrada não é um número. Nesse caso `scanf` não modifica a entrada (exceto
  por descartar caracteres white-space iniciais) e ela pode ser lida
  futuramente.
- O número digitado pode não ser representável em um `int`. Nesse caso o
  comportamento do programa é indefinido.
- O número digitado pode conter casas decimais, e nesse caso o separador decimal
  e todos dígitos seguintes serão ignorados.

Com a especificação `%d` a sequência de dígitos será lida até um caractere de
outro tipo (ex. uma letra) ser encontrado. Com a entrada `163p90`, `scanf`
associará `163` ao `%d` e `p90` continuará na entrada para ser lido futuramente.

```admonish example "Lendo <code>163p90</code>"
Podemos decompor a entrada `163p90` em dois objetos `int` e um `char` da
seguinte forma:

~~~c
// A ordem de definição das variáveis não importa
int  a;
char b;
int  c;

scanf("%d%c%d", &a, &b, &c);

printf("a: %d\n"
       "b: %c\n"
       "c: %d\n",
       a, b, c);
~~~

> a: 163<br>
b: p<br>
c: 90
```

No exemplo acima a `scanf` acima associa `163` ao primeiro `%d`, armazena o
valor em `a` e a sequência `p90` continua na entrada. O próximo caractere (`'p'`
nesse caso) se associa ao `%c` e é armazenado em `b`. O último `%d` recebe o
inteiro `90` que é armazenado em `c`. Depois, os valores são exibidos com
`printf`.

Quando um caractere da string de formato não faz parte de uma especificação de
conversão, `scanf` verificará se esse caractere é igual ao próximo caractere da
entrada. Se sim, o caractere da entrada é descartado e prosseguimos com a string
de formato, caso contrário a execução de `scanf` para.

```admonish example "Exemplo"
~~~c
printf("Quantos anos você tem? ");
int idade;
scanf("Eu tenho %d", &idade);
~~~
```

No exemplo acima a `scanf` acima só chega ao `%d` se os caracteres anteriores
corresponderem à entrada. Se a entrada for `Eu tenho 5`, o valor de `idade` será
5, mas a entrada `Eu tinha 5` não armazena nada em `idade` e seu valor é
indeterminado. Um espaço na string de formato corresponde a zero ou mais
caracteres white-space na entrada, então a entrada `Eutenho5` também funciona
corretamente.

A string de formato `"Eu tenho%d"` também funciona corretamente, pois como
supracitado, a especificação `%d` faz com que `scanf` descarta qualquer espaço
em branco até encontrar um caractere non-white-space (caracteres não
white-space, como letras e dígitos).

Não se esqueça que após um número ser digitado e lido, `scanf` não descarta a
quebra de linha (`\n`) do final da linha de entrada. Isso pode fazer com que
esse caractere se associe a uma futura especificação `%c` e isso pode ser
indesejado. Para descartar esse caractere de uma forma simples, utilize um
espaço antes da especificação `%c` e isso pulará a quebra de linha.

```admonish example "Exemplo"
Aqui está um código em que a quebra de linha na entrada pode ser prejudicial:

~~~c
int num;
scanf("%d", &num);

char ch;
scanf("%c", &ch); // Isso lerá uma quebra de linha se o usuário tiver digitado
                  //  um número e pressionado ENTER.

printf("O caractere lido foi '%c'\n", ch);
~~~

E aqui está uma versão que se previne disso:

~~~c
int num;
scanf("%d", &num);

char ch;

//     ↓
scanf(" %c", &ch); // O usuário pode inserir espaços e pressionar ENTER o quanto
                   // quiser. Apenas um caractere non-white-space se associará.

printf("O caractere lido foi '%c'\n", ch);
~~~

Alternativamente, o espaço pode estar após a especificação `%d`:
`scanf("%d ", &num)`.
```
