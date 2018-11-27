# Payloads

São as requisições enviadas pelo webhook do Cobrato para uma determinada URL notificando a ocorrência de [certos eventos](#eventos-notificados).

Quando um destes eventos ocorre, o webhook envia o payload (para a URL definida na criação do Webhook) em uma requisição HTTP do tipo POST com os seguintes _headers_:

- **Accept**: application/json
- **Content-Type**: application/json
- **User-Agent**: Cobrato v1
- **X-Cobrato-Signature**: \<some-signature>
- **X-Cobrato-Requestid**: \<some-request-id>

Os dois últimos fazem parte da assinatura do payload, detalhada a seguir.

<aside class="notice">
  A URL definida na criação do Webhook deve estar disponível e respondendo com HTTP 200 ok aos payloads. O Cobrato fará 5 tentativas de notificação. Após a 5ª tentativa sem sucesso, os administradores da conta serão notificados via e-mail e o endpoint deste webhook será marcado como "Com erro". O Cobrato fará então mais 5 tentativas no intervalo de 48 horas até não tentar mais.
</aside>

### Assinatura do Payload

Por medidas de segurança, você pode verificar a assinatura do payload antes de tomar qualquer ação em relação ao payload recebido. Isso pode evitar que alguém se passe pelo Cobrato e enviei payloads falsos de eventos que não ocorreram de fato.

```ruby
# EXEMPLO DE CÁCULO PARA VERIFICAÇÃO DA SIGNATURE (ruby)

secret = 'segredo definido na criação do Webhook'
content = "#{request.headers['X-Cobrato-RequestId']}#{request.body}"
cobrato_signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha1'), secret, content)

cobrato_signature == request.headers['X-Cobrato-Signature']
# => true
```

**X-Cobrato-RequestId**

Este header é único para cada requisição e é utilizado no cálculo do `X-Cobrato-Signature`.

**X-Cobrato-Signature**

Este header é a assinatura do webhook. Este valor pode ser calculado com o HMAC hex digest do `X-Cobrato-RequestId` concatenado ao corpo do payload, utilizando o **Segredo** (definido na criação do Webhook) como a chave.

### Eventos notificados

Os eventos notificados são os seguintes:

| Objeto          | Evento                | Descrição                                         |
|-----------------|-----------------------|---------------------------------------------------|
| charge          | created               | quando a cobrança é criada                        |
| charge          | updated               | quando a cobrança é atualizada                    |
| charge          | destroyed             | quando a cobrança é excluída                      |
| charge          | received              | quando a cobrança é recebida                      |
| charge          | undone_receivement    | quando a cobrança tem seu recebimento desfeito    |
| charge_config   | created               | quando a configuração de cobrança é criada        |
| charge_config   | updated               | quando a configuração de cobrança é atualizada    |
| charge_config   | destroyed             | quando a configuração de cobrança é excluída      |
| charge_config   | deactivated           | quando a configuração de cobrança é desativada    |
| credit_card     | created               | quando o cartão de crédito é criado               |
| credit_card     | updated               | quando o cartão de crédito é atualizado           |
| charge_template | created               | quando o modelo de cobrança é criado              |
| charge_template | updated               | quando o modelo de cobrança é atualizado          |
| charge_template | destroyed             | quando o modelo de cobrança é excluído            |
| payer           | created               | quando o pagador é criado                         |
| payer           | updated               | quando o pagador é atualizado                     |
| payer           | destroyed             | quando o pagador é excluído                       |
| payment         | created               | quando o pagamento é criado                       |
| payment         | updated               | quando o pagamento é atualizado                   |
| payment         | canceled              | quando o pagamento é cancelado                    |
| payment         | destroyed             | quando o pagamento é excluído                     |
| payment         | unauthorized          | quando o pagamento é marcado como não autorizado  |
| payment         | registered_with_error | quando o pagamento é marcado com Erro no registro |
| payment         | registered            | quando o pagamento é registrado                   |
| payment         | rescheduled           | quando o pagamento é reagendado                   |
| payment         | edited                | quando o pagamento tem a edição confirmada        |
| payment         | paid                  | quando o pagamento é efetivado                    |
| remittance_cnab | updated               | quando o arquivo de remessa é atualizado          |
| regress_cnab    | updated               | quando o arquivo de retorno é atualizado          |


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

Este payload é disparado quando o recebimento da Cobrança é desfeito. No caso da
cobrança do tipo **boleto**, ele indica apenas que no Cobrato o recebimento da
Cobrança foi desfeito, mas não tem qualquer relação com o estado do boleto no
banco. Já no caso da cobrança do tipo **gateway de pagamento**, está cobrança
foi cancelada.

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

## Configuração de Cobrança criada

```shell
Configuração de Cobrança Criada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"charge_config",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charges_configs/7"
    }]
  }

```

Informações enviadas quando uma Configuração de Cobrança é Criada.

## Configuração de Cobrança Atualizada

```shell
Configuração de Cobrança Atualizada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"charge_config",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_configs/7"
    }]
  }
```

Informações enviadas quando uma Configuração de Cobrança é atualizada.

## Configuração de Cobrança Excluída

```shell
Configuração de Cobrança Excluída

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"destroyed",
    "object_type":"charge_config",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_configs/7"
    }]
  }

```

Informações enviadas quando uma Configuração de Cobrança é excluída.

## Configuração de Cobrança desativada

```shell
Configuração de Cobrança Desativada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"deactivated",
    "object_type":"charge_config",
    "object_id":7,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_configs/7"
    }]
  }

```

Informações enviadas quando uma Configuração de Cobrança é Desativada.

## Cartão de crédito criado

```shell
Cartão de crédito Criado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"credit_card",
    "object_id":23,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/credit_card/23"
    }]
  }

```

Informações enviadas quando um Cartão de crédito é criado.

## Cartão de crédito Atualizado

```shell
Cartão de crédito Atualizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"credit_card",
    "object_id":23,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/credit_card/23"
    }]
  }
```

Informações enviadas quando um Cartão de crédito é atualizado.

## Modelo de Cobrança Criado

```shell

Modelo de Cobrança Criado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"charge_template",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_templates/12"
    }]
  }

```

Informações enviadas quando um Modelo de cobraça é criado.

## Modelo de cobrança Atualizado

```shell
Modelo de cobrança Atualizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"charge_template",
    "object_id":13,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_templates/13"
    }]
  }
```

Informações enviadas quando um Modelo de cobrança é atualizado.

## Modelo de cobrança Excluído

```shell
Modelo de cobrança Excluído

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"charge_template",
    "object_id":14,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/charge_templates/14"
    }]
  }
```

Informações enviadas quando um Modelo de cobrança é excluído.

## Pagador criado

```shell
Pagador Criado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"payer",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payers/12"
    }]
  }

```

Informações enviadas quando uma Pagador é criado.

## Pagador Atualizado

```shell
Pagador Atualizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"payer",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payers/12"
    }]
  }

```

Informações enviadas quando uma Pagador é atualizado.

## Pagador Excluído

```shell
Pagador Excluído

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"destroyed",
    "object_type":"payer",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payers/12"
    }]
  }

```

Informações enviadas quando uma Pagador é excluído.

## Pagamento criado

```shell
Pagamento Criado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"created",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é criado.

## Pagamento Atualizado

<aside class="notice">
  O payload de pagamento atualizado <strong>não é</strong> enviado pelo webhook se outros webhooks específicos são disparados. Ou seja, quando há uma mudança no pagamento para registrado, será enviado o webhook (e consequentemente o payload) de pagamento registrado. Isso vale para os outros webhooks como: não autorizado, erro no registro, edição confirmada ou efetivado.
</aside>

```shell
Pagamento Atualizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é atualizado.

## Pagamento Efetivado

```shell
Pagamento Efetivado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"paid",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é efetivado.

## Pagamento Excluído

```shell
Pagamento Excluído

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"destroyed",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é excluído.

## Pagamento Marcado como Não Autorizado

```shell
Pagamento Marcado como Não Autorizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"unauthorized",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é marcado como Não Autorizado.

## Pagamento registrado

```shell
Pagamento Registrado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"registered",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é registrado.

## Pagamento com edição confirmada

```shell
Pagamento com edição confirmada

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"edited",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento tem sua edição confirmada.

## Pagamento Efetivado

```shell
Pagamento Efetivado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"paid",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é efetivado.

## Pagamento Marcado com Erro no Registro

```shell
Pagamento Marcado com Erro no Registro

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"registered_with_error",
    "object_type":"payment",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/payments/12"
    }]
  }

```

Informações enviadas quando um Pagamento é marcado com Erro no Registro.

## Arquivo de remessa Atualizado

```shell
Arquivo de remessa Atualizadao

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"remittance_cnab",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/remittance_cnabs/12"
    }]
  }

```

Informações enviadas quando um Arquivo de remessa é atualizado.

## Arquivo de retorno Atualizado

```shell
Arquivo de retorno Atualizado

EXEMPLO DE PAYLOAD

  {
    "created_at":"2015-05-21T16:13:33Z",
    "event":"updated",
    "object_type":"regress_cnab",
    "object_id":12,
    "_links":[{
      "rel":"self",
      "method":"GET",
      "url":"https://app.cobrato.com/api/v1/regress_cnabs/12"
    }]
  }

```

Informações enviadas quando um Arquivo de retorno é atualizado.
