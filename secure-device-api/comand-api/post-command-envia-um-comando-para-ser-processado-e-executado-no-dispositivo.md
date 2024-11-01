# POST /command Envia um comando para ser processado e executado no dispositivo

Este endpoint permite enviar um comando para um dispositivo específico, que será processado e executado. Ele é útil para emitir comandos que precisam ser realizados de forma remota em dispositivos registrados.

#### Requisição

* **URL**: `/command`
* **Método**: `POST`
* **Autenticação**: Requerida (especificar o tipo de autenticação, se aplicável)

**Corpo da Requisição**

O corpo da requisição deve ser enviado no formato `JSON` e conter os detalhes do comando que será executado no dispositivo.

| Parâmetro     | Tipo     | Obrigatório | Descrição                                                          |
| ------------- | -------- | ----------- | ------------------------------------------------------------------ |
| `deviceId`    | `string` | Sim         | O identificador único do dispositivo de destino.                   |
| `commandType` | `string` | Sim         | O tipo do comando a ser executado (ex.: `reiniciar`, `atualizar`). |
| `parameters`  | `object` | Não         | Parâmetros adicionais para o comando, se necessário.               |

**Exemplo de Corpo da Requisição**

```json
jsonCopiar código{
  "deviceId": "12345",
  "commandType": "reiniciar",
  "parameters": {
    "delay": 10
  }
}
```

#### Respostas

| Código | Descrição                                                                                          |
| ------ | -------------------------------------------------------------------------------------------------- |
| 201    | Comando enviado com sucesso. Retorna os dados do comando criado, incluindo seu status inicial.     |
| 400    | Requisição inválida. Verifique o corpo da requisição e os parâmetros obrigatórios.                 |
| 404    | Dispositivo não encontrado. O `deviceId` fornecido não corresponde a nenhum dispositivo existente. |
| 500    | Erro interno no servidor.                                                                          |

**Exemplo de Resposta com Sucesso (`201`)**

```json
jsonCopiar código{
  "commandId": "cmd123",
  "deviceId": "12345",
  "commandType": "reiniciar",
  "status": "pendente",
  "issuedAt": "2023-01-01T12:00:00Z",
  "parameters": {
    "delay": 10
  }
}
```

#### Notas Adicionais

* **Parâmetros do Comando**: O campo `parameters` é flexível para permitir configurações específicas de cada tipo de comando.
* **Status Inicial**: O comando é inicialmente criado com o status `pendente` e será atualizado conforme o dispositivo o processa.

***

Esta documentação fornece uma visão detalhada do endpoint `POST /command`, incluindo os parâmetros de entrada, estrutura da requisição e formatos de resposta, facilitando o envio de comandos para dispositivos.
