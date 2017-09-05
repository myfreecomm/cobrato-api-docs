# Webhook

```shell
Webhook

EXEMPLO

  {
    "id": 1,
    "url": "http://www.seusitema.com/cobrato",
    "description": "teste",
    "secret": "my-secret-token",
    "_links": [
      {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/webhooks/1"},
      {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/webhooks/1"},
      {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/webhooks/1"}
    ]
  }

```

É possível ter indeterminados webhooks, que enviarão requisições para uma determinada URL quando certas ações ocorrem no Cobrato ([Payloads](#payloads)).

**Parâmetros**

| Campo       | Tipo   | Comentário                                                                                          |
|-------------|--------|-----------------------------------------------------------------------------------------------------|
| url         | string | **(requerido)** URL na qual serão feitas as requisições GET e POST, esperando HTTP 200 como retorno |
| description | string | (opcional) descrição opcional do Webhook                                                            |
| secret      | string | **(requerido)** Segredo pra ser adicionado no header de todas as requisições                        |

## Informações do Webhook

```shell
Mostra Webhook

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/webhooks/:webhook_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/webhooks/:webhook_id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id": 1,
    "url": "http://www.seusitema.com/cobrato",
    "description": "teste",
    "secret": "my-secret-token",
    "_links": [
      {"rel":"self","method":"GET","href":"https://app.cobrato.com/api/v1/webhooks/1"},
      {"rel":"update","method":"PUT","href":"https://app.cobrato.com/api/v1/webhooks/1"},
      {"rel":"destroy","method":"DELETE","href":"https://app.cobrato.com/api/v1/webhooks/1"}
    ]
  }

```

Retorna as informações detalhadas do webhook em formato JSON.

## Lista de Todos os Webhooks

```shell

Listar Webhooks

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/webhooks

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/webhooks

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "webhooks":
      [
        {
          // informações webhook 1
        },
        {
          // informações webhook 2
        },
        ...
      ]
  }
```

Retorna uma lista em JSON contendo todos os webhooks pertencentes a sua Conta de Serviço.

## Criação de Webhook

```shell
Criar Webhook

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/webhooks

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/webhooks \
    -d '{
        "url": "http://www.seusitema.com/cobrato",
        "description": "Webhook teste",
        "secret": "my-secret-token"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    201 Created

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors": {
      "url": [
        "não é válida",
        "não pode ficar em branco"
      ]
    }
  }

```

Cria um novo webhook, retornando as informações do mesmo caso haja sucesso. Para realizar o cadastro é necessária que a URL informa aceite requisições POST, respondendo sempre com HTTP 200. No momento da criação, afim verificar a URL informada, o Cobrato fará uma requisição de teste à mesma. A requisição de teste será um [payload](#payloads) com o corpo `{"test": true}`.

**Parâmetros**

| Campo       | Tipo   | Comentário                                                                                          |
|-------------|--------|-----------------------------------------------------------------------------------------------------|
| url         | string | **(requerido)** URL na qual serão feitas as requisições GET e POST, esperando HTTP 200 como retorno |
| description | string | (opcional) descrição opcional do Webhook                                                            |


## Atualização de Webhook

```shell
Atualizar Webhook

DEFINIÇÃO

  PUT https://app.cobrato.com/api/v1/webhooks/:webhook_id
  PATCH https://app.cobrato.com/api/v1/webhooks/:webhook_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X PATCH https://app.cobrato.com/api/v1/webhooks/:webhook_id \
    -d '{
        "descripction": "Webhook teste",
        "secret": "my-secret-token"
      }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM BENEFICIÁRIO INEXISTENTE

    404 Not Found

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

```

Atualiza a descrição do webhook. Não é possível alterar a URL de um Webhook. A requisição não diferencia a utilização dos verbos PUT e PATCH.

**Parâmetros**

| Campo       | Tipo   | Comentário                                       |
|-------------|--------|--------------------------------------------------|
| description | string | (opcional) descrição opcional do Webhook         |
| secret      | string | (requerido) segredo à ser adicionado aos readers |

## Exclusão de Webhook

```shell
Excluir Webhook

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/webhooks/:webhook_id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/webhooks/:webhook_id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM WEBHOOK INEXISTENTE

    404 Not Found

```

Exclui determinado webhook. A exclusão é irreversível.
