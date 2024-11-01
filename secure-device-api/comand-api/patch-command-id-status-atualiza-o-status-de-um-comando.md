# PATCH /command/{id}/status Atualiza o status de um comando

Este endpoint permite atualizar o status de um comando específico, identificado pelo `{id}`. Ele é útil para modificar o estado de um comando enviado a um dispositivo, acompanhando seu progresso ou conclusão.

#### Requisição

* **URL**: `/command/{id}/status`
* **Método**: `PATCH`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Parâmetros de Caminho**

| Parâmetro | Tipo     | Obrigatório | Descrição                         |
| --------- | -------- | ----------- | --------------------------------- |
| `id`      | `string` | Sim         | O identificador único do comando. |

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e conter o novo status do comando.

| Parâmetro | Tipo     | Obrigatório | Descrição                                                         |
| --------- | -------- | ----------- | ----------------------------------------------------------------- |
| `status`  | `string` | Sim         | O novo status do comando (ex.: `pendente`, `executado`, `falha`). |

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "status": "executado"
}
```

#### Respostas

| Código | Descrição                                                                             |
| ------ | ------------------------------------------------------------------------------------- |
| 200    | Sucesso. O status do comando foi atualizado. Retorna os dados atualizados do comando. |
| 400    | Requisição inválida. Verifique o corpo da requisição e o parâmetro `status`.          |
| 404    | Comando não encontrado. O `id` fornecido não corresponde a nenhum comando existente.  |
| 500    | Erro interno no servidor.                                                             |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "commandId": "cmd123",
  "deviceId": "12345",
  "commandType": "reiniciar",
  "status": "executado",
  "updatedAt": "2023-01-10T10:00:00Z"
}
```

#### Notas Adicionais

* **Estados do Comando**: Certifique-se de que o valor fornecido no campo `status` é válido para o ciclo de vida do comando (ex.: `pendente`, `executado`, `falha`).

***

Esta documentação fornece uma visão detalhada do endpoint `PATCH /command/{id}/status`, incluindo parâmetros, estrutura da requisição e formatos de resposta, facilitando a atualização do status de um comando específico.
