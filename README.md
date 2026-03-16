# PonderadaUX_D3.JS

É dividido por visualização de cada dupla.

## Visualização 1

**Arquivo:** `marco-henrique/marco-henrique.html`  
**Responsáveis:** Marco e Henrique

### Tema

Mapa operacional de focos de incêndio no Brasil, com bases de atendimento, focos ativos e rotas de resposta.

### O que a visualização mostra

- Bases operacionais distribuídas por estados.
- Focos de incêndio com diferentes níveis de prioridade.
- Situação de atendimento de cada foco, distinguindo casos atendidos e pendentes.
- Rotas entre bases e focos já atendidos.
- Indicadores visuais de risco e pressão operacional por estado.

### Recursos implementados

- Mapa geográfico renderizado com `D3.js`.
- Carregamento de GeoJSON externo dos estados do Brasil.
- Projeção geográfica para posicionamento correto dos elementos no mapa.
- Botões de filtro por prioridade: crítica, alta, média e baixa.
- Tooltip com detalhes de cada foco ou base.
- Uso de cores, halos e rotas para reforçar leitura de risco e alocação.

### Trecho de código D3.js da dupla (Marco e Henrique)

```js
const projection = d3.geoMercator();
const geoPath = d3.geoPath(projection);

d3.json(brazilGeoJsonUrl).then(geojson => {
	projection.fitExtent([[30, 30], [width - 30, height - 30]], geojson);

	statePaths = mapLayer.selectAll(".state")
		.data(geojson.features)
		.join("path")
		.attr("class", "state")
		.attr("d", geoPath)
		.attr("fill", "#0f2233");

	drawBases();
	render();

	svg.call(
		d3.zoom()
			.scaleExtent([1, 7])
			.on("zoom", event => {
				root.attr("transform", event.transform);
			})
	);
});
```

### Imagem da visualização (Marco e Henrique)

![Visualização 1 - Marco e Henrique](marco-henrique/Captura%20de%20Tela%202026-03-16%20%C3%A0s%2000.04.32.png)

### Objetivo da solução

Permitir uma leitura rápida da operação, destacando quais focos são mais urgentes, quais já receberam atendimento e onde há maior concentração de risco.

## Visualização 2

**Arquivo:** `sarah-livia/ponderada.html`  
**Responsáveis:** Sarah e Lívia

### Tema

Mapa da cidade de São Paulo combinado com um grafo de despacho de recursos para ocorrências.

### O que a visualização mostra

- Distritos/subprefeituras de São Paulo como base cartográfica.
- Pontos do tipo rastreador, que funcionam como bases de recurso.
- Pontos do tipo ocorrência, que representam destinos de atendimento.
- Conexões entre origem e destino indicando envio de recurso.
- Tabela lateral com o resumo dos despachos realizados.

### Recursos implementados

- Leitura de arquivo GeoJSON local com os polígonos de São Paulo.
- Renderização do mapa com `d3.geoMercator()` e `d3.geoPath()`.
- Nós coloridos para diferenciar rastreadores e ocorrências.
- Setas e linhas para representar fluxo de atendimento.
- Filtro por tipo de recurso: brigadista, caminhão-pipa e veículo 4x4.
- Redimensionamento dos nós conforme a quantidade de recursos disponível.
- Popup com detalhes do ponto selecionado.

### Trecho de código D3.js da dupla (Sarah e Lívia)

```js
const projection = d3.geoMercator().fitSize([width, height], geojson);
const pathGenerator = d3.geoPath().projection(projection);

svg.append("g")
	.selectAll("path")
	.data(geojson.features)
	.enter()
	.append("path")
	.attr("class", "distrito")
	.attr("d", pathGenerator);

const nodes = svg.append("g")
	.selectAll("circle")
	.data(pontos)
	.enter()
	.append("circle")
	.attr("class", "node")
	.attr("cx", d => projection(d.coords)[0])
	.attr("cy", d => projection(d.coords)[1])
	.attr("fill", d => d.type === "rastreador" ? "#3498db" : "#e74c3c")
	.attr("r", 8);
```

### Imagem da visualização (Sarah e Lívia)

![Visualização 2 - Sarah e Lívia](sarah-livia/Captura%20de%20Tela%202026-03-16%20%C3%A0s%2000.04.15.png)

### Objetivo da solução

Mostrar de forma integrada a distribuição espacial das ocorrências e o fluxo de despacho dos recursos, facilitando a análise de origem, destino e tipo de atendimento.

## Como executar

Como os arquivos são HTML com D3.js, a forma mais simples de visualizar é abrir cada arquivo no navegador:

- `marco-henrique/marco-henrique.html`
- `sarah-livia/ponderada.html`

Se houver bloqueio de carregamento local no navegador, recomenda-se servir a pasta com um servidor HTTP simples.

## Verificação em relação ao enunciado

O enunciado pede:

1. Um arquivo `.md` documentando e explicando as visualizações geradas, indicando a dupla responsável por cada uma.
2. Os arquivos e códigos das visualizações desenvolvidas em D3.js.

### Status atual

- Item 1: agora atendido por este `README.md`.
- Item 2: atendido, pois os arquivos HTML com D3.js e o GeoJSON de apoio estão no repositório.

## Observação

Na visualização de `marco-henrique/marco-henrique.html`, o mapa do Brasil é carregado por URL externa. Isso funciona melhor com internet ativa. Já a visualização de `sarah-livia/ponderada.html` depende do arquivo local `saopaulo_subprefeituras_poligonos.geojson`, que já está incluído no projeto.
