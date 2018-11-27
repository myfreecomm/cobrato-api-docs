# Modelo de Cobrança

```shell
Charge Template

EXEMPLO

  {
    "id": 1,
    "name": "Nome do Modelo",
    "charge_config_id": 1,
    "charged_amount": 1,
    "document_kind": "DM",
    "instructions": "",
    "demonstrative": "",
    "registrable": false,
    "interest_amount_per_month": "4.56",
    "mulct_type": 1,
    "mulct_value": "",
    "auto_send_billet": false,
    "email_sender_name": "Nome da Empresa",
    "email_subject": "Boleto de cobrança",
    "email_text": "",
    "email_reply_to": "name@company.com",
    "_links": [
      {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/charge_templates/1"},
      {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/charge_templates/1"},
      {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/charge_templates/1"}
    ]
  }

```

É possível ter indeterminados modelos. Cada modelo de cobrança pertence à uma configuração de cobrança.

**Parâmetros**

| Campo                     | Tipo             | Comentário                                                                                                                                              |
|---------------------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| name                      | string           | **(requerido)** Nome identificador do modelo de cobrança                                                                                                |
| charge_config_id          | integer          | **(requerido)** id da configuração de cobrança                                                                                                          |
| charged_amount            | decimal          | (opcional) valor cobrado no boleto                                                                                                                      |
| instructions              | integer          | (opcional) instruções de pagamento do boleto, por padrão "Pagável em qualquer agência até data do vencimento." (pode ser linhas separadas por "\n")     |
| demonstrative             | integer          | (opcional) demonstrativo do Boleto, por padrão "Não receber após o vencimento." (pode ser linhas separadas por "\n")                                    |
| registrable               | boolean          | (opcional) indica se a cobrança é registrável (do tipo que deve ser registrada no banco). Por padrão é o que está definido na Configuração de Cobrança  |
| mulct_type                | string           | (opcional) indica o tipo de multa que deve ser aplicada em caso de atraso ("percentage" para porcentagem, "currency" para valor em reais)               |
| mulct_value               | decimal          | (opcional) valor da multa que deve ser aplicada em caso de atraso, com base em seu tipo                                                                 |
| auto_send_billet          | boolean          | (opcional) Padrão "false". Envio ou não de boleto por email                                                                                             |
| email_sender_name         | string           | (opcional) Nome do remetente do email de notificação de cobrança                                                                                        |
| email_subject             | string           | (opcional) Assunto do email de notificação de cobrança                                                                                                  |
| email_text                | string           | (opcional) Texto do email de notificação de cobrança                                                                                                    |
| email_reply_to            | string           | (opcional) Endereço de email a ser utilizado na respsta ao email de notificação de cobrança                                                             |

**Parâmetros específicos para configuração de cobrança via Banco ou gateway PJBank**

| Campo                          | Tipo             | Comentário                                                                                                                                         |
|--------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| document_kind                  | string           | (opcional) espécie do documento, podendo ser DM (Duplicata Mercantil), DS (Duplicata de Serviço), NP (Nota Promissória) ou DV (Diversos)           |
| interest_amount_per_month      | decimal          | (opcional) porcentagem de juros mensal que deve ser aplicado em caso de atraso. Esse valor será dividido por 30 para ser encontrata a taxa diária  |

**Parâmetros específicos para configuração de cobrança via gateway Iugu**

| Campo                          | Tipo             | Comentário                                                                                                                                    |
|--------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| per_day_interest               | boolean          | (opcional) indica que será cobrado 1% de juros ao mês pró-rata em caso de atraso. Este valor é fixado pelo Iugu.                              |

## Informações do Modelo de Cobrança

```shell
Mostra Modelo de Cobrança

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/charge_templates/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/charge_templates/:id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id": 1,
    "name": "Nome do Modelo",
    "charge_config_id": 1,
    "charged_amount": 1,
    "document_kind": "DM",
    "instructions": "",
    "demonstrative": "",
    "registrable": false,
    "interest_amount_per_month": "4.56",
    "mulct_type": 1,
    "mulct_value": "",
    "auto_send_billet": true,
    "email_sender_name": "Nome da Empresa",
    "email_subject": "Boleto de cobrança",
    "email_text": "",
    "email_reply_to": "name@company.com",
    "_links": [
      {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/charge_templates/1"},
      {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/charge_templates/1"},
      {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/charge_templates/1"}
    ]
  }

```

