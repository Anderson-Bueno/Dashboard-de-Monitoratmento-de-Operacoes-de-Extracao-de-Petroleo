# Dashboard Personalizado para Monitorar Desempenho das Operações de Extração de Petróleo

Este projeto consistiu no desenvolvimento de um dashboard personalizado para monitorar o desempenho das operações de extração de petróleo em uma área específica de produção. O objetivo era fornecer uma ferramenta visual intuitiva e informativa que permitisse aos gerentes e engenheiros acompanhar o progresso das operações em tempo real e tomar decisões estratégicas com base nos dados apresentados.

## Modelo Conceitual dos Dados

### Entidades:
1. **Ponto de Extração de Petróleo**: Representa um local específico onde ocorre a extração de petróleo. Inclui informações como ID do ponto, localização geográfica (latitude e longitude) e tipo de equipamento utilizado.
2. **Produção de Petróleo**: Representa os dados de produção diária de petróleo em cada ponto de extração. Inclui informações como data, volume de petróleo produzido, temperatura, pressão e composição do petróleo.
3. **Eficiência Operacional**: Representa os dados de eficiência operacional em cada ponto de extração. Inclui informações como energia consumida, água utilizada, horas de trabalho e taxa de utilização de equipamentos.
4. **Falhas e Manutenções**: Representa os dados de falhas e manutenções em cada ponto de extração. Inclui informações como tipo de falha, causa da falha, tempo de inatividade e ações corretivas realizadas.
5. **Indicadores-Chave de Desempenho (KPIs)**: Representa os indicadores-chave de desempenho monitorados em cada ponto de extração. Inclui informações como tempo médio entre falhas (MTBF), tempo médio para reparo (MTTR), taxa de disponibilidade e taxa de utilização.

### Relacionamentos:
1. Um **Ponto de Extração de Petróleo** pode ter uma ou várias **Produções de Petróleo** ao longo do tempo.
2. Um **Ponto de Extração de Petróleo** pode ter uma ou várias **Eficiências Operacionais** ao longo do tempo.
3. Um **Ponto de Extração de Petróleo** pode ter uma ou várias **Falhas e Manutenções** registradas ao longo do tempo.
4. Um **Ponto de Extração de Petróleo** pode ter vários **Indicadores-Chave de Desempenho (KPIs)** associados a ele.

Este é um modelo conceitual básico e genérico que pode ser adaptado e expandido com base nos requisitos específicos do projeto e nos detalhes dos dados disponíveis. Ele fornece uma estrutura inicial para entender os diferentes componentes envolvidos no monitoramento das operações de extração de petróleo.

## Modelo Lógico dos Dados

### Entidades:
1. **Ponto de Extração de Petróleo (ExtractionPoint)**:
   - `IDPonto` (PK): Identificador único do ponto de extração.
   - `Latitude`: Coordenada de latitude do ponto de extração.
   - `Longitude`: Coordenada de longitude do ponto de extração.
   - `TipoEquipamento`: Tipo de equipamento utilizado no ponto de extração.

2. **Produção de Petróleo (OilProduction)**:
   - `IDProducao` (PK): Identificador único da produção de petróleo.
   - `IDPonto` (FK): Chave estrangeira referenciando o ponto de extração.
   - `DataProducao`: Data da produção de petróleo.
   - `VolumeProduzido`: Volume de petróleo produzido.
   - `Temperatura`: Temperatura durante a produção.
   - `Pressao`: Pressão durante a produção.
   - `Composicao`: Composição do petróleo.

3. **Eficiência Operacional (OperationalEfficiency)**:
   - `IDEficiencia` (PK): Identificador único da eficiência operacional.
   - `IDPonto` (FK): Chave estrangeira referenciando o ponto de extração.
   - `DataEficiencia`: Data da medição da eficiência operacional.
   - `EnergiaConsumida`: Energia consumida no ponto de extração.
   - `AguaUtilizada`: Quantidade de água utilizada.
   - `HorasTrabalho`: Horas de trabalho do equipamento.

