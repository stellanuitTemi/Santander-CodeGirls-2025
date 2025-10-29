# 👩🏻‍💻 Projeto 02 - Workflow do AWS Step Functions

## Introdução

O segundo projeto consiste em um laboratório que tem como objetivo consolidar seus **workflows automatizados com AWS Step Functions** na AWS. O entregável consite em um repositório organizado contendo anotações, diagramas, insights obtidos durante a prática.

## Descrição do Desafio

Para este projeto, usei o **AWS Step Functions Workflow Studio** para criar um workflow de microserviços que utiliza o AWS Lambda e Amazon SNS Com o objetivo de simular o fluxo de um serviço que autentica se o usuário possui Multi Factor Authentication habilitado.

## Objetivos de Aprendizagem

Ao finalizar este desafio fui capaz de criar um workflow onde:

- AWS Step Functions invoca uma função Lambda para verificar se o usuário possui MFA (CheckUserMFA)
- Com base no resultado, o Step Functions aciona uma segunda Lambda para notificar:
  - MFA configurado → NotifySNSMFAConfigured (SNS)
  - MFA não configurado → NotifySNSMFANotConfigured (SNS)
- O fluxo encerra com sucesso quando MFA está configurado; caso contrário, falha com um erro específico.

## Workflow

![Workflow Step Functions com microserviços do Lambda e Notificações SNS](https://i.imgur.com/K1ytIkU.png "Workflow Step Functions com microserviços do Lambda e Notificações SNS")

## Conceitos Importantes

### 🔸 AWS Lambda

AWS Lamba é um serviço de computação sem servidor que executa códigos em resposta à eventos e com possibilidade de escala automática. Com o Lamba é possível executar códigos das seguintes linguagens: Node.js, Python, Java, Go, Ruby e .NET (C#).

**Com o AWS Lambda, é possível:**

- Usar APIs web e microserviços (com API Gateway)
- Processar dados e ETL (S3, DynamoDB, Kinesis)
- Análise de dados em tempo real e streaming
- Automação e agendamento de tarefas (EventBridge/CloudWatch)
- Backend para serviços leves como mobile e IoT

### 🔸 AWS Step Functions

O AWS Step Functions é um serviço de orquestração sem servidor que lhe permite coordenar múltiplos serviços AWS em modelos de workflows que são duráveis e escaláveis. Esses modelos, chamados de state machines ou estado de máquinas, podem ser criadas com uma interface de design visual direto no console.

O Step Functions pode se integrar com diversos serviços da AWS incluindo o Lambda, ECS, DynamoDB, API Gateway, SQS, SNS, entre outras), permitindo workflow de multisserviços complexas.

**Como o Step Functions funciona:**

- Primeiro define-se a state machine usando o Amazon States Language (ASL), um arquivo JSON que descreve os passos (states) e como os dados fluem entre si.

- Inicia-se a execução ao providenciar um dado de entrada (input). O serviço executa o workflow, movendo-se de um state ao outro de acordo com sua definição.

- Cada state realiza uma tarefa (Task), realiza decisões (Choice), espera (Wait), executa códigos e/ou serviços em paralelo, itera sobre os items (Map), ou simplesmente passa os dados (Pass) para então enviar uma resposta de finalização, que pode ser tanto sucesso ou falha (Succeed, Fail).

- O Step Functions lida com passagem de dados, realiza nova tentativas, executa timeouts e tratamento de erros. Você pode observar o histórico de execução diretamente no console ou nos logs do CloudWatch

### 🔸 Amazon SNS e SQS

**O Amazon SNS (Simple Notification Service)** é um serviço de mensagens entre publicadores (publishers) e assinantes (subscribers) de maneira assíncrona. O Amazon SNS suporta diversos protocolos, tais quais o HTTP/S, Email, SMS, Lambda, SQS, entre outros.

O Amazon SNS funciona através da criação de mensagens publicas através de tópicos que envia uma cópia da mensagem para cada assinante cadastrado.

**O Amazon SQS (Simple Queue Service)** é um serviço que oferece uma fila de hospedada segura, durável e disponível que permite integrar e desacoplar sistemas de software e componentes distribuídos, e processamento assíncrono. O Amazon SQS suporta filas de mensagens mortas, tags de alocação de custos, recebimento e envio em lote.

### 🔸 Amazon ECS e EKS

**O Amazon ECS (Elastic Container Service)** é um serviço totalmente gerenciado de orquestração de containers Docker, ajudando a implantar, gerenciar e dimensionar facilmente aplicações conteinerizadas.

Com o Amazon ECS é possível utilizar de containers dockers para, por exemplo, fazer deploy de uma web app como serviço através de um Application Load Balancer, onde o ECS lida com os agendamentos, checagem de status e auto escala da aplicação.

**O Amazon EKS (Elastic Kubernetes Service)** é um serviço totalmente gerenciável de Kubernetes que permite executar o Kubernetes facilmente na Nuvem AWS e em data centers on-premises.

Com o Amazon EKS é possível fazer o deploy de um microsserviço utilizando o gerenciamento da infraestrutura de clusters do Kubernetes, via LoadBalancer ou Ingress

**Diferenças entre ECS e EKS:**

- ECS é nativo da AWS, simples de se usar para criação e gerenciamento de containers que permanecem na AWS, mais fácil de ser gerenciar do que Kubernetes.

- EKS entrega a experencia completa de se utilizar Kubernetes, oferecendo portabilidade e compatibilidade a um ecossistema completo, com o revés de oferecer uma maior complexidade.
