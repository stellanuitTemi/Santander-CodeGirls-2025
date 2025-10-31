# 👩🏻‍💻 Projeto 04 - Implementando Infraestrutura Automatizada com AWS CloudFormation

## Introdução

O quarto projeto consiste em **implementar uma infraestrutura automatizada com AWS CloudFormation**. O entregável consite em um repositório organizado contendo anotações, diagramas, insights obtidos durante a prática.

## Descrição do Desafio

Para este projeto, usei o **AWS CloudFormations** para criar um sumário sobre a automatização da implementação de infraestruturas com o AWS CloudFormation além de elencar as principais diferenças entre o AWS CloudFormation e o Terraform.

## O que é AWS CloudFormation

O AWS CloudFormation é um serviço que permite definir e gerenciar uma infraestrutura AWS usando apenas código. É possível criar a infraestrutura utilizando-se templates em YAML ou JSON que descrevem cada recurso (instâncias EC2, buckets do S3, roles do IAM, etc.) e como eles são ulitizados.

Através do template, o CloudFormation lê as informaçoes e cria conjunto de recursos em execução, chamados de “stack”, permitindo que a infraestrutura seja reproduzível e automatizada.

## Automação de Infraestrutura

Automação significa usar software para provisionar, configurar, implantar, escalar e gerenciar recursos da infraestrutura de nuvem sem precisar realizar cada etapa manualmente, permitindo realizar tarefas repetitivas de forma confiável e rápida, minimizando erros humanos.

Automação normalmente é feita na infraestrutura (servidores e redes), implantações, monitoramento, backups e escalação.

**Benefícios da automação**

- Consistência e repetitividade: Mesma infraestrutura todas as vezes.
- Velocidade e eficiência: Provisionamento e implantações rápidas.
- Infraestrutura visionável: Templates são rastreados como código, permitindo reversão.
- Implantações mais seguras: Change sets mostram exatamente como as mudanças serão feitas antes de aplicá-las.
- Recuperação de desastres simplificada: Ambientes podem ser recriados com templates.
- Erro humano reduzido: Diminui etapas manuais e repetitivas
- Melhor colaboração com CI/CD: Mudanças da infraestrutura podem ser automatizadas como parte da pipeline.
- Drift control e Observabilidade: Templates servem com fonte única e verdadeira; detecção de drifts destaca divergências.

## Criação de uma Stack

Para se criar uma stack, basta abrir o CloudFormation no console AWS e seguir os seguintes passos:

1. Clique em “Create Stack”
2. Escolha a opção, “Upload a template file” e envie o arquivo criado em YAML ou JSON. Exemplo: template.yaml ou template.json
3. Avance e dê um nome para a sua stack.
4. Se o seu template tiver parâmetros, informe os valores.
5. Avance e se quiser configure tags, permissões e outras opções da stack.
6. Clique em “Create Stack” para finalizar.
7. Monitore o status da sua stack na aba de eventos ou no CloudWatch até que o status mude para CREATE_COMPLETE.
8. Verifique os Outputs para qualquer valor retornado.

## Diferença entre AWS CloudFormation e Terraform

| Aspecto                              | CloudFormation                                                                                           | Terraform                                                                                                     |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Scope / Provedores                   | Infraestrutura como código nativa da AWS; recursos da AWS; pode ser expandido com recursos customizáveis | Múltiplas nuvens e provedores; AWS, Azure, GCP, Kubernetes, SaaS, etc.                                        |
| Linguagem / Sintaxe                  | Templates em YAML ou JSON                                                                                | HCL (HashiCorp Configuration Language) ou JSON                                                                |
| Gerenciamento de estados             | Estados são gerenciados pelo CloudFormation dentro da AWS (não é necessário arquivos externos)           | Mantém um arquivo de estado separado; pode ser usado por backends locais ou remotos ( S3, Terraform Cloud)    |
| Modularidade / reuso                 | Nested stacks; evoluindo com módulos do CloudFormation                                                   | Módulos e registros de módulos; extensa comunidade de módulos                                                 |
| Gerenciamento de Mudanças / Previews | Visualize previamente updates com Change sets antes de finalizar                                         | Visualize mudanças previamente com o "terraform plan" antes de finalizar                                      |
| Detecção de drift                    | Detecção de drift interna para stacks                                                                    | Detecção de Drift não intrínseco; depende de planejamento/aplicação e ferramentas externas                    |
| Updates / Ciclo de vida              | Updates substituem ou modificam recursos a depender do tipo de recurso pode usar políticas de updates    | Update de recursos segue blocos de ciclo de vida (create_before_destroy) e dependências implícitas/explícitas |
| Reversão em caso de falhas           | Reversão automática por padrão se uma stack falhar                                                       | Aplicação parcial pode deixar recursos; reversão não é automático a não ser que haja um script                |
| Colaboração / Governança             | Acesso baseado no IAM; StackSets para múltiplas contas; governança nativa do AWS                         | Terraform Cloud/Enterprise, backends remotos, team workspaces, políticas como código (Sentinel)               |
| Ecossistema / Adoção                 | Integração profunda com o AWS; extensivo suporte a templates comunitários da AWS                         | Grande ecossistema de múltiplos provedores, vasta quantidade módulos da comunidade                            |
| Custo / Hospedagem                   | Grátis; Não é necessário hospedagem separada; recursos faturados pela AWS                                | Open-source; Terraform Cloud/Enterprise tem planos pagos                                                      |

## Quando escolher CloudFormation ou Terraform

**Escolha CloudFormation se:**

- Sua estrutura é estritamente AWS e você quer completa integração com paridade de recursos e governança da AWS.

- Você prefere as ferramentas nativas do AWS, integração com IAM e StackSets para deploy em diversas contas.

**Escolha Terraform se:**

- Você trabalha com múltiplas nuvens e precisa de uma ferramenta única para diferentes provedores.

- Você quer uma grande coleção de módulos da comunidade e um gerenciamento de estados remotos flexível
