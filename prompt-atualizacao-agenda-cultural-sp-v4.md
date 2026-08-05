# Prompt-mestre: Atualização do app Agenda Cultural SP

> Cole este prompt inteiro sempre que pedir uma atualização. Reescreve o bloco de
> dados do **`agenda-cultural-sp.html`** — o arquivo standalone publicado no
> Netlify (não o artifact `.jsx` de versões anteriores, que ficou defasado
> assim que passamos a publicar fora do Claude.ai). Sem quebrar favoritos
> salvos (os `id` de eventos que continuam válidos não podem mudar).
>
> Ao final, o arquivo atualizado deve ser entregue pronto pra arrastar de
> novo no Netlify Drop (ou, se GitHub/Replit estiver conectado naquele
> momento, publicado direto).

---

## 1. Objetivo

Atualizar a agenda cultural de [MÊS/ANO] do app **Agenda Cultural SP**, cobrindo
a cidade de São Paulo como um todo (sem recorte de bairro ou raio). Buscar
informações reais e verificadas — nunca usar conhecimento de treinamento sem
confirmar, já que a programação cultural muda mensalmente.

## 2. Locais de curadoria fixa (buscar cada um individualmente)

Buscas genéricas ("agenda cultural SP agosto") favorecem sempre os mesmos 2-3
resultados mais indexados. Cada local abaixo precisa de sua própria busca
específica (ex: `"Sesc Pompeia" programação agosto 2026`).

**Sesc — cada unidade separadamente:**
Sesc Pompeia · Sesc 14 Bis · Sesc Belenzinho · Sesc Avenida Paulista ·
Sesc 24 de Maio · guia "Em Cartaz" mensal (sescsp.org.br/editorial/emcartaz)
como checagem cruzada.

**Música ao vivo:**

