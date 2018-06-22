# Configuração de Cobrança

```shell
Configuração de Cobrança

EXEMPLO

  {
    "id": 1,
    "type": "billet",
    "payee_id": 1,
    "bank_account_id": 1,
    "portfolio_code": "17",
    "agreement_code": "12345678",
    "agreement_code_digit": "1",
    "name": "Configuração de Cobrança por Boleto",
    "initial_number": 1,
    "next_number": 1,
    "end_number": 1000,
    "status": "pending",
    "registered_charges": true,
    "remittance_agreement_code": 4576361,
    "remittance_cnab_pattern": 400,
    "initial_remittance_number": 1,
    "transmission_code": "987655",
    "pre_released_billet": false,
    "writing_off_deadline": null,
    "available_charge_types": ["billet"],
    "_links":
      [
        {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"bank_account","method":"GET","href":"https://app.cobrato.com/api/v1/bank_accounts/1"},
        {"rel":"payee","method":"GET","href":"https://app.cobrato.com/api/v1/payee/1"}
      ]
  }

```

As Configurações de Cobrança podem ser de tipos diferentes. Sendo assim, os parâmetros e algums comportamentos irão variar de acordo com o tipo. Atualmente temos os tipos:

- Conta Bancária (billet)
- Gateway de pagamento (payment_gateway)

<aside class="warning">
  As Configurações de Cobrança <strong>precisam ser homologadas antes de serem utilizadas normalmente</strong>. Veja como homologar cada tipo de Configuração de Cobrança em suas informações específicas.
</aside>

### Conta bancária

As Configurações de Cobrança do tipo **Conta bancária** (billet), pertencem as suas contas bancárias, sendo assim é necessário que sempre haja ao menos uma conta bancária para criação desse tipo configuração de cobrança, que também tem suas validações de acordo com o banco de sua conta bancária.

<aside class="info">
  Para homologar a Configuração de Cobrança existe uma série de passos que você encontra em
  <a href="https://app.cobrato.com/charge_configs">nossa interface web</a>. Cada gateway de pagamento tem um processo
  de homologação específico. Até que a Configuração tenha o status "ok" (Homologado), todas as cobranças criadas para
  esta Configuração deverão ser para homologação.
</aside>

**Parâmetros**

| Campo                     | Tipo             | Comentário                                                                                                                                                                |
|---------------------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                        | integer          |                                                                                                                                                                           |
| type                      | string           | indica o tipo da configuração de cobrança. Nesse caso 'billet'                                                                                                            |
| name                      | string           | nome que identifica esta configuração de cobrança                                                                                                                         |
| status                    | string           | 'ok' ou 'pending' para indicar se configuração de cobrança está ou não homologada, respectivamente                                                                        |
| payee_id                  | integer          | identificador do beneficiário desta configuração de cobrança no Cobrato                                                                                                   |
| bank_account_id           | integer          | identificador da conta bancária desta configuração de cobrança no Cobrato                                                                                                 |
| portfolio_code            | string           | código de portfólio                                                                                                                                                       |
| agreement_code            | string           | código de convênio ou do beneficiário, de acordo com o banco. No caso do Itaú deve ser igual ao campo 'account' da conta bancária                                         |
| agreement_code_digit      | string           | verificador do código de convênio, de acordo com o banco                                                                                                                  |
| initial_number            | integer          | número inicial do nosso número, sendo atribuído automaticamente e sequencialmente as cobranças                                                                            |
| next_number               | integer          | próximo nosso número a ser atribuído a uma cobrança criada a partir desta configuração de cobrança                                                                        |
| end_number                | integer          | número final do nosso número, sendo o último número a ser atribuído, após isso a sequência é reiniciada                                                                   |
| registered_charges        | boolean          | informa se a configuração de cobrança utiliza boletos registrados ou não, sendo false por padrão                                                                          |
| remittance_agreement_code | integer          | número do convênio com o banco (apenas para o Bradesco)                                                                                                                   |
| remittance_cnab_pattern   | integer          | padrão utilizado no arquivo CNAB de remessa                                                                                                                               |
| initial_remittance_number | integer          | número inicial de remessa, ou seja, qual foi o último número sequencial de remessa enviado para o banco (apenas para o Bradesco)                                          |
| transmission_code         | string           | código de transmissão (apenas para o Santander)                                                                                                                           |
| pre_released_billet       | boolean          | caso a configuração de cobrança utilize boletos registrados, este atributo indica se os boletos podem ser acessados antes do registro no banco ser confirmado             |
| writing_off_deadline      | integer          | número de dias após o vencimento da cobrança para que seja feita a baixa automática do título no banco (apenas para cobranças registradas com padrão 240)                 |
| available_charge_types    | array of strings | tipos de cobrança disponíveis. No caso de Configuração de Cobrança por Conta Bancária, será disponível somente a opção "billet". Este campo será gerenciado pelo Cobrato  |
| _links                    | array of object  | links da configuração de cobrança e de sua conta bancária                                                                                                                 |


