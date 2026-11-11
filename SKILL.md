---
name: bank-of-memory
description: Dream do Devin CLI, inspirado no Dreaming do Devin web. É uma consolidação de memória ("sonho") que lê os resumos de sessão em %APPDATA%\Devin\cli\summaries, normaliza datas, junta, resolve contradições, poda e reindexa o memory bank em %USERPROFILE%\devin-memory.md, e mostra um relatório para aprovação antes de gravar. Use quando o usuário chamar /bank-of-memory ou pedir para fazer o dream, "sonhar", "consolidar a memória" ou "atualizar a memória".
---

# Bank of Memory: o dream do Devin CLI

O Devin CLI não guarda memória entre sessões, mas guarda um resumo de cada conversa. Esta skill é um dream: assim como o sono consolida o que vivemos no dia, ela transforma esses resumos num memory bank curto e confiável, que as próximas sessões leem antes de começar.

| Arquivo | Papel |
|---|---|
| `%APPDATA%\Devin\cli\summaries\` | entrada, só leitura |
| `%USERPROFILE%\devin-memory.md` | a memória, lida pelas sessões |
| `%USERPROFILE%\devin-memory.archive.md` | o que foi podado; as sessões não leem |
| `%USERPROFILE%\devin-memory.md.bak` | a versão anterior, para desfazer |

A memória precisa continuar pequena: se ela só crescer, piora o desempenho do agente que a lê (context rot). Por isso podar é tão importante quanto acrescentar.

## Fase 1: Orientar

1. Leia `devin-memory.md`, se existir. Anote a data da primeira linha ("consolidado até"), o número de linhas e os itens de "Contexto ativo" cujo prazo já passou.
2. Se o arquivo não existir, este é o primeiro dream: use só os resumos dos últimos 7 dias e crie a memória no formato abaixo.

## Fase 2: Coletar sinal

1. Liste os arquivos de `summaries` por data de modificação e use só os mais novos que "consolidado até". Se não houver nenhum, diga isso e pare.
2. Procure nos resumos, nesta ordem de prioridade:
   - **Correções do usuário:** "na verdade", "não é isso", "errado", "já falei", "para de".
   - **Decisões:** "vamos com", "decidimos", "fica assim", "troca para".
   - **Preferências:** "prefiro", "sempre", "nunca", "a partir de agora", "lembra que".
   - **Conhecimento do sistema e o que não funcionou:** serviços, repositórios, filas, armadilhas, tentativas que falharam.
3. Se forem muitos resumos, busque esses sinais em vez de ler cada arquivo inteiro.
4. Para cada achado, registre o fato, a data absoluta (a partir da data do resumo), a fonte (o nome do arquivo) e a confiança: **alta** se foi dito ou confirmado explicitamente, **média** se foi inferido.

## Fase 3: Consolidar

Aplique as operações nesta ordem:

1. **Normalizar datas:** converta datas relativas em absolutas a partir da data do resumo. Nunca grave "ontem" ou "semana passada".
2. **Juntar:** o mesmo fato vira uma entrada só, com a data e a fonte mais recentes.
3. **Resolver:** se um fato novo contradiz um antigo, substitua e anote `(atualizado em AAAA-MM-DD; antes: ...)`. Se não der para saber qual vale, mantenha o antigo e leve a dúvida ao relatório.
4. **Acrescentar:** o que é durável e ainda não está na memória.
5. **Podar:** retire o que é transitório e já resolvido (bugs corrigidos, tentativas superadas), o contexto ativo vencido e o que foi substituído. Na dúvida, não pode.
6. **Reindexar:** reescreva "Essencial" com os fatos que mais afetam qualquer sessão.

## Formato de devin-memory.md

```markdown
<!-- consolidado até: 2026-11-13 09:12 -->
# Memória do Devin CLI

## Essencial
- [PACs] Alias de Lambda muda nela e em quem a chama; o SQS pode estar em outro repo.

## Contexto ativo
- [PACs] Troca de alias nas Lambdas do fluxo em andamento [expira: fim da demanda]

## Sistema
- [2026-11-12] [PACs] O SQS que chama a Lambda X fica em outro repositório. (fonte: <arquivo>; confiança: alta)

## Decisões

## O que não funcionou

## Preferências
```

- No máximo 100 linhas no total e cerca de 150 caracteres por linha.
- "Essencial" tem até 10 itens, curtos, sem data nem fonte.
- "Contexto ativo" guarda o que só vale enquanto uma demanda está aberta, sempre com `[expira: ...]`.
- Nas demais seções, uma entrada por linha: `- [AAAA-MM-DD] [Demanda] Fato. (fonte: <arquivo>; confiança: alta|média)`. Use `[Demanda]` só quando a entrada for específica de uma.
- A primeira linha guarda a data de modificação do resumo mais novo que você leu.

## Fase 4: Revisar e gravar

1. Mostre o relatório (formato abaixo) e pergunte: **gravar, ajustar ou descartar?**
2. Se o usuário pedir ajuste, aplique e mostre de novo. Se descartar, não grave nada.
3. Se aprovar:
   - copie a memória atual para `devin-memory.md.bak`, sobrescrevendo a anterior;
   - acrescente as entradas podadas ao fim de `devin-memory.archive.md`, sob `## Dream AAAA-MM-DD`;
   - grave o novo `devin-memory.md`.
4. Verifique antes de encerrar: no máximo 100 linhas, nenhuma data relativa e nenhuma entrada duplicada. Se algo falhar, corrija.

## Relatório

```
Dream 2026-11-13 · 6 resumos lidos (desde 12/11 18:10)
Juntou 2 · Resolveu 1 · Podou 3 · Acrescentou 4 · Datas corrigidas 2
Memória: 64 → 61 linhas

NOVO    "[PACs] O SQS que chama a Lambda X fica em outro repositório" (resumo de 12/11)
PODADO  "Lambda Y com timeout ao subir" (resolvido em 12/11)
DÚVIDA  "deploy em homologação é automático" × "precisa de aprovação": qual vale?

Gravar, ajustar ou descartar?
```

Mostre no máximo 5 itens NOVO e 5 PODADO; o resto aparece só na contagem. Toda DÚVIDA aparece.

## Regras

- **Nunca altere nem apague** os arquivos de `summaries`.
- **Nunca grave sem a aprovação** do usuário.
- **Nada sensível:** não grave senhas, tokens, chaves, caminhos de certificados nem dados de clientes. Se aparecer algo assim num resumo, ignore e avise no relatório.
