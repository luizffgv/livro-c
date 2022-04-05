# Saída básica

As funções de saída do C permitem ao programa interagir com o usuário exibindo
informações. Algumas funções para isso são `puts`, `putchar` e `printf`—todas
incluídas em `<stdio.h>`.

## Função `puts`

A função `puts` recebe uma string (sequência de caracteres) e a exibe.

```admonish example "Exemplo"
Podemos exibir a string `"Olá, Mundo!"` simplesmente utilizando-a como argumento
de `puts`:

~~~c
puts("Olá, Mundo!");
~~~

> Olá, Mundo!
```

```admonish info "Aspas duplas ou simples?"
Diferente de um `char`, uma string não deve ser delimitada por aspas simples;
uma sequência de caracteres entre aspas simples é um `int` e não uma string.

Sequências de escape em C são interpretadas como caracteres únicos.
```

<!-- "Sequências de escape em C são interpretadas como caracteres únicos.". Isso
se aplica a todas as sequências de escape padrão? -->

A função `puts` automaticamente insere uma quebra de linha (`\n`) na saída após
a string fornecida, portanto a próxima operação de saída ocorrerá na linha
seguinte.

```admonish example "Exemplo"
~~~c
puts("Essa é a 1ª linha");
puts("Essa é a 2ª linha");
puts("Essa é a 3ª linha");
~~~

> Essa é a 1ª linha<br>
Essa é a 2ª linha<br>
Essa é a 3ª linha
```

Várias chamadas seguidas de `puts` com literais string podem ser substituídas
por apenas uma.

```admonish example "Exemplo"
~~~c
puts("Essa é a 1ª linha\n"
     "Essa é a 2ª linha\n"
     "Essa é a 3ª linha");
~~~

> Essa é a 1ª linha<br>
Essa é a 2ª linha<br>
Essa é a 3ª linha
```

```admonish info "Literais string"
Literais string são strings especificadas diretamente em código, entre aspas
duplas. `"a"`, `"Hello, World!"` e `"123.917"` são exemplos de literais string.
```

Note que as três strings passadas para `puts` não estão separadas por vírgula,
portanto o compilador as mescla em uma só (processo que ocorre com literais
string). O resultado final é o mesmo que ao utilizar a string
`"Essa é a 1ª linha\nEssa é 2ª linha\nEssa é a 3ª linha"`, porém dividir as
linhas torna o código mais compreensível. Utilize essa funcionalidade para uma
melhor legibilidade de código.

Tentar separar as três strings utilizando vírgulas resultará em um erro, pois
serão consideradas três argumentos e a função `puts` deve receber apenas um.

```admonish example "Exemplo"
~~~c
// Erro: Passando três argumentos para uma função que recebe apenas um
puts("Essa é a 1ª linha\n",
     "Essa é a 2ª linha\n",
     "Essa é a 3ª linha");
~~~
```

```admonish info "Exibição de caracteres estendidos"
Se os caracteres `é` e/ou `ª` não forem exibidos corretamente, seu terminal pode
estar utilizando um conjunto de caracteres que não os suporta.
```

## Função `putchar`

A função `putchar` é similar à função `puts`, porém exibe apenas um caractere e
não insere uma quebra de linha. Seu uso é simples, basta fornecer um caractere.

```admonish example "Exemplo"
~~~c
putchar('O');
putchar('i');
putchar('!');
~~~

> Oi!
```

```admonish hint "Variáveis como argumentos"
Não esqueça que o identificador de uma variável é uma expressão, portanto pode
ser utilizado como argumento. Imaginando que `v` denota uma variável,
`putchar(v);` exibirá o caractere correspondente a seu valor.
```

```admonish info "Parâmetro de <code>putchar</code>"
`putchar` recebe um `int`, porém um `char` será implicitamente convertido para
`int` nesse contexto.

```

```admonish example "Mais um exemplo"
Aqui está um programa simples, com uma função (`ExibirDuo`) que recebe dois
caracteres e os exibe com uma exclamação no final:

~~~c
#include <stdio.h>

void ExibirDuo(char primeiro, char segundo)
{
    putchar(primeiro);
    putchar(segundo);
    putchar('!');
}

int main(void)
{
    ExibirDuo('O', 'i');

    return 0;
}
~~~

> Oi!
```

