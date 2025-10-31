# 👩🏻‍💻 Projeto 05 - Tarefas Automatizadas com AWS Lambda e Amazon S3

## Introdução

O quinto projeto consiste em **consolidar seus conhecimentos em tarefas automatizadas com Lambda Function e S3**. O entregável consite em um repositório organizado contendo anotações, diagramas, insights obtidos durante a prática.

## Descrição do Desafio

Para este projeto, usei o **AWS Lambda e o Amazon S3** para explorar a criação de tarefas automatizadas com o objetivo de aprender a automatizar processos na nuvem.

## O que é Amazon S3?

Amazon Simple Storage Service ou Amazon S3 é um serviço provido pela AWS que permite armazenar, organizar e recuperar grandes volumes de dados na web.

O Amazon S3 fornece armazenamento de objetos desenvolvido para armazenar e recuperar qualquer quantidade de informação ou dado de qualquer lugar da internet.

## O que é AWS Lambda?

AWS Lamba é um serviço de computação sem servidor que executa códigos em resposta à eventos e com possibilidade de escala automática. Com o Lamba é possível executar códigos das seguintes linguagens: Node.js, Python, Java, Go, Ruby e .NET (C#).

**Com o AWS Lambda, é possível:**

- Usar APIs web e microserviços (com API Gateway)
- Processar dados e ETL (S3, DynamoDB, Kinesis)
- Análise de dados em tempo real e streaming
- Automação e agendamento de tarefas (EventBridge/CloudWatch)
- Backend para serviços leves como mobile e IoT

## Exemplo de Código Lambda (Ruby)

**Exemplo real**: Quando um arquivo CSV é enviado para o S3, a função Lambda pode automaticamente ler o arquivo, processar os dados e enviar um resumo por e-mail.

```bash
require 'aws-sdk-s3'
require 'aws-sdk-sesv2'
require 'csv'
require 'uri'

def lambda_handler(event:, context:)
  region  = ENV['AWS_REGION'] || 'us-east-1'
  s3      = Aws::S3::Client.new(region: region)
  ses     = Aws::SESv2::Client.new(region: region)

  sender    = ENV['SES_SENDER']    || 'sender@example.com'
  recipient = ENV['SES_RECIPIENT'] || 'recipient@example.com'

  rec = event['Records']&.first
  return { status: 'skipped' } unless rec && rec['eventName']&.start_with?('ObjectCreated')

  bucket = rec.dig('s3','bucket','name')
  key    = URI.decode_www_form_component(rec.dig('s3','object','key').to_s)

  csv_text = s3.get_object(bucket: bucket, key: key).body.read

  rows = 0
  total = 0.0
  CSV.parse(csv_text, headers: true) do |row|
    rows += 1
    total += row['amount'].to_f
  end
  avg = rows > 0 ? total / rows : 0.0

  body = "CSV Summary\nFile: #{key}\nRows: #{rows}\nTotal: #{'%0.2f' % total}\nAverage: #{'%0.2f' % avg}"

  ses.send_email(
    from_email_address: sender,
    destination: { to_addresses: [recipient] },
    content: {
      simple: {
        subject: { data: "CSV Summary for #{key}" },
        body: { text: { data: body } }
      }
    }
  )

  { status: 'success', bucket: bucket, key: key, rows: rows, total: total, average: avg }
end

```
