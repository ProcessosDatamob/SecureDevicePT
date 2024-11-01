# PATCH /register/{id}/status Atualiza o status de um dispositivo

Este endpoint permite atualizar o status de um dispositivo específico, identificado pelo `{id}`. Ele é útil para alterar o estado de um dispositivo sem modificar outros dados.

#### Requisição

* **URL**: `/register/{id}/status`
* **Método**: `PATCH`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Parâmetros de Caminho**

| Parâmetro | Tipo     | Obrigatório | Descrição                             |
| --------- | -------- | ----------- | ------------------------------------- |
| `id`      | `string` | Sim         | O identificador único do dispositivo. |

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e deve conter o novo status do dispositivo.

| Parâmetro | Tipo     | Obrigatório | Descrição                                               |
| --------- | -------- | ----------- | ------------------------------------------------------- |
| `status`  | `string` | Sim         | O novo status do dispositivo (ex.: `ativo`, `inativo`). |

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "status": "inativo"
}
```

#### Respostas

| Código | Descrição                                                                                     |
| ------ | --------------------------------------------------------------------------------------------- |
| 200    | Sucesso. O status do dispositivo foi atualizado. Retorna os dados atualizados do dispositivo. |
| 400    | Requisição inválida. Verifique o corpo da requisição e o parâmetro `status`.                  |
| 404    | Dispositivo não encontrado. O `id` fornecido não corresponde a nenhum dispositivo existente.  |
| 500    | Erro interno no servidor.                                                                     |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "id": "12345",
  "name": "Dispositivo A",
  "status": "inativo",
  "updatedAt": "2023-01-10T10:00:00Z"
}
```

#### Notas Adicionais

* **Valores de Status**: O campo `status` deve corresponder aos valores aceitos pelo sistema (ex.: `ativo`, `inativo`), garantindo consistência nos estados dos dispositivos.

***

Esta documentação fornece uma visão detalhada do endpoint `PATCH /register/{id}/status`, incluindo os parâmetros, estrutura da requisição e os formatos de resposta, facilitando a atualização do status de um dispositivo específico.

\
