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
        "credit_other_ownership",
        "credit_same_ownership",
        "credit_savings_account",
        "doc_other_ownership",
        "doc_same_ownership",
        "ted_other_ownership",
        "ted_same_ownership",
        "tribute_with_barcode",
        "dealership",
        "billet_same_bank",
        "billet_other_bank",
        "gps",
        "darf",
        "das",
        "ipva",
        "icms_sp",
        "dpvat",
        "fgts"
      ]
  }

```

Retorna uma lista em JSON contendo todos os Métodos de Pagamento possíveis.
