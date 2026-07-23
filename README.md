# ✍️ slop-check

> Removes signs of AI-generated writing ("AI slop") from text — 45 patterns across structure, vocabulary, punctuation, and rhetoric.
> Based on Wikipedia's "Signs of AI writing" guide, extended with tells from real-world AI-detector bypass research.
>
> Not affiliated with, and not to be confused with, other tools named "humanizer" (e.g. [blader/humanizer](https://github.com/blader/humanizer)).

**[Claude Code](https://docs.claude.com/en/docs/claude-code) skill** · Markdown-based · Draft → audit → final rewrite loop

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Skill](https://img.shields.io/badge/Claude%20Code-Skill-8A2BE2)](https://docs.claude.com/en/docs/claude-code)

🌐 **Languages / Idiomas:** **[English](#-english)** · **[Português](#-português)**

---

## 🇬🇧 English

### What is this?

`slop-check` is a reusable **Claude Code skill** that edits text to remove the statistical fingerprints of LLM writing — the constructions, vocabulary, and rhythms that make a paragraph read as machine-generated instead of human-written. It does not just delete AI-isms; it rewrites around them while preserving meaning, register, and the author's voice.

The base of the skill is [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained by WikiProject AI Cleanup — patterns observed across thousands of AI-generated Wikipedia edits. On top of that, this version adds patterns identified from AI-detector bypass research (rhetorical devices, structural artifacts, and technical leakage that Wikipedia's guide doesn't cover, since Wikipedia prose and general/marketing prose fail differently).

### Why 45 patterns and not one prompt

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
| Technical leakage | markdown residue in plain-text contexts, unfilled placeholders, leftover chatbot UTM parameters, clustered default names (Emily/Sarah) |

Full detail, before/after examples, and the complete vocabulary swap list live in `SKILL.md`.

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
git clone https://github.com/renatodpaula/slop-check.git ~/.claude/skills/slop-check
```

Then invoke it in Claude Code:

```
/slop-check
```

Or just paste text and ask to "check this for AI tells," "make it not sound like AI," or "humanize this" — the skill triggers on intent.

### Repository structure

```
slop-check/
├── SKILL.md      # the full skill: 45 patterns, voice calibration, process & output
├── README.md     # this file
└── LICENSE       # MIT
```

### A narrower sibling for sales copy

A separate, shorter checklist variant — still named `humanizer`, unrelated to this rename — lives at the user level (`~/.claude/skills/humanizer`), scoped specifically to customer-facing copy — WhatsApp/email outreach, landing pages, CTAs — where the deliverable is a pass/fail verdict with an exact correction, not a full rewrite loop. It shares the em-dash and negative-parallelism rules with this skill but skips patterns that don't apply to short commercial copy (fractal summaries, colon-split headings, etc.).

---

## 🇧🇷 Português

### O que é isto?

`slop-check` é uma **skill reusável de Claude Code** que edita texto pra remover as marcas estatísticas da escrita de LLM — as construções, o vocabulário e o ritmo que fazem um parágrafo soar gerado por máquina em vez de escrito por gente. Não só apaga os tiques de IA; reescreve em volta deles preservando sentido, registro e a voz do autor.

Não afiliado, e não deve ser confundido, com outras ferramentas chamadas "humanizer" (ex: [blader/humanizer](https://github.com/blader/humanizer)).

A base da skill é o [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), mantido pela WikiProject AI Cleanup — padrões observados em milhares de edições geradas por IA na Wikipedia. Em cima disso, esta versão adiciona padrões identificados em pesquisa de bypass de detector de IA (dispositivos retóricos, artefatos estruturais e vazamento técnico que o guia da Wikipedia não cobre, já que prosa de Wikipedia e prosa geral/marketing falham de jeitos diferentes).

### Por que 45 padrões e não um prompt só

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
| Vazamento técnico | markdown sobrando em texto puro, placeholder não preenchido, UTM de chatbot esquecido, nome-clichê de personagem inventado (Emily/Sarah) |

Detalhe completo, exemplos antes/depois e a lista de troca de vocabulário estão no `SKILL.md`.

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
git clone https://github.com/renatodpaula/slop-check.git ~/.claude/skills/slop-check
```

Depois invoque no Claude Code:

```
/slop-check
```

Ou só cole o texto e peça pra "checar tique de IA nisso", "tirar o cheiro de IA", ou "humanizar isso" — a skill dispara por intenção.

### Estrutura do repositório

```
slop-check/
├── SKILL.md      # a skill completa: 45 padrões, calibração de voz, processo & output
├── README.md     # este arquivo
└── LICENSE       # MIT
```

### Uma irmã mais enxuta pra copy de venda

Uma variante mais curta, em formato de checklist — ainda chamada `humanizer`, sem relação com essa renomeação — mora no nível de usuário (`~/.claude/skills/humanizer`), escopada especificamente pra copy cliente-facing — abordagem de WhatsApp/e-mail, landing page, CTA — onde o entregável é um veredito aprovado/reprovado com correção exata, não um loop completo de reescrita. Compartilha a regra de travessão e negative parallelism com esta skill, mas pula padrões que não se aplicam a copy comercial curta (resumo fractal, título com dois-pontos, etc.).

---

## 👤 Author / Autor

**Renato de Paula**

- 📧 Email: [renato@renatodpaula.com.br](mailto:renato@renatodpaula.com.br)
- 📸 Instagram: [@renatodpaula.ai](https://instagram.com/renatodpaula.ai)
- 🐙 GitHub: [@renatodpaula](https://github.com/renatodpaula)

## 📄 License / Licença

[MIT](LICENSE) © 2026 Renato de Paula
