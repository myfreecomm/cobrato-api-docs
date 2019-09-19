# Estabelecimento

```shell
Estabelecimento

EXEMPLO

  {
    "id":1,
    "national_identifier_type":"cpf",
    "national_identifier":"38031171513",
    "name":"João Silveira",
    "zipcode":"99000-750",
    "city":"Carapebus",
    "state":"RJ",
    "neighbourhood":"Centro",
    "street":"Rua Julio de Castilhos",
    "number":"100",
    "complement": "Ao lado da lotérica.",
    "_links":
      [
        {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/payees/1"},
        {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/payees/1"},
        {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/payees/1"}
      ]
  }
```

É possível ter indeterminados estabelecimentos, e a eles que pertencem as contas bancárias, configurações de cobrança, e as próprias cobranças do sistema. Podem ser tanto pessoas físicas como pessoas jurídicas.

**Parâmetros**

| Campo                    | Tipo            | Comentário                                                           |
|--------------------------|-----------------|----------------------------------------------------------------------|
| id                       | integer         |                                                                      |
| national_identifier_type | string          | tipo de identificação nacional ('cpf' ou 'cnpj')                     |
| national_identifier      | string          | número válido de cnpj ou cpf, de acordo com o campo anterior         |
| name                     | string          | nome completo do estabelecimento                                        |
| city                     | string          | nome da cidade do domicílio do estabelecimento                          |
| state                    | string          | uf do estado do domicílio do estabelecimento (duas letras, p. ex. 'RJ') |
| neighbourhood            | string          | bairro do domicílio do estabelecimento                                  |
| street                   | string          | logradouro do estabelecimento                                           |
| number                   | string          | número da logradouro do estabelecimento                                 |
| zipcode                  | string          | cep do domicílio do estabelecimento                                     |
| complement               | string          | complemento para o endereço de domicilio do estabelecimento             |
| _links                   | array of object | links do estabelecimento                                                |

## Informações do Estabelecimento

```shell
Mostrar Estabelecimento

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payees/:payee_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payees/:payee_id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id":1,
    "national_identifier_type":"cpf",
    "national_identifier":"38031171513",
    "name":"João Silveira",
    "zipcode":"99000-750",
    "city":"Carapebus",
    "state":"RJ",
    "neighbourhood":"Centro",
    "street":"Rua Julio de Castilhos",
    "number":"100",
    "complement": "Ao lado da lotérica.",
    "_links":
      [
        {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/payees/1"},
        {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/payees/1"},
        {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/payees/1"}
      ]
  }
```

Retorna as informações detalhadas do estabelecimento informado em JSON.

## Lista de Todos os Estabelecimentos

```shell
Listar Estabelecimentos

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payees

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payees

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "payees":
      [
        {
          // informações estabelecimento 1
        },
        {
          // informações estabelecimento 2
        },
        ...
      ]
  }
```

Retorna uma lista em JSON contendo todos os estabelecimentos pertencentes a sua Conta de Serviço.

## Criação de Estabelecimento

```shell
Criar Estabelecimento

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/payees

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/payees \
    -d '{
        "name": "João Silva",
        "city": "Caxias do Sul",
        "national_identifier_type": "cpf",
        "national_identifier": "38031171513",
        "state": "RS",
        "street": "Rua Principal",
        "neighbourhood": "Centro",
        "number": "174",
        "zipcode": "95055-777"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":{
      "name": ["não pode ficar em branco"],
      "city": ["não pode ficar em branco"],
      "national_identifier_type": ["não pode ficar em branco","não está incluído na lista"],
      "state":["não pode ficar em branco","não possui o tamanho esperado (2 caracteres)"],
      "neighbourhood": ["não pode ficar em branco"],
      "street": ["não pode ficar em branco"],
      "number": ["não pode ficar em branco"],
      "zipcode": ["não pode ficar em branco"]
    }
  }

```

Cria um novo estabelecimento, retornando as informações do mesmo caso haja sucesso. Se houverem erros eles serão informados no corpo da resposta.

**Parâmetros**

| Campo                    | Tipo   | Comentário                                                                           |
|--------------------------|--------|--------------------------------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo de identificação nacional ('cpf' ou 'cnpj')                     |
| national_identifier      | string | **(requerido)** número válido de cnpj ou cpf, de acordo com o campo anterior         |
| name                     | string | **(requerido)** nome completo do estabelecimento                                        |
| city                     | string | **(requerido)** nome da cidade do domicílio do estabelecimento                          |
| state                    | string | **(requerido)** uf do estado do domicílio do estabelecimento (duas letras, p. ex. 'RJ') |
| neighbourhood            | string | **(requerido)** bairro do domicílio do estabelecimento                                  |
| street                   | string | **(requerido)** logradouro do estabelecimento                                           |
| number                   | string | **(requerido)** número da logradouro do estabelecimento                                 |
| zipcode                  | string | **(requerido)** cep do domicílio do estabelecimento                                     |
| complement               | string | (opcional)  complemento para o endereço de domicilio do estabelecimento                 |

## Atualização de Estabelecimento

```shell
Atualizar Estabelecimento

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/payees/:payee_id
  PATCH https://app.cobrato.com/api/v1/payees/:payee_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/payees/:payee_id \
    -d '{
        "city": "Farroupilha",
        "state": "RS"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM BENEFICIÁRIO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

    {
      "errors":{
        "national_identifier_type":["não está incluído na lista"]
      }
    }

```

Atualiza o estabelecimento determinado, retornando as informações do mesmo caso haja sucesso. Se houverem erros eles serão informados no corpo da resposta. A requisição não diferencia a utilização dos verbos PUT e PATCH.

**Parâmetros**

| Campo                    | Tipo   | Comentário                                                                           |
|--------------------------|--------|--------------------------------------------------------------------------------------|
| national_identifier_type | string | **(requerido)** tipo de identificação nacional ('cpf' ou 'cnpj')                     |
| national_identifier      | string | **(requerido)** número válido de cnpj ou cpf, de acordo com o campo anterior         |
| name                     | string | **(requerido)** nome completo do estabelecimento                                        |
| city                     | string | **(requerido)** nome da cidade do domicílio do estabelecimento                          |
| state                    | string | **(requerido)** uf do estado do domicílio do estabelecimento (duas letras, p. ex. 'RJ') |
| neighbourhood            | string | **(requerido)** bairro do domicílio do estabelecimento                                  |
| street                   | string | **(requerido)** logradouro do estabelecimento                                           |
| number                   | string | **(requerido)** número da logradouro do estabelecimento                                 |
| zipcode                  | string | **(requerido)** cep do domicílio do estabelecimento                                     |
| complement               | string | (opcional)  complemento para o endereço de domicilio do estabelecimento                 |

## Exclusão de Estabelecimento

```shell
Excluir Estabelecimento

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/payees/:payee_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/payees/:payee_id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM BENEFICIÁRIO INEXISTENTE

    404 Not Found
```

Exclui determinado estabelecimento e junto a ele todas suas configurações de cobrança, contas bancárias e as cobranças. As mudanças são irreversíveis.

