# livro-c

[![Markdownlint](https://github.com/luizffgv/livro-c/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/luizffgv/livro-c/actions/workflows/markdownlint.yml)
[![GitHub Pages build](https://github.com/luizffgv/livro-c/actions/workflows/gh-pages.yml/badge.svg)](https://github.com/luizffgv/livro-c/actions/workflows/gh-pages.yml)

Este livro virtual gratuito é um projeto que pretende trazer uma fonte moderna,
confiável e completa para o aprendizado de C.

[GitHub Pages](https://luizffgv.github.io/livro-c/)

## Requisitos

Este livro utiliza [mdBook](https://github.com/rust-lang/mdBook) e os plugins
[mdbook-admonish](https://github.com/tommilligan/mdbook-admonish),
[mdbook-linkcheck](https://github.com/Michael-F-Bryan/mdbook-linkcheck) e
[mdbook-mermaid](https://github.com/badboy/mdbook-mermaid).

```sh
cargo install mdbook mdbook-admonish mdbook-linkcheck mdbook-mermaid
```

Na raiz do repositório, execute:

```sh
mdbook-admonish install
mdbook-mermaid install
```

## Uso

Para criar um servidor local e testar o livro, execute `mdbook serve`. Veja a
[documentação do mdBook](https://rust-lang.github.io/mdBook/) para mais
funcionalidades.

## Licenças

[![CC BY-SA 4.0](https://i.creativecommons.org/l/by-sa/4.0/80x15.png)](http://creativecommons.org/licenses/by-sa/4.0/)

A prosa escrita contida nos arquivos Markdown está licenciada sob os termos da
licença [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
