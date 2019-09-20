# Cartão de Crédito

```shell
Cartão de Crédito

EXEMPLO

  {
    "id": 8,
    "token": "kUzSKmYvKpGQTAZtXbgefPFUt/i1N+rNHb4UJGM0u2E=",
    "national_identifier": "444.023.930-78",
    "number": "545301******6167",
    "holder_name": "John Doe",
    "brand": "amex",
    "expiration": "05/18",
    "avs_address": "Rua Julio de Castilhos",
    "avs_number": "100",
    "avs_complement": "Apto 103",
    "avs_district": "Centro",
    "avs_zipcode": "99000-750",
    "reusability_status": "error",
    "reusability_error_message": "Código de segurança inválido",
    "payer_id": 1,
    "charge_config_id": 12,
    "_links": [
      { "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/credit_cards/8" }
    ]
  }
```

Os Cartões de Crédito pertencem ao Pagador utilizado no momento de sua criação (primeira utilização em uma Cobrança) e, dessa forma, só pode ser reutilizado em Cobranças onde o Pagador é o mesmo.

**Parâmetros**

| Campo                     | Tipo            | Comentário                                                                                                                               |
|---------------------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------|
| token                     | string          | token do cartão gerado com o CobratoJS                                                                                                   |
| national_identifier       | string          | cpf do portador do cartão                                                                                                                |
| number                    | string          | números do cartão (incompleto, apenas para identificação)                                                                                |
| expiration                | string          | expiração do cartão, no formato "mm/aa"                                                                                                  |
| holder_name               | string          | nome do dono do cartão                                                                                                                   |
| brand                     | string          | bandeira do cartão (visa, mastercard, amex, elo, diners, discover, jcb, aura)                                                            |
| avs_address               | string          | endereço de cobrança do cartão                                                                                                           |
| avs_number                | string          | número do endereço de cobrança do cartão                                                                                                 |
| avs_complement            | string          | complemento endereço de cobrança do cartão                                                                                               |
| avs_district              | string          | bairro do endereço de cobrança do cartão                                                                                                 |
| avs_zipcode               | string          | cep do endereço de cobrança do cartão                                                                                                    |
| reusability_status        | string          | status da configuração para possibilitar o reuso o cartão em futuras cobranças (pending, ok, error)                                      |
| reusability_error_message | string          | informa o motivo do erro na configuração de reuso, apenas quando o atributo reusability_status tem o valor "error"                       |
| payer_id                  | integer         | identificador do Payer ao qual este cartão pertence                                                                                      |
| charge_config_id          | integer         | identificador da ChargeConfig à qual este cartão pertence                                                                                |
| _links                    | array of object | links do estabelecimento                                                                                                                    |

**reusability_status**

O atributo `reusability_status` pode ter os seguintes valores:

| Valor        | Descrição                                                                                                                  |
|--------------|----------------------------------------------------------------------------------------------------------------------------|
| pending      | assim que é criado e ainda não foi feita verificação do cartão através de uma cobrança                                     |
| error        | quando ocorre um erro na utilização do cartão (o erro ficará descrito no atributo `reusability_error_message`)             |
| reusable     | quando já foi feita uma cobrança com sucesso utilizando o cartão e ele foi salvo para ser reutilizado em futuras cobranças |
| not_reusable | quando o cartão não foi salvo para ser reutilizado                                                                         |


## Informações do Cartão de Crédito

```shell
Mostrar Cartão de Crédito

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/credit_cards/:credit_card_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/credit_cards/:credit_card_id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id": 8,
    "token": "kUzSKmYvKpGQTAZtXbgefPFUt/i1N+rNHb4UJGM0u2E=",
    "national_identifier": "444.023.930-78",
    "number": "545301******6167",
    "holder_name": "John Doe",
    "brand": "amex",
    "expiration": "05/18",
    "avs_address": "Rua Julio de Castilhos",
    "avs_number": "100",
    "avs_complement": "Apto 103",
    "avs_district": "Centro",
    "avs_zipcode": "99000-750",
    "reusability_status": "error",
    "reusability_error_message": "Código de segurança inválido",
    "payer_id": 1,
    "charge_config_id": 12,
    "_links": [
      { "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/credit_cards/8" }
    ]
  }
```