Retorna as informações detalhadas do modelo de cobrança em formato JSON.

## Lista de Todos os Modelos de Cobrança

```shell

Listar Modelos de cobrança

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/charge_templates

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/charge_templates

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "charge_templates":
      [
        {
          // informações modelo 1
        },
        {
          // informações modelo 2
        },
        ...
      ]
  }
```

Retorna uma lista em JSON contendo todos os modelos de cobrança pertencentes a sua conta de serviço. É possível filtrar os Modelos pela configuração de cobrança passando o charge_config_id

## Criação de Modelo de Cobrança

```shell
Criar Modelo de Cobrança

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/charge_templates

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/charge_templates \
    -d '{
        "name": "Nome do Modelo",
        "charge_config_id": 1,
        "charged_amount": 1,
        "document_kind": "DM",
        "instructions": "",
        "demonstrative": "",
        "registrable": false,
        "interest_amount_per_month": "4.56",
        "mulct_type": 1,
        "mulct_value": "",
        "auto_send_billet": true,
        "email_sender_name": "Nome da Empresa",
        "email_subject": "Boleto de cobrança",
        "email_text": "",
        "email_reply_to": "name@company.com"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors": {
      "name": [
        "não é válido",
        "não pode ficar em branco"
      ]
    }
  }

```

Cria um novo modelo de cobrança, retornando as informações do mesmo caso haja sucesso.

**Parâmetros**

| Campo                     | Tipo    | Comentário                                                                                                                                              |
|---------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| name                      | string  | **(requerido)** Nome identificador do modelo de cobrança                                                                                                |
| charge_config_id          | integer | **(requerido)** id da configuração de cobrança                                                                                                          |
| charged_amount            | decimal | (opcional) valor cobrado no boleto                                                                                                                      |
| instructions              | integer | (opcional) instruções de pagamento do boleto, por padrão "Pagável em qualquer agência até data do vencimento." (pode ser linhas separadas por "\n")     |
| demonstrative             | integer | (opcional) demonstrativo do Boleto, por padrão "Não receber após o vencimento." (pode ser linhas separadas por "\n")                                    |
| registrable               | boolean | (opcional) indica se a cobrança é registrável (do tipo que deve ser registrada no banco). Por padrão é o que está definido na Configuração de Cobrança  |
| mulct_type                | string  | (opcional) indica o tipo de multa que deve ser aplicada em caso de atraso ("percentage" para porcentagem, "currency" para valor em reais)               |
| mulct_value               | decimal | (opcional) valor da multa que deve ser aplicada em caso de atraso, com base em seu tipo                                                                 |
| auto_send_billet          | boolean | (opcional) Padrão "false". Envio ou não de boleto por email                                                                                             |
| email_sender_name         | string  | (opcional) Nome do remetente do email de notificação de cobrança                                                                                        |
| email_subject             | string  | (opcional) Assunto do email de notificação de cobrança                                                                                                  |
| email_text                | string  | (opcional) Texto do email de notificação de cobrança                                                                                                    |
| email_reply_to            | string  | (opcional) Endereço de email a ser utilizado na respsta ao email de notificação de cobrança                                                             |

**Parâmetros específicos para configuração de cobrança via Banco ou gateway PJBank**

| Campo                          | Tipo             | Comentário                                                                                                                                         |
|--------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| document_kind                  | string           | (opcional) espécie do documento, podendo ser DM (Duplicata Mercantil), DS (Duplicata de Serviço), NP (Nota Promissória) ou DV (Diversos)           |
| interest_amount_per_month      | decimal          | (opcional) porcentagem de juros mensal que deve ser aplicado em caso de atraso. Esse valor será dividido por 30 para ser encontrata a taxa diária  |

**Parâmetros específicos para configuração de cobrança via gateway Iugu**