### Gateway de Pagamento

<aside class="info">
  Para homologar a Configuração de Cobrança existe uma série de passos que você encontra em
  <a href="https://app.cobrato.com/wizard/payment_gateway/configs/new">nossa interface web</a>. Até
  que a Configuração tenha o status "ok" (Homologado), todas as cobranças criadas para esta Configuração
  serão consideradas Cobranças para homologação.
</aside>

**Parâmetros comuns a todos os Gateways**

| Campo                   | Tipo             | Comentário                                                                                                                                                                             |
|-------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                      | integer          |                                                                                                                                                                                        |
| type                    | string           | indica o tipo da configuração de cobrança. Nese caso 'payment_gateway'                                                                                                                 |
| name                    | string           | nome que identifica esta configuração de cobrança                                                                                                                                      |
| status                  | string           | indica o status, ou etapa, de homologação em que configuração de cobrança está ('pending', 'production_tests', 'ok')                                                                   |
| payee_id                | integer          | identificador do beneficiário desta configuração de cobrança no Cobrato                                                                                                                |
| gateway_name            | string           | nome do gateway de pagamento ('cielo-ws15', 'cielo-api30', 'pjbank')                                                                                                                   |
| available_charge_types  | array of strings | tipos de cobrança disponíveis. No caso de Configuração de Cobrança por Gateway de Pagamento, as opções possíveis são "billet" e "credit_card". Este campo será gerenciado pelo Cobrato |
| _links                  | array of object  | links da configuração de cobrança e de sua conta bancária                                                                                                                              |

**Parâmetros específicos para gateway Cielo**

| Campo        | Tipo            | Comentário                                                                                                            |
|--------------|-----------------|-----------------------------------------------------------------------------------------------------------------------|
| gateway_id   | string          | número de afiliação do contrato com o gateway de pagamento                                                            |
| gateway_key  | string          | chave de acesso atribuída pelo gateway de pagamento                                                                   |
| use_avs      | boolean         | define se será feita a solicitação e a confirmação do endereço de cobrança da fatura do cartão utilizado no pagamento |

**Parâmetros específicos para gateway PJBank**

| Campo              | Tipo            | Comentário                                                                                                      |
|--------------------|-----------------|-----------------------------------------------------------------------------------------------------------------|
| gateway_id         | string          | credencial do contrato com o gateway de pagamento para cobranças de **cartão de crédito**                       |
| gateway_key        | string          | chave de acesso atribuída pelo gateway de pagamento para cobranças de **cartão de crédito**                     |
| billet_gateway_id  | string          | credencial do contrato com o gateway de pagamento para cobranças de **boleto**                                  |
| billet_gateway_key | string          | chave de acesso atribuída pelo gateway de pagamento para cobranças de **boleto**                                |


## Informações da Configuração de Cobrança

