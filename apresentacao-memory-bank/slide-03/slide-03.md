# Slide 03 — Lembrar de nada ou de tudo: os dois falham

> **Seção:** 01 problema · o problema real

## Imagem do Slide

![Slide 03 - Lembrar de nada ou de tudo: os dois falham](slide-03.png)

## Fala Sugerida (Roteiro Melhorado)

Aí você pensa: 'é só jogar todo o histórico no contexto'. Só que já está provado — e a prática confirma — o efeito de *Context Rot*: quanto mais histórico e ruído você joga no prompt, pior o modelo raciocina. Então a gente fica preso entre dois extremos ruins: começar do zero sem saber nada, ou entupir o contexto e degradar a resposta. O desafio real não é guardar tudo, é escolher o que fica.

## Conteúdo na Tela

- **Card 1 (`// sem memória`):** **do zero** — Cada sessão do Devin CLI começa sem lembrar da anterior. O contexto só volta se eu repetir. *(Devin Docs - CLI e agente local)*
- **Card 2 (`// memória demais`):** **18 de 18** — modelos avaliados perderam desempenho conforme o input cresceu — mesmo em tarefas simples. *(Hong, Troynikov & Huber · Context Rot · Chroma, 2025)*
- **Destaque:** *O problema não é guardar. É escolher o que fica.*

## Nota / Roteiro Original

Sem memória o agente não sabe nada, e com tudo no contexto os modelos pioram. O problema é escolher o que fica.
