# Pagamento

```shell
Pagamentos

EXEMPLO

  {
    "id": 10,
    "amount": "456.78",
    "date": "2017-12-07",
    "our_number": null,
    "payment_method": "ted_same_ownership",
    "payment_type": "benefit",
    "account": "12345",
    "account_digit": "9",
    "agency": "4321",
    "bank_code": "033",
    "doc_goal": null,
    "payee_document": "123.456.789-09",
    "payee_name": "John Doe",
    "ted_goal": "00300",
    "_links": [
      { "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "update", "method": "PUT", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "destroy", "method": "DELETE", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "payment_config", "method": "GET", "href": "https://app.cobrato.com/api/v1/payment_configs/1" }
    ]
  }

```

**Parâmetros**

| Campo                     | Tipo    | Comentário                                                                                                                                                                                                                                                                                                  |
|---------------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payment_config_id         | integer | código de identificação da configuração de pagamento à qual o pagamento irá pertencer                                                                                                                                                                                                                       |
| amount                    | decimal | valor do pagamento                                                                                                                                                                                                                                                                                          |
| date                      | date    | data do pagamento                                                                                                                                                                                                                                                                                           |
| payment_method            | string  | forma de pagamento ('credit_other_ownership', 'credit_same_ownership', 'credit_savings_account', 'doc_other_ownership', 'doc_same_ownership', 'ted_other_ownership', 'ted_same_ownership', 'dealership', 'billet_same_bank', 'billet_other_bank', 'gps', 'darf', 'das', 'ipva', 'icms_sp', 'dpvat', 'fgts') |
| payment_type              | string  | tipo de pagamento. Os possíveis valores variam de acordo com o "payment_method" (vide tabela 1)                                                                                                                                                                                                             |
| bank_code                 | string  | código de 3 dígitos do banco da conta bancária para o pagamento                                                                                                                                                                                                                                             |
| account                   | string  | número da conta bancária para o pagamento                                                                                                                                                                                                                                                                   |
| account_digit             | string  | dígito da conta bancária para fazer o pagamento                                                                                                                                                                                                                                                             |
| agency                    | string  | número da agência da conta bancária para fazer o pagamento                                                                                                                                                                                                                                                  |
| payee_id                  | integer | identificador do beneficiário                                                                                                                                                                                                                                                                               |
| payee_name                | string  | nome do beneficiário                                                                                                                                                                                                                                                                                        |
| payee_document_type       | string  | tipo do documento do beneficiário                                                                                                                                                                                                                                                                           |
| payee_document            | string  | número do documento do beneficiário                                                                                                                                                                                                                                                                         |
| doc_goal                  | string  | código referente ao objetivo do DOC. Possíveis valores na tabela 2                                                                                                                                                                                                                                          |
| ted_goal                  | string  | código referente ao objetivo do TED. Possíveis valores na tabela 3                                                                                                                                                                                                                                          |
| our_number                | string  | número que identifica o pagamento no banco                                                                                                                                                                                                                                                                  |
| gps_payment_code          | string  | código do GPS, de 4 dígitos                                                                                                                                                                                                                                                                                 |
| competency_month          | string  | mês de competência do GPS, repesentado por 2 dígitos                                                                                                                                                                                                                                                        |
| competency_year           | string  | ano de competência do GPS, repesentado por 4 dígitos                                                                                                                                                                                                                                                        |
| other_entities_amount     | decimal | valor extra para outras entidades                                                                                                                                                                                                                                                                           |
| monetary_update           | decimal | atualização monetária, incluindo valores de juros e multa                                                                                                                                                                                                                                                   |
| discount_amount           | decimal | valor do desconto                                                                                                                                                                                                                                                                                           |
| barcode                   | string  | código de barras                                                                                                                                                                                                                                                                                            |
| due_date                  | date    | data de vencimento                                                                                                                                                                                                                                                                                          |
| taxpayer_document_type    | string  | Tipo do documento do contribuinte                                                                                                                                                                                                                                                                           |
| taxpayer_document         | string  | Número do documento do contribuinte                                                                                                                                                                                                                                                                         |
| registration_status       | string  | status de registro do pagamento ('without_remittance', 'remitted', 'registered', 'canceled', 'edit_amount_started', 'reschedule_started', 'registered_with_error', 'cancelation_started', 'canceled_awaiting_confirmation', 'amount_edited_awaiting_confirmation', 'rescheduled_awaiting_confirmation')     |
| note                      | string  | Oberservação do pagamento                                                                                                                                                                                                                                                                                   |


