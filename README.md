# Projeto NetLogo – Agentes Racionais

Simulação multiagente de exploração e recolha de recursos, desenvolvida em **NetLogo** no âmbito do **Trabalho Prático 1 de Introdução à Inteligência Artificial (IIA), 2026/2027**.

O projeto estuda como a composição da população, a comunicação entre agentes e a distribuição dos recursos influenciam a recolha e entrega de recursos numa base comum.

## Autores

- **Ricardo Santos** — 2024117073
- **Marcelo Moreno** — 2024153039

## O modelo

O ambiente é uma grelha de **33 × 33 células**, com uma base central, obstáculos e recursos distribuídos de forma aleatória ou agrupada. Cada célula de recurso começa com **6 unidades**.

Existem dois tipos de agentes:

| Agente | Função | Perceção | Energia inicial |
| --- | --- | --- | --- |
| Explorador | Explorar o ambiente e comunicar localizações de recursos | Raio de 5 células | 220 |
| Coletor | Localizar, recolher e transportar recursos até à base | Raio de 2 células | 180 |

Os coletores transportam até **6 unidades** e recolhem uma unidade por tick. Quando a comunicação está ativa, os exploradores podem transmitir uma localização conhecida a coletores num raio de 2 células que ainda não tenham um destino.

As decisões usam perceção local, memória individual das últimas 150 posições e gestão de energia. O movimento evita obstáculos e favorece posições menos visitadas; quando existe um destino conhecido, considera também a distância até esse destino. Os agentes regressam à base para recarregar energia e, no caso dos coletores, depositar a carga.

### Legenda do ambiente

| Elemento | Representação |
| --- | --- |
| Terreno livre | Castanho |
| Obstáculo | Cinzento |
| Base | Azul |
| Recursos | Verde |
| Explorador | Azul-claro, forma de inseto |
| Coletor | Vermelho, forma de pessoa |

## Como executar

O modelo foi guardado com **NetLogo 7.0.4**. Utilize esta versão para acompanhar a configuração original.

1. Descarregue o repositório através de **Code → Download ZIP** e extraia os ficheiros, ou clone-o:
   ```bash
   git clone https://github.com/Ricardo2024117073/Projeto-NetLogo-Agentes-Racionais.git
   ```
2. Abra `TP1.nlogox` no NetLogo.
3. Configure os parâmetros na interface.
4. Clique em **setup** para criar o ambiente e os agentes.
5. Clique em **go** para iniciar a simulação; volte a clicar para a pausar.

Para iniciar uma nova simulação, clique novamente em **setup**. A execução termina quando atinge `max-ticks` ou quando já não existem agentes vivos.

### Parâmetros principais

| Parâmetro | Descrição | Valor guardado |
| --- | --- | --- |
| `n-exploradores` | Número inicial de exploradores | 5 |
| `n-coletores` | Número inicial de coletores | 5 |
| `n-recursos` | Número de células com recursos, sujeito ao espaço disponível | 80 |
| `percentagem-obstaculos` | Probabilidade percentual de uma célula elegível ser um obstáculo | 15 |
| `max-ticks` | Limite de passos da simulação | 700 |
| `comunicacao-ativa?` | Ativa a transmissão de localizações entre exploradores e coletores | Desativada |
| `distribuicao-recursos` | Distribuição `Aleatoria` ou `Agrupada` | `Aleatoria` |

**Nota sobre a interface:** o interruptor `modelo-melhorado?` está presente, mas não é consultado pelos procedimentos da versão atual. Alterá-lo não muda o comportamento implementado.

Os monitores mostram os recursos depositados, os recursos ainda no ambiente, o número de agentes vivos e a energia média de cada tipo de agente.

## Experiências com BehaviorSpace

O ficheiro do modelo inclui três experiências, com **30 repetições por configuração**:

| Experiência | Comparação |
| --- | --- |
| **E1 — População** | Proporções exploradores/coletores: 10/40, 20/30, 25/25, 30/20 e 40/10, com comunicação ativa |
| **E2 — Comunicação** | Comunicação desativada e ativada, com 40 exploradores e 10 coletores |
| **E3 — Distribuição de recursos** | Distribuição aleatória e agrupada, com 40 exploradores, 10 coletores e comunicação ativa |

Para executar uma experiência, abra o **BehaviorSpace** no menu **Tools**, selecione a experiência pretendida, reveja as configurações e escolha os ficheiros de saída.

As métricas registadas no final de cada execução são:

- Recursos depositados na base;
- Número de exploradores e coletores vivos;
- Recursos restantes no ambiente;
- Número de ticks.

### Reprodutibilidade

O modelo utiliza aleatoriedade e não define uma semente fixa, pelo que novas execuções podem produzir resultados diferentes.

E2 e E3 fixam 80 células de recursos, 8% de obstáculos e 700 ticks. Em E1, os parâmetros não definidos na experiência dependem dos valores atuais da interface. Além disso, E1 tem um limite BehaviorSpace de 800 passos, mas `go` também respeita `max-ticks`; confirme ambos antes de executar.

## Ficheiros do repositório

| Ficheiro | Conteúdo |
| --- | --- |
| [TP1.nlogox](TP1.nlogox) | Código, interface e experiências BehaviorSpace |
| [Relatorio_TP1_IIA_2026.pdf](Relatorio_TP1_IIA_2026.pdf) | Relatório do trabalho |
| [Resultados_Finais_IIA.xlsx](Resultados_Finais_IIA.xlsx) | Folha de cálculo com os resultados finais |
| `TP1 E1 - população-*.csv` | Exportações da experiência sobre a população |
| `TP1 E2 - Comunicação-*.csv` | Exportações da experiência sobre a comunicação |
| `TP1 E3 - Distribuição dos Recursos-*.csv` | Exportações da experiência sobre a distribuição de recursos |

Os ficheiros `*-table.csv` correspondem às exportações em tabela do BehaviorSpace e os `*-stats.csv` às exportações estatísticas. Consulte o relatório e a folha de cálculo para a análise dos resultados.

