# Como mexer neste site

Manual de manutenção do `index.html`. Escrito para você editar na mão, sem depender de mim e sem
instalar nada.

O site inteiro é **um arquivo só**: `index.html`, ~1,1 MB, 2.674 linhas. Dentro dele estão o HTML,
todo o CSS, todo o JavaScript, as quatro fontes, a pixel art e os quatro currículos em PDF. Não tem
build, não tem framework, não tem dependência. Você abre num editor de texto, muda, salva e sobe.

> **Editor recomendado:** VS Code. Ele numera as linhas, dobra os blocos e tem busca por `Ctrl+F`.
> O manual todo é baseado em **buscar um texto** e mexer ali — nunca em "vá para a linha N", porque
> o número muda a cada edição.

---

## Sumário

1. [Como o arquivo é organizado](#1-como-o-arquivo-é-organizado)
2. [As regras de ouro](#2-as-regras-de-ouro)
3. [Cores e a identidade visual](#3-cores-e-a-identidade-visual)
4. [Português e inglês](#4-português-e-inglês)
5. [Seção por seção: o que mudar e onde](#5-seção-por-seção-o-que-mudar-e-onde)
6. [O jogo](#6-o-jogo)
7. [A música](#7-a-música)
8. [A pixel art](#8-a-pixel-art)
9. [SEO](#9-seo)
10. [Os currículos](#10-os-currículos)
11. [Como publicar a alteração](#11-como-publicar-a-alteração)
12. [Receitas rápidas](#12-receitas-rápidas)
13. [Quando algo quebrar](#13-quando-algo-quebrar)

---

## 1. Como o arquivo é organizado

Na ordem em que aparece. A coluna "buscar" é o texto que você digita no `Ctrl+F` para pular direto
para lá.

| # | Bloco | Buscar | O que é |
|---|---|---|---|
| 1 | Cabeçalho e SEO | `<title>` | Título da aba, descrição, OpenGraph, dados estruturados |
| 2 | Fontes | `@font-face` | As 4 fontes em base64. **Não mexa.** É ~25% do arquivo |
| 3 | Tokens | `:root{` | As cores, os raios de borda, a largura máxima |
| 4 | CSS geral | `MOLDURA GERAL` | Menu, hero, seções, cards, tudo |
| 5 | CSS cyberpunk | `#cyber{` | O fundo com grade em perspectiva e neon |
| 6 | Menu | `<nav class="nav"` | A pílula flutuante do topo |
| 7 | Hero | `<header class="hero"` | O título grande e os três botões |
| 8 | 01 Skills | `<section id="skills"` | Os seis blocos de tecnologia |
| 9 | 02 Projetos | `<section id="projetos"` | O filtro e os 13 cards |
| 10 | 03 Imprensa | `<section id="imprensa"` | As 4 matérias |
| 11 | 04 Games | `<section id="arcade"` | A ficha, o jogo, a conquista, a faixa, o código |
| 12 | 05 Contato | `<section id="contato"` | Texto, botões e download dos CVs |
| 13 | JavaScript | `<script>` | Do idioma ao código secreto |
| 14 | Motor do jogo | `RUNNER INFINITO` | Física, obstáculos, pontuação |
| 15 | Música | `TRILHA 8-BIT` | A melodia e os efeitos |

**Regra prática:** os primeiros ~92% do arquivo são fontes, CSS, HTML e os PDFs. O JavaScript
inteiro está nos últimos 8%, a partir da linha ~1.770.

---

## 2. As regras de ouro

1. **Faça uma cópia antes de mexer.** `index.html` → `index-backup.html`. Custa 2 segundos e salva
   a tarde.
2. **Nunca mexa em nada que comece com `data:`.** São blocos gigantes em base64: as fontes, os
   sprites e os quatro PDFs dos currículos. Um caractere trocado quebra o arquivo. Se o VS Code
   mostrar uma linha com dezenas de milhares de caracteres, é uma dessas — pule.
3. **Toda mudança de texto vem em par.** Existe uma versão em português e uma em inglês. Ver a
   [seção 4](#4-português-e-inglês).
4. **Depois de salvar, abra o arquivo no navegador e aperte `F12`.** Se a aba *Console* estiver
   limpa, você não quebrou nada. Se aparecer texto vermelho, desfaça a última mudança.
5. **Aspas curvas quebram o código.** Se copiar texto do Word, ele troca `"` por `"` e `'` por `'`.
   Dentro do JavaScript isso dá erro. No texto visível, tudo bem.

---

## 3. Cores e a identidade visual

Buscar: **`:root{`**

Todas as cores do site saem daqui. Trocar uma linha muda o site inteiro.

```css
:root{
  --bg:#040404;        /* fundo geral, o preto de fora */
  --frame:#0a0a09;     /* a moldura arredondada       */
  --surface:#111110;   /* fundo de card e painel      */
  --surface-2:#171715; /* card quando o mouse passa   */
  --line:#232321;      /* borda discreta              */
  --line-2:#2f2f2c;    /* borda um pouco mais forte   */
  --text:#f2f1ee;      /* texto principal             */
  --text-2:#a9a8a1;    /* texto secundário            */
  --muted:#9d9b93;     /* texto de apoio              */
  --faint:#84827a;     /* texto bem fraco             */
  --yellow:#FFDD33;    /* o amarelo da marca          */
  --amber:#F5A524;
  --ember:#DE5B1F;
  --violet:#8B7BF0;
}
```

> ⚠ **Se mudar `--text`, `--muted` ou `--faint`, confira o contraste.** O site passou por auditoria
> WCAG 2.1 AA e essas três foram calibradas para isso. Cole a cor nova e o `--surface` em
> [webaim.org/resources/contrastchecker](https://webaim.org/resources/contrastchecker/): texto
> normal precisa de **4,5:1**.

### Cores dos neons do fundo

Buscar: **`--neon-c`**

```css
:root{ --neon-c:#22D3EE; --neon-m:#C86BF5; --neon-y:#FFDD33; }
```

### Cores das categorias de projeto

Buscar: **`.fl[data-f="games"]`**

```css
.fl[data-f="games"]{--fc:#FFDD33}   /* amarelo */
.fl[data-f="dados"]{--fc:#5FA8FF}   /* azul    */
.fl[data-f="ia"]{--fc:#F5A524}      /* laranja */
.fl[data-f="app"]{--fc:#B9B7AE}     /* neutro  */
```

Essa é só a bolinha do filtro. A cor do **card** vem do atributo `style` de cada projeto:

```html
<article class="card" id="p-2" data-cat="dados" style="--accent:#5FA8FF">
```

Se trocar a cor de uma categoria, troque nos dois lugares: no `.fl[data-f=...]` **e** em todos os
`style="--accent:..."` daquela categoria. Para achar todos, busque `data-cat="dados"`.

---

## 4. Português e inglês

O site tem os dois idiomas **no mesmo HTML**. O CSS esconde um e mostra o outro:

```css
[data-lang="pt"] .l-en, [data-lang="en"] .l-pt { display:none !important }
```

Na prática, todo texto aparece assim:

```html
<span class="l-pt">Projetos que eu construí</span>
<span class="l-en">Projects I built</span>
```

**Se você mudar só o `l-pt`, quem abrir em inglês vê o texto antigo.** Sempre mexa nos dois.

Para testar: abra `index.html?lang=en` no navegador, ou clique no `PT`/`EN` do menu.

### Título e descrição por idioma

O título da aba também troca com o idioma. Buscar: **`var META = {`**

```js
var META = {
  pt: { t: 'Pedro Albertasse — Engenheiro de Dados & IA | Data Engineer',
        d: 'Engenheiro de dados, IA aplicada e games. ...', loc: 'pt_BR', alt: 'en_US' },
  en: { t: 'Pedro Albertasse — Data & AI Engineer | Game and Tools Programmer',
        d: 'Data and automation engineer, ...', loc: 'en_US', alt: 'pt_BR' }
};
```

Mudou aqui? Mude também no `<title>` e na `<meta name="description">` lá em cima, que é o que
aparece antes do JavaScript rodar.

---

## 5. Seção por seção: o que mudar e onde

### Menu do topo

Buscar: **`<nav class="nav"`**

```html
<a class="nl" href="#skills"><span class="l-pt">Skills</span><span class="l-en">Skills</span></a>
```

Para tirar um item do menu, apague a linha `<a class="nl" ...>` inteira. Para renomear, mude o
texto dentro dos dois `<span>`. O `href="#skills"` tem que bater com o `id` da seção.

### Hero — o título grande

Buscar: **`<h1 class="display">`**

```html
<span class="ln"><span>Programador de jogos</span></span>
<span class="ln"><span>que virou engenheiro de dados.</span></span>
```

Cada `<span class="ln">` é uma linha e tem a animação de subida. **Se você acrescentar uma terceira
linha, copie a estrutura inteira**, incluindo os dois `<span>` aninhados — o de fora corta, o de
dentro sobe.

O parágrafo abaixo: buscar **`class="lede"`**. Os botões: buscar **`Ver os projetos`**.

### 01 Skills

Buscar: **`<section id="skills"`**

Cada bloco é assim:

```html
<div class="stk"><h4>Games</h4>
  <div class="row"><span class="tag">Unity</span><span class="tag">C#</span></div></div>
```

Para acrescentar uma tecnologia: copie um `<span class="tag">…</span>` e troque o texto.
Para acrescentar um bloco inteiro: copie um `<div class="stk">…</div>` inteiro. São 3 por linha no
desktop, então múltiplos de 3 ficam mais bonitos (hoje são 6).

### 02 Projetos

Buscar: **`<section id="projetos"`**

Cada card tem esta forma:

```html
<article class="card" id="p-2" data-cat="dados" style="--accent:#5FA8FF">
  <button class="card-head" aria-expanded="false" aria-controls="b-p-2">
    <span class="ch-top"><span class="idn">02</span><span class="ch-sign"></span></span>
    <h3>… título …</h3>
    <p class="role">… FLOW · o que você fez …</p>
  </button>
  <div class="card-body" id="b-p-2" hidden>
    … parágrafo, lista, métricas, imagens …
  </div>
  <div class="tags"><span class="tag hl">BigQuery</span>…</div>
</article>
```

Regras deste bloco:

- **`id="p-2"` e `aria-controls="b-p-2"` precisam casar.** O `id` do corpo é sempre `b-` + o id do
  card. Se duplicar um card para criar outro, troque os dois.
- **`data-cat`** define a categoria e o filtro: `games`, `dados`, `ia` ou `app`.
- **`--accent`** é a cor da borda de cima, do cargo e das tags destacadas.
- **`class="tag hl"`** deixa a tag colorida; **`class="tag"`** sozinha deixa neutra.
- Fechado, o card mostra só uma linha de tags. É de propósito, para a grade ficar regular.

Para **mudar o número do filtro** depois de acrescentar ou remover card, busque `class="fl on"` e
ajuste os `<span class="fl-n">13</span>`. Eles são escritos na mão, não contam sozinhos.

### 03 Imprensa

Buscar: **`<section id="imprensa"`**

Cada matéria é um `<article class="pr">`. O trecho `<div class="pr-from">` é a âncora que liga a
matéria ao projeto que gerou o dado:

```html
<div class="pr-from">
  <span class="l-pt">Saiu do meu estudo</span>
  <a href="#p-5">Trocas de CEO no Ibovespa</a>
</div>
```

O `href="#p-5"` tem que ser o `id` de um card existente na seção 02.

### 05 Contato

Buscar: **`<section id="contato"`**

E-mail: aparece **três vezes** no `index.html` — no `href="mailto:"`, no texto do botão e nos dados estruturados. Busque `albertasse.dev@gmail.com` e troque em todas.

---

## 6. O jogo

Buscar: **`RUNNER INFINITO`**

### Os números que controlam a dificuldade

Buscar: **`var G = 0.78`**

```js
var G = 0.78,      // gravidade. Maior = cai mais rápido, pulo mais curto
    PULO = -13.4,  // força do pulo. Mais negativo = pula mais alto
    ALT = 44,      // altura do herói em pé, em pixels
    BAIXO = 26;    // altura do herói abaixado
```

Buscar: **`jogo = { spd: 4.4`**

```js
var jogo = { spd: 4.4, ... };   // velocidade inicial
```

Buscar: **`jogo.spd = Math.min(11.5`**

```js
jogo.spd = Math.min(11.5, 4.4 + jogo.pts / 190);
//                  ↑ teto      ↑ base   ↑ quanto mais alto, mais devagar acelera
```

Buscar: **`jogo.pts = Math.floor(jogo.t / 6)`** — divide por 6: um ponto a cada 6 quadros, ou seja
10 pontos por segundo. Aumente o 6 para pontuar mais devagar.

### Quando os obstáculos nascem

Buscar: **`function nascerObstaculo`**

```js
var chaoAlto = jogo.pts > 90 && Math.random() < .28;
//                       ↑ a partir de 90 pontos      ↑ 28% de chance de vir voando

var n = jogo.pts > 160 && Math.random() < .3 ? (Math.random() < .35 ? 3 : 2) : 1;
//                 ↑ a partir de 160 pontos, fila de 2 ou 3 slimes

var base = 290 - Math.min(120, jogo.spd * 13);
jogo.prox = (base + Math.random() * 210) * ESC;
//           ↑ distância até o próximo. Menor = mais difícil
```

Buscar: **`function nascerMoeda`** para a frequência das moedas.

### A escala por largura de tela

Buscar: **`ESC = Math.max(.9`**

```js
ESC = Math.max(.9, Math.min(1.75, W / 720));
```

Isso multiplica a velocidade **e** a distância entre obstáculos, então o tempo de reação é o mesmo
num notebook e num monitor grande. Se mexer, mexa consciente: mudar só a velocidade deixa o jogo
injusto em tela larga.

### Quantas moedas liberam a conquista

Buscar: **`jogo.moedas === 5`**

### O tamanho da cena

Buscar: **`.field{position:relative`** → `height:230px` no desktop, `190px` no celular (logo abaixo,
dentro do `@media(max-width:640px)`).

### O código secreto

Buscar: **`var SEQ = `**

```js
var SEQ = ['ArrowUp','ArrowUp','ArrowDown','ArrowDown',
           'ArrowLeft','ArrowRight','ArrowLeft','ArrowRight','b','a'];
```

Se mudar a sequência, mude também os botões visíveis: buscar **`id="kkRow"`**.

---

## 7. A música

Buscar: **`TRILHA 8-BIT`**

Não existe arquivo de áudio. A música é gerada nota por nota pelo navegador, com a Web Audio API.
São três faixas, cada uma com 32 posições — cada posição é uma **colcheia**.

```js
var BPM = 132;                    // velocidade base
var LEAD  = [76,0,79,0, 81,0,79,76, …];   // melodia
var BAIXO = [45,0,45,45, 45,0,45,0, …];   // baixo
var PERC  = [1,2,0,2, 1,2,0,2, …];        // percussão
```

- Os números da melodia e do baixo são **notas MIDI**. `60` é o dó central, `69` é o lá do
  diapasão. Somar 12 sobe uma oitava, subtrair 12 desce.
- **`0` é silêncio.**
- Na percussão: **`1` = bumbo**, **`2` = chimbau**, **`3` = caixa**, `0` = nada.
- As três listas precisam ter o **mesmo tamanho**. Hoje são 32. Se quiser uma música mais longa,
  aumente as três juntas, em múltiplos de 8 para o compasso fechar.

Referência rápida de notas MIDI, oitava do meio:

| dó | ré | mi | fá | sol | lá | si |
|----|----|----|----|-----|----|----|
| 60 | 62 | 64 | 65 | 67  | 69 | 71 |

Para uma melodia melancólica, use lá menor: 69, 71, 72, 74, 76, 77, 79.
Para algo mais alegre, dó maior: 60, 62, 64, 65, 67, 69, 71.

### O volume

Buscar: **`MASTER.gain.value`** → `.5`. Vai de 0 a 1.

Volume de cada faixa: no `function agendar()`, o último número de cada `voz(...)`:

```js
if (LEAD[i])  voz(LEAD[i],  t, d * .9,  'square',   .16, 6);   // .16 = volume da melodia
if (BAIXO[i]) voz(BAIXO[i], t, d * 1.1, 'triangle', .30);      // .30 = volume do baixo
```

### O timbre

O quarto parâmetro do `voz(...)` é a forma de onda:

- `'square'` — quadrada, o som clássico de NES
- `'triangle'` — triangular, macia, boa para baixo
- `'sawtooth'` — dente de serra, áspera
- `'sine'` — senoidal, limpa e sem graça

### Os efeitos

Buscar: **`function sfxPulo`**, **`function sfxMoeda`**, **`function sfxBatida`**.
Cada um é curto e comentado. O do pulo, por exemplo, varre de 520 Hz a 1180 Hz em 90 ms.

### A música acelera junto com o jogo

Buscar: **`function durPasso`** — o passo da colcheia encurta conforme `jogo.spd` sobe. Trocar o
`30` por um número menor faz a música acelerar mais.

### O botão de som

Fica ligado por padrão e a escolha é lembrada no navegador. Para começar **desligado**, busque
**`pa_run_som`** e troque:

```js
somLigado = localStorage.getItem('pa_run_som') !== 'off';   // padrão ligado
somLigado = localStorage.getItem('pa_run_som') === 'on';    // padrão desligado
```

---

## 8. A pixel art

Cada sprite é um `<svg>` feito de retângulos de 1 pixel. Buscar: **`class="px"`**.

```html
<svg class="px" viewBox="0 0 16 16" width="16" height="16" shape-rendering="crispEdges">
  <rect x="5" y="0" width="6" height="1" fill="#141018"/>
  …
</svg>
```

- `x` e `y` são a posição no grid de 16×16, `fill` é a cor.
- Para **trocar a cor de um sprite** (a camisa do herói, por exemplo), ache o sprite e substitua
  todas as ocorrências daquele `fill`. No VS Code: selecione o hexadecimal e `Ctrl+D` seleciona a
  próxima igual.
- Para **desenhar um sprite novo**, o caminho realista é usar um editor de pixel art (Piskel,
  Aseprite), exportar em SVG e colar. Desenhar retângulo por retângulo na mão dá muito trabalho.
- O jogo usa os sprites `hero-a`, `hero-b`, `slime`, `orb` e `coin`. Eles vivem em
  `window.__SPR` — buscar **`window.__SPR`**. É um objeto JSON com o SVG de cada um.

> ⚠ O SVG dentro do `window.__SPR` **não tem `xmlns`** e não pode ter: ele é injetado na hora, e o
> motor do jogo adiciona o atributo quando converte para imagem. Se você colar um SVG com `xmlns`
> ali, não quebra, mas fica duplicado.

---

## 9. SEO

### O endereço do site

Aparece em cinco lugares. Se você mudar de endereço, troque em todos:

1. `index.html` → buscar **`rel="canonical"`**
2. `index.html` → buscar **`og:url`**
3. `index.html` → buscar **`hreflang`** (três linhas)
4. `robots.txt` → a linha `Sitemap:`
5. `sitemap.xml` → todas as `<loc>`

A página tem uma proteção: se detectar que está rodando em outro endereço, corrige o `canonical`
sozinha no navegador. Mas `robots.txt` e `sitemap.xml` são arquivos estáticos e precisam da troca
na mão.

### Dados estruturados

Buscar: **`application/ld+json`**

É um JSON com 10 entidades que descrevem quem você é para o Google e para assistentes de IA. Ele
está numa linha só, comprimido. **Se for editar, cole num formatador de JSON antes**
(`jsonformatter.org`) — um vírgula fora do lugar e o Google ignora o bloco inteiro.

Depois de mexer, valide em [validator.schema.org](https://validator.schema.org).

### `llms.txt` e `resume.json`

São arquivos separados, em markdown e JSON simples. Pode editar direto, são fáceis de ler.

---

## 10. Os currículos

Os quatro PDFs estão **duas vezes** no repositório:

- soltos em `cv/`, que é o que o `sitemap.xml` indexa;
- embutidos dentro do `index.html` como `data:application/pdf;base64,...`, que é o que os botões de
  download usam. São 414 KB dos 1,1 MB do arquivo.

**Para trocar um currículo você tem que trocar os dois.** O de dentro do HTML é um bloco base64 de
uns 110 mil caracteres — não dá para editar na mão.

Se quiser só substituir o arquivo em `cv/` e fazer os botões apontarem para lá, é simples: busque
`data:application/pdf;base64,` e troque o valor inteiro do `href` por `cv/CV-Pedro-Albertasse-Dados-PT.pdf`.
O arquivo fica bem menor. A contrapartida é que a página deixa de funcionar sozinha se você mandar
só o `index.html` por e-mail.

**Os `.docx` em `cv-docx/`** são independentes: pode abrir no Word, editar e subir por cima.

---

## 11. Como publicar a alteração

O site está em **github.com/Xigante/Xigante.github.io** e a publicação é automática: qualquer
commit no branch `main` vai para o ar em 1 a 2 minutos.

**Pelo navegador**, que é o jeito mais simples:

1. Abra o repositório no GitHub.
2. Clique no arquivo que quer trocar → ícone de lápis → cole o conteúdo novo → *Commit changes*.
3. Ou, para trocar o arquivo inteiro: **Add file → Upload files**, arraste o `index.html` novo,
   escreva o que mudou e *Commit changes*.
4. Espere o ponto amarelo virar verde. Recarregue `xigante.github.io` com `Ctrl+Shift+R` para
   furar o cache.

**Se o site não atualizar:** é cache. `Ctrl+Shift+R` no Windows, `Cmd+Shift+R` no Mac. Se ainda
assim, abra em janela anônima.

---

## 12. Receitas rápidas

**Trocar o amarelo do site inteiro**
Buscar `--yellow:#FFDD33` → troque o hexadecimal. Confira o contraste dos textos amarelos depois.

**Acrescentar um projeto novo**
Copie um `<article class="card">` inteiro, troque `id="p-14"` e `aria-controls="b-p-14"`, o
`data-cat`, o `--accent`, o número em `<span class="idn">14</span>`, o título, o cargo e as tags.
Depois ajuste os contadores do filtro.

**Tirar a seção do jogo**
Apague de `<section id="arcade"` até o `</section>` correspondente, e o item `<a href="#arcade">`
do menu. O JavaScript do jogo não quebra sem a seção: ele checa se os elementos existem antes de
rodar.

**Deixar o jogo mais fácil**
`PULO = -14.6` (pula mais alto) e, em `nascerObstaculo`, `var base = 340` (mais espaço entre
obstáculos).

**Trocar a música**
Reescreva `LEAD`, `BAIXO` e `PERC` mantendo o mesmo tamanho nas três. Comece mexendo só na `LEAD`.

**Mudar o e-mail**
Buscar `albertasse.dev@gmail.com` — aparece no contato (duas vezes), no `llms.txt`, no
`resume.json` e nos dados estruturados. Nos PDFs dos currículos não dá para trocar sem regerar.

---

## 13. Quando algo quebrar

| Sintoma | Causa provável | Como resolver |
|---|---|---|
| Página em branco | Erro de JavaScript | `F12` → *Console* → a mensagem diz a linha |
| Texto sumiu ao trocar de idioma | Mexeu só no `l-pt` ou só no `l-en` | Confira o par |
| Card não abre | `id` e `aria-controls` não batem | `id="p-N"` ↔ `aria-controls="b-p-N"` |
| Jogo não desenha nada | SVG do sprite inválido | `F12` → *Console* |
| Sem som | Navegador exige um clique antes | Clique em COMEÇAR; confira o botão ♪ |
| Filtro com número errado | `fl-n` é escrito na mão | Busque `class="fl-n"` e corrija |
| Google não atualiza | Cache do buscador | Search Console → *Inspecionar URL* → *Solicitar indexação* |

**O plano de emergência:** o GitHub guarda todas as versões. Abra o repositório → aba **Commits**
→ clique no commit anterior → *Browse files* → abra o `index.html` → *Raw* → salve. Você volta ao
estado exato de antes, sempre.

---

*Última atualização: 16 de agosto de 2026.*

---

# Triangulação de contato — o projeto 08

Este é o único projeto do portfólio que tem **repositório próprio e demo no ar**. Ele vive em
dois lugares e os dois precisam ser atualizados juntos.

## Os dois lugares

| Onde | O que serve | Como atualizar |
|---|---|---|
| `github.com/Xigante/triangulacao-c2c` | o código, os testes, a especificação, e o demo em `demo.html` | commit direto no repo |
| `xigante.github.io/demos/triangulacao-c2c.html` | uma cópia do mesmo demo, servida do portfólio | subir o arquivo em `demos/` |

A cópia existe porque o card do portfólio deve ter demo clicável mesmo que o outro repositório
saia do ar. **Se você mexer no demo, atualize as duas cópias** — senão o portfólio mostra uma
versão velha e o repo outra.

O link do card aponta para a versão do repositório (`xigante.github.io/triangulacao-c2c/demo.html`),
não para a cópia local. Isso é de propósito: quem clica cai no lugar onde também está o código.

## Como o demo é gerado

No repositório `triangulacao-c2c`:

```
gerar_dados.py    a base sintética de 22 pessoas fictícias
score.py          o motor: os cinco eixos
testes.py         38 testes — rode ANTES de publicar
build_demo.py     junta os dois e escreve demo.html
```

```bash
python3 testes.py      # tem que dar "✓ 38 testes passaram"
python3 build_demo.py  # reescreve demo.html
```

**Nunca edite `demo.html` à mão.** Ele é gerado. Toda edição manual se perde no próximo build.

### Mexer no ranking

Os pesos estão no topo do `score.py`, em `TETO`. Se mudar um peso, a normalização acompanha
sozinha (o total é dividido por `TETO_TOTAL`), mas **rode os testes**: vários deles fixam números
exatos e vão falhar de propósito, para você conferir se a mudança é a que queria.

Os vocabulários (`CORPORATIVO`, `NEGOCIO`, `SENIORIDADE`) são listas de termos. Acrescentar termo é
seguro. **Mudar a ordem de `SENIORIDADE` não é** — é escada de primeira-regra-que-casa, e trocar a
ordem reclassifica gente em silêncio.

### Mexer nas pessoas do demo

`gerar_dados.py` tem um comentário no topo com o checklist de cobertura: cada caminho da árvore de
decisão precisa de pelo menos uma pessoa que caia nele. Se você tirar alguém, confira o checklist —
o valor do demo é provar o motor inteiro, não desenhar cartões bonitos.

## A regra que não se negocia

**Nenhum dado real vai para nenhuma das duas cópias.** Nem nome de executivo, nem nome de colega,
nem número de projeto, nem nome de cliente, nem link de LinkedIn de terceiro, nem link de HubSpot.

O sistema real roda sobre base de candidatos com pessoas físicas identificadas. Publicar isso é
violação de LGPD com dano direto a terceiros — a pessoa descobre pelo Google que está na shortlist
de um concorrente.

Existe um script de barreira (`verificar.py`, fora do repositório) que varre os arquivos públicos
contra a lista de nomes reais e falha se achar qualquer um. Ele fica fora do repo porque carrega
justamente a lista que não pode ser publicada. Se você for republicar o demo com dados novos,
rode-o antes.

## Se precisar tirar a especificação do ar

A especificação completa do score, com pesos e limiares, está num arquivo só: `METODO.md`. Foi
deixada isolada de propósito. Apagar é um commit de um arquivo, e só o `README.md` e o `demo.html`
citam o nome dele — os dois em links, que viram 404 e não quebram nada.

---

# O fundo do hero — shooter em attract mode

O hero tinha um gradiente âmbar estático com quatro blobs desfocados. Agora tem um shooter
horizontal rodando atrás do texto. Três arquivos participam:

| Arquivo | O que faz |
|---|---|
| `src/page_naves.html` | o jogo inteiro: sprites, ondas, colisão, nebulosa, loop |
| `src/page_css3.css` | o fundo escuro do hero, a máscara do canvas, o texto claro |
| `src/sec_topo.html` | uma linha: `<canvas id="naves">` |

## Por que é horizontal

O hero é largo e baixo — uns 1900×650 num desktop. Shooter vertical deixaria dois terços da
largura vazios. Horizontal preenche o formato e a rolagem das estrelas da direita para a esquerda
dá sensação de voo para frente.

## As duas regras que sustentam o desenho

**1. A ação nunca acontece na banda do texto.** Os inimigos só nascem em duas faixas: `0.07–0.21`
e `0.80–0.93` da altura. O miolo, onde ficam a headline e o lede, fica livre. Além disso a máscara
CSS em `#naves` derruba o canvas para ~13% de opacidade no centro, então qualquer coisa que passe
por ali vira risco fantasma.

**2. A nave caça o inimigo mais próximo.** Isso não é capricho de IA — é o que mantém o tiro fora
do texto. O tiro nasce na altura da nave; se ela passeasse livre, riscaria a headline. Perseguindo
alvos que só existem nas faixas, ela fica nas faixas por consequência. Tem uma rede de segurança
também: `noTexto` bloqueia o tiro se a nave estiver entre `0.26` e `0.72` por qualquer motivo.

Se você mexer nas faixas, mexa nas duas coisas juntas — faixa e banda proibida.

## Mexer no jogo

Tudo que importa está no topo de `page_naves.html`:

- **`C`** — as cores. `motor` é o amarelo da marca; mudar ali muda o tiro e o rastro.
- **`MAPS`** — os sprites, como mapa de caracteres. Cada letra é uma cor em `COR`. Editar é
  desenhar em texto: acrescente linhas e colunas à vontade, o rasterizador se ajusta.
- **`onda()`** — as formações (`linha`, `v`, `onda`, `duplo`), quantos inimigos, a velocidade.
- **`relogio % 15`** no tiro — cadência. Menor = mais tiro.
- **`inimigos.length < 9`** — quantos cabem na tela. Subir isso vira borrão.

Não existe arquivo de imagem: os sprites são rasterizados no carregamento, num canvas offscreen, e
depois é só blit. Desenhar retângulo a retângulo a cada quadro sairia caro.

## O que protege a página

- `pointer-events:none` no canvas — o clique atravessa e chega nos três botões do CTA. Isso é
  testado; se você tirar, os botões param de funcionar.
- `IntersectionObserver` — para de gastar quadro quando o hero sai da tela. A página é longa.
- `visibilitychange` — para quando a aba perde o foco.
- `prefers-reduced-motion` — desenha 240 passos de uma vez, pinta um quadro e **não liga o loop**.
- Passo de tempo fixo de 16,667 ms — sem isso a nave anda mais rápido em monitor de 144 Hz.
- Densidade de estrela proporcional à área, e escala de pixel pela altura.

## A parte de performance, que valeu mais que o jogo

Medindo para conferir que o shooter não pesava, apareceu que a página **já estava lenta antes**:
7,7 fps em Chromium sem GPU. O shooter custava 0,5 fps — o problema era outro, e eram dois:

**`.mesh` no hero** — quatro elementos de ~55% da viewport com `filter:blur(84px)`, animados. Blur
é filtro de pintura: cada quadro repinta a camada inteira. Removidos. A nebulosa agora é um
`drawImage` de um canvas de 1/7 da resolução, onde o borrão sai do próprio upscale, de graça.

**`#cyber`** — camada `position:fixed` sempre visível, em toda a página, com três `blur(90px)` de
34–46vw animados e uma grade em perspectiva animando `background-position`. Animar
`background-position` num elemento mascarado e transformado força repaint de tela cheia a cada
quadro. Os três halos viraram `radial-gradient` estático no pai (um radial a 20% de opacidade já
*é* um halo borrado — o blur em cima não acrescentava desenho, só custo), e a grade passou a animar
por `transform`, que é composto na GPU e não repinta.

**Resultado: 7,7 → 60 fps na página inteira**, com o jogo rodando. Se você for acrescentar efeito
de fundo, meça antes e depois — `filter:blur` grande e animação de `background-position` são as
duas armadilhas que estavam aqui.
