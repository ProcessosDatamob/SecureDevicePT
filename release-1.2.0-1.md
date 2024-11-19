# Release 1.2.1

### Informação de Licença

Nome do Projeto: Device Seguro&#x20;

Descrição: DSLIB - Biblioteca Android

Copyright (c) 2024 Datamob Sistemas. Todos os direitos reservados.

Este software é de propriedade exclusiva de Datamob Sistemas e está protegido pelas leis de direitos autorais e outras leis de propriedade intelectual.

O uso, distribuição ou modificação deste código fonte é estritamente proibido sem a permissão expressa por escrito de Datamob Sistemas.

Autor(es): Teixeira, P; Manica, L; Spotti, L. Email: suporte@datamob.net.br

### Histórico de versão

#### Versão 1.2.1

Data: 19/11/2024

**Changelog**

* Remove as dependências das libs material, appcompat e core-ktx;
* Ajusta labels e ícones dos serviços de Acessibilidade e DeviceAdmin, configurando o mapeamento para o String e ícone utilizado no aplicativo.

#### Versão 1.2.0

Data: 18/10/2024

**Changelog**

* Ajusta regras do Proguard relaxando a ofuscação de nomes de pacotes;
* Implementa comando remoto para remoção do registro do dispositivo;
* Melhora as validações de phoneNumber e token nos pré-requisitos do registro;
* Adiciona método auxiliar para obter a Intent de Configuração de Acessibilidade;
* Estende a documentação para novos métodos públicos.

#### Versão 1.1.0

Data: 24/07/2024

**Changelog**

* Implementa mudanças na interface pública dos objetos DeviceSeguro, DeviceSeguroPreRequisitesHelper, DeviceSeguroAcessibilityService, onde revisamos a exposição de funcões e propriedades internas;
* Adiciona novo modelo de validação de tipo de segurança utilizada na tela de bloqueio do dispositivo, ampliado as informações disponíveis para o controle de ativação da funcionalidade limpeza de tela;
* Implementa mudanças para o suporte da funcionalidade de limpeza do dispositivo com base no SDK Android 34.
* Adiciona novas Intent Actions destinadas para o DeviceSeguroReceiver.
* Inclui melhorias de manutenibilidade do Serviço DeviceSeguroAcessibilityService.

#### Versão 1.0.0

Data: 19/07/2024

## Como Utilizar

A biblioteca está estruturada como um módulo Android (Kotlin) e é disponibilizada na forma de um pacote Java e distribuída no repositório Maven do fornecedor. O acesso é realizado através de credenciais exclusivas do cliente, que contém as seguintes informações:

REPOSITORY\_URL: Url de acesso aos recursos da biblioteca.&#x20;

USERNAME: Identificação de acesso do usuário.&#x20;

ACCESS\_TOKEN: Token de autenticação.

1. Adicione a declaração do repositório Maven no arquivo de configuração do projeto.

```
repositories {
    maven {
        url = uri("https://<REPOSITORY_URL>")
        name = "dslib"
        credentials(PasswordCredentials::class) {
            username = "<USERNAME>"
            password = "<ACCESS_TOKEN>"
        }
    }
}
```

2. Declare a dependência no arquivo de configuração.

```
dependencies {
    implementation("br.net.datamob.mobile:dslib:<VERSION>")
}
```

Para instruções detalhadas, consulte:

* [Guia de Integração da biblioteca (formato DOC)](release-1.2.0-2/guia-de-integracao-e-uso-da-biblioteca-deviceseguro-v1.2.0.md)
* [Referência da Biblioteca (javadoc)](https://drive.google.com/drive/folders/1ehfXPIr7xKbp8kCNqzJkIJ9Po5rFYz-z?usp=sharing)

### Permissões utilizadas

```
// Utilizada para comunicação via rede - Firebase
<uses-permission android:name="android.permission.INTERNET" />

// Utilizada para controle do pré-requisito da conta Google
<uses-permission android:name="android.permission.GET_ACCOUNTS" />

```

### Recursos disponibilizados

* Device Administrator Receiver
* Serviço de Acessibilidade

### Requisitos de Sistema

* **SDK Mínimo**: 24 (Android 7.0 Nougat)
* **SDK Target**: 34 (Android 14)
* **Tamanho do arquivo**: 24KB

### Outros Requisitos de UI e integração:

* Nenhum.

### Performance

* Device Admin Receiver: Permanece ativo pelo sistema para receber Intents de Administração do Dispositivo. Frequência de acionamento baixa.
* Serviço de Acessibilidade: Permanece ativo pelo sistema para receber eventos do componente com.android.systemui. Frequência de acionamento alta.

### Segurança

A biblioteca utiliza armazenamento Shared Preferences criptografado (AES\_256). A biblioteca não trafega dados externamente. A comunicação é realizada entre App e SDK.

Os dados utilizados são:

* Telefone: usado na composição do identificador do aparelho;
* Token de ativação: utilizado para geração dos hashes das operações.

## Instruções de download

Realize o download do pacote ZIP dslib-version.zip através da URL fornecida a você pela nossa equipe. Extraia o binário (.aar) utilizando a senha fornecida para liberar o acesso ao conteúdo do arquivo.

### Suporte e assistência

Email: suporte@datamob.net.br
