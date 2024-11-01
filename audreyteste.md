# PATCH /register/{id}/data

## Descrição
Atualiza os valores adicionais de um registro de dispositivo existente. Este endpoint permite adicionar ou modificar dados complementares de um dispositivo específico, identificado pelo `id`, mesclando-os aos dados complementares já presentes.

## Parâmetros

### Path Parameters

- **id** (obrigatório): Identificador único do dispositivo cujo registro será atualizado.
  - Tipo: `string`
  - Exemplo: `34731ae384834d46bfa4452300bf7691`

### Body Parameters

- **body** (obrigatório): Objeto JSON contendo os dados adicionais que serão adicionados ao registro do dispositivo. Estes dados complementares serão mesclados com os existentes.
  - Tipo: `object`
  - Exemplo:
    ```json
    {
      "xxx": "yyyy"
    }
    ```

## Respostas

- **200 OK**: Retorna o registro atualizado do dispositivo, com todos os dados incluindo os novos valores adicionais.
  - **Exemplo de resposta:**
    ```json
    {
      "id": "34731ae384834d46bfa4452300bf7691",
      "type": "ios",
