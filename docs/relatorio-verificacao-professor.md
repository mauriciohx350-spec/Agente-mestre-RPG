# Relatorio de verificacao - Trabalho Avaliativo A1

Projeto: Santuário do Mestre - Agente de RPG com IA  
Equipe: Vitor Camillo e Mauricio Tolosa  
Fonte analisada: `C:\Users\vitor\Downloads\Eng_Prompt_Trab_Avaliativo_Segundo_A1_1.pdf`  
Data da verificacao: 18/06/2026

## 1. O que o professor pediu

O PDF solicita um trabalho em grupo com apresentacao e defesa, usando Node-RED para criar um agente de automacao com IA externa. O agente deve executar um fluxo completo:

```text
gatilho -> processamento -> decisao -> resposta
```

Requisitos principais:

- Criar um agente de automacao usando Node-RED.
- Integrar obrigatoriamente uma IA externa.
- Usar a IA como parte ativa na tomada de decisao do agente.
- Ter 1 componente obrigatorio de IA.
- Ter 1 componente de automacao, como ETL, API ou decisao.
- Ter 1 componente de saida, como interface ou resposta estruturada.
- Fazer com que a IA influencie diretamente na decisao do agente.
- Entregar fluxo do Node-RED exportado em JSON.
- Entregar arquivo HTML, se houver, ou demais codigos fonte.
- Entregar relatorio curto em PDF ou DOC contendo funcionamento, regras, prints, uso da IA e limitacoes.

O PDF tambem informa que a avaliacao considera:

- Funcionamento correto do agente: 25%.
- Clareza da logica e regras: 20%.
- Integracao com IA: 20%.
- Uso do Node-RED: 15%.
- Organizacao do fluxo: 10%.
- Documentacao do grupo: 5%.
- Trabalho em equipe: 5%.

## 2. Comparacao com o projeto entregue

| Pedido do professor | Situacao no projeto | Evidencia |
| --- | --- | --- |
| Fluxo em Node-RED | Atendido | `flows.json` contem endpoints, funcoes, chamadas HTTP e respostas. |
| Interface ou codigo fonte | Atendido | `formulario.html` contem a interface web e esta sincronizado no template do Node-RED. |
| IA externa obrigatoria | Atendido com pendencia de configuracao | O fluxo chama Google Gemini 2.5 Flash, mas a chave ainda esta como `SUA_CHAVE_API_AQUI`. |
| IA como parte ativa da decisao | Atendido na logica | O prompt de `/api/rpg` pede resultado, vida perdida, XP, ouro e narrativa. |
| Gatilho | Atendido | `GET /rpg`, `POST /api/introducao` e `POST /api/rpg`. |
| Processamento | Atendido | Nos function montam prompts e tratam respostas. |
| Decisao | Atendido | IA classifica resultado como sucesso, falha ou critico e calcula consequencias. |
| Resposta | Atendido | Interface web e JSON com narrativa/resultado. |
| Relatorio curto | Criado agora | `docs/relatorio-professor.pdf` e este arquivo Markdown. |
| Prints do funcionamento | Parcialmente atendido | `docs/design-preview.png` mostra a interface. Ainda e recomendavel adicionar print com Gemini funcionando apos configurar a chave. |

## 3. Veredito

O trabalho esta bem alinhado ao PDF do professor. A proposta de um Mestre de RPG com IA atende ao conceito de agente automatico, usa Node-RED como orquestrador, usa Gemini como IA externa e possui interface web.

O ponto critico antes da entrega final e configurar a chave real da API Gemini nos dois nos function:

- `Montar prompt`
- `Montar Prompt Introducao`

Enquanto a chave permanecer como `SUA_CHAVE_API_AQUI`, o fluxo nao funcionara com IA real no ambiente do professor. A interface possui uma previa local, mas essa previa nao substitui a execucao real exigida no PDF.

## 4. Nivel de complexidade estimado

Classificacao: Intermediario.

Justificativa:

- Nao e apenas uma chamada superficial de IA.
- A IA recebe contexto da campanha, interpreta acao do jogador e decide consequencias.
- O fluxo combina API, prompt, resposta estruturada e interface web.
- Ainda nao chega a avancado porque nao ha multiplas etapas complexas, persistencia de estado da campanha ou validacao de regras por rodada.

## 5. O que explicar na apresentacao

Resumo sugerido:

> Nosso agente se chama Santuário do Mestre. Ele funciona como um Mestre de RPG virtual. O jogador configura sistema, tom e local da aventura pela interface. O Node-RED recebe esses dados, monta um prompt com regras narrativas e envia para o Gemini. A IA gera a introducao ou interpreta a acao do jogador, decidindo resultado, consequencias, XP, dano, ouro e narrativa. O Node-RED interpreta a resposta e devolve para a interface.

Pontos para defender:

- O Node-RED orquestra o fluxo completo.
- A IA externa usada e Google Gemini.
- A IA influencia diretamente a decisao porque determina sucesso/falha/critico e consequencias.
- A saida aparece na interface e tambem pode ser estruturada em JSON.
- As regras do agente impedem a IA de controlar o jogador e limitam o tamanho/resposta.

## 6. Pendencias recomendadas antes da entrega

1. Configurar a chave Gemini real ou `global.get("GEMINI_API_KEY")` no Node-RED.
2. Rodar `http://localhost:1880/rpg` com o fluxo importado.
3. Gerar uma introducao real via Gemini.
4. Enviar uma acao real e confirmar que a resposta volta para a tela.
5. Tirar um print da resposta real funcionando e, se necessario, substituir ou complementar `docs/design-preview.png`.
6. Conferir se todos os integrantes enviarao o trabalho no Blackboard durante o periodo da aula.

