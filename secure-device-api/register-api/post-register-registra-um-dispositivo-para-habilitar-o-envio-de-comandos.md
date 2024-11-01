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

# POST /register Registra um dispositivo para habilitar o envio de comandos

Este endpoint permite registrar um novo dispositivo no sistema para habilitar o envio de comandos a ele. Ao registrar o dispositivo, ele se torna rastreável e pode receber comandos através de outros endpoints da API.

#### Requisição

* **URL**: `/register`
* **Método**: `POST`
* **Autenticação**: Requerida (especificar tipo de autenticação, se aplicável)

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e deve incluir as informações necessárias para registrar o dispositivo.

| Parâmetro  | Tipo     | Obrigatório | Descrição                                             |
| ---------- | -------- | ----------- | ----------------------------------------------------- |
| `name`     | `string` | Sim         | O nome do dispositivo a ser registrado.               |
| `type`     | `string` | Sim         | O tipo do dispositivo (exemplo: `sensor`, `atuador`). |
| `location` | `string` | Não         | A localização do dispositivo (exemplo: `Sala 1`).     |
| `status`   | `string` | Não         | O status inicial do dispositivo (exemplo: `ativo`).   |
| `metadata` | `object` | Não         | Informações adicionais sobre o dispositivo.           |

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "name": "Dispositivo A",
  "type": "sensor",
  "location": "Sala 1",
  "status": "ativo",
  "metadata": {
    "fabricante": "Empresa X",
    "modelo": "XYZ123",
    "capacidade": "Alta"
  }
}
```

#### Respostas

| Código | Descrição                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------- |
| 201    | Dispositivo registrado com sucesso. Retorna os dados do dispositivo registrado.                |
| 400    | Requisição inválida. Verifique o corpo da requisição e os parâmetros obrigatórios.             |
| 409    | Conflito. Já existe um dispositivo com as mesmas características principais (ex.: nome único). |
| 500    | Erro interno no servidor.                                                                      |

**Exemplo de Resposta com Sucesso (`201`)**

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

* **Unicidade**: Certifique-se de que o `name` do dispositivo é único para evitar conflitos de registro.
* **Metadados**: O campo `metadata` pode conter informações específicas do dispositivo para melhor controle e identificação no sistema.

***

Esta documentação fornece uma visão detalhada do endpoint `POST /register`, incluindo parâmetros, estrutura da requisição e formatos de resposta, para facilitar o uso e integração do registro de dispositivos na API.