## Informações do Pagamento

```shell
Mostrar Pagamento

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payments/:payment_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payments/:payment_id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id": 10,
    "amount": "456.78",
    "date": "2017-12-07",
    "our_number": null,
    "payment_method": "ted_same_ownership",
    "payment_type": "benefit",
    "account": "12345",
    "account_digit": "9",
    "agency": "4321",
    "bank_code": "033",
    "doc_goal": null,
    "payee_document": "123.456.789-09",
    "payee_name": "John Doe",
    "ted_goal": "00300",
    "note": "Pagamento feito para outra conta",
    "_links": [
      { "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "update", "method": "PUT", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "destroy", "method": "DELETE", "href": "https://app.cobrato.com/api/v1/payments/10" },
      { "rel": "payment_config", "method": "GET", "href": "https://app.cobrato.com/api/v1/payment_configs/1" }
    ]
  }

```

Retorna em JSON as informações detalhadas do Pagamento informado e também suas referências.

## Lista de todos os Pagamentos

```shell
Listar Pagamentos

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payments

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payments

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "payments":
      [
        {
          // informações pagamento 1
        },
        {
          // informações pagamento 2
        },
        ...
      ]
  }

```

Retorna uma lista em JSON contendo todos os Pagamentos que pertencem a sua Conta de Serviço.

## Criação de Pagamento

```shell
Criar Pagamento

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payments

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/payments \
    -d '{
          "payment_config_id": "1",
          "payment_type": "provider",
          "payment_method": "ted_other_ownership",
          "date": "2017-10-22",
          "amount": "255.99",
          "bank_code": "341",
          "agency": "9358",
          "account": "21500",
          "account_digit": "3",
          "payee_document_type": "cpf",
          "payee_document": "123.456.789-09",
          "payee_name": "Jane Doe"
          "note": "Pagamento para fornecedores",
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "payment_config_id":["não pode ficar em branco"],
        "payment_type":["não pode ficar em branco"]
      }
  }

```

Cria um novo Pagamento, retornando as informações do mesmo em caso de sucesso. Se houverem erros eles serão informados no corpo da resposta.

**Parâmetros comuns à todas as formas de pagamento**

