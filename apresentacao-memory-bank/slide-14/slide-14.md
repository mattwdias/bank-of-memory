# Slide 14 — Sessão nova, 8 perguntas da semana

> **Seção:** 03 resultado

## Imagem do Slide

![Slide 14 - Sessão nova, 8 perguntas da semana](slide-14.png)

## Fala Sugerida (Roteiro Melhorado)

Para testar se isso fazia diferença na prática, peguei uma sessão zerada e fiz 8 perguntas reais sobre o trabalho da semana — prazos de certificado, pipelines, GMUD. Sem memória, o agente acertou metade, levou quase 8 minutos e gastou 11,3 ACUs — que é a unidade de computação do Devin — porque ficou batendo cabeça e chamando ferramentas erradas. Com a memória carregada, ele acertou 8 de 8, caiu para 2 minutos e custou 1,7 ACU. Foi quase 4 vezes mais rápido e 7 vezes mais barato usando exatamente o mesmo modelo.

## Conteúdo na Tela

- **`devin -p` · sem memória:**
  - Acerto: **4,5 de 8**
  - Tempo: `7 min 48 s · 191 ferramentas`
  - Custo: **11,3 ACU**
  - Errou: certificado, pipeline e GMUD: "não sei".
- **`devin -p` · com `/memory-bank lembrar`:**
  - Acerto: **8 de 8**
  - Tempo: `2 min 10 s · 76 ferramentas`
  - Custo: **1,7 ACU**
  - Acertou: até o prazo do certificado: 05/12.
- **Destaque:** *Mesmo modelo, mesmas perguntas: a diferença é a memória.* (1ª tentativa sem memória: foi direto no MCP do GitHub, que eu corrigi em 4 sessões).

## Nota / Roteiro Original

Mesmo modelo, e com memória ele acertou tudo, cerca de 4x mais rápido e 7x mais barato. Sem memória, ele foi direto no MCP do GitHub, que eu tinha corrigido 4 vezes.