Retorna as informações detalhadas do cartão de crédito informado em JSON.


## Lista dos Cartões de crédito

```shell
Listar Cartões de Crédito

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/credit_cards

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/credit_cards?charge_config_id=12

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "credit_cards":
      [
        {
          // informações cartão de crédito 1
        },
        {
          // informações cartão de crédito 2
        },
        ...
      ]
  }

```

Retorna uma lista em JSON contendo os Cartões de Crédito pertencentes à sua Conta de Serviço.

É possível filtrar a lista através dos parâmetros: `payer_id`, `charge_config_id`, `number`, `holder_name`, `brand`, `reusability_status`

## Criação de Cartão de Crédito

```shell
Criar Cartão de Crédito

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/credit_cards

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/credit_cards \
    -d '{
        "token": "kUzSKmYvKpGQTAZtXbgefPFUt/i1N+rNHb4UJGM0u2E=",
        "national_identifier": "444.023.930-78",
        "number": "5453010000066167",
        "holder_name": "John Doe",
        "brand": "mastercard",
        "expiration": "05/18",
        "cvv": "123",
        "avs_address": "Rua Julio de Castilhos",
        "avs_number": "100", 
        "avs_complement": "Apto 103",
        "avs_district": "Centro",
        "avs_zipcode": "99000-750",
        "payer_id": 1,
        "charge_config_id": 12,
        "soft_descriptor": "CompanyName"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":{
      "number": ["não pode ficar em branco"],
      "holder_name": ["não pode ficar em branco"]
    }
  }

```

Cria um novo Cartão de Crédito com o objetivo de utilizá-lo em futuras cobranças
sem a necessidade de solicitar novamente ao usuário os dados do cartão. Para que
o cartão seja homologado, é feita uma cobrança com o valor entre R$ 1,00 e R$
2,00 que é automaticamente cancelada em seguida.

Se houverem erros a criação o cartão, eles serão informados no corpo da resposta.

Em caso de sucesso, as informações do cartão são retornadas. Contudo, o cartão
ainda não estará apto para re-utilização em novas cobranças. Isto só ocorrerá
quando a cobrança de homologação for concluída com sucesso. Esta informação pode
ser obtida através do atributo `reusability_status`. Caso ele tenha o valor
"pending", quer dizer que a cobrança ainda não foi feita. Caso tenha o valor
"reusable" quer dizer que o cartão pode ser reutilizado. Caso tenha o valor
"error",  significa que ocorreu um erro na cobrança de homologação, e o motivo
pode ser verificado no atributo `reusability_error_message`.

**Parâmetros**

| Campo               | Tipo    | Comentário                                                                                                                                                               |
|-------------------  |---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| token               | string  | **(requerido para cobranças PJBank)** token do cartão                                                                                                                    |
| national_identifier | string  | **(requerido para cobranças PJBank)** cpf do portador do cartão                                                                                                          |
| number              | string  | **(requerido)** número do cartão                                                                                                                                         |
| expiration          | string  | **(requerido)** expiração do cartão, no formato "mm/aa" ou "mm/aaaa"                                                                                                     |
| holder_name         | string  | **(requerido)** nome do dono do cartão                                                                                                                                   |
| cvv                 | string  | **(requerido)** código de segurança do cartão                                                                                                                            |
| brand               | string  | **(requerido)** bandeira do cartão (visa, mastercard, amex, elo, diners, discover, jcb, aura)                                                                            |
| charge_config_id    | integer | **(requerido)** identificador da ChargeConfig à qual este cartão pertence                                                                                                |
| payer_id            | integer | **(requerido, se não enviar payer_attributes )** identificador do pagador ao qual este cartão pertence (caso seja fornecido, o parâmetro payer_attributes será ignorado) |
| payer_attributes*   | object  | **(requerido, se não enviar payer_id )** atributos para a criação de um novo pagador ou atualização de um pagador existente com o mesmo documento (national_identifier)  |
| avs_address         | string  | (opcional) endereço de cobrança do cartão                                                                                                                                |
| avs_number          | string  | (opcional) número do endereço de cobrança do cartão                                                                                                                      |
| avs_complement      | string  | (opcional) complemento endereço de cobrança do cartão                                                                                                                    |
| avs_district        | string  | (opcional) bairro do endereço de cobrança do cartão                                                                                                                      |
| avs_zipcode         | string  | (opcional) cep do endereço de cobrança do cartão                                                                                                                         |
| soft_descriptor     | string  | (opcional) descritor que irá aparecer na fatura do cartão referente à cobrança de homologação (no máximo 13 caracteres)                                                  |