| Campo                     | Tipo    | Comentário                                                                                                                                                                                                                                                  |
|---------------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payment_config_id         | integer | **(requerido)** código de identificação da configuração de pagamento à qual o pagamento irá pertencer                                                                                                                                                       |
| payment_method            | string  | **(requerido)** forma de pagamento ('credit_other_ownership', 'credit_same_ownership', 'credit_savings_account', 'doc_other_ownership', 'doc_same_ownership', 'ted_other_ownership', 'ted_same_ownership', 'gps', 'darf', 'das', 'ipva', icms_sp', 'dpvat') |
| payment_type              | string  | **(requerido)** tipo de pagamento. Os possíveis valores variam de acordo com o "payment_method" (vide tabela 1)                                                                                                                                             |
| amount                    | decimal | **(requerido)** valor do pagamento                                                                                                                                                                                                                          |
| date                      | date    | **(requerido)** data do pagamento                                                                                                                                                                                                                           |
| note                      | string  | (opcional) oberservação do pagamento                                                                                                                                                                                                                        |
| payee_name                | string  | (opcional) nome do beneficiário                                                                                                                                                                                                                             |

### Transferências (DOC, TED, Crédito)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros comuns aos pagamentos via transferência, além de alguns espefíficos para cada tipo de transferência.

**Parâmetros comuns à todos os pagamentos via transferência**

| Campo         | Tipo    | Comentário                                                                                                                                                                       |
|---------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account       | string  | **(requerido)** número da conta bancária para o pagamento                                                                                                                        |
| account_digit | string  | **(requerido)** dígito da conta bancária para fazer o pagamento                                                                                                                  |
| agency        | string  | **(requerido)** número da agência da conta bancária para fazer o pagamento                                                                                                       |
| payee_id      | string  | **(requerido, se não enviar payee)** identificador do beneficiário (caso seja fornecido, o parâmetro `payee` será ignorado)                                                      |
| payee*        | object  | **(requerido, se não enviar payee_id)** atributos para a criação de um novo beneficiário ou atualização de um beneficiário existente com o mesmo documento (national_identifier) |

**Parâmetros quando payment_method é 'doc_other_ownership' ou 'doc_same_ownership'**

| Campo                     | Tipo    | Comentário                                                                      |
|---------------------------|---------|---------------------------------------------------------------------------------|
| bank_code                 | string  | **(requerido)** código de 3 dígitos do banco da conta bancária para o pagamento |
| doc_goal                  | string  | (opcional) código referente ao objetivo do DOC. Possíveis valores na tabela 2   |

**Parâmetros quando payment_method é 'ted_other_ownership'**

| Campo                     | Tipo    | Comentário                                                                      |
|---------------------------|---------|---------------------------------------------------------------------------------|
| bank_code                 | string  | **(requerido)** código de 3 dígitos do banco da conta bancária para o pagamento |
| ted_goal                  | string  | (opcional) código referente ao objetivo do TED. Possíveis valores na tabela 3   |

### Boleto Bancário (Boleto de mesmo banco, Boleto de outro Banco)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros espefíficos para o pagamento de boletos bancários.

<aside class="info">
O attributo <code>amount</code> nesse caso é opcional, pois ele é identificado a partir do código de barras.
</aside>

**Parâmetros quando payment_method é 'billet_same_bank' ou 'billet_other_bank'**

| Campo           | Tipo    | Comentário                                                                                                                                                                       |
|-----------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| barcode         | string  | **(requerido)** Código de barras do boleto bancário                                                                                                                              |
| payee_id        | string  | **(requerido, se não enviar payee)** identificador do beneficiário (caso seja fornecido, o parâmetro `payee` será ignorado)                                                      |
| payee*          | object  | **(requerido, se não enviar payee_id)** atributos para a criação de um novo beneficiário ou atualização de um beneficiário existente com o mesmo documento (national_identifier) |
| due_date        | date    | (opicional, já que é identificado no código de barras) Data de vencimento do boleto                                                                                              |
| discount_amount | decimal | (opcional) valor do desconto                                                                                                                                                     |

### Boleto de Tributo (Concecionárias, Tributo com código de barras, FGTS)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros espefíficos para o pagamento de boletos de concecionárias ou tributos.

<aside class="info">
O attributo <code>amount</code> nesse caso é opcional, pois ele é identificado a partir do código de barras.
</aside>

**Parâmetros quando payment_method é 'dealdership' ou 'tribute_with_barcode'**

| Campo                     | Tipo    | Comentário                                          |
|---------------------------|---------|-----------------------------------------------------|
| barcode                   | string  | **(requerido)** Código de barras do boleto bancário |
| due_date                  | date    | **(requerido)** Data de vencimento do boleto        |

**Parâmetros quando payment_method é 'fgts'**

| Campo                  | Tipo    | Comentário                                                          |
|------------------------|---------|---------------------------------------------------------------------|
| barcode                | string  | **(requerido)** Código de barras do boleto bancário                 |
| taxpayer_document_type | string  | **(requerido)** Tipo do documento do contribuinte ("cnpj" ou "cei") |
| taxpayer_document      | string  | **(requerido)** Número do documento do contribuinte                 |

### Tributos sem código de barras (GPS, DARF, DAS, IPVA, ICMS-SP, DPVAT)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros específicos para cada tipo de tributo:

<aside class="info">
O attributo <code>payment_type</code> é automaticamente definido como <code>"tribute"</code>.
</aside>

**Parâmetros quando payment_method é 'gps'**

| Campo                     | Tipo    | Comentário                                                           |
|---------------------------|---------|----------------------------------------------------------------------|
| gps_payment_code          | string  | **(requerido)** código do GPS, de 4 dígitos                          |
| competency_month          | string  | **(requerido)** mês de competência do GPS, repesentado por 2 dígitos |
| competency_year           | string  | **(requerido)** ano de competência do GPS, repesentado por 4 dígitos |
| other_entities_amount     | decimal | (opcional) valor extra para outras entidades                         |
| monetary_update           | decimal | (opcional) atualização monetária, incluindo valores de juros e multa |

**Parâmetros quando payment_method é 'darf'**

| Campo                     | Tipo    | Comentário                                              |
|---------------------------|---------|---------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                      |
| calculation_period        | date    | **(requerido)** período de apuração                     |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos |
| reference_number          | string  | (opcional) número de referência                         |
| mulct_amount              | decimal | (opcional) valor da multa                               |
| interest_amount           | decimal | (opcional) valor do juros                               |

**Parâmetros quando payment_method é 'das'**

| Campo                     | Tipo    | Comentário                                              |
|---------------------------|---------|---------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                      |
| calculation_period        | date    | **(requerido)** período de apuração                     |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos |
| gross_revenue             | decimal | **(requerido)** Valor da receita bruta                  |
| gross_revenue_percentage  | decimal | **(requerido)** Valor da porcentagem da receita bruta   |
| mulct_amount              | decimal | (opcional) valor da multa                               |
| interest_amount           | decimal | (opcional) valor do juros                               |


**Parâmetros quando payment_method é 'ipva'**

| Campo                     | Tipo    | Comentário                                                                                  |
|---------------------------|---------|---------------------------------------------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                                                          |
| city_code                 | integer | **(requerido)** código da cidade                                                            |
| competency_year           | string  | **(requerido)** ano de competência do IPVA, repesentado por 4 dígitos                       |
| license_plate             | string  | **(requerido)** placa do carro                                                              |
| payment_option            | string  | **(requerido)** opção de pagamento. Possíveis valores na tabela 4                           |
| renavam                   | string  | **(requerido)** número do Renavam                                                           |
| uf                        | string  | **(requerido)** estado, representado por seu acrônimo (RJ, SC, etc)                         |
| discount_amount           | decimal | (opcional, requerido quando `payment_option` for 'single_with_discount') valor do desconto. |

**Parâmetros quando payment_method é 'icms_sp'**

| Campo                     | Tipo    | Comentário                                                               |
|---------------------------|---------|--------------------------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                                       |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos                  |
| competency_month          | string  | **(requerido)** mês de competência do ICMS-SP, repesentado por 2 dígitos |
| competency_year           | string  | **(requerido)** ano de competência do ICMS-SP, repesentado por 4 dígitos |
| state_registration        | string  | **(requerido)** registro estadual                                        |
| active_debt_registration  | string  | **(requerido)** registro de dívida ativa                                 |
| installment_number        | string  | **(requerido)** número da prestação                                      |
| mulct_amount              | decimal | (opcional) valor da multa                                                |
| interest_amount           | decimal | (opcional) valor do juros                                                |

**Parâmetros quando payment_method é 'dpvat'**

| Campo                     | Tipo    | Comentário                                                             |
|---------------------------|---------|------------------------------------------------------------------------|
| competency_year           | string  | **(requerido)** ano de competência do DPVAT, repesentado por 4 dígitos |
| license_plate             | string  | **(requerido)** placa do carro                                         |
| renavam                   | string  | **(requerido)** número do Renavam                                      |
| uf                        | string  | **(requerido)** estado, representado por seu acrônimo (RJ, SC, etc)    |
| discount_amount           | decimal | (opcional) valor do desconto.                                          |
| due_date                  | date    | (opcional) data de vencimento                                          |
| city_code                 | integer | (opcional) código da cidade                                            |

**payee**

| Campo                    | Tipo   | Comentário                                                                                                |
|--------------------------|--------|-----------------------------------------------------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo do documento do beneficiário (cpf ou cnpj)                                           |
| national_identifier      | string | **(requerido)** documento do beneficiário                                                                 |
| name                     | string | **(requerido)** nome do beneficiário                                                                      |


## Atualização de Pagamento

```shell
Atualizar Pagamento

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/payments/:id
  PATCH https://app.cobrato.com/api/v1/payments/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/payents/:id \
    -d '{
          "amount": "125.99"
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "amount": ["não pode ficar em branco"]
      }
  }

```

Atualiza um determinado Pagamento, retornando as informações do mesmo em caso de sucesso. Se houverem erros, eles serão informados no corpo da resposta. A requisição não diferencia a utilização dos verbos PUT e PATCH.

**Parâmetros comuns a todas as formas de pagamento**

| Campo                     | Tipo    | Comentário                           |
|---------------------------|---------|--------------------------------------|
| amount                    | decimal | **(requerido)** valor do pagamento   |
| date                      | date    | **(requerido)** data do pagamento    |
| note                      | string  | (opcional) oberservação do pagamento |

### Transferências (DOC, TED, Crédito)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros comuns aos pagamentos via transferência, além de alguns espefíficos para cada tipo de transferência.

**Parâmetros comuns à todos os pagamentos via transferência**

| Campo         | Tipo    | Comentário                                                                                                                                                                       |
|---------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| bank_code     | string  | **(requerido)** código de 3 dígitos do banco da conta bancária para o pagamento                                                                                                  |
| account       | string  | **(requerido)** número da conta bancária para o pagamento                                                                                                                        |
| account_digit | string  | **(requerido)** dígito da conta bancária para fazer o pagamento                                                                                                                  |
| agency        | string  | **(requerido)** número da agência da conta bancária para fazer o pagamento                                                                                                       |
| payee_id      | string  | **(requerido, se não enviar payee)** identificador do beneficiário (caso seja fornecido, o parâmetro `payee` será ignorado)                                                      |
| payee*        | object  | **(requerido, se não enviar payee_id)** atributos para a criação de um novo beneficiário ou atualização de um beneficiário existente com o mesmo documento (national_identifier) |

**Parâmetros quando payment_method é 'doc_other_ownership' ou 'doc_same_ownership'**

| Campo                     | Tipo    | Comentário                                                                    |
|---------------------------|---------|-------------------------------------------------------------------------------|
| doc_goal                  | string  | (opcional) código referente ao objetivo do DOC. Possíveis valores na tabela 2 |

**Parâmetros quando payment_method é 'ted_other_ownership'**

| Campo                     | Tipo    | Comentário                                                                    |
|---------------------------|---------|-------------------------------------------------------------------------------|
| ted_goal                  | string  | (opcional) código referente ao objetivo do TED. Possíveis valores na tabela 3 |

### Boleto Bancário (Boleto de mesmo banco, Boleto de outro Banco)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros espefíficos para o pagamento de boletos bancários.

**Parâmetros quando payment_method é 'billet_same_bank' ou 'billet_other_bank'**

| Campo           | Tipo    | Comentário                                                                                                                                                                       |
|-----------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payee_id        | string  | **(requerido, se não enviar payee)** identificador do beneficiário (caso seja fornecido, o parâmetro `payee` será ignorado)                                                      |
| payee*          | object  | **(requerido, se não enviar payee_id)** atributos para a criação de um novo beneficiário ou atualização de um beneficiário existente com o mesmo documento (national_identifier) |
| due_date        | date    | **(requerido)** Data de vencimento do boleto                                                                                                                                     |
| discount_amount | decimal | (opcional) valor do desconto                                                                                                                                                     |

### Boleto de Tributo (Concecionárias, Tributo com código de barras, FGTS)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros espefíficos para o pagamento de boletos de concecionárias ou tributos.

**Parâmetros quando payment_method é 'dealdership' ou 'tribute_with_barcode'**

| Campo                     | Tipo    | Comentário                                          |
|---------------------------|---------|-----------------------------------------------------|
| due_date                  | date    | **(requerido)** Data de vencimento do boleto        |

**Parâmetros quando payment_method é 'fgts'**

| Campo                  | Tipo    | Comentário                                                          |
|------------------------|---------|---------------------------------------------------------------------|
| taxpayer_document_type | string  | **(requerido)** Tipo do documento do contribuinte ("cnpj" ou "cei") |
| taxpayer_document      | string  | **(requerido)** Número do documento do contribuinte                 |

### Tributos sem código de barras (GPS, DARF, DAS, IPVA, ICMS-SP, DPVAT)

Além dos parâmetros comuns à todas as formas de pagamento, temos parâmetros específicos para cada tipo de tributo:

**Parâmetros quando payment_method é 'gps'**

| Campo                     | Tipo    | Comentário                                                           |
|---------------------------|---------|----------------------------------------------------------------------|
| gps_payment_code          | string  | **(requerido)** código do GPS, de 4 dígitos                          |
| competency_month          | string  | **(requerido)** mês de competência do GPS, repesentado por 2 dígitos |
| competency_year           | string  | **(requerido)** ano de competência do GPS, repesentado por 4 dígitos |
| other_entities_amount     | decimal | (opcional) valor extra para outras entidades                         |
| monetary_update           | decimal | (opcional) atualização monetária, incluindo valores de juros e multa |

**Parâmetros quando payment_method é 'darf'**

| Campo                     | Tipo    | Comentário                                              |
|---------------------------|---------|---------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                      |
| calculation_period        | date    | **(requerido)** período de apuração                     |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos |
| reference_number          | string  | (opcional) número de referência                         |
| mulct_amount              | decimal | (opcional) valor da multa                               |
| interest_amount           | decimal | (opcional) valor do juros                               |

**Parâmetros quando payment_method é 'das'**

| Campo                     | Tipo    | Comentário                                              |
|---------------------------|---------|---------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                      |
| calculation_period        | date    | **(requerido)** período de apuração                     |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos |
| gross_revenue             | decimal | **(requerido)** Valor da receita bruta                  |
| gross_revenue_percentage  | decimal | **(requerido)** Valor da porcentagem da receita bruta   |
| mulct_amount              | decimal | (opcional) valor da multa                               |
| interest_amount           | decimal | (opcional) valor do juros                               |

**Parâmetros quando payment_method é 'ipva'**

| Campo                     | Tipo    | Comentário                                                                                  |
|---------------------------|---------|---------------------------------------------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                                                          |
| city_code                 | integer | **(requerido)** código da cidade                                                            |
| competency_year           | string  | **(requerido)** ano de competência do IPVA, repesentado por 4 dígitos                       |
| license_plate             | string  | **(requerido)** placa do carro                                                              |
| payment_option            | string  | **(requerido)** opção de pagamento. Possíveis valores na tabela 4                           |
| renavam                   | string  | **(requerido)** número do Renavam                                                           |
| uf                        | string  | **(requerido)** estado, representado por seu acrônimo (RJ, SC, etc)                         |
| discount_amount           | decimal | (opcional, requerido quando `payment_option` for 'single_with_discount') valor do desconto. |

**Parâmetros quando payment_method é 'icms_sp'**

| Campo                     | Tipo    | Comentário                                                               |
|---------------------------|---------|--------------------------------------------------------------------------|
| due_date                  | date    | **(requerido)** data de vencimento                                       |
| receita_federal_code      | string  | **(requerido)** código da receita federal, de 4 dígitos                  |
| competency_month          | string  | **(requerido)** mês de competência do ICMS-SP, repesentado por 2 dígitos |
| competency_year           | string  | **(requerido)** ano de competência do ICMS-SP, repesentado por 4 dígitos |
| state_registration        | string  | **(requerido)** registro estadual                                        |
| active_debt_registration  | string  | **(requerido)** registro de dívida ativa                                 |
| installment_number        | string  | **(requerido)** número da prestação                                      |
| mulct_amount              | decimal | (opcional) valor da multa                                                |
| interest_amount           | decimal | (opcional) valor do juros                                                |

**Parâmetros quando payment_method é 'dpvat'**

| Campo           | Tipo    | Comentário                                                             |
|-----------------|---------|------------------------------------------------------------------------|
| competency_year | string  | **(requerido)** ano de competência do DPVAT, repesentado por 4 dígitos |
| license_plate   | string  | **(requerido)** placa do carro                                         |
| renavam         | string  | **(requerido)** número do Renavam                                      |
| uf              | string  | **(requerido)** estado, representado por seu acrônimo (RJ, SC, etc)    |
| discount_amount | decimal | (opcional) valor do desconto.                                          |
| due_date        | date    | (opcional) data de vencimento                                          |
| city_code       | integer | (opcional) código da cidade                                            |

**payee**

| Campo                    | Tipo   | Comentário                                                      |
|--------------------------|--------|-----------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo do documento do beneficiário (cpf ou cnpj) |
| national_identifier      | string | **(requerido)** documento do beneficiário                       |
| name                     | string | **(requerido)** nome do beneficiário                            |

## Exclusão de Pagamento

```shell
Excluir Pagamento

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/payment/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/payment/:id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

```

Exclui determinado Pagamento. As mudanças são irreversíveis.

## Cancelamento de Pagamento

```shell
Cancelar Pagamento

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payment/:id/cancel

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/payment/:id/cancel

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "registration_status": ["não permite cancelamento. Somente pagamentos com status 'Pagamento registrado' podem ser cancelados"]
      }
  }

```

Inicia o processo de cancelamento de um determinado Pagamento, retornando JSON contendo as informações do pagamento em caso de sucesso ou os erros, caso haja algum.

Após iniciar o processo de cancelamento será necessário gerar um arquivo de remessa, enviar para o banco e esperar o arquivo de retorno confirmando o cancelamento.

## Marcar Pagamento como não autorizado

```shell
Marcar Pagamento como não autorizado

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payment/:id/unauthorize

  EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/payment/:id/unauthorize

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "registration_status": ["Não é possível marcar este pagamento como não autorizado. Somente pagamentos com status 'registrado', NÃO efetivados e vencidos podem ser marcados como não autorizados"]
      }
  }

```

Marca um determinado Pagamento como não autorizado, retornando JSON com as informações do pagamento em caso de sucesso ou, caso contrário, os erros.

## Reagendar Pagamento


```shell
Reagendar Pagamento

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payments/:id/reschedule

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/payents/:id/reschedule \
    -d '{
          "date": "2018-10-02"
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "date": ["não pode ficar em branco"]
        "registration_status": ["não permite reagendar pagamento. Somente pagamentos com status 'Pagamento registrado', podem ser reagendados"]
      }
  }

```

Reagenda um determinado Pagamento. Se houverem erros, eles serão informados no corpo da resposta.

## Marcar pagamento com Erro no Registro

```shell
Marcar pagamento com Erro no Registro

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payment/:id/register_error

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/payment/:id/register_error

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM PAGAMENTO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "registration_status": ["não permite marcar como Erro no Registro"]
      }
  }

```

Marca o pagamento com Erro no registro manualmente.

Importante para pagamentos que tiveram o lote rejeitado pelo sistema do banco. Neste caso o banco não envia nenhum erro no arquivo de retorno e é necessário marcar manualmente.

## Schema de Pagamento

```shell
Schema de Pagamento

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payments/schema

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payments/schema?payment_config_id=1&payment_method=ted_other_ownership

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE CORPO DA RESPOSTA COM SUCESSO

  {
    "schema": {
      // json schema
    },
    "form": {
      // json schema form
    }
  }

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors": {
      "payment_method":["ao menos um dos parâmetros deve ser enviado: payment_method e barcode"],
      "barcode":["ao menos um dos parâmetros deve ser enviado: payment_method e barcode"],
      "payment_config_id":["não pode ficar em branco"]
    }
  }

```

Retorna o [json schema](http://json-schema.org/) e o [json schema form](https://github.com/myfreecomm/nexaas-json-schema-form) com as informações necessárias para criar um pagamento, baseado nos dados enviados.

**Parâmetros**

| Campo             | Tipo    | Comentário                                                                                                                                                                                                                                                              |
|-------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payment_config_id | integer | **(requerido)** código de identificação da configuração de pagamento à qual o pagamento irá pertencer                                                                                                                                                                   |
| payment_method    | string  | **(requerido, ou barcode)** forma de pagamento ('credit_other_ownership', 'credit_same_ownership', 'credit_savings_account', 'doc_other_ownership', 'doc_same_ownership', 'ted_other_ownership', 'ted_same_ownership', 'gps', 'darf', 'das', 'ipva', icms_sp', 'dpvat') |
| barcode           | string  | **(requerido, ou payment_method)** código de barras do pagamento                                                                                                                                                                                                        |

## Tabelas

### Possíveis valores para payment_type (tabela 1)

| payment_type ⟶ <br> payment_method ↴ | salary <br>&nbsp; | dividend <br>&nbsp; | debenture <br>&nbsp; | traveling_expense <br>&nbsp; | authorized_representative <br>&nbsp; | provider <br>&nbsp; | benefit <br>&nbsp; | insurance_claim <br>&nbsp; | investment_fund <br>&nbsp; | other <br>&nbsp; | tribute <br>&nbsp; |
|---------------------------------------:|:-----------------:|:-------------------:|:--------------------:|:----------------------------:|:------------------------------------:|:-------------------:|:------------------:|:--------------------------:|:--------------------------:|:----------------:|:------------------:|
| credit_other_ownership                 | X                 | X                   | X                    | X                            | X                                    | X                   | X                  | X                          | X                          | X                |                    |
| credit_same_ownership                  |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| credit_savings_account                 |                   | X                   |                      |                              |                                      | X                   | X                  | X                          |                            | X                |                    |
| doc_other_ownership                    |                   | X                   | X                    | X                            | X                                    | X                   | X                  | X                          |                            | X                |                    |
| doc_same_ownership                     |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| ted_other_ownership                    |                   | X                   | X                    | X                            | X                                    | X                   | X                  | X                          |                            | X                |                    |
| ted_same_ownership                     |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| billet_other_bank                      |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| billet_same_bank                       |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| dealdership                            |                   |                     |                      |                              |                                      | X                   |                    |                            |                            | X                |                    |
| tribute_with_barcode                   |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| fgts                                   |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| gps                                    |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| darf                                   |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| das                                    |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| ipva                                   |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| icms_sp                                |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |
| dpvat                                  |                   |                     |                      |                              |                                      |                     |                    |                            |                            |                  | X                  |

### Possíveis valores para doc_goal (tabela 2)

Quando *payment_method* for 'doc_other_ownership' todos os valores são aceitos. Contudo, quando *payment_method* for 'doc_same_ownership', apenas os valores '01' e '11' são aceitos.

| Código | Descrição                                                                  |
|--------|----------------------------------------------------------------------------|
| 01     | Crédito em Conta                                                           |
| 02     | Pagamento de Aluguel / Condomínio                                          |
| 03     | Pagamento de Duplicata / Títulos                                           |
| 04     | Pagamento de Dividendos                                                    |
| 05     | Pagamento de Mensalidade Escolar                                           |
| 06     | Pagamento de Salários                                                      |
| 07     | Pagamento de Fornecedores / Honorários                                     |
| 08     | Operações de Câmbio / Fundos                                               |
| 09     | Repasse de Arrecadação / Pagamento de Tributos                             |
| 10     | Transferência Internacional de Reais                                       |
| 11     | DOC para Poupança                                                          |
| 12     | DOC para Depósito Judicial                                                 |
| 13     | Pensão Alimentícia                                                         |
| 99     | Outros                                                                     |

### Possíveis valores para ted_goal (tabela 3)

| Código | Descrição                                                                  |
|--------|----------------------------------------------------------------------------|
| 00001  | Pagamento de Impostos, Tributos e Taxas                                    |
| 00002  | Pagamento a Concessionárias de Serviço Público                             |
| 00003  | Pagamento de Dividendos                                                    |
| 00004  | Pagamento de Salários                                                      |
| 00005  | Pagamento de Fornecedores                                                  |
| 00006  | Pagamento de Honorários                                                    |
| 00007  | Pagamento de Aluguéis e Taxas e Condomínio                                 |
| 00008  | Pagamento de Duplicatas e Títulos                                          |
| 00009  | Pagamento de Honorários                                                    |
| 00010  | Crédito em Conta                                                           |
| 00011  | Pagamento a Corretoras                                                     |
| 00016  | Crédito em Conta Investimento                                              |
| 00100  | Depósito Judicial                                                          |
| 00101  | Pensão Alimentícia                                                         |
| 00200  | Transferência Internacional de Reais                                       |
| 00201  | Ajuste Posição Mercado Futuro                                              |
| 00204  | Compra/Venda de Ações - Bolsas de Valores e Mercado de Balcão              |
| 00205  | Contrato referenciado em Ações/Índices de Ações - BV/BMF                   |
| 00300  | Restituição de Imposto de Renda                                            |
| 00500  | Restituição de Prêmio de Seguros                                           |
| 00501  | Pagamento de indenização de Sinistro de Seguro                             |
| 00502  | Pagamento de Prêmio de Co-seguro                                           |
| 00503  | Restituição de prêmio de Co-seguro                                         |
| 00504  | Pagamento de indenização de Co-seguro                                      |
| 00505  | Pagamento de prêmio de Resseguro                                           |
| 00506  | Restituição de prêmio de Resseguro                                         |
| 00507  | Pagamento de Indenização de Sinistro de Resseguro                          |
| 00508  | Restituição de Indenização de Sinistro de Resseguro                        |
| 00509  | Pagamento de Despesas com Sinistros                                        |
| 00510  | Pagamento de Inspeções/Vistorias Prévias                                   |
| 00511  | Pagamento de Resgate de Título de Capitalização                            |
| 00512  | Pagamento de Sorteio de Título de Capitalização                            |
| 00513  | Pagamento de Devolução de Mensalidade de Título de Capitalização           |
| 00514  | Restituição de Contribuição de Plano Previdenciário                        |
| 00515  | Pagamento de Benefício Previdenciário de Pecúlio                           |
| 00516  | Pagamento de Benefício Previdenciário de Pensão                            |
| 00517  | Pagamento de Benefício Previdenciário de Aposentadoria                     |
| 00518  | Pagamento de Resgate Previdenciário                                        |
| 00519  | Pagamento de Comissão de Corretagem                                        |
| 00520  | Pagamento de Transferências/Portabilidade de Reserva de Seguro/Previdência |

### Possíveis valores para payment_option (tabela 4)

| Opção de pagamento       | Descrição              |
|--------------------------|------------------------|
| single_with_discount     | Simples com desconto   |
| single_without_discount  | Simples sem desconto   |
| installment_1            | Primeira prestação     |
| installment_2            | Segunda prestação      |
| installment_3            | Terceira prestação     |
| installment_4            | Quarta prestação       |
| installment_5            | Quinta prestação       |
| installment_6            | Sexta prestação        |
