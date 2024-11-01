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

# GET /register/{id} Obtém as informações de um registro específico pelo ID

Este endpoint permite obter as informações detalhadas de um registro de dispositivo específico, identificado pelo `{id}`. Ele é útil para acessar todos os detalhes de um dispositivo registrado no sistema.

#### Requisição

* **URL**: `/register/{id}`
* **Método**: `GET`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Parâmetros de Caminho**

| Parâmetro | Tipo     | Obrigatório | Descrição                                         |
| --------- | -------- | ----------- | ------------------------------------------------- |
| `id`      | `string` | Sim         | O identificador único do registro do dispositivo. |

#### Respostas

| Código | Descrição                                                                                 |
| ------ | ----------------------------------------------------------------------------------------- |
| 200    | Sucesso. Retorna os dados do dispositivo solicitado.                                      |
| 404    | Registro não encontrado. O `id` fornecido não corresponde a nenhum dispositivo existente. |
| 500    | Erro interno no servidor.                                                                 |

**Exemplo de Resposta com Sucesso (`200`)**

```json
jsonCopiar código{
  "id": "12345",
  "name": "Dispositivo A",
  "type": "sensor",
  "location": "Sala 1",
  "status": "ativo",
  "registeredAt": "2023-01-01T12:00:00Z",
  "metadata": {
    "fabricante": "Empresa X",
    "modelo": "XYZ123",
    "capacidade": "Alta"
  }
}
```

#### Notas Adicionais

* **Detalhamento**: Este endpoint fornece todos os detalhes armazenados de um dispositivo, incluindo metadados adicionais que podem ter sido especificados durante o registro.

***

Esta documentação detalha o endpoint `GET /register/{id}`, incluindo a estrutura da requisição e os formatos de resposta, facilitando o acesso às informações de um dispositivo específico pelo ID.