**payer_attributes**

<aside class="notice">
Caso exista um Pagador (Payer) com o mesmo <code>national_identifier</code>, não será criado um novo, mas sim atualizado o existente.
</aside>

| Campo                    | Tipo   | Comentário                                                           |
|--------------------------|--------|----------------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo do documento do pagador (cpf ou cnpj)           |
| national_identifier      | string | **(requerido)** documento do pagador                                 |
| name                     | string | **(requerido)** nome do pagador                                      |
| number                   | string | (opcional) número do endereço do pagador                             |
| complement               | string | (opcional) complemento do endereço do pagador                        |
| street                   | string | (opcional) rua do endereço do pagador                                |
| neighbourhood            | string | (opcional) bairro do endereço do pagador                             |
| zipcode                  | string | (opcional) cep do endereço do pagador                                |
| city                     | string | (opcional) cidade do endereço do pagador                             |
| state                    | string | (opcional) sigla do estado do endereço do pagador ("RJ" por exemplo) |

## Atualização de Cartão de Crédito

```shell
Atualizar Cartão de Crédito

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/credit_cards/:credit_card_id
  PATCH https://app.cobrato.com/api/v1/credit_cards/:credit_card_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/credit_cards/1 \
    -d '{
        "payer_id": 5
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM BENEFICIÁRIO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

    {
      "errors": {
        "payer_id": ["não existe para a sua conta"]
      }
    }

```

Atualiza um determinado Cartão de Crédito, retornado as informações do mesmo caso haja sucesso. Se houverem erros, eles serão informados no corpo da resposta.

**Parâmetros**

| Campo             | Tipo    | Comentário                                                                                                                                                               |
|-------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| payer_id          | integer | **(requerido, se não enviar payer_attributes )** identificador do pagador ao qual este cartão pertence (caso seja fornecido, o parâmetro payer_attributes será ignorado) |
| payer_attributes* | object  | **(requerido, se não enviar payer_id )** atributos para a criação de um novo pagador ou atualização de um pagador existente com o mesmo documento (national_identifier)  |

**payer_attributes**

<aside class="notice">
Caso exista um Pagador (Payer) com o mesmo <code>national_identifier</code>, não será criado um novo, mas sim atualizado o existente.
</aside>

| Campo                    | Tipo   | Comentário                                                           |
|--------------------------|--------|----------------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo do documento do pagador (cpf ou cnpj)           |
| national_identifier      | string | **(requerido)** documento do pagador                                 |
| name                     | string | **(requerido)** nome do pagador                                      |
| number                   | string | (opcional) número do endereço do pagador                             |
| complement               | string | (opcional) complemento do endereço do pagador                        |
| street                   | string | (opcional) rua do endereço do pagador                                |
| neighbourhood            | string | (opcional) bairro do endereço do pagador                             |
| zipcode                  | string | (opcional) cep do endereço do pagador                                |
| city                     | string | (opcional) cidade do endereço do pagador                             |
| state                    | string | (opcional) sigla do estado do endereço do pagador ("RJ" por exemplo) |


## Lista de Todas as cobranças feitas com o cartão de crédito

```shell
Listar as Cobranças realizadas com o Cartão de Crédito

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/credit_cards/:id/charges

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/credit_cards/12/charges

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "charges":
      [
        {
          // informações cobrança 1
        },
        {
          // informações cobrança 2
        },
        ...
      ]
  }

```

Retorna uma lista paginada em JSON contendo todos as Cobranças realizadas com o
Cartão de Crédito.

É possível filtrar a lista através dos parâmetros: `total_amount`, `received`, `payment_gateway_status`.
