# 👩🏻‍💻 Projeto 03 - AWS CloudFormation - Infraestrutura como Código

## Introdução

O terceiro projeto consiste em **implementar sua primeira Stack com AWS CloudFormation**. O entregável consite em um repositório organizado contendo anotações, diagramas, insights obtidos durante a prática.

## Descrição do Desafio

Para este projeto, usei o **AWS CloudFormations** para criar um sumário sobre o AWS CloudFormation e passos para a criação de um template JSON/YAML e uma Stack.

## O que é AWS CloudFormation

O AWS CloudFormation é um serviço que permite definir e gerenciar uma infraestrutura AWS usando apenas código. É possível criar a infraestrutura utilizando-se templates em YAML ou JSON que descrevem cada recurso (instâncias EC2, buckets do S3, roles do IAM, etc.) e como eles são ulitizados.

Através do template, o CloudFormation lê as informaçoes e cria conjunto de recursos em execução, chamados de “stack”, permitindo que a infraestrutura seja reproduzível e automatizada.

Conceitos Principais do CloudFormation:

- Template:  Declara recursos, parâmetros e saídas

- Stack: Uma instância em execução do template

- Paramenters: Valores customizados no momento de criação do template

- Changesets: Visualização prévia das mudanças antes da finalização

- Drift Detection: Verifica se os recursos reais são diferentes do template

- Nested Stacks/StackSets: Cria módulos dos templates e os gerencias através de várias contas ou regiões

## Criando um Template e Stack

Para se criar um template e uma stack com o AWS CloudFormation, basta seguir alguns simples passos, começando pela criação do arquivo que servirá como o nosso template.

1. Planejamento - Decida o que você deseja criar

- Defina quais recursos serão utilizados, como por exemplo, instâncias EC2, buckets S3, VPC, sub-redes, ou uma combinação de vários recursos.

2. Escolha um formato

- Defina qual o formato será escrito o template. YAML, normalmente é mais fácil de ser lido, porém JSON também é suportado.

3. Adicione parâmetros, recursos e outputs

- Defina os valores customizados dos parâmetros que serão utilizados durante o deploy, além de quais recursos da AWS serão necessários e suas respectivas propriedades, e os valores que serão exportados do template (outputs).

4. Valide o template

- Verifique a sintaxe e estrutura do template no console AWS ou através do CLI.

Com o template criado, basta abrir o CloudFormation no console AWS e seguir os seguintes passos:

1. Clique em “Create Stack”
2. Escolha a opção, “Upload a template file” e envie o arquivo criado em YAML ou JSON. Exemplo: template.yaml ou template.json
3. Avance e dê um nome para a sua stack.
4. Se o seu template tiver parâmetros, informe os valores.
5. Avance e se quiser configure tags, permissões e outras opções da stack.
6. Clique em “Create Stack” para finalizar.
7. Monitore o status da sua stack na aba de eventos ou no CloudWatch até que o status mude para CREATE_COMPLETE.
8. Verifique os Outputs para qualquer valor retornado.

## Para que serve uma Stack?

Uma Stack é uma coleção de recursos em execução da AWS que o CloudFormation cria, atualiza, ou deleta como se fossem um único recurso através da utilização de um template.

Ao utilizarmos uma stack, nós podemos ter:

- Reprodutividade: É possível fazer deploy a mesma infraestrutura usando sempre o mesmo template.

- Consistência de ambiente: Crie com facilidade ambientes de desenvolvimento, testes e produção com a mesma configuração.

- Atualizações seguras: Utilize changesets para visualizar previamente mudanças antes de aplicá-las.

- Reverta erros: Automaticamente reverta para versões anteriores para manter o ambiente livre de falhas.

- Governança centralizada: Gerencie recursos como código e utilize versionamento.

- Gerenciamento de dependências: O CloudFormation lida com criação de recursos e dependências. (Exemplo, VPC antes do EC2).

## Exemplo de um template

```bash
AWSTemplateFormatVersion: '2010-09-09'
    Description: Simple S3 bucket example
    Parameters:
      BucketName:
        Type: String
        Description: Name of the S3 bucket
    Resources:
      MyBucket:
        Type: AWS::S3::Bucket
        Properties:
          BucketName: !Ref BucketName
    Outputs:
      BucketName:
        Value: !Ref MyBucket
        Description: Name of the created bucket

```

Ao utilizar esse template, será criado uma stack que fornecerá uma unidade única do bucket S3