· JazzB (site oficial tem agenda completa e confiável — https://www.jazzb.com.br/shows — usar sympla como alternativa — https://www.sympla.com.br/produtor/jazznosfundos) 

· Blue Note São Paulo (site oficial tem agenda completa e confiável — https://bluenotesp.com/shows/ — usar eventim como alternativa — https://www.eventim.com.br/artist/blue-note-sp/) 

· Casa de Francisca (site oficial tem agenda completa e confiável —
casadefrancisca.art.br/novo/programacao) 

· Cine Joia (agenda de shows —
cinejoia.com.br/agenda — usar shotgun como alternativa — https://shotgun.live/pt-br/venues/cine-joia — o site oficial costuma bloquear extração automática; se isso acontecer, tentar shotgun e, na falta de resultado, buscar diretamente por `"Cine Joia" [mês] [ano]` antes de desistir para o mês inteiro).

**Grandes instituições:**

· Theatro Municipal e Praça das Artes  (agenda de espetáculo https://theatromunicipal.org.br/programacao/)

· Sala São Paulo / Temporada Osesp (https://salasaopaulo.art.br/salasp/pt/programacao-ingressos)

· MASP (https://masp.org.br/exposicoes e https://masp.org.br/espetaculos-eventos)

· Pinacoteca (Luz, Estação, Contemporânea) (https://pinacoteca.org.br/programacao/tipo/exposicoes/ — checar sempre se uma exposição "em cartaz" anterior já não saiu de circulação antes de repeti-la)

· CCBB (https://ccbb.com.br/sao-paulo/programacao/?cartaz=mes)

· CCSP (Vergueiro) (https://centrocultural.sp.gov.br/ e https://centrocultural.sp.gov.br/agenda/)

· Cinemateca Brasileira (https://cinemateca.org.br/ e https://cinemateca.org.br/programacao/)

**Bixiga e entorno histórico:**

· Teatro Oficina (buscar também como "Teat(r)o Oficina Uzyna Uzona") (https://teatroficina.com/ e  https://site.bileto.sympla.com.br/teatrooficina/)

· Vila Itororó (checar vilaitororo.prefeitura.sp.gov.br/programacao e https://spmaiscultura.prefeitura.sp.gov.br/)

· Mundo Pensante (https://www.mundopensante.com.br/ e https://shotgun.live/pt-br/venues/mundo-pensante)

· Galeria Metrópole (https://www.instagram.com/galeriametropole.sp/ e https://metropolegaleria.com.br/)

**Cultura japonesa:**

· Japan House São Paulo (https://japanhousesp.com.br/programacao/)

· Bunkyo (https://bunkyo.org.br/br/ e https://bunkyo.org.br/br/noticias-e-eventos/eventos/.

**Feiras:**

· Jabuticaba

· Gengibrão - Rasga e Quebra

· Barbotina

· Feiras do livro

· impressos/zines/publicações independentes.

## 3. Locais sugeridos para ampliar a curadoria

Instituto Tomie Ohtake, Museu da Língua Portuguesa, Farol Santander, Auditório do Ibirapuera, Museu Afro Brasil, Galeria Ouro Velho/Ugra. Buscar antes de incluir — só entram se houver evento real no mês.

## 4. Metodologia de busca

1. Uma busca por local — nunca agrupar vários locais numa query só.
2. Tentar `web_fetch` direto na página
   oficial de programação.
3. Confirmar sempre o ano — muito conteúdo indexado é de anos anteriores. Quando a fonte
   mencionar o dia da semana (ex: "dia 23, sexta-feira"), cruzar com o calendário real do
   mês/ano em questão antes de usar a data — é o jeito mais confiável de pegar conteúdo
   reindexado de anos anteriores que passaria despercebido só pelo texto.
4. **Se a agenda do mês não estiver publicada, não inventar**: registrar na
   watchlist (ver seção 6). Esta regra tem prioridade sobre qualquer meta de
   cobertura da seção 9.
5. **Casas com agenda contínua (JazzB, Blue Note, Cine Joia, entre outros) devem ter
   TODOS os eventos do mês registrados individualmente — sem resumir, sem escolher só
   "os mais notáveis" para caber no app.** Se o site oficial lista 25 shows no mês, o
   `WEEKS` tem 25 entradas para aquela casa (distribuídas na semana de cada data), não
   uma linha genérica tipo "confira a agenda completa no site". Isso vale mesmo que o
   resultado fique visualmente denso — completude vem antes de economia de espaço.
6. Instagram: só posts públicos individuais que o usuário/pesquisa passar como link —
   perfis inteiros costumam bloquear sem login.
7. Para Sesc, tentar o padrão `unidade.sescsp.org.br/programacao/?data=MM/YYYY`
   quando disponível, mas validar se retornou dado real antes de usar.
8. Puxar a atração/obra principal para o início do campo `desc` (ver seção 5.1).

## 5. Estrutura de dados (não alterar o formato)

```js
{ id: "e-slug-unico", date: "DD" ou "DD–DD", title: "Nome do evento",
  venue: "Nome do local", cat: "musica|teatro|expo|cinema|feira",
  desc: "1-2 frases com o dado mais interessante (artista convidado,
  preço especial, motivo de ser destaque)", highlight: true|false }
```

Regras:
- Nunca reutilizar ou alterar um `id` de evento que permaneça no mês seguinte
  ou já tenha sido favoritado.
- `id` novo = `e-` + slug curto e descritivo.
- Categoria (`cat`) é sempre uma das cinco suportadas — um mesmo local pode
  ter eventos de categorias diferentes no mesmo mês (ex: CCBB com exposição
  E teatro), isso não é erro, é normal.

### 5.1 Atração principal no início do `desc`
Nas primeiras palavras do `desc`, priorizar o nome do artista/obra/diretor
central, não o contexto genérico. Ex: "Hamilton de Holanda (bandolim) estreia
repertório inédito..." em vez de "Show de música instrumental...".

### 5.2 Critério para `highlight: true`
6-8 eventos por mês, escolhidos por relevância real: raridade, exclusividade
(estreia/temporada curta), relevância nacional/internacional, ou proximidade
de casa. **Não existe cota obrigatória por critério** — se o mês tiver só 4
eventos genuinamente destacáveis, o app tem 4 destaques, não 6 forçados. Isso
vale mesmo quando a pesquisa da seção 4.5 traz dezenas de eventos de agenda
contínua: a maioria entra com `highlight: false` — a cota de 6-8 é sobre
relevância, não sobre volume de eventos coletados.

## 6. Seção "Fique de olho" (WATCHLIST)

Formato do item — curto, sem parágrafo explicativo:

```js
{ name: "Nome do local ou item", note: "Frase de até ~6 palavras dizendo por
que não entrou (agenda não publicada / bloqueado / dados não batem)", url: "link
direto para a página onde o leitor pode checar por conta própria" }
```

Se não houver uma página única para linkar (ex: um grupo de feiras sem site
comum), deixar `url: ""` — o app já trata isso e não renderiza o link vazio.

Regras:
- Só entram locais **confirmadamente** sem programação publicada até a data da
  busca, ou com dado que não pôde ser validado (ex: datas que não batem com o
  calendário do ano). Nunca usar a watchlist para disfarçar uma busca que
  simplesmente não foi feita — isso é erro metodológico, não achado.
- **Cada atualização deve re-verificar os itens que já estavam na watchlist da
  vez anterior — não apenas copiá-los.** Um local pode ter publicado a agenda
  desde a última rodada. Se a nota antiga for reaproveitada sem nova checagem,
  isso precisa ficar explícito no relatório da seção 9 (não pode ler como se
  fosse verificação fresca).
- Nota factual e específica, não genérica: "site não teve a data checada" é
  errado; "agenda de agosto não publicada" ou "bloqueado por proteção anti-bot"
  está correto.

## 7. Identidade do app (fixo)

- Nome do app: **Agenda Cultural SP**. Título visível no header: **Agenda
  Cultural — Centro de São Paulo** (não alterar a menos que pedido).
- `MONTH_LABEL`/`YEAR_LABEL` mudam a cada atualização; o nome e o título do
  app não.
- `LAST_UPDATED` reflete a data real da atualização, formato `DD/MM/AAAA`,
  sem contador de revisão.
- **Identidade visual "Modernist" (fixa a partir desta versão)**: fundo
  grafite (`#201e1d`) no header, tipografia Archivo (Google Fonts, pesos
  400/600/700/800) em caixa alta nos títulos, vermelho `#ec3013` como cor de
  destaque, fundo geral `#f3f2f2`. Grade de cards em `repeat(auto-fit,
  minmax(380px, 1fr))` — uma coluna em telas estreitas, duas ou mais em telas
  largas. Esse layout é fixo — não recriar do zero a cada atualização, só
  substituir os dados (`WEEKS`, `ONGOING`, `WATCHLIST`, `MONTH_LABEL`,
  `YEAR_LABEL`, `LAST_UPDATED`).

## 8. Priorização temporal

- Eventos na última semana de temporada (encerram em ≤7 dias) ganham nota
  "Últimos dias!" no início do `desc`.
- Eventos com datas múltiplas (ex: 06–08): mencionar no `desc` se algum dia
  específico tem preço especial ou atração extra, só quando for verdade.

## 9. Relatório de atualização (obrigatório ao final)

Ao fim de cada atualização, reportar ao usuário:

**✅ Locais confirmados** — quantos eventos por local.
**⚠️ Locais sem programação encontrada** — com nota factual do que foi
verificado (não "não encontrei nada", e sim "verifiquei X e a fonte diz Y").
Indicar explicitamente quais itens da watchlist foram re-checados nesta
rodada e quais foram apenas mantidos de uma rodada anterior sem nova checagem.
**🔍 Novos locais pesquisados nesta rodada** (se houver).
**📊 Estatísticas gerais** — total de eventos, destaques, fontes principais
consultadas.
**⚠️ Observações de acuracidade** — dado incerto, inferência feita, fonte
oficial fora do ar/substituída por alternativa.

Estas são **estatísticas descritivas do que foi encontrado**, não metas a
cumprir — se a cobertura real for menor que o esperado, isso deve aparecer
no relatório como está, não ser inflado.

---
