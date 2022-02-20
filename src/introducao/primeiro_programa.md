# Primeiro programa

## Código-Fonte

O primeiro programa que várias pessoas costumam escrever consiste em exibir
"Hello, World!" ("Olá, Mundo!" em inglês). Um simples código C para essa tarefa
é o seguinte:

<div id="hello-world"></div>

```c
#include <stdio.h>

int main(void)
{
    puts("Hello, World!");
    return 0;
}
```

Códigos-fonte C costumam estar em arquivos com extensão "c", portanto digamos
que o código acima é o conteúdo do arquivo "main.c".

Esse código simples é composto por várias partes. Primeiro, `<stdio.h>` é o
arquivo que fornece as principais funções de entrada e saída no C. A linha
`#include <stdio.h>` essencialmente permite ao programa usar essas funções.

`main` é o ponto de entrada do programa, ou seja, onde começa a execução do
código. As chaves `{` e `}` representam o corpo do `main`, e o código entre elas
será executado.

A primeira tarefa realizada em nosso `main` é a linha `puts("Hello, World!");`.
`puts` é uma das funções de entrada e saída fornecidas em `<stdio.h>`, e ela
exibe seu argumento—`"Hello, World!"`—na tela.

Logo após isso temos a linha `return 0;`, que termina a execução da função. Em
`main`, retornar `0` indica que o programa executou corretamente.

## Execução

O [código-fonte acima](#código-fonte) está completo, mas ainda precisamos
utilizar um compilador C para transformá-lo em código objeto. Esse processo é
chamado compilação e, por si só, não é suficiente para produzir um executável.
Antes da compilação deve ocorrer o pré-processamento e, após a compilação, a
ligação (_linkage_). Ambos os processos são realizados automaticamente em
compiladores atuais (como [GCC](https://gcc.gnu.org/) e
[Clang](https://clang.llvm.org/)), portanto ainda não serão detalhados.

Uma forma simples de criar um executável utilizando o compilador GCC é fornecer
como argumento o caminho para o arquivo (em nosso caso `main.c`) contendo o
código-fonte. No caso do programa acima, o comando seria `gcc main.c`. O
executável comumente será chamado "a.exe" ou "a.out", mas o nome pode ser
alterado fornecendo a opção `-o` seguida pelo caminho de destino. Para criar o
executável "Programa" usaríamos o comando `gcc main.c -o Programa`.

Se tudo der certo, a execução do programa exibirá "Hello, World!".