```shell
Mostrar Configuração de Cobrança

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/charge_configs/:charge_config_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/charge_configs/:charge_config_id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA (BOLETO)

  {
    "id": 1,
    "type": "billet",
    "payee_id": 1,
    "bank_account_id": 1,
    "portfolio_code": "17",
    "agreement_code": "12345678",
    "agreement_code_digit": "1",
    "name": "Configuração de Cobrança por Boleto",
    "initial_number": 1,
    "next_number": 1,
    "end_number": 1000,
    "status": "pending",
    "registered_charges": true,
    "remittance_agreement_code": 4576361,
    "remittance_cnab_pattern": 400,
    "initial_remittance_number": 1,
    "transmission_code": "987655",
    "pre_released_billet": false,
    "writing_off_deadline": null,
    "available_charge_types": ["billet"],
    "deactivated_at": "2018-04-10T17:46:01.253Z",
    "_links":
      [
        {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel":"bank_account","method":"GET","href":"https://app.cobrato.com/api/v1/bank_accounts/1"},
        {"rel":"payee","method":"GET","href":"https://app.cobrato.com/api/v1/payees/1"}
      ]
  }

```

Retorna as informações detalhadas da Configuração de Cobrança informada em JSON e também suas referências.

## Lista de Todas as Configurações de Cobrança

```shell
Listar Configurações de Cobrança

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/charge_configs

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/charge_configs

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "charge_configs":
      [
        {
          // informações configuração de cobrança 1
        },
        {
          // informações configuração de cobrança 2
        },
        ...
      ]
  }

```

Retorna uma lista em JSON contendo todas as Configurações de Cobrança que pertencem a sua Conta de Serviço.

É possível filtrar a lista através dos seguintes parâmetros:

- `type`: Filtra pelo tipo de configuração de cobrança. O valor a ser informado é string com um dos tipos existentes de configuração de cobrança.
- `charge_type`: Filtra pelo tipo de cobrança disponível para a configuração, ou seja retornará as configurações que suportam o tipo de cobrança informado. O valor a ser informado é a string com um dos tipos de cobrança disponíveis ("billet" ou "credit_card" até o momento).
- `bank_code`: Filtrar pelo código do banco da configuração de cobrança. O valor a ser informado é uma string com o código do banco. Por exemplo "341" para Itaú, "237" para Bradesco e etc.
- `payee_ids`: Filtra pelos beneficiários informados. O valor informado é uma **lista\*** de ids dos beneficiários.
- `payee_national_identifiers`: Filtra pelos beneficiários informados. O valor informado é uma **lista\*** de número de documentos dos beneficiários.

**lista\*** Os valores em "lista" devem ser enviados da seguinte forma: `url?payee_ids[]=15&payee_ids[]=42`.

## Criação de Configuração de Cobrança

```shell
Criar Configuração de Cobrança

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/charge_configs

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/charge_configs \
    -d '{
          "type": "billet",
          "payee_id": "1",
          "bank_account_id": "1",
          "portfolio_code": "17",
          "agreement_code": "12345678",
          "agreement_code_digit": "1",
          "name": "Configuração de Cobrança por Boleto",
          "initial_number": "1",
          "end_number": "1000",
          "registered_charges": "true",
          "remittance_agreement_code": "4576361",
          "remittance_cnab_pattern": "400",
          "initial_remittance_number": "1"
          "transmission_code": "987655"
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "name":["não pode ficar em branco"],
        "portfolio_code":["não pode ficar em branco"],
        "agreement_code":["não pode ficar em branco"],
        "agreement_code_digit":["não pode ficar em branco"]
      }
  }

```

Cria uma nova Configuração de Cobrança, retornando as informações da mesma em caso de sucesso. Se houverem erros eles serão informados no corpo da resposta.

### Boleto

**Parâmetros**

