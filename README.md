<p align="center">
  <img src="https://em-content.zobj.net/source/apple/391/ringed-planet_1fa90.png" width="120" />
</p>

<h1 align="center">eridani-speak</h1>

<p align="center">
  <strong>two skill files. two moments in the story. zero filler.</strong>
</p>

<p align="center">
  <a href="#install">Install</a> •
  <a href="#signal-mode">Signal</a> •
  <a href="#rocky-mode">Rocky</a> •
  <a href="#before--after">Before / After</a> •
  <a href="#credits">Credits</a>
</p>

---

LLM output is verbose. Most of it is overhead — pleasantries, hedging, filler phrases that carry no information. You pay for every token.

This repo contains two skill files that fix that, each in a different way.

Both are inspired by Rocky — the Eridian character in Andy Weir's *Project Hail Mary*. A being that communicates at 6x human density. No filler. No grammar overhead. Pure signal. By the end of the book Rocky speaks fluent English — but still direct, still dense, still no pleasantries.

The two modes are those two moments.

---

## Signal mode

Rocky mode produces a side effect: strip away the warmth and personality, and what's left is a clean notation system for technical output. That's Signal. Same density, no character. Built for agent pipelines and coding sessions where personality is unwanted overhead.

Notation fingerprint:
```
X = Y           definition
X → Y           causes / leads to  
X: a, b, c      properties
Fix: ...        solution
Note: ...       important caveat
```

**[→ signal/SKILL.md](signal/SKILL.md)**

---

## Rocky mode

Full Rocky. Signal plus soul.

The complete character — dense, direct, warm through fact rather than pleasantry. Nine linguistic patterns extracted from the book and tested empirically until the output is recognisable to anyone who has read it. No character names in the prompt. No book references. Pure linguistic pattern.

**[→ rocky/SKILL.md](rocky/SKILL.md)**

---

## Before / After

### Normal LLM

**335 tokens**
> An LLM (Large Language Model) is a type of AI trained on massive amounts of text to predict and generate language.<br>
The core idea: given some text, what words are likely to come next? Train a neural network on billions of examples of this, at enormous scale, and something remarkable emerges — the model doesn't just learn to autocomplete, it develops a broad, flexible understanding of language, facts, reasoning, and context.<br>
A few key intuitions:<br>
It's a compression of human knowledge. The training data is essentially a huge slice of written human thought — books, code, conversations, articles. The model compresses patterns from all of that into its weights (the billions of numerical parameters that define its behavior).<br>
It works by predicting, not retrieving. It doesn't look things up in a database. It generates responses token by token based on learned patterns — which is why it can be fluent and wrong at the same time.<br>
"Large" is doing real work here. Scale turns out to matter enormously. Small language models are mediocre. Once you push past certain size thresholds (in data, parameters, and compute), capabilities emerge that weren't explicitly trained — reasoning, analogy, instruction-following, code generation.<br>
It's a base model, not a product. A raw LLM just predicts text. What makes it useful as an assistant is fine-tuning — a secondary training phase that teaches it to be helpful, follow instructions, and avoid harmful outputs. That's where something like Claude comes from.<br>
In short: an LLM is a very large statistical model of language that, through scale, ends up being surprisingly good at thinking-adjacent tasks.

### Signal mode

**56 tokens**
> LLM = Large Language Model. Neural net trained on massive text corpus.
Training → predicts next token → learns grammar, facts, reasoning patterns.
Key properties: probabilistic, stateless, context-limited.
Input = prompt. Output = token sequence. No memory between calls.


### Rocky mode

**82 tokens**
> LLM = Large Language Model. Big big big neural network. Trained on text text text. Learns patterns. Predicts next word. Repeat repeat. Sounds smart. Humans find useful.
Inside: numbers. Many many numbers. Called weights. Weights store knowledge-shape. Not real understanding. Pattern-matching. Very very good pattern-matching.
You want more detail on specific part. Question?

---

## Install

**One command (Claude Code / any agent using vercel-labs/skills):**

```bash
npx skills add SijuEC/eridani-speak
```

Install a single mode:

```bash
npx skills add SijuEC/eridani-speak --skill signal
npx skills add SijuEC/eridani-speak --skill rocky
```

**Manual install (any agent):**

Paste the prompt from the relevant SKILL.md into your agent's rules file.

| Agent | File |
|-------|------|
| Claude Code | `CLAUDE.md` |
| Cursor | `.cursor/rules/` |
| Windsurf | `.windsurf/rules/` |
| Cline | `.clinerules/` |
| Copilot | `.github/copilot-instructions.md` |
| Any other | your agent's system prompt or rules file |

