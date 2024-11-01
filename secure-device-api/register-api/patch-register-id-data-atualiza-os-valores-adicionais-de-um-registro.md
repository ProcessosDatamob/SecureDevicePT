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

# PATCH /register/{id}/data Atualiza os valores adicionais de um registro

Este endpoint permite atualizar os valores adicionais de um registro de dispositivo específico, identificado pelo `{id}`. Ele é útil para modificar dados suplementares associados a um registro sem alterar as informações principais do dispositivo.

#### Requisição

* **URL**: `/register/{id}/data`
* **Método**: `PATCH`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Parâmetros de Caminho**

| Parâmetro | Tipo     | Obrigatório | Descrição                                         |
| --------- | -------- | ----------- | ------------------------------------------------- |
| `id`      | `string` | Sim         | O identificador único do registro do dispositivo. |

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e conter os campos adicionais que se deseja atualizar.

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "additionalField1": "novo valor",
  "additionalField2": 123,
  "additionalField3": true
}
```

#### Respostas

| Código | Descrição                                                                                                  |
| ------ | ---------------------------------------------------------------------------------------------------------- |
| 200    | Sucesso. Os valores adicionais do registro foram atualizados. Retorna os dados atualizados do dispositivo. |
| 400    | Requisição inválida. Verifique o corpo da requisição e os parâmetros obrigatórios.                         |
| 404    | Registro não encontrado. O `id` fornecido não corresponde a nenhum registro existente.                     |
| 500    | Erro interno no servidor.                                                                                  |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "id": "12345",
  "additionalField1": "novo valor",
  "additionalField2": 123,
  "additionalField3": true,
  "updatedAt": "2023-01-10T10:00:00Z"
}
```

#### Notas Adicionais

* **Campos Adicionais**: Este endpoint permite a atualização apenas de campos suplementares do registro, mantendo os dados principais do dispositivo inalterados.

***

Esta documentação fornece uma visão completa do endpoint `PATCH /register/{id}/data`, incluindo os parâmetros, estrutura da requisição e os formatos de resposta, facilitando a atualização de valores adicionais de um registro específico.