| Campo                     | Tipo    | Comentário                                                                                                                                                                                                      |
|---------------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type                      | string  | (opcional) indica o tipo da configuração de cobrança. Neste caso deve ser informado "billet" ou deixado em branco, pois este é o valor padrão                                                                   |
| payee_id                  | integer | **(requerido)** código de identificação do beneficiário ao qual a configuração de cobrança irá pertencer                                                                                                        |
| bank_account_id           | integer | **(requerido)** código de identificação da conta bancária em que a configuração de cobrança irá pertencer                                                                                                       |
| portfolio_code            | string  | **(requerido)** código de portfólio, validação conforme o banco                                                                                                                                                 |
| agreement_code            | string  | **(requerido, com exceção do Itaú onde é preenchido automaticamente)** código de convênio ou do beneficiário, de acordo com o banco                                                                             |
| agreement_code_digit      | string  | **(requerido, com exceção do HSBC e Itaú, sendo preenchido automaticamente para o último)** verificador do código de convênio, de acordo com o banco                                                            |
| name                      | string  | **(requerido)** nome que identifica esta configuração de cobrança                                                                                                                                               |
| initial_number            | integer | **(requerido)** número inicial do nosso número, sendo atribuído automaticamente e sequencialmente às cobranças                                                                                                  |
| end_number                | integer | (opcional) número final do nosso número, sendo o último número a ser atribuído, após isso a sequência é reiniciada                                                                                              |
| next_number               | integer | (opcional) próximo nosso número a ser atribuído a uma cobrança criada a partir desta configuração de cobrança (por padrão inicia com o valor de `initial_number` e é incrementado automatica e sequencialmente) |
| registered_charges        | boolean | (opcional) informa se a configuração de cobrança utiliza boletos registrados ou não, sendo false por padrão                                                                                                     |
| remittance_agreement_code | integer | (opcional, requerido apenas se registered_charges for `true`) número do convênio com o banco (apenas para o Bradesco)                                                                                           |
| remittance_cnab_pattern   | integer | (opcional, requerido apenas se registered_charges for `true`) padrão utilizado no arquivo CNAB de remessa. Os valores permitidos são 240 ou 400                                                                 |
| transmission_code         | string  | (opcional, requerido apenas se registered_charges for `true`) código de transmissão (apenas para o Santander)                                                                                                   |
| initial_remittance_number | integer | (opcional) número inicial de remessa, ou seja, qual foi o último número sequencial de remessa enviado para o banco (apenas para o Bradesco). Por padrão o valor é 1                                             |
| pre_released_billet       | boolean | (opcional) caso a configuração de cobrança utilize boletos registrados, este atributo indica se os boletos podem ser acessados antes do registro no banco ser confirmado. Por padrão é `false`                  |
| writing_off_deadline      | integer | (opcional) número de dias após o vencimento da cobrança para que seja feita a baixa automática do título no banco. Valor pode variar entre 7 e 90. (apenas para cobranças registradas com padrão 240)           |

<aside class="warning">
  <strong>ATENÇÃO!</strong> Caso seu cliente pague o boleto antes do banco ter confirmado seu registro, <strong>o pagamento pode ser devolvido</strong> e/ou o banco pode te cobrar uma sobretaxa. Ao definir o campo <code>pre_released_billet</code> como <code>true</code>, você está assumindo este risco.
</aside>

### Gateway de Pagamento

**Parâmetros comuns a todos os Gateways**

| Campo        | Tipo    | Comentário                                                                                                                                            |
|--------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| type         | string  | **(requerido)** indica o tipo da configuração de cobrança. Neste caso deve ser informado "payment_gateway"                                            |
| payee_id     | integer | **(requerido)** código de identificação do beneficiário ao qual a configuração de cobrança irá pertencer                                              |
| name         | string  | **(requerido)** nome que identifica esta configuração de cobrança                                                                                     |
| gateway_name | string  | **(requerido)** nome do gateway de pagamento ('cielo-ws15', 'cielo-api30', 'pjbank')*                                                                 |

**Parâmetros para o gateway Cielo**

| Campo        | Tipo    | Comentário                                                                                                                                            |
|--------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| gateway_id   | string  | **(requerido)** número de afiliação do contrato com o gateway de pagamento                                                                            |
| gateway_key  | string  | **(requerido)** chave de acesso atribuída pelo gateway de pagamento                                                                                   |
| use_avs      | boolean | (opcional) define se será feita a solicitação e a confirmação do endereço de cobrança da fatura do cartão utilizado no pagamento (`false` por padrão) |
| status       | string  | (opcional, default "pending") indica o status, ou etapa, de homologação em que configuração de cobrança está ('pending', 'production_tests', 'ok')    |

