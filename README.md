# Ontologia de Gerenciamento de Domnio Especfico
A Ontologia projetada para gerenciar workflows no processo de Descoberta de Conhecimento em Bases de Dados (KDD).A ontologia define classes, propriedades, restrições e regras de inferência para organizar processos, tarefas, algoritmos e objetos informacionais. Ela foi criada com intuito de servir a uma interface onde os usuários podem explorar relações entre processos, tarefas e algoritmos e gerenciá-los, facilitando a execução de workflows em aplicações KDD.

## Classes e Hierarquia

As classes foram planejadas como objetos que poderiam ser gerenciados e usados durante o processo, incluindo objetos mais abstratos para auxiliar na organização do processo. Todas as classes estão relacionadas diretamente ou indiretamente, mas nem todas são mais especializadas nas subclasses.

- **DM_Workflow** representa o fluxo geral do processo KDD e com ele carrega o objetivo do trabalho e o contexto em que está inserido. Essa é classe principal, que contém diretamente ou indiretamente os objetos que fazem parte do processo.
- **DMProcess** é a classe que abstrai os 7 principais processos do método KDD. Ela trabalha junto com o workflow para ditar o fluxo do trabalho e são necessárias tarefas específicas para cada processo.
- **Dm_Task** detalha o processo para um objetivo mais evidente aproximando-se mais da parte prática. A task especializa o que o algoritmo deve gerar e partir de qual objeto.
- **Dm_Algorithm** é o algoritmo que performa uma tarefa para gerar um objeto informativo(Output) a partir de outro(Input)
- **DM_InformationalObject** Representa os dados, modelos, relatórios gerados ou qualquer outro tipo de objeto que represente alguma informação importada ou gerada dentro do próprio processo.
- **DM_Operator** é o espaço que realiza o Workflow executando os algoritmos associados a ele.

## Propriedades de Objeto

As propriedades de objeto definem os relacionamentos entre as diferentes classes da ontologia. Elas são cruciais para representar como os elementos interagem no processo de workflow KDD, sendo possível demonstrar a sequência do processo, especificar a hierarquia entre as classes e muito mais.
Aqui estão algumas relações criadas no trabalho:

- **contains**: Processo contém Tasks;
- **PartOf**: Task é parte do Processo;
- **PartOfWorkflow**: Processo é parte de um Workflow;
- **hasProcess**: Workflow tem processo;
- **isMetadatOf**: Data Structure é o Metadado de um DataSet;
- **specifiesInput**: Tarefa específica o Output(DM_InformationalObject) que algoritmo tem;
- **specifiesOutput**: Tarefa específica o Input(DM_InformationalObject) que algoritmo precisa;
- **SpecifiesAlgorithm**: Tarefa específica o funcionamento do algoritmo;
- **performsTask**: Algoritmo performa a Tarefa;
- **hasMetadata**: Dataset tem um Data Structure como Metadata;
- **InputOf**: DM_InformationalObject que o Algoritmo necessita como Input;
- **OutputOf**: DM_InformationalObject que o Algoritmo vai gerar como Output;
- **hasColumn**: Data Structure tem Column_Data como coluna;
- **targertedColumn**: Column_Data é a coluna alvo do MOdelo_DM;
- **executes**: Operator_DM executa o algoritmo do DM_Algorithm;
- **isSequenceOf**: Um DM_Processo é sequência de outro DM_Process;

## Propriedades de Dados

As propriedades de dados conectam as classes a informações específicas, como valores literais ou atributos numéricos. Elas fornecem detalhes adicionais sobre os objetos, aumentando a capacidade descritiva da ontologia, característica necessária para o sistema de gerenciamento do Workflow.
Aqui estão algumas propriedades criadas no trabalho:

