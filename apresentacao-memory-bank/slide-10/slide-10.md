# Slide 10 — Fechou o ciclo? O repo aprende

> **Seção:** 02 fluxo · modo lite · por repositório

## Imagem do Slide

![Slide 10 - Fechou o ciclo? O repo aprende](slide-10.png)
![Slide 10 - Fechou o ciclo? O repo aprende](slide-10-alt.png)

## Fala Sugerida (Roteiro Melhorado)

Só que esperar até sexta-feira para aprender algo rápido sobre um repositório é muito tempo. Por isso, criei o modo *lite*. Toda vez que eu fecho um ciclo — abro um PR ou digo 'terminei' — ele leva poucos segundos para anotar no diário daquele repo o que foi feito e que padrão apareceu. Se um padrão se repete em dois ciclos fechados, ele avisa: 'isso aqui já está pronto para ir para o `AGENTS.md` do time'.

## Conteúdo na Tela

- **Exemplo (`.devin-dream/repos/<repo>.md`):** Registro da branch `feature/pac-buy`, feito, descoberta, pendente, padrão (`deploy-ordem`), doc, código e aviso: `Prontos para o AGENTS.md: deploy-ordem (2 ciclos)`.
- **Blocos:**
  - **quando roda · gatilho no `AGENTS.md`:** Um ciclo fechou: PR aberto, tasks 100%, validation PASS ou eu disse "terminei".
  - **o que lê:** Git, gh e a conversa atual. Nenhum transcript: leva segundos.
  - **o que grava:** Uma entrada no diário do repo. Padrões e lacunas de doc ficam contados.
  - **o que não faz:** Não edita `AGENTS.md` nem `README` e não commita. Só propõe, com PR.

## Nota / Roteiro Original

Esse é o modo rápido, por repo. Fechou um ciclo, ele anota em segundos, e um padrão que aparece em 2 ciclos vira proposta para o AGENTS.md.