4. **Falhas e Manutenções (FailuresMaintenance)**:
   - `IDFalha` (PK): Identificador único da falha/manutenção.
   - `IDPonto` (FK): Chave estrangeira referenciando o ponto de extração.
   - `DataFalha`: Data da falha/manutenção.
   - `TipoFalha`: Tipo de falha ocorrida.
   - `Causa`: Causa da falha.
   - `TempoInatividade`: Tempo de inatividade devido à falha.
   - `AcoesCorretivas`: Ações corretivas realizadas.

5. **Indicadores-Chave de Desempenho (KPIs)**:
   - `IDKPI` (PK): Identificador único do KPI.
   - `IDPonto` (FK): Chave estrangeira referenciando o ponto de extração.
   - `NomeKPI`: Nome do indicador-chave de desempenho.
   - `Valor`: Valor do indicador.

Este modelo lógico representa as entidades principais envolvidas no monitoramento das operações de extração de petróleo, juntamente com seus atributos correspondentes e relacionamentos. Ele fornece uma estrutura organizada para armazenar e gerenciar os dados relevantes para análise e tomada de decisões no contexto das operações de extração de petróleo.

## Modelo Dimensional dos Dados

### Dimensões:
1. **Dimensão Ponto de Extração (ExtractionPointDim)**:
   - `IDPonto` (PK): Identificador único do ponto de extração.
   - `Latitude`: Coordenada de latitude do ponto de extração.
   - `Longitude`: Coordenada de longitude do ponto de extração.
   - `TipoEquipamento`: Tipo de equipamento utilizado no ponto de extração.

2. **Dimensão Tempo (TimeDim)**:
   - `DataProducao` (PK): Data da produção de petróleo.
   - `Mes`: Mês da produção de petróleo.
   - `Ano`: Ano da produção de petróleo.
   - `Trimestre`: Trimestre da produção de petróleo.

### Fatos:
1. **Fato Produção de Petróleo (OilProductionFact)**:
   - `IDPonto` (FK): Chave estrangeira referenciando a dimensão Ponto de Extração.
   - `DataProducao` (FK): Chave estrangeira referenciando a dimensão Tempo.
   - `VolumeProduzido`: Volume de petróleo produzido.
   - `Temperatura`: Temperatura durante a produção.
   - `Pressao`: Pressão durante a produção.
   - `Composicao`: Composição do petróleo.

2. **Fato Eficiência Operacional (OperationalEfficiencyFact)**:
   - `IDPonto` (FK): Chave estrangeira referenciando a dimensão Ponto de Extração.
   - `DataEficiencia` (FK): Chave estrangeira referenciando a dimensão Tempo.
   - `EnergiaConsumida`: Energia consumida no ponto de extração.
   - `AguaUtilizada`: Quantidade de água utilizada.
   - `HorasTrabalho`: Horas de trabalho do equipamento.

3. **Fato Falhas e Manutenções (FailuresMaintenanceFact)**:
   - `IDPonto` (FK): Chave estrangeira referenciando a dimensão Ponto de Extração.
   - `DataFalha` (FK): Chave estrangeira referenciando a dimensão Tempo.
   - `TipoFalha`: Tipo de falha ocorrida.
   - `Causa`: Causa da falha.
   - `TempoInatividade`: Tempo de inatividade devido à falha.
   - `AcoesCorretivas`: Ações corretivas realizadas.

4. **Fato Indicadores-Chave de Desempenho (KPIsFact)**:
   - `IDPonto` (FK): Chave estrangeira referenciando a dimensão Ponto de Extração.
   - `DataKPI` (FK): Chave estrangeira referenciando a dimensão Tempo.
   - `NomeKPI`: Nome do indicador-chave de desempenho.
   - `Valor`: Valor do indicador.

Este modelo dimensional organiza os dados de maneira eficiente para análise e relatórios, separando as informações em dimensões e fatos. Isso permite uma estrutura mais flexível e fácil de entender para análise e tomada de decisões no contexto das operações de extração de petróleo.

### Pontos Importantes

1. **Introdução**: Descrição clara do objetivo do projeto.
2. **Modelo Conceitual dos Dados**: Detalhamento das entidades e seus relacionamentos.
3. **Modelo Lógico dos Dados**: Estrutura organizada das entidades e atributos para armazenamento e gestão de dados.
4. **Modelo Dimensional dos Dados**: Organização dos dados para análise e relatórios, separando informações em dimensões e fatos.
