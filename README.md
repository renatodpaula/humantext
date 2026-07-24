# ✍️ humantext

> Removes signs of AI-generated, machine-sounding writing from text — 52 patterns across structure, vocabulary, punctuation, rhetoric, voice, and agency.
> Based on Wikipedia's "Signs of AI writing" guide, extended with additional structural, rhetorical, and technical-leakage tells.

**[Claude Code](https://docs.claude.com/en/docs/claude-code) skill** · Markdown-based · Draft → audit → final rewrite loop

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Skill](https://img.shields.io/badge/Claude%20Code-Skill-8A2BE2)](https://docs.claude.com/en/docs/claude-code)
[![Wiki](https://img.shields.io/badge/docs-Wiki-blue)](https://github.com/renatodpaula/humantext/wiki)

🌐 **Languages / Idiomas:** **[English](#-english)** · **[Português](#-português)**

📖 **Full documentation:** [**Project Wiki →**](https://github.com/renatodpaula/humantext/wiki)

---

## 🇬🇧 English

### What is this?

`humantext` is a reusable **Claude Code skill** that edits text to remove the statistical fingerprints of LLM writing — the constructions, vocabulary, and rhythms that make a paragraph read as machine-generated instead of human-written. It does not just delete AI-isms; it rewrites around them while preserving meaning, register, and the author's voice.

The base of the skill is [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained by WikiProject AI Cleanup — patterns observed across thousands of AI-generated Wikipedia edits. On top of that, this skill adds patterns that Wikipedia's guide doesn't cover, since encyclopedic prose and general/marketing/essay prose fail in different ways: rhetorical devices, structural artifacts, technical leakage, voice and agency problems, and absolute/emphasis words.

### Why 52 patterns and not one prompt

A single instruction like "make this sound human" doesn't work — the model doesn't know which of its own habits to distrust. This skill instead names the tell, shows a before/after, and states the fix as a rule, so the check is mechanical rather than a matter of taste. Isolated tells (one em dash, one "however," curly quotes) are explicitly **not** flagged — see `DETECTION GUIDANCE` in `SKILL.md`. Only clusters of tells indicate AI authorship.

### Pattern categories

| Category | Covers |
|---|---|
| Content patterns | inflated significance, promotional language, vague attributions, "-ing" superficial analysis |
| Language & grammar | AI vocabulary words, copula avoidance, negative parallelism, rule of three, false ranges, passive voice |
| Style patterns | em dashes, boldface overuse, inline-header lists, title case, emojis, curly quotes |
| Communication patterns | leaked chatbot scaffolding, knowledge-cutoff disclaimers, sycophantic tone |
| Filler & hedging | filler phrases, excessive hedging, generic conclusions, signposting, aphorism formulas |
| Rhetorical devices | rhetorical Q&A, manufactured suspense, analogy reflex, invented concept labels, anaphora, dead metaphor flogging, both-sidesing |
| Structural artifacts | fractal summaries, prompt echo, colon-split headings |
| Technical leakage | markdown residue in plain-text contexts, unfilled placeholders, leftover chatbot UTM parameters, clustered default names |
| Voice & agency | false agency (inanimate subjects doing human verbs), narrator-from-a-distance, telling instead of showing |
| Absolutes, adverbs & emphasis | lazy extremes (always/never/everyone), adverb crutches, emphasis crutches, Wh- sentence starters |

Full detail, before/after examples, and the complete vocabulary swap list live in `SKILL.md`. An optional 1-10 × 5-dimension quick-score rubric (Directness, Rhythm, Trust, Authenticity, Density) is also in there, for triaging a lot of text before doing a full pattern pass.

### How it works

1. Read the input, identify every instance of the patterns above.
2. Write a **draft rewrite** — reads naturally aloud, varies sentence length, prefers plain constructions.
3. Ask "what makes this still obviously AI generated?" and list the remaining tells.
4. Revise into a **final rewrite** that addresses them, with zero em/en dashes.

The skill also carries an explicit `REWRITING PITFALLS` section: don't invent facts to fake concreteness, don't over-swap vocabulary into weird synonyms, don't scatter typos to fake casualness, don't scrub personality along with the tells.

### Voice calibration (optional)

Give it a writing sample and it matches sentence length, word-choice level, punctuation habits, and verbal tics from the sample instead of defaulting to a generic "natural" voice.

### Installation

This is a Claude Code skill. Clone it into your skills directory:

```bash
git clone https://github.com/renatodpaula/humantext.git ~/.claude/skills/humantext
```

Then invoke it in Claude Code:

```
/humantext
```

Or just paste text and ask to "check this for AI tells," "make it not sound like AI," or "clean up this draft" — the skill triggers on intent.

### Repository structure

```
humantext/
├── SKILL.md      # the full skill: 52 patterns, voice calibration, process & output
├── README.md     # this file
└── LICENSE       # MIT
```

### Full documentation

The complete pattern-by-pattern reference, with every before/after example, lives in the [**Wiki**](https://github.com/renatodpaula/humantext/wiki).

---

## 🇧🇷 Português

### O que é isto?

`humantext` é uma **skill reusável de Claude Code** que edita texto pra remover as marcas estatísticas da escrita de LLM — as construções, o vocabulário e o ritmo que fazem um parágrafo soar gerado por máquina em vez de escrito por gente. Não só apaga os tiques de IA; reescreve em volta deles preservando sentido, registro e a voz do autor.

A base da skill é o [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), mantido pela WikiProject AI Cleanup — padrões observados em milhares de edições geradas por IA na Wikipedia. Em cima disso, esta skill adiciona padrões que o guia da Wikipedia não cobre, já que prosa enciclopédica e prosa geral/marketing/ensaio falham de jeitos diferentes: dispositivos retóricos, artefatos estruturais, vazamento técnico, problemas de voz e agência, e palavras absolutas/de ênfase.

### Por que 52 padrões e não um prompt só

Uma instrução única tipo "deixa isso mais humano" não funciona — o modelo não sabe de qual hábito próprio desconfiar. Esta skill nomeia o tique, mostra um antes/depois, e declara a correção como regra, então o check vira mecânico em vez de questão de gosto. Tique isolado (um travessão, um "porém", aspas curvas) explicitamente **não** reprova — ver `DETECTION GUIDANCE` no `SKILL.md`. Só cluster de tiques indica autoria de IA.

### Categorias de padrão

| Categoria | Cobre |
|---|---|
| Conteúdo | significância inflada, linguagem promocional, atribuição vaga, análise superficial em "-ing" |
| Linguagem & gramática | vocabulário de IA, fuga do verbo "ser/estar", negative parallelism, rule of three, falsos intervalos, voz passiva |
| Estilo | travessão, negrito em excesso, lista com cabeçalho inline, title case, emoji, aspas curvas |
| Comunicação | resquício de chatbot ("Aqui está...", "Espero que ajude"), aviso de knowledge-cutoff, tom bajulador |
| Enchimento & hedging | frase de enchimento, hedge excessivo, conclusão genérica, signposting, fórmula de aforismo |
| Dispositivos retóricos | Q&A retórico, suspense fabricado, reflexo de analogia, rótulo de conceito inventado, anáfora, metáfora flagelada, both-sidesing |
| Artefatos estruturais | resumo fractal, eco do prompt, título com dois-pontos |
| Vazamento técnico | markdown sobrando em texto puro, placeholder não preenchido, UTM de chatbot esquecido, nome-clichê de personagem inventado |
| Voz & agência | agência falsa (sujeito inanimado fazendo verbo de gente), narrador à distância, contar em vez de mostrar |
| Absolutos, advérbios & ênfase | extremo preguiçoso (sempre/nunca/todo mundo), muleta de advérbio, muleta de ênfase, início de frase com Wh- |

Detalhe completo, exemplos antes/depois e a lista de troca de vocabulário estão no `SKILL.md`. Uma rubrica opcional de score rápido (1-10 × 5 dimensões: Directness, Rhythm, Trust, Authenticity, Density) também está lá, pra triagem de bastante texto antes de rodar a passada completa.

### Como funciona

1. Lê o texto, identifica toda instância dos padrões acima.
2. Escreve um **rascunho** — soa natural em voz alta, varia tamanho de frase, prefere construção simples.
3. Pergunta "o que ainda deixa isso obviamente gerado por IA?" e lista os tiques restantes.
4. Revisa pra uma **versão final** que resolve isso, sem travessão nenhum.

A skill também carrega uma seção explícita `REWRITING PITFALLS`: não inventa fato pra fingir concretude, não troca vocabulário por sinônimo esquisito, não espalha erro de digitação fingindo casualidade, não apaga personalidade junto com o tique.

### Calibração de voz (opcional)

Dá uma amostra de escrita e ela casa tamanho de frase, nível de vocabulário, hábito de pontuação e tique verbal da amostra em vez de cair num "natural" genérico padrão.

### Instalação

Esta é uma skill de Claude Code. Clone no seu diretório de skills:

```bash
git clone https://github.com/renatodpaula/humantext.git ~/.claude/skills/humantext
```

Depois invoque no Claude Code:

```
/humantext
```

Ou só cole o texto e peça pra "checar tique de IA nisso", "tirar o cheiro de IA", ou "limpar esse rascunho" — a skill dispara por intenção.

### Estrutura do repositório

```
humantext/
├── SKILL.md      # a skill completa: 52 padrões, calibração de voz, processo & output
├── README.md     # este arquivo
└── LICENSE       # MIT
```

### Documentação completa

A referência completa padrão-por-padrão, com todo exemplo antes/depois, está na [**Wiki**](https://github.com/renatodpaula/humantext/wiki).

---

## 👤 Author / Autor

**Renato de Paula**

- 📧 Email: [renato@renatodpaula.com.br](mailto:renato@renatodpaula.com.br)
- 📸 Instagram: [@renatodpaula.ai](https://instagram.com/renatodpaula.ai)
- 🐙 GitHub: [@renatodpaula](https://github.com/renatodpaula)

## 📄 License / Licença

[MIT](LICENSE) © 2026 Renato de Paula
