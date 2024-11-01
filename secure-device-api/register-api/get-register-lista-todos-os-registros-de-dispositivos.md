---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# GET /register Lista todos os registros de dispositivos

Este endpoint retorna uma lista de todos os registros de dispositivos. Ele é útil para recuperar informações sobre todos os dispositivos registrados no sistema.

#### Requisição

* **URL**: `/register`
* **Método**: `GET`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

#### Parâmetros de Consulta (Query Parameters)

Este endpoint suporta parâmetros de consulta opcionais para filtrar e paginar os resultados.

| Parâmetro | Tipo      | Obrigatório | Descrição                                                                   |
| --------- | --------- | ----------- | --------------------------------------------------------------------------- |
| `page`    | `integer` | Não         | Especifica o número da página para paginação.                               |
| `limit`   | `integer` | Não         | Especifica o número de registros por página.                                |
| `status`  | `string`  | Não         | Filtra os dispositivos por status (exemplo: `ativo`, `inativo`).            |
| `sort`    | `string`  | Não         | Especifica o campo para ordenação dos resultados (exemplo: `nome`, `data`). |

#### Respostas

| Código | Descrição                                                                      |
| ------ | ------------------------------------------------------------------------------ |
| 200    | Sucesso. Retorna uma lista de registros de dispositivos.                       |
| 400    | Requisição inválida. Um ou mais parâmetros de consulta podem estar incorretos. |
| 500    | Erro interno no servidor.                                                      |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "page": 1,
  "limit": 10,
  "totalRecords": 50,
  "data": [
    {
      "id": "12345",
      "name": "Dispositivo A",
      "status": "ativo",
      "registeredAt": "2023-01-01T12:00:00Z",
      "additionalInfo": {
        "location": "Sala 1",
        "type": "sensor"
      }
    },
    {
      "id": "67890",
      "name": "Dispositivo B",
      "status": "inativo",
      "registeredAt": "2023-01-05T15:30:00Z",
      "additionalInfo": {
        "location": "Sala 2",
        "type": "atuador"
      }
    }
  ]
}
```

#### Notas Adicionais

* **Pagina**: Use os parâmetros `page` e `limit` para controlar a paginação dos registros retornados.
* **Ordenação**: O parâmetro `sort` permite especificar o campo de ordenação dos registros para facilitar a organização dos dados.

***

Esta documentação fornece uma visão completa do endpoint `GET /register`, incluindo a estrutura da requisição, parâmetros de consulta opcionais e os formatos de resposta.

\