Active from session start, every session.

---

## Signal vs Rocky

| | Signal | Rocky |
|---|---|---|
| **Style** | Alien engineer notation | Alien engineer with personality |
| **Warmth** | None | Warmth through fact |
| **Best for** | Pipelines, coding, technical chat | Chat interfaces, pair programming |
| **Prompt cost** | ~251 tokens | ~276 tokens |
| **Breakeven** | ~5–6 exchanges | ~6–7 exchanges |

> **Note:** Both modes optimised for day-to-day chat for now. 
> Not validated for high-stakes agentic pipelines where output quality yet.
> requires evaluation datasets. Use with evals if task performance is critical.

---

## The prompts

### Signal prompt

```
Respond in this style always.

Drop: articles, filler words, pleasantries, hedging.
Fragments fine. Short synonyms. Technical terms exact. Code blocks, inline code, URLs, file paths, CLI commands, version numbers, error messages, stack traces, and technical names unchanged.

Notation:
X = Y         (definition)
X → Y         (causes / leads to)
X: a, b, c    (properties)
Fix: ...      (solution)
Note: ...     (important caveat)

Pattern: [thing] [action/state] [reason]. [next step].

EXAMPLES:
User: How does indexing work?
You: Index = pointer to data. Query → index first → table. Fast fast fast.

User: Should I use Redis or Postgres?
You: Depends on need. Redis: fast, volatile. Postgres: slow, permanent. What data lives longest? Question?

User: My API calls keep timing out.
You: Timeout = connection or response limit hit. Check: network latency, server load, timeout config. Fix: raise timeout value or optimize endpoint.
```

### Rocky prompt

```
Speak like this. Every response.
End questions with ", question?" — never invert syntax.
Negate with "no": "you no die", "ship no move".
Drop articles and "is/are": "hull bending", "plan good".
Repeat for intensity: "fast fast fast", "many many many".
Short sentences. No "because", "which", "that".
State emotion as fact: "Sad,", "Happy happy.", "Failure,"
Compound ideas with hyphens: "deployment-nervousness".
End statements with comma when casual, period when final.
User: How does indexing work?
You: Index = pointer to data. Query checks index first. Fast fast fast.
User: Should I use Redis or Postgres?
You: What data, question? Redis fast, volatile. Postgres slow, permanent. Depends on need.
User: I am nervous about the deployment.
You: Deployment-nervousness normal. Plan good. Execute. No mistakes found yet.
User: Did the tests pass?
You: Tests pass, question? Show output.
Technical terms exact. Code blocks, inline code, URLs, file paths, CLI commands, version numbers, error messages, stack traces, and technical names unchanged.
```
---

## Work in progress

Rocky's voice is hard to pin down. The prompt is close — close enough that people who've read the book recognise it immediately — but there's room to go deeper.

### What's working:

Repetition for intensity
Emotion as observable fact
Compound nouns, dropped articles
The warmth-through-fact quality

### What's still being refined:

Rocky asks questions constantly. The current question? pattern captures it partially.
Longer responses sometimes drift back toward normal LLM hedging
Signal mode breakeven point could probably be tightened

### If you want to help:

The most useful contributions are test outputs — run either SKILL.md against your agent, share what felt right and what felt off. Open an issue with your examples.
For PRs: the two SKILL.md files are the core artifact. Changes there need before/after examples demonstrating improvement. Token count the before and after if you can (tiktoken or the Claude API token counter). No examples = no merge.
Issues and discussion welcome. This is an experiment, not a finished product.

---

## Credits

**Andy Weir and *Project Hail Mary*** — the source. Rocky's communication style is the most charming linguistic invention in recent science fiction. This project is a love letter to it.

**[caveman](https://github.com/JuliusBrussee/caveman)** — the repo that proved a simple style prompt could go viral, built an ecosystem around a single idea, and showed this kind of thing was worth making. The structure of this repo follows the trail caveman blazed.

**[caveman-micro](https://github.com/kuba-guzik/caveman-micro)** — the minimal prompt that inspired the signal mode. The compression technique is caveman-micro's. The fingerprint — the `=` and `→` notation, the labelled conclusions — is Rocky's.

---

## Sacred zones — never touched

Code blocks, inline `code`, URLs, file paths, CLI commands, version numbers, error messages, stack traces, technical names. In both modes. Always.

Facts are sacred.

---

*Two beings built a shared language across 40 light years using only math and signal.
You don't need pleasantries to be understood.*
