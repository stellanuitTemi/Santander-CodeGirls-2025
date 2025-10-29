# 👩🏻‍💻 Projeto 01 - Gerenciamento de Instâncias EC2 na AWS

## Introdução

O primeiro projeto consiste em um laboratório que tem como objetivo consolidar os conhecimentos em **gerenciamento de Instâncias EC2** na AWS. O entregável consite em um repositório organizado contendo anotações, diagramas, insights obtidos durante a prática.

## Descrição do Desafio

Para este projeto, criei uma arquitetura simples usando o Amazon EC2 e Amazon S3 para simular o upload de um arquivo de imagem para uma plataforma de e-commerce. Com o objetivo de aplicar os conhecimentos obtidos sobre intâncias EC2 e armazenamento de arquivos na nuvem.

## Objetivos de Aprendizagem

Ao finalizar este desafio fui capaz de criar um diagrama onde:

- Usuário faz um upload de uma imagem de um produto.
- Arquivo é enviado e processado para uma aplicação de e-commerce localiza em uma instância EC2.
- A aplicação localizada na instância EC2 envia o arquivo para um bucket to Amazon S3.
- O Amazon S3 armazena o arquivo e envia a URL do mesmo de volta para a instância EC2.
- A instância EC2 retorna para o usuário uma mensagem de sucesso com a URL da imagem armazenada.

## Arquitetura Criada

![Diagrama de Gerenciamento de Instâncias EC2 na AWS](https://i.imgur.com/69X3Aum.png "Diagrama de Gerenciamento de Instâncias EC2 na AWS")

## Conceitos Importantes

### 🔸 Amazon EC2

**AWS EC2 ou Elastic Cloud Compute** é um serviço web que fornece capacidade computacional na nuvem de forma secura e escalável. Pode ser utilizada para criar várias máquinas virtuais conforme necessário.

As máquinas virtuais criadas no EC2 podem ter sistemas operacionais Windows ou Linux.

Uma EC2 é composta por:

- CPU
- Memória
- Disco
- Rede
- Sistema Operacional

### 🔸 Amazon S3

Amazon Simple Storage Service ou Amazon S3 é um serviço provido pela AWS que permite armazenar, organizar e recuperar grandes volumes de dados na web.

O Amazon S3 fornece armazenamento de objetos desenvolvido para armazenar e recuperar qualquer quantidade de informação ou dado de qualquer lugar da internet.

**Object & Bucket do AWS S3**

- Um object ou objeto consiste de dados (arquivos), key e metadados.
- Um Bucket é responsável por armazenar os objetos.
- Quando um dado (objecto) é adicionado ao bucket, o Amazon S3 cria uma ID única e a associa ao objeto.

**Tipos de Classes no Amazon S3**

- **Standard:** Para acesso frequente de dados, adequado para casos em que é necessária baixa latência.
- **Standard IA:** Para acesso infrequente de dados, pode ser usa quando os dados são de longa duração e acessados não frequentemente.
- **Amazon Glacier:** Pode ser usado quando os dados precisão ser arquivados por longuíssimos períodos e alta performance não é necessária.
- **One Zone IA Storage Class:** Pode ser usado quando o dado armazenado é acessado infrequentemente e em apenas uma única região.
- **Amazon S3 Standard Reduced Redundancy Storage:** Adequado para usa onde o dado armazenado é não crítico e reproduzido rapidamente.

### 🔸 Amazon EBS

É uma storage altamente confiável que pode ser anexada em qualquer instância EC2. Toda instância possui um volume de armazenamento.

Com o EBS conseguimos criar uma nova participação em nossa instância, igual a um HD externo.

Exemplo de uso:

- Armazenamento para banco de dados, como MySQL, PostgreSQL, Oracle.
- Arnazenar dados para aplicativos web e logs de sistema.

### 🔸 Amazon AMI

No Amazon EC2, uma **AMI (Amazon Machine Image)** é uma imagem de máquina virtual pré-configurada com as informações necessárias para iniciar uma instância, como o sistema operacional, servidors de aplicações e as aplicações.

As AMIs podem ser criadas a partir de instâncias em execução ou paradas.

As AMIs podem ser públicas ou privadas. A AWS fornece uma variedade de AMIs públicas que podem ser usadas, ou você pode criar e usar suas próprias AMIs privada para segurança e personalização.
