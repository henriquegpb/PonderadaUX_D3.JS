# Relatório da visualização — Mapa geográfico com rotas e camadas de risco

## 1. Pergunta que a visualização responde
A visualização foi construída para responder à seguinte pergunta do projeto:

**Quais focos estão sendo atendidos e quais ainda não estão sendo atendidos, considerando a prioridade da ocorrência?**

Essa pergunta é relevante porque o projeto busca apoiar a decisão de qual base deve responder a cada foco de incêndio, considerando múltiplas variáveis operacionais.

---

## 2. Por que escolhemos um mapa geográfico
A escolha de um mapa geográfico faz sentido porque o problema do projeto é fortemente espacial. A decisão operacional depende da localização do foco, da posição da base e da rota necessária para atendimento.

No mapa:
- cada **foco** aparece geograficamente posicionado;
- cada **base** aparece como origem de atendimento;
- as **rotas** mostram quais ocorrências já receberam alocação;
- os **halos de risco** destacam focos mais perigosos;
- a **cor do estado** resume a pressão operacional agregada.

Assim, a visualização facilita a leitura rápida da situação e ajuda a identificar gargalos.

---

## 3. O que cada elemento representa
### Bases
As bases são mostradas como triângulos com rótulo. Elas representam os pontos de origem dos recursos operacionais.

### Focos
Os focos são mostrados como marcadores circulares:
- **anel externo verde** = foco atendido;
- **anel externo vermelho** = foco pendente;
- **núcleo interno** = prioridade da ocorrência.

### Rotas
As rotas ligam a base ao foco apenas quando a ocorrência já está sendo atendida:
- linha contínua = resposta terrestre;
- linha tracejada = resposta aérea;
- linha pontilhada = resposta integrada.

### Camadas de risco
Cada foco possui um halo ao redor. Quanto maior o risco, maior a área visual ocupada. Isso ajuda a destacar rapidamente focos mais críticos.

### Painel lateral
O painel lateral resume:
- quantidade total de focos visíveis;
- quantos estão atendidos;
- quantos focos críticos/altos seguem pendentes;
- cobertura prioritária;
- lista ordenada dos focos por prioridade.

---

## 4. Relevância para o projeto
A visualização é relevante porque não mostra apenas onde os focos estão, mas também **o status operacional de atendimento**, que é uma questão central do projeto.

Ela ajuda a:
- identificar focos prioritários ainda sem resposta;
- perceber concentração de risco por região;
- visualizar rapidamente quais bases já foram acionadas;
- apoiar decisões de redistribuição de recursos.

---

## 5. Execução técnica em D3.js
O código foi implementado em **D3.js** com:
- carregamento de GeoJSON do Brasil;
- projeção geográfica;
- renderização de estados em SVG;
- camadas separadas para mapa, risco, rotas, bases e focos;
- filtro interativo por prioridade;
- tooltip com detalhes;
- zoom e pan para exploração.

A estrutura foi organizada para facilitar a troca dos dados fictícios por dados reais do algoritmo.

---

## 6. Decisões de design
Optamos por uma interface escura para aumentar contraste dos focos e das rotas. As cores foram escolhidas para separar claramente:
- prioridade;
- status de atendimento;
- tipo de resposta operacional.

Também foi criado um painel lateral para complementar o mapa com uma visão resumida da operação.

---

## 7. Limitações da versão atual
Esta versão utiliza **dados simulados** para demonstrar o conceito. Em uma versão conectada ao algoritmo, seria possível:
- atualizar os focos em tempo real;
- recalcular automaticamente a base ideal;
- exibir tempo estimado dinâmico;
- integrar clima, acessibilidade e disponibilidade de recursos.

---

## 8. Conclusão
A visualização escolhida atende bem ao objetivo do projeto porque transforma a decisão operacional em uma leitura visual rápida e acionável. Ela combina localização, prioridade, atendimento e risco em uma única tela, tornando mais fácil identificar onde agir primeiro.