- **Code**: Código associado a um objeto ou entidade no sistema;
- **NumOfColumns**: Representa o número de colunas de um conjunto de dados ou tabela;
- **NumOfLines**: Representa o número de linhas de um conjunto de dados ou tabela;
- **Requirements**: Descreve os requisitos necessários para o uso ou funcionamento de uma entidade;
- **Weight**: Representa o peso de um elemento, podendo ser literal ou metafórico (ex.: importância relativa);
- **context**: Indica o contexto no qual um dado ou processo está inserido;
- **createdAt**: Data e hora em que o DM_InformationalObject ou dado foi criado;
- **datatype**: Especifica o tipo de dado, como string, inteiro, ou booleano da coluna;
- **environment**: Descreve o ambiente no qual o DM_Operator opera;
- **file**: Referencia um arquivo associado ao DataSet;
- **infoDescription**: Fornece uma descrição detalhada sobre o DM Informational Object;
- **language**: Indica a linguagem de programação em que o DM_Operator  opera;
- **numProcess**: Número total de processos no Workflow;
- **numTasks**: Número de tarefas associadas a um DM_Process;
- **objective**: Específica o objetivo ou propósito do Workflow;
- **procDescription**: Descreve o processo DM_Process em detalhes;
- **source**: Origem dos dados do DataSet_Data;
- **taskDescription**: Descrição detalhada de uma tarefa DM_Task;
- **updatedAt**: Data e hora da última atualização do DM_InformationalObject;
- **MissingValues(Per)**: Percentual de valores ausentes em um DataSet_Data;
- **size(MB)**: Tamanho do DM Informational Object em megabytes;

##Restrições

As restrições estabelecem as regras que definem o comportamento esperado dos elementos na ontologia. Elas garantem consistência e especificam limites ou obrigatoriedades nos relacionamentos e valores. Elas são importantes para estabelecer limites na forma em que o usuário vai gerenciar o processo, seguindo a lógica KDD.
Aqui estão algumas restrições criadas no trabalho:

- **DM_Algorithm → performsTask some DM_Task**: Define que um algoritmo realiza pelo menos uma tarefa .
- **DM_Algorithm → performsTask max 1 DM_Task**: Restringe que um algoritmo realiza no máximo uma tarefa.
- **DM_Algorithm → Code some string**: Especifica que um algoritmo possui um bloco de código(Code).
- **DM_Operator → environment some string**: Indica que um operador está associado a um ambiente.
- **DM_Operator → language some string**: Define que um operador suporta ou utiliza uma linguagem específica.
- **DM_Workflow → numProcess some int**: Indica o número de processos no fluxo de trabalho.
- **DM_Workflow → objective some string**: Especifica que o Workflow tem um objetivo.
- **Column_Data → PartOfDataStructure some DataStruture_Data**: Indica que uma coluna de dados faz parte de pelo menos  uma estrutura de dados.
- **DM_Process → isAntecedentTo max 1 DM_Process**: Restringe que um processo seja antecedente de no máximo um outro processo.
- **DM_Process → isSequenceTo max 1 DM_Process**: Restringe que um processo seja sequencial a no máximo um outro processo.

##Regras de Inferência

As regras de inferência permitem criar novos conhecimentos com base nos elementos já definidos na ontologia. Utilizando a Semantic Web Rule Language (SWRL), é possível estabelecer um conjunto de regras para automaticamente atribuir uma classe mais específica a um indivíduo baseado em suas propriedades e relacionamentos
Liste as regras SWRL apresentadas para validar as relações:

- **Regra 9: DataMining_Task(?x) ^ specifiesAlgorithm(?x, ?a) ^ hasOutput(?a, ?m) ^ DM_Model(?m) -> Modelling_task(?x);

Descrição: Se uma DataMining_Task especifica um algoritmo que tem como Output um DM_Model, então essa task é uma Modelling_task.

- **Regra 11: Modelling_task(?x) ^ specifiesAlgorithm(?x, ?a) ^ targetedColumn(?a, ?m) -> SupervisedLearning_Task(?x);

Descrição: Se uma Modelling_task especifica um algoritmo que tem uma Coluna alvo, então essa task é uma SupervisedLearning_Task.

- **Regra 11: SupervisedLearning_Task(?x) ^ specifiesAlgorithm(?x, ?a) ^ targetedColumn(?a, ?m) ^ datatype(?m, "enum"^^rdf:PlainLiteral) -> Classification_Task(?x);

Descrição: Se uma SupervisedLearning_Task especifica um algoritmo que tem uma Coluna alvo com datatype igual a “enum”, então essa task é uma Classification_Task.

