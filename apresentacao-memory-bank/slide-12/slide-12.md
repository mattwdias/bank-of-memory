# Slide 12 — Por dentro da skill: 7 arquivos

> **Seção:** 02 fluxo · anatomia da skill

## Imagem do Slide

![Slide 12 - Por dentro da skill: 7 arquivos](slide-12.png)

## Fala Sugerida (Roteiro Melhorado)

Por baixo do capô, a arquitetura separa bem o que é raciocínio do que é determinístico. O `SKILL.md` funciona como um roteador leve e os arquivos de referência só entram sob demanda para não gastar contexto. Todo o trabalho pesado — ler o banco local, checar cache, validar citações e filtrar dados sensíveis — fica num script Python com 46 testes. O LLM julga; o Python faz o mecânico.

## Conteúdo na Tela

- **Árvore (`.devin/skills/memory-bank/`):**
  - `SKILL.md` — o roteador (100 linhas: diz o que cada pedido faz e qual arquivo ler)
  - `references/` (sob demanda): `dream.md`, `cartao.md`, `saidas.md`, `metodologias.md`
  - `scripts/dream.py` (sem LLM) — o mecânico (~2000 linhas: janela, cache, digest, sensível, gates, git e board do ServiceNow)
  - `tests/test_dream.py` — a rede do mecânico (46 testes do `dream.py`)
- **Fora da skill (os dados):** `summaries/`, `sessions.db` e board do ServiceNow (só leitura) → `digests/` → `cartoes/` → `rascunho` → `devin-memory.md`.
- **Destaque:** *O LLM julga. O script faz o mecânico.*

## Nota / Roteiro Original

O SKILL.md é o roteador, cada reference tem o seu leitor, o dream.py faz o mecânico e os testes protegem o script. O LLM julga, o script executa.
