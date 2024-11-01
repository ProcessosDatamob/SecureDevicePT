# PATCH /command/{id}/data Atualiza o status de um comando

Este endpoint permite atualizar os dados adicionais de um comando específico, identificado pelo `{id}`. Ele é útil para modificar informações suplementares associadas a um comando sem alterar o status principal do mesmo.

#### Requisição

* **URL**: `/command/{id}/data`
* **Método**: `PATCH`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Parâmetros de Caminho**

| Parâmetro | Tipo     | Obrigatório | Descrição                         |
| --------- | -------- | ----------- | --------------------------------- |
| `id`      | `string` | Sim         | O identificador único do comando. |

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e conter os campos adicionais que se deseja atualizar no comando.

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "additionalData1": "novo valor",
  "additionalData2": 10,
  "notes": "Comando reemitido com novos parâmetros"
}
```

#### Respostas

| Código | Descrição                                                                                           |
| ------ | --------------------------------------------------------------------------------------------------- |
| 200    | Sucesso. Os dados adicionais do comando foram atualizados. Retorna os dados atualizados do comando. |
| 400    | Requisição inválida. Verifique o corpo da requisição e os parâmetros obrigatórios.                  |
| 404    | Comando não encontrado. O `id` fornecido não corresponde a nenhum comando existente.                |
| 500    | Erro interno no servidor.                                                                           |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "commandId": "cmd123",
  "deviceId": "12345",
  "commandType": "reiniciar",
  "status": "pendente",
  "additionalData1": "novo valor",
  "additionalData2": 10,
  "notes": "Comando reemitido com novos parâmetros",
  "updatedAt": "2023-01-10T10:00:00Z"
}
```

#### Notas Adicionais

* **Dados Adicionais**: Este endpoint permite a atualização apenas de dados suplementares do comando, deixando o status e as informações principais inalteradas.

***

Esta documentação fornece uma visão detalhada do endpoint `PATCH /command/{id}/data`, incluindo parâmetros, estrutura da requisição e formatos de resposta, facilitando a atualização de informações adicionais de um comando específico.