| Campo                          | Tipo             | Comentário                                                                                                                                    |
|--------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| per_day_interest               | boolean          | (opcional) indica que será cobrado 1% de juros ao mês pró-rata em caso de atraso. Este valor é fixado pelo Iugu.                              |


## Atualização de Modelo de Cobrança

```shell
Atualizar Modelo de Cobrança

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/charge_templates/:id
  PATCH https://app.cobrato.com/api/v1/charge_templates/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/charge_templates \
    -d '{
        "id": "1"
        "name": "Nome do Modelo",
        "charged_amount": 1,
        "document_kind": "DM",
        "charge_config_id": 1,
        "instructions": "",
        "demonstrative": "",
        "registrable": false,
        "interest_amount_per_month": "4.56",
        "mulct_type": 1,
        "mulct_value": "",
        "auto_send_billet": false,
        "email_sender_name": "Nome da Empresa",
        "email_subject": "Boleto de cobrança",
        "email_text": "",
        "email_reply_to": "name@company.com"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM MODELO DE COBRANÇA INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

```

Atualiza campos do Modelo de Cobrança. A requisição não diferencia a utilização dos verbos PUT e PATCH.

**Parâmetros**

| Campo                     | Tipo    | Comentário                                                                                                                                              |
|---------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| name                      | string  | **(requerido)** Nome identificador do modelo de cobrança                                                                                                |
| charge_config_id          | integer | **(requerido)** id da configuração de cobrança                                                                                                          |
| charged_amount            | decimal | (opcional) valor cobrado no boleto                                                                                                                      |
| instructions              | integer | (opcional) instruções de pagamento do boleto, por padrão "Pagável em qualquer agência até data do vencimento." (pode ser linhas separadas por "\n")     |
| demonstrative             | integer | (opcional) demonstrativo do Boleto, por padrão "Não receber após o vencimento." (pode ser linhas separadas por "\n")                                    |
| registrable               | boolean | (opcional) indica se a cobrança é registrável (do tipo que deve ser registrada no banco). Por padrão é o que está definido na Configuração de Cobrança  |
| mulct_type                | string  | (opcional) indica o tipo de multa que deve ser aplicada em caso de atraso ("percentage" para porcentagem, "currency" para valor em reais)               |
| mulct_value               | decimal | (opcional) valor da multa que deve ser aplicada em caso de atraso, com base em seu tipo                                                                 |
| auto_send_billet          | boolean | (opcional) Padrão "false". Envio ou não de boleto por email                                                                                             |
| email_sender_name         | string  | (opcional) Nome do remetente do email de notificação de cobrança                                                                                        |
| email_subject             | string  | (opcional) Assunto do email de notificação de cobrança                                                                                                  |
| email_text                | string  | (opcional) Texto do email de notificação de cobrança                                                                                                    |
| email_reply_to            | string  | (opcional) Endereço de email a ser utilizado na respsta ao email de notificação de cobrança                                                             |

**Parâmetros específicos para configuração de cobrança via Banco ou gateway PJBank**

| Campo                          | Tipo             | Comentário                                                                                                                                         |
|--------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| document_kind                  | string           | (opcional) espécie do documento, podendo ser DM (Duplicata Mercantil), DS (Duplicata de Serviço), NP (Nota Promissória) ou DV (Diversos)           |
| interest_amount_per_month      | decimal          | (opcional) porcentagem de juros mensal que deve ser aplicado em caso de atraso. Esse valor será dividido por 30 para ser encontrata a taxa diária  |

**Parâmetros específicos para configuração de cobrança via gateway Iugu**

| Campo                          | Tipo             | Comentário                                                                                                                                    |
|--------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| per_day_interest               | boolean          | (opcional) indica que será cobrado 1% de juros ao mês pró-rata em caso de atraso. Este valor é fixado pelo Iugu.                              |

## Exclusão de Modelo de Cobrança

```shell
Excluir Modelo de Cobrança

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/charge_templates/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/charge_templates/:id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM MODELO DE COBRANÇA INEXISTENTE

    404 Not Found

```

Exclui determinado modelo de cobrança. A exclusão é irreversível.
