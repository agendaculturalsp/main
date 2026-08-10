# Agenda Cultural SP

Um app de página única (standalone HTML) com a agenda cultural mensal de
São Paulo: shows, exposições, teatro, feiras e agendas contínuas de uma
curadoria fixa de locais pela cidade.

Sem backend, sem build step. Abre direto no navegador ou publica direto no
GitHub Pages a partir deste repositório.

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | O app em si — HTML único com React + Babel carregados via CDN. É o que se publica. |
| `prompt-atualizacao-agenda-cultural-sp-v4.md` | Prompt-mestre para pedir uma atualização mensal a um assistente de IA. Cola o conteúdo inteiro no chat junto com o HTML atual. |

## Como funciona

- **Sem instalação**: `index.html` roda sozinho — os scripts do
  React, ReactDOM e Babel Standalone vêm de CDN (unpkg), e o JSX é
  transpilado no navegador, na hora.
- **Sem servidor**: os dados do mês ficam embutidos no próprio HTML, nos
  arrays `WEEKS` e `ONGOING`, perto do topo do arquivo.
- **Favoritos**: salvos em `localStorage`, no navegador de quem acessa. Não
  há conta nem sincronização entre dispositivos.
- **Quatro abas**: Semanas (agenda navegável por semana), Em Cartaz
  (exposições e temporadas que passam de uma semana), Destaques (6-8
  eventos por mês, curados por relevância) e Favoritos.

## Estrutura de dados

Cada evento segue este formato:

```js
{
  id: "e-slug-unico",           // nunca muda, mesmo em atualizações — preserva favoritos
  date: "DD" ou "DD–DD",        // só em WEEKS
  title: "Nome do evento",
  venue: "Nome do local",
  cat: "musica | teatro | expo | cinema | feira",
  desc: "1-2 frases com o dado mais interessante",
  highlight: true | false,      // aparece na aba Destaques
  url: "link direto pro evento", // opcional — habilita "Ver página do evento" e o link no compartilhamento
}
```

Itens de `ONGOING` (a aba "Em Cartaz") usam `period` (texto livre, ex:
`"Até 03/08"`) no lugar de `date`.

## Como atualizar o mês

1. Abra uma conversa com um assistente de IA com acesso a busca na web.
2. Cole o conteúdo de `prompt-atualizacao-agenda-cultural-sp-v4.md` e anexe
   o `index.html` atual.
3. O prompt pede pesquisa individual em cada local da curadoria fixa (Sescs,
   JazzB, Blue Note, Casa de Francisca, grandes instituições, Bixiga,
   cultura japonesa, feiras), verificação cruzada de ano/dia-da-semana, e
   devolve o HTML reescrito só nos dados — o layout não muda.
4. Ao final, pede um relatório: o que foi confirmado, o que ficou de fora e
   por quê, e observações de acuracidade.
5. Commita e dá push do `index.html` atualizado neste repositório — o GitHub
   Pages publica a versão nova a partir daí.

## Como publicar

- **GitHub Pages**, direto deste repositório — já que é um arquivo estático
  único, sem build, sem dependências além dos CDNs carregados no `<head>`.
  Basta habilitar Pages apontando pra branch `main` (se ainda não estiver
  habilitado); depois disso, todo `git push` atualiza o site publicado.

## Identidade visual (fixa)

Fundo grafite (`#201e1d`) no header, tipografia Archivo (Google Fonts) em
caixa alta nos títulos, vermelho `#ec3013` como destaque, fundo geral
`#f3f2f2`. Grade responsiva de cards (uma coluna em telas estreitas, duas ou
mais em telas largas). Esse layout não deve ser recriado do zero a cada
atualização — só os dados mudam.