## Função `printf`

A função `printf`, diferente de `puts`, tem a capacidade de formatar os dados
antes de exibi-los. O primeiro parâmetro da função é uma string de formato, que
informa à função a série de operações de saída a serem realizadas.

A string `"Hello, World!"`, ao ser usada como string de formato, faz com que
`printf` simplesmente a exiba. Para realizarmos operações de saída mais
complexas, utilizamos especificações de conversão—e.g. `%d`.

- `%`: Introduz uma especificação de conversão.
- `d`: Um _especificador_ de conversão que indica um valor do tipo `int` em
  base 10.

Ao exibir, `printf` substitui as especificações de conversão pelos valores dos
argumentos recebidos.

```admonish example "Exemplo com um argumento"
~~~c
// %d é substituído pelo argumento 5
printf("O valor de 5 é %d", 5);
~~~

> O valor de 5 é 5
```

Quando há várias especificações de conversão, a enésima especificação é
substituída pelo enésimo argumento após a string de formato.

```admonish example "Exemplo com vários argumentos"
~~~c
// O 1º %d é substituído pelo 1º argumento após a string de formato (5)
// O 2º %d é substituído pelo 2º argumento após a string de formato (9)
printf("O valor de 5 é %d e o valor de 9 é %d", 5, 9);
~~~

> O valor de 5 é 5 e o valor de 9 é 9
```

Para os diversos tipos há diversos especificadores de conversão. Vejamos alguns
deles:

| Especificador | Significado                                          |
| :-----------: | ---------------------------------------------------- |
|      `c`      | Um `char`, exibido como um caractere                 |
|      `u`      | Um `unsigned`, exibido em base 10                    |
|      `f`      | Um `double`, exibido com 6 casas decimais por padrão |
|      `s`      | Uma string                                           |

```admonish example "Especificação <code>%s</code>"
~~~c
// %s é substituído por "World".
printf("Hello, %s!", "World");
~~~

> Hello, World!
```

```admonish example "Especificação <code>%f</code>"
~~~c
// %f é substituído pelo valor da expressão acos(-1), função de <math.h>.
// Isso exibirá um valor aproximado de π com 6 casas decimais, e pode variar
// conforme o seu sistema. Teste você mesmo.
printf("O valor de pi é %f", acos(-1));
~~~
```

```admonish example "Especificação <code>%c</code>"
~~~c
// %c é substituído pelo caractere "+".
printf("1 %c 1", '+');
~~~

> 1 + 1
```

Diferente do que acontece com `puts`, o repetido uso de `printf` acima irá
exibir toda a saída em uma linha apenas. Para iniciar uma nova linha utilize a
sequência de escape `\n` no final da string de formato anterior ou no início da
string de formato atual.

```admonish example "Exemplo"
~~~c
printf("Hello, %s!\n", "World");
printf("Goodbye, %s!", "World");
~~~

Ou, alternativamente:

~~~c
printf("Hello, %s!", "World");
printf("\nGoodbye, %s!", "World");
~~~
```

```admonish info "Duas linhas em um <code>printf</code>"
Nos exemplos acima seria melhor utilizar `printf` apenas uma vez. Aqui estão
duas formas de exibir duas linhas com apenas um `printf`:

~~~c
printf("Hello, %s!\n"
       "Goodbye, %s!",
       "World", "World");
~~~

~~~c
printf("Hello, %s!\nGoodbye, %s!", "World", "World");
~~~

Na primeira opção acima os primeiros dois literais string se tornam um argumento
só, efetivamente causando o mesmo resultado que a segunda opção. Esse processo
foi explicado em [Função `puts`](#função-puts).
```

```admonish hint "<code>%f</code> para <code>float</code>?"
O especificador de conversão `f` irá funcionar até quando o argumento
correspondente for `float` e o especificador `d` irá funcionar até quando o
argumento correspondente for `short`. A razão disso é um assunto mais avançado.
```

<!-- Isso é devido às default argument promotions -->
