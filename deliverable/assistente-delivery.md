# Criando um Assistente de Delivery com AWS Step Functions e Bedrock

O desenvolvimento de um aplicativo de delivery de comida é feito de várias aplicações distribuídas. A primeira aplicação ao utilizar o sistema é uma API de User Management que visa guardar o histórico de pedidos e o histórico de cupons. A segunda aplicação é um gerenciador de push notifications que informa o status do pedido ao cliente e ao restaurante. A terceira aplicação é uma API que gerencia a lista de pedidos. Assim, as três ferramentas trabalham juntas que seguem um fluxo de passos acionados por gatilho, sendo que cada passo depende de alguma ação que foi efetuada em outra aplicação: a comunicação dessa interdependência é efetuada por algum publisher, i.e., um agente de mensageria. Cada aplicativo conectado pelo publisher é um subscriber. Esse trabalho pode ser feito pelo *AWS Step Functions*: serve para usar low-code para orquestrar a utilização conjunta de diversos serviços da AWS.
O *AWS Step Functions* cria workflows que usa os produtos da AWS visando
- desenvolver aplicações distribuídas;
- automatizar os processos;
- orquestrar os microsserviços;
- criar pipelines de dados com machine learning.
Tal serviço oferece vários benefícios:
- integração rápida: usa uma interface drag-drop para montar lógicas de negócios que podem ser complicadas;
- automação simples: usa os produtos da AWS de modo automático e sem precisar fazer manutenção de código; 
- processamento de dados sob demanda: usa workflows paralelos;
- visualização da arquitetura orientada por eventos: os workflows são flexíveis.
Dentre os possíveis casos de uso, destacam-se:
- criação de workflows automáticos para responder a incidentes de segurança;
- processamento iterativo de big data;
- execução de múltiplas tarefas de ETL;
- combinação de múltiplas funções lambda dentro de aplicações serverless e microsserviços.

## Máquinas de estado
O projeto de *Step Functions* é uma **_máquina de estado_**: aplicativo que controla a várias etapas do workflow. Assim, o projeto começa ao criar uma máquina de estado. A AWS oferece vários templates, inclusive blank. Também vale notar que cada template é editável e pode ser adaptado de modo específico.

## Workflow Studio
O **_Workflow Studio_** é a IDE utilizada para projetar e codificar as máquinas de estado do *Step Functions*. O catálogo oferece todos os serviços AWS necessários para criar algum workflow. As máquinas de estado são definidas ao escrever o código utilizando Amazon States Language (ASL, doravante). O ASL é uma linguagem estruturada baseada em JSON. As opções para codificar a máquina de estados são os seguintes:
- **Ações**: cada um dos serviços da AWS que pode ser incluídas no workflow;
- **Fluxo**: a parte lógica do algoritmo que programa as condições;
- **Padrões**: scripts prontos para serem utilizados no workflow.
Assim que o algoritmo já está pronto: basta criar a máquina de estado. 

## Exemplo Prático: criação de um app de assistente de delivery
A criação de um app pode ser feita seguindo as seguintes etapas:
- criar uma máquina de estados;
- escolher um modelo: neste exemplo, é um template *Execute o encadeamento de prompts de IA com o Amazon Bedrock*;
- determinar a execução do modelo;
- determinar para *implantar e executar*;
- editar o app;
- configurar a permissão: anexar as políticas do Bedrock;
- na seção de *Design*: determinar o modelo para cada prompt (neste exemplo, o modelo é o Haiku);
- ainda na seção de *Design*: configurar os prompts diretamente no JSON do ASL;
- então, precisa configurar a saída do resultado;
- salvar e executar;
- daí a IA gera o output respectivo ao input;
- após o uso: basta excluir a máquina de estado.