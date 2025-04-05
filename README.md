# 🛢️ Análise Histórica da Produção de Petróleo Offshore no Brasil (2010–2024)

## 📑 Tabela de Conteúdos

- [Introdução](#introdução)  
- [Objetivo](#-objetivo)
- [Arquitetura e Pipeline de Dados](#arquitetura-e-pipeline-de-dados)  
- [Modelagem e Catálogo de Dados](#modelagem-e-catálogo-de-dados)  
- [Carga e Processamento com ETL](#carga-e-processamento-com-etl)  
- [Análises e Respostas](#análises-na-camada-ouro)  
- [Discussões e Insights](#discussões-e-insights)  
- [Repositório de Notebooks](#repositório-de-notebooks)  
- [Referências](#referências)  

---

## 🧭 Introdução

A produção de petróleo e gás offshore no Brasil — especialmente nas reservas do pré-sal — representa um dos maiores ativos energéticos do século XXI, com impacto direto na economia nacional, na segurança energética e no cenário geopolítico global. Entender a evolução, o comportamento produtivo e os padrões operacionais desses campos é fundamental para subsidiar decisões estratégicas, otimizar a gestão de recursos e apoiar políticas públicas.

Contudo, a análise desse tipo de dado apresenta desafios estruturais: a fragmentação dos arquivos, a necessidade de tratamento extensivo, e a ausência de uma base integrada que permita comparações históricas e análises avançadas. Os dados são disponibilizados pela **Agência Nacional do Petróleo (ANP)** em arquivos CSV mensais, com alto grau de granularidade, mas exigem pré-processamento rigoroso para que possam ser utilizados de forma eficiente.

Este projeto se propõe a resolver esse problema técnico e analítico através da construção de um pipeline estruturado em camadas, inspirado na arquitetura **medallion** (Bronze, Prata e Ouro), utilizando a plataforma **Databricks** como ambiente principal de desenvolvimento e execução.

Além do processamento e enriquecimento dos dados, o projeto também propõe uma abordagem analítica profunda, integrando métricas derivadas, visualizações e questionamentos estratégicos sobre a produção offshore brasileira. O resultado é uma base sólida e reutilizável para exploração, análise e tomada de decisão baseada em dados confiáveis.

A fonte dos dados é a **Agência Nacional do Petróleo (ANP)**, que publica mensalmente arquivos CSV com informações por poço produtor. Contudo, devido à exigência de captcha no site da ANP, os dados foram previamente baixados e incluídos neste repositório nas pastas organizadas por ano [`datasets/monthly_production/`](./datasets/monthly_production), viabilizando um pipeline de dados automatizado a partir dos arquivos locais.


## 🎯 Objetivo

O objetivo desta análise é transformar os dados brutos de produção de petróleo e gás em informações valiosas, que permitam compreender melhor o comportamento da produção nacional — com foco especial nos campos offshore.

A partir disso, buscamos responder perguntas estratégicas como:

- Quantos campos produtores estão ativos em cada estado e em cada bacia?
- Qual o número de campos offshore atualmente em produção?
- Quais são os campos offshore com maior produção de óleo nos últimos 12 meses da amostra?
- Como evolui a produção de óleo, gás natural e água nos importantes campos da Bacia de Campos Tupi, Sapinhoá e Jubarte?
- Qual é o perfil de maturação desses campos com base na produção acumulada?
- Como variam, ao longo do tempo, os índices GOR (Gas-Oil Ratio) e GOW (Gas-Over Water) nesses campos?

Estas perguntas orientam toda a etapa analítica e servirão como base para as respostas e interpretações discutidas na seção de Análise.


## 🏗️ Arquitetura e Pipeline de Dados

A arquitetura deste projeto foi construída com base no modelo **Medallion Architecture**, organizado em três camadas principais: **Bronze**, **Prata** e **Ouro**. Essa estrutura permite rastreabilidade, reprocessamento eficiente e separação clara entre dados brutos, tratados e analíticos.

A execução do pipeline foi feita na plataforma **Databricks**, utilizando notebooks em PySpark, aproveitando o suporte nativo à engine Delta Lake, ao versionamento de dados e à performance otimizada para leitura e escrita em grandes volumes.

### 🔸 Camada Bronze — Ingestão

- Leitura dos arquivos CSV mensais da produção por poço diretamente da pasta `datasets/monthly_production/`.
- Padronização da leitura usando `;` como delimitador e codificação `'latin-1'`, preservando os dados originais conforme disponibilizados pela ANP.
- Escrita em Delta Lake, com conversões mínimas de tipos e sem aplicação de regras de negócio.
- Objetivo: manter os dados íntegros e rastreáveis, servindo como "fonte da verdade".

### 🔸 Camada Prata — Limpeza e Estruturação

- Tratamento de dados faltantes, remoção de duplicatas e padronização de colunas.
- Conversões de unidades: produção de petróleo e gás padronizada para barris por dia (bbl/d) e m³/dia, conforme necessário.
- Separação em dois DataFrames principais: **produção por poço** e **características físico-químicas do óleo e gás**, permitindo flexibilidade para análises mais direcionadas.
- Escrita em Delta Lake com esquema estruturado e validado.

### 🔸 Camada Ouro — Enriquecimento e Métricas Derivadas

- Agregações temporais por campo, bacia, estado e tipo de fluido.
- Cálculo de métricas como:
  - Volume mensal (convertido de produção diária).
  - GOR (Gas-Oil Ratio) e GOW (Gas over Water).
  - Produção acumulada por campo.
- Integração dos dados em uma estrutura flat analítica, pronta para dashboards, exploração via SQL e análise visual.


Essa arquitetura garante escalabilidade, reutilização e facilidade de manutenção, permitindo que o pipeline seja adaptado para incluir novos dados mensais e que análises históricas possam ser reproduzidas com consistência. O modelo foi desenhado para suportar tanto análises exploratórias quanto estudos estratégicos mais aprofundados.


## Modelagem e Catálogo de Dados

A modelagem dos dados deste projeto adota uma arquitetura em camadas (Bronze, Prata e Ouro), com o objetivo de garantir rastreabilidade, qualidade e reutilização dos dados em análises futuras. 

Na camada Bronze, optamos por manter todas as colunas disponíveis, incluindo propriedades físico-químicas e frações de hidrocarbonetos, por se tratar de uma camada bruta que visa garantir a rastreabilidade completa dos dados originais. Já na camada Prata, colunas relacionadas à composição físico-química do óleo e frações de hidrocarbonetos foram omitidas. A decisão foi baseada no foco principal da análise, que está centrada na produção, sua evolução temporal e características operacionais.

### 🗂️ Catálogo de Dados

#### 🔹 Camada Bronze — `producao_db.bronze`

| Campo                          | Tipo     | Descrição                                                  |
|--------------------------------|----------|-------------------------------------------------------------|
| estado                         | STRING   | Estado de localização do poço                              |
| bacia                          | STRING   | Nome da bacia sedimentar                                   |
| nome_poco_anp                  | STRING   | Nome do poço segundo a ANP                                 |
| nome_poco_operador             | STRING   | Nome do poço segundo o operador                            |
| campo                          | STRING   | Nome do campo de produção                                  |
| operador                       | STRING   | Nome da operadora                                          |
| numero_contrato                | STRING   | Número do contrato do ativo                                |
| periodo                        | STRING   | Mês/ano da produção (formato texto)                        |
| oleo_bbldia                    | DOUBLE   | Produção de óleo em bbl/dia                                |
| condensado_bbldia              | DOUBLE   | Produção de condensado em bbl/dia                          |
| petroleo_bbldia                | DOUBLE   | Soma de óleo + condensado em bbl/dia                       |
| gas_natural_m3dia_assoc        | DOUBLE   | Gás associado (m³/dia)                                     |
| gas_natural_m3dia_nassoc       | DOUBLE   | Gás não-associado (m³/dia)                                 |
| gas_natural_m3dia_total        | DOUBLE   | Gás total produzido (m³/dia)                               |
| volume_gas_royalties_m3mes     | DOUBLE   | Volume de gás sujeito a royalties no mês (m³)             |
| agua_bbldia                    | DOUBLE   | Produção de água em bbl/dia                                |
| instalacao_destino             | STRING   | Nome da instalação de destino                              |
| tipo_instalacao                | STRING   | Tipo da instalação (FPSO, plataforma fixa etc.)            |
| tempo_producao_hspormes        | INTEGER  | Tempo de produção no mês em horas                          |
| periodo_carga                  | STRING   | Período de carga dos dados                                 |
| corrente                       | STRING   | Tipo de corrente do petróleo                               |
| grau_api                       | STRING   | Grau API do óleo                                           |
| fracao_destilados_lev_corte    | STRING   | Temperatura de corte de destilados leves                   |
| fracao_destilados_lev_vol      | STRING   | Volume de destilados leves                                 |
| fracao_destilados_med_corte    | STRING   | Temperatura de corte de destilados médios                  |
| fracao_destilados_med_vol      | STRING   | Volume de destilados médios                                |
| fracao_destilados_pes_corte    | STRING   | Temperatura de corte de destilados pesados                 |
| fracao_destilados_pes_vol      | STRING   | Volume de destilados pesados                               |
| perc_vol_metano                | STRING   | Teor de metano (% vol.)                                    |
| perc_vol_etano                 | STRING   | Teor de etano (% vol.)                                     |
| perc_vol_propano               | STRING   | Teor de propano (% vol.)                                   |
| perc_vol_isobutano             | STRING   | Teor de isobutano (% vol.)                                 |
| perc_vol_butano                | STRING   | Teor de butano (% vol.)                                    |
| perc_vol_isopentano            | STRING   | Teor de isopentano (% vol.)                                |
| perc_vol_npentano              | STRING   | Teor de n-pentano (% vol.)                                 |
| perc_vol_hexanos               | STRING   | Teor de hexanos (% vol.)                                   |
| perc_vol_heptanos              | STRING   | Teor de heptanos (% vol.)                                  |
| perc_vol_octanos               | STRING   | Teor de octanos (% vol.)                                   |
| perc_vol_nonanos               | STRING   | Teor de nonanos (% vol.)                                   |
| perc_vol_decanos               | STRING   | Teor de decanos (% vol.)                                   |
| perc_vol_undecanos             | STRING   | Teor de undecanos (% vol.)                                 |
| perc_vol_oxigenio              | STRING   | Teor de oxigênio (% vol.)                                  |
| perc_vol_nitrogenio            | STRING   | Teor de nitrogênio (% vol.)                                |
| perc_vol_gas_carbonico         | STRING   | Teor de gás carbônico (% vol.)                             |
| densidade_glp_gas              | STRING   | Densidade do GLP na fase gasosa                            |
| densidade_glp_liquido          | STRING   | Densidade do GLP na fase líquida                           |
| pcs_gp_kj_m3                   | STRING   | Poder calorífico superior (kJ/m³)                          |
| data_atualizacao               | STRING   | Data de atualização da linha de produção                   |

---

#### 🟦 Camada Prata — `producao_db.prata`

| Campo                          | Tipo       | Descrição                                             |
|--------------------------------|------------|--------------------------------------------------------|
| estado                         | STRING     | Estado de localização do poço                         |
| bacia                          | STRING     | Nome da bacia sedimentar                              |
| nome_poco_anp                  | STRING     | Nome oficial do poço (ANP)                            |
| campo                          | STRING     | Campo de produção                                     |
| operador                       | STRING     | Nome da operadora                                     |
| periodo                        | TIMESTAMP  | Mês de referência                                     |
| oleo_bbldia                    | DOUBLE     | Produção de óleo (bbl/dia)                            |
| condensado_bbldia              | DOUBLE     | Produção de condensado (bbl/dia)                      |
| petroleo_bbldia                | DOUBLE     | Produção total de petróleo (óleo + condensado)        |
| gas_natural_m3dia_assoc        | DOUBLE     | Produção de gás associado (m³/dia)                    |
| gas_natural_m3dia_nassoc       | DOUBLE     | Produção de gás não-associado (m³/dia)                |
| gas_natural_m3dia_total        | DOUBLE     | Produção total de gás (m³/dia)                        |
| volume_gas_royalties_m3mes     | DOUBLE     | Volume sujeito a royalties (m³/mês)                   |
| agua_bbldia                    | DOUBLE     | Produção de água (bbl/dia)                            |
| instalacao_destino             | STRING     | Nome da instalação de destino                         |
| tipo_instalacao                | STRING     | Tipo da instalação                                    |
| tempo_producao_hspormes        | INTEGER    | Tempo de produção no mês (em horas)                   |

---

#### 🟨 Camada Ouro — `producao_db.ouro`

| Campo                           | Tipo       | Descrição                                                  |
|----------------------------------|------------|-------------------------------------------------------------|
| estado                           | STRING     | Estado da instalação ou poço                               |
| bacia                            | STRING     | Nome da bacia sedimentar                                   |
| nome_poco_anp                    | STRING     | Nome oficial do poço                                       |
| campo                            | STRING     | Nome do campo de produção                                  |
| operador                         | STRING     | Nome da operadora                                          |
| periodo                          | TIMESTAMP  | Mês de referência                                          |
| instalacao_destino               | STRING     | Nome da instalação de destino                              |
| tipo_instalacao                  | STRING     | Tipo da instalação                                         |
| tempo_producao_hspormes         | DOUBLE     | Horas de produção no mês                                   |
| gas_natural_mmscf_assoc          | DOUBLE     | Gás associado (em MMSCF/dia)                               |
| gas_natural_mmscf_nassoc         | DOUBLE     | Gás não-associado (MMSCF/dia)                              |
| gas_natural_mmscf_total          | DOUBLE     | Gás total (MMSCF/dia)                                      |
| volume_gas_royalties_mmscf       | DOUBLE     | Volume de gás sujeito a royalties (MMSCF)                  |
| oleo_kbd                         | DOUBLE     | Produção de óleo (KBD)                                     |
| condensado_kbd                   | DOUBLE     | Produção de condensado (KBD)                               |
| petroleo_kbd                     | DOUBLE     | Produção de petróleo (óleo + condensado) em KBD            |
| agua_kbd                         | DOUBLE     | Produção de água (KBD)                                     |
| dias_no_mes                      | INT        | Número de dias no mês                                      |
| gas_natural_assoc_mmscf_mes      | DOUBLE     | Produção mensal de gás associado                           |
| gas_natural_nassoc_mmscf_mes     | DOUBLE     | Produção mensal de gás não-associado                       |
| gas_natural_total_mmscf_mes      | DOUBLE     | Produção mensal de gás total                               |
| volume_gas_royalties_mmscf_mes  | DOUBLE     | Volume mensal de gás sujeito a royalties                   |
| oleo_kb_mes                      | DOUBLE     | Produção mensal de óleo (mil barris)                       |
| condensado_kb_mes                | DOUBLE     | Produção mensal de condensado (mil barris)                 |
| petroleo_kb_mes                  | DOUBLE     | Produção mensal total de petróleo (mil barris)             |
| agua_kb_mes                      | DOUBLE     | Produção mensal de água (mil barris)                       |
| gor                              | DOUBLE     | Gas-Oil Ratio (m³/bbl ou MMSCF/KBD equivalente)           |
| gow                              | DOUBLE     | Gas-Over-Water Ratio (indicador analítico)                 |

---


## 📊 Camada Ouro – Análises e Métricas Derivadas

Na camada Ouro, transformamos os dados brutos em informações analíticas por meio de agregações, cálculos e visualizações. As análises realizadas incluem:

### 🔹 Análises Gerais

- Total de **campos produtores por estado**.
- Total de **campos produtores por bacia**.
- Número total de **campos offshore em produção**.

### 🔹 Análise Ampla da Produção Offshore Nacional

- Identificação dos **maiores produtores de óleo offshore** nos **últimos 12 meses da amostra**.
- Cálculo do **delta de produção de óleo** (crescimento ou declínio).
- Geração de um **ranking com os 10 maiores produtores offshore** do Brasil no período analisado.

### 🔹 Análises Focadas – Bacia de Campos (Tupi, Sapinhoá e Jubarte)

Analisamos três campos relevantes da Bacia de Campos para entender seu comportamento de produção:

- **Produção agregada por campo**:
  - Agregação da produção de óleo, gás natural e água somando todos os poços de cada campo por período.
  - Visualizações da evolução temporal da produção entre os três campos.

- **Produção acumulada por campo**:
  - Cálculo da produção acumulada de óleo para avaliação dos perfis de curva.
  - Identificação dos **estágios de maturação** de cada campo com gráficos comparativos.

- **Análise de GOR e GOW**:
  - Cálculo dos índices GOR (*Gas-Oil Ratio*) e GOW (*Gas-Over Water*) por campo e período.
  - Análise da evolução temporal desses índices com comparações entre Tupi, Sapinhoá e Jubarte.


## Carga e Processamento com ETL

Os dados utilizados neste projeto são provenientes da **Agência Nacional do Petróleo (ANP)**, que disponibiliza relatórios mensais de produção de petróleo, gás, água e derivados por poço. Entretanto, os arquivos originais exigem captcha para download, o que inviabiliza a automação direta da coleta e dificulta a replicação dos estudos. Para contornar essa limitação e viabilizar a replicabilidade dos processos, os arquivos foram previamente organizados e disponibilizados no repositório público do GitHub, com estrutura semelhante à da ANP, separados por ano e tipo de produção (`Mar` e `Pré-Sal`).

📁 [datasets/monthly_production](https://github.com/brainopensource/datascience-mvp/tree/main/datasets/monthly_production)

O código responsável pela ingestão dos dados pode ser encontrado no notebook:

📓 [`notebooks/scraper.ipynb`](notebooks/scraper.ipynb)

O Scraper gera dinamicamente os links por ano pra mar e pré-sal, carregando os CSVs em dataframes pandas, e apenas tem as colunas renomeadas para evitar problemas na criação de bancos de dados removendo espaços ou caracteres especiais. Também são concatenados alguns arquivos CSVs, pois o dado de Mar e do Pré-Sal não vem junto da fonte ANP. Mas isso é indiferente pois na tabela bronze do Banco de Dados será tudo uma única tabela, já que as colunas são as mesmas.



## Análises e Respostas


## Discussões e Insights


## Repositório de Notebooks


## Referências
