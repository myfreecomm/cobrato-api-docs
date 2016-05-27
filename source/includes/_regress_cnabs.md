# CNAB de Retorno

```shell
CNAB de Retorno

EXEMPLO

  {
    "id": 1,
    "charge_config_id": 9,
    "status": "processed",
    "report": {
      "charges_not_found": 0,
      "received_charges": [{
        "id": 46,
        "_links": [{ "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/charges/46" }]
      }],
      "registered_charges": [{
        "id": 45,
        "_links": [{ "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/charges/45" }]
      }]
    },
    "_links":
      [
        {"rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1"},
        {"rel": "destroy", "method": "DELETE", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1"},
        {"rel": "charge_config", "method": "GET", "href": "https://app.cobrato.com/api/v1/charge_config/1"},
        {"rel": "file", "method": "GET", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1/file"}
      ]
  }
```

Os arquivos CNABs de retorno, pertencem a uma determinada conta de cobrança, contendo informações de uma ou mais cobranças desta conta.

<aside class="warning">
A utilização desta API não é autorizada a contas com o plano <strong>Gratuito</strong>, resultando na resposta com o estado <strong>403 Forbidden</strong>!
</aside>

**Parâmetros**

| Campo            | Tipo            | Comentário                                                                                                                              |
|------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| id               | integer         | identificador do CNAB de retorno                                                                                                        |
| charge_config_id | string          | identificador da configuração de cobrança no Cobrato                                                                                    |
| status           | string          | situação do arquivo CNAB, podendo ser "processing" (processando), "processed" (processado) e "processing_error" (erro de processamento) |
| report           | string          | relatório de processamento do arquivo CNAB, os parâmetros do relatório se encontram na tabela abaixo                                    |
| _links           | array of object | links relacionado CNAB de retorno                                                                                                       |

**Parâmetros do Relatório de Processamento**

| Campo              | Tipo             | Comentário                                                                              |
|--------------------|------------------|-----------------------------------------------------------------------------------------|
| charges_not_found  | integer          | Quantidade de cobranças que estavam no CNAB, mas não foram localizadas no sistema       |
| received_charges   | array of objects | Informações das cobranças recebidas pelo CNAB, contendo o código identificador e link   |
| registered_charges | array of objects | Informações das cobranças registradas pelo CNAB, contendo o código identificador e link |

## Informações do CNAB de Retorno

```shell
Mostrar CNAB de Retorno

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/regress_cnabs/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/regress_cnabs/:id

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "id": 1,
    "charge_config_id": 9,
    "status": "processed",
    "report": {
      "charges_not_found": 0,
      "received_charges": [{
        "id": 46,
        "_links": [{ "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/charges/46" }]
      }],
      "registered_charges": [{
        "id": 45,
        "_links": [{ "rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/charges/45" }]
      }]
    },
    "_links":
      [
        {"rel": "self", "method": "GET", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1"},
        {"rel": "destroy", "method": "DELETE", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1"},
        {"rel": "charge_config", "method": "GET", "href": "https://app.cobrato.com/api/v1/charge_configs/1"},
        {"rel": "file", "method": "GET", "href": "https://app.cobrato.com/api/v1/regress_cnabs/1/file"}
      ]
  }

```

Retorna as informações detalhadas em JSON do CNAB de retorno informado.

## Lista de Todas as CNABs de Retorno

```shell
Listar CNABs de Retorno

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/regress_cnabs

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/regress_cnabs

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "regress_cnabs":
      [
        {
          // informações do CNAB de retorno 1
        },
        {
          // informações do CNAB de retorno 2
        },
        ...
      ]
  }

```

Retorna uma lista em JSON contendo todos os CNABs de retorno que pertencem a sua Conta de Serviço.

## Criação de CNAB de Retorno

```shell
Criar CNAB de Retorno

DEFINIÇÃO

  POST https://app.cobrato.com/api/v1/regress_cnabs

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X POST https://app.cobrato.com/api/v1/regress_cnabs \
    -d '{
          "charge_config_id": 1,
          "cnabs": {
            "content":      "MDJSRVRPUk5PMDFDT0JSQU5DQSAgICAgICAzMTMwMDAyMjY5OTAgICA...",
            "content_type": "text/plain"
            "filename":     "example.RET"
          }
        }'

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    202 Accepted

EXEMPLO DE ESTADO DA RESPOSTA COM INSUCESSO

    422 Unprocessable Entity

EXEMPLO DE CORPO DA RESPOSTA COM INSUCESSO

  {
    "errors":{
      "charge_config_id": ["não pode ficar em branco"],
      "cnabs": ["não pode ficar em branco"]
    }
  }

```

Cria um CNAB de retorno inicia o processamento do arquivo.

**Parâmetros**

| Campo            | Tipo   | Comentário                                                                                                                       |
|------------------|--------|----------------------------------------------------------------------------------------------------------------------------------|
| charge_config_id | string | **(requerido)** identificador da configuração de cobrança à qual o arquivo CNAB de retorno pertence                              |
| cnabs            | object | **(requerido)** dados do arquivo CNAB de retorno. O "content" deve ser uma string com o conteúdo do arquivo codificado em Base64 |

## Exclusão de CNAB de retorno

```shell
Excluir CNAB de retorno

DEFINIÇÃO

  DELETE https://app.cobrato.com/api/v1/regress_cnabs/:id

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X DELETE https://app.cobrato.com/api/v1/regress_cnabs/:id

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    204 No Content

EXEMPLO DE ESTADO DA RESPOSTA COM CONTA BANCÁRIA INEXISTENTE

    404 Not Found

```

Exclui determinado CNAB de retorno. A exclusão é irreversível.

## Arquivo do CNAB de Retorno

```shell
Mostrar Arquivo do CNAB de Retorno (URL)

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/regress_cnabs/:id/file

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/regress_cnabs/:id/file

EXEMPLO DE ESTADO DA RESPOSTA COM SUCESSO

    200 OK

EXEMPLO DE ESTADO DA RESPOSTA COM COBRANÇA INEXISTENTE

    404 Not Found

EXEMPLO DE CORPO DA RESPOSTA COM SUCESSO

  {
    "url":"https://cobrato-uploads.s3.amazonaws.com/regress_cnabs/cnabs/1/B425065A.RET?AWSAccessKeyId=AKIAIRJFH3YRXV5YRVTQ&Expires=1452277155&Signature=IJ1P%2Bc%2F9vC%2FKlBWuHGIBEl%2BAHKk%3D"
  }
```

Mostra o link da url do arquivo de determinado CNAB de retorno.

<aside class="warning">
As URLs disponibilizadas são válidas por apenas 60 minutos. Sendo assim, não armazene o retorno e sempre que for necessário realize uma nova chamada à API.
</aside>