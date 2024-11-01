# GET /command Lista todos os comandos enviados

Este endpoint retorna uma lista de todos os comandos enviados para os dispositivos registrados. Ele é útil para rastrear e consultar o histórico de comandos emitidos.

#### Requisição

* **URL**: `/command`
* **Método**: `GET`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

#### Parâmetros de Consulta (Query Parameters)

Este endpoint suporta parâmetros de consulta opcionais para filtrar e paginar os resultados.

| Parâmetro  | Tipo      | Obrigatório | Descrição                                                               |
| ---------- | --------- | ----------- | ----------------------------------------------------------------------- |
| `page`     | `integer` | Não         | Especifica o número da página para paginação.                           |
| `limit`    | `integer` | Não         | Especifica o número de comandos por página.                             |
| `deviceId` | `string`  | Não         | Filtra os comandos pelo `id` do dispositivo destinatário.               |
| `status`   | `string`  | Não         | Filtra os comandos por status (ex.: `enviado`, `executado`).            |
| `dateFrom` | `string`  | Não         | Filtra os comandos enviados a partir de uma data específica (ISO 8601). |
| `dateTo`   | `string`  | Não         | Filtra os comandos enviados até uma data específica (ISO 8601).         |

#### Respostas

| Código | Descrição                                                                      |
| ------ | ------------------------------------------------------------------------------ |
| 200    | Sucesso. Retorna uma lista de comandos enviados para os dispositivos.          |
| 400    | Requisição inválida. Um ou mais parâmetros de consulta podem estar incorretos. |
| 500    | Erro interno no servidor.                                                      |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "page": 1,
  "limit": 10,
  "totalCommands": 100,
  "data": [
    {
      "commandId": "cmd123",
      "deviceId": "12345",
      "commandType": "reiniciar",
      "status": "executado",
      "issuedAt": "2023-01-01T12:00:00Z",
      "executedAt": "2023-01-01T12:05:00Z"
    },
    {
      "commandId": "cmd124",
      "deviceId": "67890",
      "commandType": "atualizar",
      "status": "pendente",
      "issuedAt": "2023-01-02T15:30:00Z"
    }
  ]
}
```

#### Notas Adicionais

* **Filtragem por Data**: Use os parâmetros `dateFrom` e `dateTo` para restringir os resultados a um período específico.
* **Pagina**: Os parâmetros `page` e `limit` permitem controlar a paginação dos registros retornados.
* **Status do Comando**: O campo `status` indica o estado atual do comando (ex.: `enviado`, `pendente`, `executado`).

***

Esta documentação fornece uma visão completa do endpoint `GET /command`, incluindo a estrutura da requisição, parâmetros de consulta opcionais e os formatos de resposta, facilitando a consulta dos comandos enviados para os dispositivos.
