# MVP Análise de Dados e Boas Práticas para Pós-Graduação em Ciência de Dados e Analytics (PUC Rio) - Análise da Produção de Petróleo no Pré-Sal do Brasil.


## Tabela de Conteúdos
- [Introdução](#introdução)
- [Desenvolvimento do Mínimo Produto Viável (MVP)](#desenvolvimento-do-mínimo-produto-viável-mvp)
- [Análises Estatísticas e Pré-processamento](#análises-estatísticas-e-pré-processamento)
- [Upstream do Pré-Sal do Brasil nos Últimos Anos](#upstream-do-pré-sal-do-brasil-nos-últimos-anos)
- [Possibilidades para Implementações Futuras](#possibilidades-para-implementações-futuras)
- [Conclusão](#conclusão)
- [Dados de Contato](#dados-de-contato)


## Introdução

O pré-sal brasileiro, uma vasta região de reservas de petróleo localizada abaixo de uma camada de sal no fundo do oceano, representa uma das maiores descobertas de petróleo da última década. Desde sua exploração inicial, a produção tem se intensificado, destacando-se como um componente crítico para a matriz energética do Brasil. Este projeto visa analisar a produção de petróleo no pré-sal nos últimos anos, oferecendo uma visão detalhada das tendências e projeções futuras.


## Desenvolvimento do Mínimo Produto Viável (MVP)

Este notebook apresenta o desenvolvimento de um Mínimo Produto Viável (MVP) como parte do primeiro módulo da Pós-Graduação em Ciência de Dados e Analytics da PUC-Rio. Utilizando dados abertos recentes sobre a produção de petróleo e gás no Brasil, disponibilizados pela Agência Nacional de Petróleo (ANP), o objetivo deste projeto é aplicar técnicas de ciência de dados para explorar, processar e gerar insights iniciais, abrindo caminho para futuras análises de maior valor.

A proposta central é explorar os dados de produção de petróleo e gás na região do pré-sal a partir de 2020, com foco em estatísticas descritivas, pré-processamento e visualizações que destaquem as dinâmicas produtivas. O escopo inicial inclui operações de limpeza e organização dos dados, bem como a construção de insights preliminares sobre o setor de upstream, abordando a produção por poço e suas características específicas.

Este MVP não só contribui para uma maior compreensão da indústria de petróleo e gás no Brasil nos últimos cinco anos, como também estabelece uma base sólida para análises preditivas e avanços no uso de técnicas de machine learning em projetos futuros. Assim, o projeto serve tanto a propósitos acadêmicos quanto práticos, fornecendo uma visão inicial sobre a produção de petróleo no pré-sal e potencializando aplicações futuras.


## Análises Estatísticas e Pré-processamento

O pré-processamento dos dados é um passo crucial para garantir a precisão da análise. Este projeto envolveu as seguintes etapas:

- **Coleta de Dados**: Os dados de produção de petróleo foram coletados de fontes confiáveis, incluindo dados mensais de produção disponíveis pela ANP (Agência Nacional do Petróleo, Gás Natural e Biocombustíveis).

- **Limpeza de Dados**: As informações foram tratadas para remover inconsistências, valores nulos e registros duplicados.

- **Conversão de Dados**: As datas e colunas com valores de produção foram convertidas para o formato apropriado, facilitando a análise temporal.

- **Adição de Colunas**: Colunas para ano e mês foram adicionadas para permitir análises mais detalhadas por período.


## Upstream do Pré-Sal do Brasil nos Últimos Anos

Nos últimos anos, o Brasil tem experimentado um crescimento significativo na produção de petróleo no pré-sal. A produção diária aumentou de maneira consistente, refletindo o investimento contínuo em tecnologia e infraestrutura.

- **Produção em Crescimento**: O volume de petróleo produzido tem superado as expectativas, com algumas das maiores plataformas de produção contribuindo substancialmente para a oferta nacional.

- **Inovação e Tecnologia**: O uso de tecnologia avançada, como o sistema de perfuração em águas profundas, tem permitido a exploração mais eficiente dos reservatórios de petróleo.

- **Impacto Econômico**: A produção do pré-sal tem um impacto econômico significativo, contribuindo para a arrecadação de impostos e royalties que ajudam a financiar programas sociais e investimentos em infraestrutura.

- **Desafios**: Apesar do crescimento, o setor enfrenta desafios, como a flutuação dos preços do petróleo no mercado internacional e questões ambientais associadas à exploração do petróleo e questões geopolíticas.


## Possibibilidade para implementações futuras

Neste trabalho iremos nos preparar para construir modelos úteis para analisar a produção de petróleo e gás natural por poço no futuro, enquanto aplicamos as técnicas do curso. Por ser um MVP, temos um recorte dos últimos anos de produção apenas que poderá ser extendido para a produção histórica completa no futuro. Tal recorte captura as tendências mais recentes da indústria e nos permite explorar os fatores que influenciam a produtividade e a eficiência. A partir da aplicação de técnicas de ciência de dados, buscamos identificar padrões produtivos, anomalias e insights que possam otimizar a alocação de recursos e aumentar a eficiência e previsibilidade operacional e financeira.

A riqueza dos dados por poço oferece oportunidades significativas para análises detalhadas. Através de métodos estatísticos e, futuramente, de algoritmos de aprendizado de máquina, pretendemos explorar diversas aplicações, incluindo:

- Análise de Eficiência da Produção
- Geração de Curvas de Decaimento de Poços
- Classificação de Poços e Campos por Eficiência
- Previsão da Produção Total por Campo
- Previsão de Royalties

Essas análises iniciais geram insights valiosos para a gestão e a operação de poços e campos. O pré-processamento dos dados e a análise exploratória formam a base necessária para futuras implementações de machine learning, facilitando o desenvolvimento de modelos preditivos robustos e a criação de ferramentas analíticas capazes de fornecer uma visão mais profunda das dinâmicas de produção. Isso permitirá decisões mais assertivas e bem embasadas no contexto da produção de petróleo e gás natural no Brasil.

## Conclusão

Este projeto proporciona uma análise abrangente da produção de petróleo no pré-sal do Brasil, oferecendo insights valiosos sobre o desempenho passado e projeções futuras. Com a continuação dos esforços de investimento e inovação, o pré-sal permanece uma peça chave na matriz energética do Brasil, com potencial para influenciar o mercado global de petróleo.


## Referências

- **Agência Nacional de Petróleo (ANP)**: [Consulta à Produção por Poço](https://cdp.anp.gov.br/ords/r/cdp_apex/consulta-dados-publicos-cdp/consulta-produ%C3%A7%C3%A3o-por-po%C3%A7o)
- **Dados Abertos da ANP**: [Produção de Petróleo e Gás Natural por Poço](https://www.gov.br/anp/pt-br/centrais-de-conteudo/dados-abertos/producao-de-petroleo-e-gas-natural-por-poco)


## Dados de Contato

- **E-mail:** [rochanft@gmail.com](mailto:rochanft@gmail.com)
- **LinkedIn:** [Lucas Rocha](https://br.linkedin.com/in/lucsrocha/pt)
