# Métodos de pagamento

## Lista de todos os Métodos de Pagamento

```shell
Listar Métodos de Pagamento

DEFINIÇÃO

  GET https://app.cobrato.com/api/v1/payment_methods

EXEMPLO DE REQUISIÇÃO

  $ curl -i -u $API_TOKEN:X \
    -H 'User-Agent: My App 1.0' \
    -H 'Accept: application/json' \
    -H 'Content-type: application/json' \
    -X GET https://app.cobrato.com/api/v1/payment_methods

EXEMPLO DE ESTADO DA RESPOSTA

    200 OK

EXEMPLO DE CORPO DA RESPOSTA

  {
    "payment_methods":
      [
        { 
          "identifier": 'credit_other_ownership',
          "group": 'transfer',
          "label": 'Crédito em conta Corrente - Outra titularidade' 
        },
        { 
          // informações de outro método 
        },
        ...
      ]
  }

```

Retorna um objeto JSON contendo todos os Métodos de Pagamento possíveis.