**Parâmetros para o gateway PJBank**

| Campo               | Tipo    | Comentário                                                                                                                                                           |
|---------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| gateway_id          | string  | **(requerido, somente quando o campo 'gateway_key' estiver preenchido)** credencial do contrato com o gateway de pagamento para cobranças de **cartão de crédito**   |
| gateway_key         | string  | **(requerido, somente quando o campo 'gateway_id' estiver preenchido)** chave de acesso atribuída pelo gateway de pagamento para cobranças de **cartão de crédito**  |
| billet_gateway_id   | string  | **(requerido, somente quando o campo 'billet_gateway_key' estiver preenchido)** credencial do contrato com o gateway de pagamento para cobranças de **boleto**       |
| billet_gateway_key  | string  | **(requerido, somente quando o campo 'billet_gateway_id' estiver preenchido)** chave de acesso atribuída pelo gateway de pagamento para cobranças de **boleto**      |


<strong>*</strong> Os possíveis valores para o <code>gateway_name</code> são os seguintes:</p>

<dl>
  <dt>cielo-api30</dt>
  <dd>API e-Commerce Cielo</dd>
</dl>
<dl>
  <dt>cielo-ws15</dt>
  <dd>Webservice 1.5</dd>
</dl>
<dl>
  <dt>pjbank</dt>
  <dd>PJBank</dd>
</dl>

## Atualização de Configuração de Cobrança

```shell
Atualizar Configuração de Cobrança

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/charge_configs/:charge_config_id
  PATCH https://app.cobrato.com/api/v1/charge_configs/:charge_config_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/charge_configs/:charge_config_id \
    -d '{
          "portfolio_code": "17",
          "agreement_code": "12345678",
          "agreement_code_digit": "1",
          "name": "Novo Nome"
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM CONFIGURAÇÃO DE COBRANÇA INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":
      {
        "bank_code": ["não possui o tamanho esperado (3 caracteres)"],
        "agency": ["não é um número"],
        "account": ["não é um número"],
      }
  }

```

Atualiza a Configuração de Cobrança determinada, retornando as informações da mesma em caso de sucesso. Se houverem erros, eles serão informados no corpo da resposta. A requisição não diferencia a utilização dos verbos PUT e PATCH.

### Boleto

**Parâmetros**

| Campo                     | Tipo    | Comentário                                                                                                                                                                                            |
|---------------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payee_id                  | integer | **(requerido)** código de identificação do beneficiário ao qual a configuração de cobrança irá pertencer                                                                                              |
| portfolio_code            | string  | **(requerido)** código de portfólio, validação conforme o banco                                                                                                                                       |
| agreement_code            | string  | **(requerido, com exceção do Itaú onde é preenchido automaticamente)** código de convênio ou do beneficiário, de acordo com o banco                                                                   |
| agreement_code_digit      | string  | **(requerido, com exceção do HSBC e Itaú, sendo preenchido automaticamente para o último)** verificador do código de convênio, de acordo com o banco                                                  |
| name                      | string  | **(requerido)** nome que identifica esta configuração de cobrança                                                                                                                                     |
| initial_number            | integer | **(requerido)** número inicial do nosso número, sendo atribuído automaticamente e sequencialmente às cobranças                                                                                        |
| end_number                | integer | (opcional) número final do nosso número, sendo o último número a ser atribuído, após isso a sequência é reiniciada                                                                                    |
| next_number               | integer | (opcional) próximo nosso número a ser atribuído a uma cobrança criada a partir desta configuração de cobrança (é incrementado automatica e sequencialmente)                                           |
| registered_charges        | boolean | (opcional) informa se a configuração de cobrança utiliza boletos registrados ou não, sendo false por padrão                                                                                           |
| remittance_agreement_code | integer | (opcional, requerido apenas se registered_charges for `true`) número do convênio com o banco (apenas para o Bradesco)                                                                                 |
| remittance_cnab_pattern   | integer | (opcional, requerido apenas se registered_charges for `true`) padrão utilizado no arquivo CNAB de remessa. Os valores permitidos são 240 ou 400                                                       |
| transmission_code         | string  | (opcional, requerido apenas se registered_charges for `true`) código de transmissão (apenas para o Santander)                                                                                         |
| initial_remittance_number | integer | (opcional) número inicial de remessa, ou seja, qual foi o último número sequencial de remessa enviado para o banco (apenas para o Bradesco). Por padrão o valor é 1                                   |
| pre_released_billet       | boolean | (opcional) caso a configuração de cobrança utilize boletos registrados, este atributo indica se os boletos podem ser acessados antes do registro no banco ser confirmado. Por padrão é `false`        |
| writing_off_deadline      | integer | (opcional) número de dias após o vencimento da cobrança para que seja feita a baixa automática do título no banco. Valor pode variar entre 7 e 90. (apenas para cobranças registradas com padrão 240) |

