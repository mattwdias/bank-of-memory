# Perguntas e Respostas (Q&A) — Apresentação Devin CLI (`memory-bank`)

## Validade dos resultados

- **"8 perguntas, 1 pessoa, 1 semana. Isso não prova nada."**
  É verdade, é um piloto e não um benchmark. Assuma isso logo, antes que alguém aponte. O que vale é o sinal: com o mesmo modelo, o acerto subiu de 4,5 para 8 e o custo caiu de 11,3 para 1,7 ACU. O próximo passo é repetir com mais gente e perguntas que não fui eu que escrevi.
- **"Você escreveu as perguntas sabendo o que estava na memória. Não é viciado?"**
  Pode ter viés, sim. As perguntas eram sobre fatos da semana, que qualquer sessão deveria conseguir descobrir sozinha. A sessão sem memória teve acesso a tudo (git, repos, ferramentas) e mesmo assim respondeu "não sei" em 3 delas.
- **"Quanto custa rodar o dream?"**
  Se não tiver o número, não invente. Diga que o map roda um subagente por sessão, mas usa cache: no dream de 23/11 foram 13 sessões novas e 25 reaproveitadas. Medir o custo por dream é um próximo passo.

## Segurança e dados (em banco, essas vão vir)

- **"Você está guardando conversas com dados sensíveis num arquivo?"**
  A skill não copia transcripts, ela só lê os que o Devin CLI já grava localmente. O que ela gera passa por um filtro que esconde senhas, tokens e chaves, e o script reprova cartões com dados sensíveis. Tudo fica na máquina do usuário. O próprio slide diz que o filtro é heurístico, então não prometa garantia.
- **"Como você acessa o ServiceNow? Isso é aprovado?"**
  É a pergunta mais delicada. A skill usa a sessão do próprio usuário: ela abre o Edge, você faz login e ela captura a sessão para ler o board. Ela só lê e só vê o que você já veria no navegador. Admita que o ideal é uma integração oficial (API com OAuth ou conta de serviço) e que esse é o caminho se escalar. Lembre também que a integração é opcional: sem ela, o dream funciona só com as conversas.
- **"E se a memória vazar ou alguém subir num repo?"**
  O `devin-memory.md` fica no perfil do usuário, fora dos repos. A skill nunca faz commit nem push. O que vai para o `AGENTS.md` passa por aprovação e PR, e o filtro de sensível roda antes.

## Confiabilidade

- **"LLM resumindo LLM. E se ele inventar um fato e eu gravar?"**
  Por isso existem 3 travas:
  1. Toda frase do cartão cita a mensagem de origem, e o script reprova citação de mensagem que não existe.
  2. Só vira padrão o que se repetiu em ciclos fechados.
  3. Nada entra sem o meu sim.
  Se algo errado passar, tem `.bak` para desfazer, archive do que foi podado e itens com data para expirar.
- **"E se a memória ficar desatualizada e o agente seguir uma regra velha?"**
  A cada dream ele resolve contradições: o fato novo substitui o antigo e a mudança fica marcada. O contexto ativo tem data de validade, e o que já está no `AGENTS.md` é podado para existir uma fonte só.
- **"Você usou Context Rot para dizer que contexto grande piora. Sua memória não vira o mesmo problema?"**
  É por isso que existe o limite de 100 linhas, cobrado pelo script. A memória carrega o essencial, e o detalhe fica nos cartões, que só são lidos sob demanda.

## Escolha de design

- **"Por que não usar RAG / banco vetorial?"**
  Markdown é auditável: eu leio, aprovo e edito, e qualquer agente lê. Com 100 linhas não é preciso busca. RAG resolve achar coisas num acervo grande, e o problema aqui era decidir o que vale guardar.
- **"Por que não usar a memória do Devin web?"**
  Ela não existe no CLI. O CLI tem só `AGENTS.md`, que é do time e manual. A skill aplica no CLI a mesma ideia do Dreaming.
- **"Por que semanal e não diário?"**
  O lite cobre o dia a dia, porque roda a cada ciclo fechado. O dream semanal acompanha o ritmo do sprint e dá distância para separar o que se repetiu do que foi ruído. Ele também roda quando eu peço, com a janela de datas que eu quiser.
- **"Revisar a memória toda semana não vira outra tarefa?"**
  É uma revisão de minutos: o relatório mostra só o que mudou (NOVO, PODADO, DÚVIDA) e eu respondo gravar, ajustar ou descartar. É bem menos trabalho do que repetir o mesmo contexto em toda sessão.

## Manutenção e escala

- **"São 2000 linhas de Python. Quem mantém? E se o Devin CLI mudar o formato?"**
  É o risco técnico real: a skill depende do formato dos transcripts e do `sessions.db`. A mitigação são os 46 testes e o fato de o dream continuar funcionando com só uma das fontes. Seja honesto: hoje quem mantém sou eu.
- **"Funciona para o time todo?"**
  Hoje é pessoal, de propósito. Levar ao time é opt-in: cada pessoa aprova o que sai e o padrão vira PR. O diário por repo já é o primeiro passo.
- **"Isso não vira monitoramento das pessoas?"**
  Essa é a do slide "Trabalho, não pessoas". A memória é do engenheiro, fica na máquina dele e nada sai sem aprovação dele. Ela registra o sistema e o trabalho, não avalia quem trabalhou.
- **"Fine-tuning com conversa interna? E o jurídico?"**
  Por isso está como "se aprovado" e é o último degrau. Só acontece com governança, aval do jurídico sobre os termos dos provedores e dado curado.

## Provocações filosóficas (boas para o bate-papo)

- **"No fim você criou um AGENTS.md com passos extras."**
  O `AGENTS.md` é o destino. O que faltava era o processo que descobre o que merece ir para lá, com prova, sem eu ter que lembrar.
- **"O agente deveria decidir sozinho o que esquecer."**
  Devolva a pergunta do último slide para a plateia. A sua posição: hoje, num banco, o humano decide, e talvez isso mude quando houver avaliação confiável.
