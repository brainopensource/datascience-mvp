# MVP Machine Learning para Previsão de Produção de Petróleo no Pré-Sal do Brasil

## Tabela de Conteúdos
- [Introdução](#introdução)
- [Desenvolvimento do Mínimo Produto Viável Machine Learning (MVP)](#desenvolvimento-do-mínimo-produto-viável-mvp)
- [Análises Estatísticas e Pré-processamento](#análises-estatísticas-e-pré-processamento)
- [Upstream do Pré-Sal do Brasil nos Últimos Anos](#upstream-do-pré-sal-do-brasil-nos-últimos-anos)
- [Possibilidades para Implementações Futuras](#possibilidades-para-implementações-futuras)
- [Conclusão](#conclusão)
- [Dados de Contato](#dados-de-contato)

## Introdução

O pré-sal brasileiro, uma vasta região de reservas de petróleo localizada abaixo de uma camada de sal no fundo do oceano, representa uma das maiores descobertas de petróleo da última década. A produção de petróleo no pré-sal tem se intensificado significativamente nos últimos anos, com destaque para a contribuição fundamental dessa região para a matriz energética do Brasil. Este projeto visa não apenas analisar a produção histórica, mas também desenvolver um modelo preditivo utilizando técnicas de machine learning para prever a produção de petróleo por campo, mês a mês, a partir de variáveis chave como produção de óleo, água, gás, GOW (Gas/Oil Water ratio) e GOR (Gas/Oil ratio), além do tempo total de produção individual de cada campo indicando potencialmente sua maturação.

## Desenvolvimento do Mínimo Produto Viável (MVP)

O notebook [Colab MVP Machine Learning](https://github.com/brainopensource/datascience-mvp/blob/main/MVP_Machine_Learning_%26_Analytics.ipynb) apresenta o desenvolvimento de um Mínimo Produto Viável (MVP) focado em previsão de produção de petróleo por campo utilizando machine learning, como parte do primeiro módulo da Pós-Graduação em Ciência de Dados e Analytics da PUC-Rio. Utilizando dados abertos fornecidos pela Agência Nacional de Petróleo (ANP), este projeto tem como objetivo construir um modelo preditivo capaz de estimar a produção mensal de petróleo por campo. O modelo será treinado com dados históricos, incluindo informações sobre a produção de água, gás, GOW, GOR e tempo de operação de cada campo de petróleo.

A proposta inicial envolve a aplicação de técnicas de machine learning para prever a produção futura de petróleo, utilizando um conjunto de variáveis preditoras, permitindo não apenas entender os padrões históricos, mas também fornecer estimativas valiosas para planejamento e operações futuras.

## Análises Estatísticas e Pré-processamento

Utilizando os conhecimentos da ultima sprint foi feito o pré-processamento dos dados e esse notebook do colab foi utilizado como auxílio para poder compilar a informação de maneira mais eficiente e prática, para então ser utilizado no notebook de Machine Learning eficientemente e focando na parte de Inteligencia Artificial, separando a parte de pré-processamento [Colab Auxiliar MVP Pré-Processamento](https://github.com/brainopensource/datascience-mvp/blob/main/MVP_An%C3%A1lise_de_Dados_e_Boas_Pr%C3%A1ticas.ipynb)

O pré-processamento dos dados foi uma etapa fundamental para garantir a qualidade dos modelos preditivos. As principais etapas realizadas foram:

- **Coleta de Dados**: Os dados de produção de petróleo, água e gás, além de GOW, GOR e tempo de operação, foram coletados de fontes confiáveis, incluindo os dados mensais da ANP.

- **Limpeza de Dados**: Foram realizadas limpezas para remover inconsistências, registros duplicados e valores ausentes. Este processo também envolveu a remoção de outliers e tratamento adequado das variáveis categóricas.

- **Conversão de Dados**: As variáveis temporais foram transformadas para permitir uma análise mais eficaz das séries temporais, incluindo a separação de dados por ano e mês.

- **Criação de Variáveis Derivadas**: Foram geradas novas variáveis para melhor representar as interações entre as variáveis preditoras, como a normalização das produções de gás e água para facilitar a modelagem.

- **Divisão de Dados**: Os dados foram divididos em conjuntos de treino e teste, para garantir que os modelos desenvolvidos fossem validados de forma adequada.

## Upstream do Pré-Sal do Brasil nos Últimos Anos

Nos últimos anos, o Brasil tem experimentado um crescimento significativo na produção de petróleo no pré-sal, com impactos diretos na economia e na matriz energética do país. A evolução da produção está intrinsecamente ligada ao uso de tecnologias inovadoras de exploração e à evolução das condições dos campos de petróleo.

- **Produção em Crescimento**: A produção de petróleo tem alcançado novos recordes, com destaque para as plataformas e campos de pré-sal.

- **Tecnologia e Eficiência**: O uso de tecnologias de ponta, como a perfuração em águas profundas e técnicas avançadas de análise de dados, tem otimizado a eficiência da produção.

- **Impacto Econômico**: O pré-sal tem gerado significativos recursos financeiros, com impactos positivos em diversos setores da economia, incluindo investimentos em infraestrutura e programas sociais.

- **Desafios Operacionais**: A indústria enfrenta desafios relacionados a variabilidade na produção, flutuação de preços internacionais e riscos operacionais em ambientes complexos.

## Possibilidades para Implementações Futuras

O desenvolvimento deste MVP oferece um ponto de partida para a aplicação de machine learning na previsão de produção de petróleo no Brasil. Com o uso de técnicas avançadas de modelagem, como regressão, árvores de decisão, redes neurais e séries temporais, pretendemos:

- **Previsão Mensal da Produção de Petróleo**: Estimar a produção de petróleo por campo de forma precisa, mês a mês, com base em variáveis como produção de água, gás, GOW e GOR.

- **Análise de Eficiência de Produção**: A partir das previsões, será possível analisar a eficiência de cada campo de petróleo e otimizar os processos de operação.

- **Identificação de Padrões e Anomalias**: Detectar padrões anômalos de produção e identificar potenciais falhas ou oportunidades de melhoria.

- **Aprimoramento de Modelos de Machine Learning**: Expandir o escopo de dados e explorar novas técnicas, como aprendizado de máquina profundo (deep learning), para melhorar a acurácia das previsões.

Este projeto visa fornecer uma base sólida para a construção de modelos de previsão mais robustos e aplicáveis no contexto real de operações de petróleo.

## Conclusão

Este MVP de previsão de produção de petróleo no pré-sal representa uma importante aplicação de técnicas de machine learning para um dos setores mais estratégicos da economia brasileira. O desenvolvimento e refinamento dos modelos preditivos permitirão um planejamento mais eficiente das operações e a otimização da produção de petróleo. Com as melhorias contínuas na análise de dados e no uso de algoritmos mais sofisticados, a previsão de produção pode se tornar uma ferramenta essencial para a gestão dos campos de petróleo no Brasil.

## Referências

- **Agência Nacional de Petróleo (ANP)**: [Consulta à Produção por Poço](https://cdp.anp.gov.br/ords/r/cdp_apex/consulta-dados-publicos-cdp/consulta-produ%C3%A7%C3%A3o-por-po%C3%A7o)
- **Dados Abertos da ANP**: [Produção de Petróleo e Gás Natural por Poço](https://www.gov.br/anp/pt-br/centrais-de-conteudo/dados-abertos/producao-de-petroleo-e-gas-natural-por-poco)

## Dados de Contato

- **LinkedIn:** [Lucas Rocha](https://br.linkedin.com/in/lucsrocha/pt)
