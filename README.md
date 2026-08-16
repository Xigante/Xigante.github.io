# Portfólio — Pedro Albertasse

**[xigante.github.io](https://xigante.github.io)**

Engenheiro de dados e automação. Bacharel em Programação de Jogos Digitais.
Português e inglês, no botão `PT`/`EN` do topo.

## O que é

Uma página só, escrita à mão, sem framework e sem build. Todo o CSS, o JavaScript, as fontes, a
pixel art e os quatro currículos em PDF estão dentro do `index.html`. Abrir o arquivo funciona,
inclusive offline.

```
index.html            a página inteira
COMO-MEXER.md         manual de manutenção: o que mexer e onde
llms.txt              resumo em markdown, padrão llmstxt.org
resume.json           currículo no padrão JSON Resume
cv/                   4 currículos em PDF (dados e games, PT e EN)
cv-docx/              os mesmos 4 em .docx, coluna única, para ATS
og.png · icon-512.png · manifest.webmanifest · robots.txt · sitemap.xml
```

## Mexer no site

**[COMO-MEXER.md](COMO-MEXER.md)** é o manual: mapa do arquivo, as cores num lugar só, como
acrescentar um projeto, os números que controlam a dificuldade do jogo, como reescrever a melodia,
e o que fazer quando quebrar.

## Detalhes que valem olhar

- **A pixel art é original.** Cada sprite é um mapa de caracteres compilado em retângulos SVG de
  1 px, gerado por script.
- **Tem um runner infinito jogável.** Clique em COMEÇAR: espaço pula, seta para baixo abaixa.
  Motor próprio em canvas, com passo de tempo fixo, colisão AABB, dificuldade progressiva e
  recorde salvo no navegador.
- **Tem código secreto.** ↑ ↑ ↓ ↓ ← → ← → B A.
- **A trilha é sintetizada na hora.** Não existe arquivo de áudio: melodia, baixo, percussão e
  efeitos saem da Web Audio API, nota por nota, e o andamento acelera junto com o jogo.
- **Acessibilidade auditada em WCAG 2.1 AA:** contraste de texto e de componente, alvo de toque
  de 44 px, navegação completa por teclado com foco visível, e `prefers-reduced-motion`
  desligando todas as animações.
- **Sem rastreador, sem cookie, sem analytics.** Nada sai do navegador de quem abre.

## Contato

albertasse.dev@gmail.com · [LinkedIn](https://www.linkedin.com/in/pedro-albertasse)

Aberto a freelance e projeto remoto em dados, IA aplicada e games.