<aside class="warning">
  <strong>ATENÇÃO!</strong> Caso seu cliente pague o boleto antes do banco ter confirmado seu registro, <strong>o pagamento pode ser devolvido</strong> e/ou o banco pode te cobrar uma sobretaxa. Ao definir o campo <code>pre_released_billet</code> como <code>true</code>, você está assumindo este risco.
</aside>

### Gateway de Pagamento

**Parâmetros comuns a todos os Gateways**

| Campo        | Tipo    | Comentário                                                                                                                                            |
|--------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| name         | string  | **(requerido)** nome que identifica esta configuração de cobrança                                                                                     |
| payee_id     | integer | **(requerido)** código de identificação do beneficiário ao qual a configuração de cobrança irá pertencer                                              |
| gateway_name | string  | **(requerido)** nome do gateway de pagamento ('cielo-ws15', 'cielo-api30', 'pjbank')*                                                                 |

**Parâmetros para o gateway Cielo**

| Campo        | Tipo    | Comentário                                                                                                                                            |
|--------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| gateway_id   | string  | **(requerido)** número de afiliação do contrato com o gateway de pagamento                                                                            |
| gateway_key  | string  | **(requerido)** chave de acesso atribuída pelo gateway de pagamento                                                                                   |
| use_avs      | boolean | (opcional) define se será feita a solicitação e a confirmação do endereço de cobrança da fatura do cartão utilizado no pagamento (`false` por padrão) |
| status       | string  | (opcional, default "pending") indica o status, ou etapa, de homologação em que configuração de cobrança está ('pending', 'production_tests', 'ok')    |

**Parâmetros para o gateway PJBank**

| Campo               | Tipo    | Comentário                                                                                                                                                           |
|---------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| gateway_id          | string  | **(requerido, somente quando o campo 'gateway_key' estiver preenchido)** credencial do contrato com o gateway de pagamento para cobranças de **cartão de crédito**   |
| gateway_key         | string  | **(requerido, somente quando o campo 'gateway_id' estiver preenchido)** chave de acesso atribuída pelo gateway de pagamento para cobranças de **cartão de crédito**  |
| billet_gateway_id   | string  | **(requerido, somente quando o campo 'billet_gateway_key' estiver preenchido)** credencial do contrato com o gateway de pagamento para cobranças de **boleto**       |
| billet_gateway_key  | string  | **(requerido, somente quando o campo 'billet_gateway_id' estiver preenchido)** chave de acesso atribuída pelo gateway de pagamento para cobranças de **boleto**      |

## Exclusão de Configuração de Cobrança

```shell
Excluir Configuração de Cobrança

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/charge_configs/:charge_config_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/charge_configs/:charge_config_id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM CONFIGURAÇÃO DE COBRANÇA INEXISTENTE

    404 Not Found

```

Exclui determinada Configuração de Cobrança e junto a ela todas suas Cobranças. As mudanças são irreversíveis.

## Desativação de Configuração de Cobrança

```shell
Desativar Configuração de Cobrança

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/charge_configs/:id/deactivate

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/charge_configs/:id/deactivate

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM CONFIGURAÇÃO DE COBRANÇA INEXISTENTE

    404 Not Found

```

Desativa determinada Configuração de Cobrança.
