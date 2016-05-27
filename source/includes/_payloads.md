# Payloads

São as requisições enviadas pelo webhook do Cobrato para uma determinada URL para notificar que certas ações ocorreram. Estas ações notificadas são as seguintes:

| Objeto         | Evento             | Descrição                                      |
|----------------|--------------------|------------------------------------------------|
| charge         | created            | quando a cobrança é criada                     |
| charge         | updated            | quando a cobrança é atualizada                 |
| charge         | destroyed          | quando a cobrança é excluída                   |
| charge         | received           | quando a cobrança é recebida                   |
| charge         | undone_receivement | quando a cobrança tem seu recebimento desfeito |
| charge_account | created            | quando a conta de cobrança é criada            |
| charge_account | updated            | quando a conta de cobrança é atualizada        |
| charge_account | destroyed          | quando a conta de cobrança é excluída          |

### Assinatura do Payload

```ruby
# EXEMPLO DE CÁCULO PARA VERIFICAÇÃO DA SIGNATURE (ruby)

secret = 'segredo definido na criação do Webhook'
content = "#{request.headers['X-Cobrato-RequestId']}#{request.body}"
cobrato_signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha1'), secret, content)

cobrato_signature == request.headers['X-Cobrato-Signature']
# => true
```

Quando um destes eventos ocorre, o webhook envia o payload (para a URL definida na criação do Webhook) em uma requisição HTTP do tipo POST com dois headers específicos:

**X-Cobrato-RequestId**

Este header é único para cada requisição e é utilizado no cálculo do `X-Cobrato-Signature`.

**X-Cobrato-Signature**

Este header é a assinatura do webhook. Este valor pode ser calculado com o HMAC hex digest do `X-Cobrato-RequestId` concatenado ao corpo do payload, utilizando o **Segredo** (definido na criação do Webhook) como a chave.


## Cobrança criada

```shell
Cobrança Criada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Informações enviadas quando uma Cobrança é criada.

## Cobrança Atualizada

```shell
Cobrança Atualizada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Informações enviadas quando uma Cobrança é atualizada.

## Cobrança Excluída

```shell
Cobrança Excluída

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"destroyed",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Informações enviadas quando uma Cobrança é excluída.

## Cobrança Recebida

```shell
Cobrança Recebida

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"received",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Este payload é enviado para todos os tipos de Cobrança e indica que uma Cobrança foi recebida. De acordo com seu tipo uma cobrança é dita recebida quando:

- Boleto: o usuário indica o recebimento de forma manual ou através de arquivo de retorno.
- Gateway de pagamento: o gateway de pagamento informa o recebimento.

## Recebimento de Cobrança desfeito

```shell
Recebimento de Cobrança desfeito

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"undone_receivement",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Este payload é enviado **apenas para cobranças do tipo boleto** e é disparado
quando o recebimento da Cobrança de desfeito manualmente pelo usuário. Ele
indica apenas que no Cobrato o recebimento da Cobrança foi desfeito, mas não tem
qualquer relação com o estado do boleto no banco.

## Cobrança Cancelada

```shell
Cobrança Cancelada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"canceled",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Este payload é enviado **apenas para cobranças do tipo gateway de pagamento** e
é disparado quando o gateway de pagamento informa sobre o cancelamento de uma
Cobrança, que pode ter sido pedido pelo próprio usuário ou não. Ele indica que a
Cobrança teve seu pagamento cancelado, ou seja, estornado.

## Erro no recebimento de uma cobrança

```shell
Erro no recebimento de uma cobrança

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"receivement_error",
    "retryable":false,
    "card_error":true,
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Este payload é enviado **apenas para cobranças do tipo gateway de pagamento** e
é disparado quando o gateway de pagamento informa sobre um erro na tentativa de
recebimnto de uma Cobrança. O parâmetro _retryable_ indica se é passível ou não
de retentativa. Já o parâmetro _card\_error_ indica se o erro foi oriundo de um
problema no cartão ou não.

## Erro no cancelamento de uma cobrança

```shell
Erro no cancelamento de uma cobrança

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"cancellation_error",
    "object_type":"charge",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges/12"
    }]
  }

```

Este payload é enviado **apenas para cobranças do tipo gateway de pagamento** e
é disparado quando o gateway de pagamento informa sobre um erro na tentativa de
cancelamento de uma Cobrança.

## Conta de Cobrança criada

```shell
Conta de Cobrança Criada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"charge_account",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges_accounts/7"
    }]
  }

```

Informações enviadas quando uma Conta de Cobrança é Criada.

## Conta de Cobrança Atualizada

```shell
Conta de Cobrança Atualizada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"charge_account",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_accounts/7"
    }]
  }
```

Informações enviadas quando uma Conta de Cobrança é atualizada.

## Conta de Cobrança Excluída

```shell
Conta de Cobrança Excluída

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"destroyed",
    "object_type":"charge_account",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_accounts/7"
    }]
  }

```

Informações enviadas quando uma Conta de Cobrança é excluída.