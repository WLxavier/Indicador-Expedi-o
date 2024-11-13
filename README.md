# Sistema de Métricas de Produtividade para Expedição

## Descrição do Projeto

Este projeto visa a criação de uma visualização analítica da produtividade de funcionários do setor de expedição, como parte de uma iniciativa para implementar um modelo de premiação por produtividade. Através da análise dos indicadores, é possível monitorar a performance dos colaboradores em atividades como coleta e conferência de produtos, bem como calcular pontos e bonificações com base no desempenho. O objetivo é motivar a equipe e otimizar a eficiência nas operações da expedição.

Após a implementação do modelo de premiação, foi observada uma melhora significativa na eficiência do setor, resultando em uma redução de equipe necessária e de tempo para completar as tarefas. O uso de dados gerados pela view SQL e o posterior processo de ETL permitiu uma análise detalhada no Power BI, possibilitando tomadas de decisão com base em dados reais.

## Problema

O setor de expedição enfrentava desafios relacionados à produtividade e motivação dos funcionários. As atividades de conferência e coleta de produtos exigiam o envolvimento de muitos colaboradores e demandavam tempo prolongado para serem completadas. Para enfrentar esse problema, a empresa decidiu implementar um modelo de premiação que recompensa os funcionários por produtividade, criando incentivos diretos para melhorar o desempenho.

Com a implantação desse modelo, foi possível:
- **Reduzir a equipe de conferência**: De 19 funcionários necessários para a conferência, passou-se a precisar de apenas 14.
- **Otimizar a equipe de coleta**: De 9 funcionários para 6, devido à maior eficiência dos trabalhadores.
- **Reduzir a jornada dos funcionários**: Em média, houve uma economia de 1 hora e 30 minutos por dia na jornada de trabalho, já que as demandas de expedição passaram a ser finalizadas mais rapidamente devido ao aumento da motivação e produtividade.

Essas mudanças trouxeram benefícios financeiros para a empresa e aumentaram o engajamento dos funcionários, que passaram a receber bonificações e pontos adicionais pelo desempenho.

## Solução

### Etapas do Projeto

1. **Criação da View SQL**: Uma view em PL/SQL foi criada para consolidar os dados de produtividade dos funcionários. A view `AD_INDICADOR_ESTOQUE` reúne informações como:
   - Horários de início e fim das atividades.
   - Tempo total de execução.
   - Projeção de tempo ideal de acordo com os padrões da empresa.
   - Percentual de produtividade com base em metas de tempo.
   - Quantidade de itens e linhas processadas.
   - Pontuação e bonificação para o funcionário.

2. **Processo ETL**: Os dados gerados pela view SQL foram extraídos, transformados e carregados (ETL) para uma estrutura que permitiu fácil manipulação no Power BI.

3. **Visualização no Power BI**: Com os dados tratados, foi possível criar dashboards analíticos no Power BI. Essas visualizações permitem:
   - Monitorar a performance individual e da equipe.
   - Avaliar o percentual de produtividade de cada funcionário.
   - Visualizar a pontuação e bonificação alcançadas.
   - Identificar gargalos ou áreas para melhoria.

### Principais Componentes do Código SQL

- **Cálculo de Indicadores de Produtividade**:
  - **Início e Fim das Tarefas**: Campos que mostram a hora de início e término das atividades de conferência e coleta.
  - **Tempo Total e Tempo Sem Conversão**: Tempo gasto nas tarefas, calculado em diferentes formatos.
  - **Projeção de Tempo**: Estimativa do tempo ideal de acordo com o número de itens, para servir como base de comparação com o tempo real.
  - **Percentual de Produtividade**: Relação entre o tempo ideal e o tempo real, indicando a eficiência.
  - **Bonificação e Pontuação**: Cálculos baseados na produtividade e no percentual de metas atingidas.

- **Agrupamento e Organização dos Dados**:
  - A query agrupa os dados por `NUMAGRUPADOR`, `NUMOS`, ou `TIPOERRO`, dependendo do tipo de operação, e usa JOINs para integrar informações de múltiplas tabelas (`PCEMPR`, `PCENDERECO`, `WL_EQUIPES_EXP`, entre outras).

- **Condições e Filtros**:
  - Foram aplicados filtros para considerar apenas operações de sucesso (`CODOPER = 'S'`), excluir dados de operações não concluídas e calcular indicadores apenas para os dados relevantes.

### Benefícios do Modelo de Premiação

- **Aumento da Produtividade**: Com o incentivo financeiro atrelado à produtividade, os funcionários passaram a se engajar mais nas tarefas de expedição.
- **Redução de Custos Operacionais**: A eficiência maior permitiu a redução da equipe necessária, resultando em economia de recursos humanos.
- **Otimização de Tempo**: As demandas foram concluídas mais rapidamente, reduzindo a jornada e aumentando a disponibilidade dos colaboradores para outras tarefas.

## Requisitos do Projeto

- **Banco de Dados**: Oracle PL/SQL, para execução da query e criação da view.
- **Ferramenta de Visualização**: Power BI, para a construção de dashboards com os dados extraídos.
- **Ferramenta ETL**: Processo de ETL básico para manipulação e carregamento de dados para visualização.

## Instruções de Execução

1. **Executar o Script SQL**: Rodar o código PL/SQL no banco de dados para criar a view `AD_INDICADOR_ESTOQUE`.
2. **Configurar o Processo de ETL**: Extrair os dados da view, transformar conforme necessário (como ajuste de formatação e limpeza de dados) e carregar no Power BI.
3. **Montar o Dashboard no Power BI**: Utilizar os dados carregados para criar gráficos e tabelas que mostrem os principais KPIs de produtividade e os indicadores de bonificação dos funcionários.

## Considerações Finais

A implementação do modelo de premiação por produtividade teve um impacto positivo na expedição, motivando os funcionários e melhorando os índices de eficiência. O uso de dados consolidados e a criação de uma análise visual detalhada permitiram à equipe de gestão tomar decisões informadas para ajustes contínuos. O projeto demonstrou que a análise de dados pode ser uma ferramenta poderosa para melhorar processos e incentivar o engajamento dos colaboradores.
