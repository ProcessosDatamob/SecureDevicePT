# Guia de Integração e Uso da Biblioteca DeviceSeguro V1.3.0

### 1. Introdução à biblioteca

A biblioteca **DeviceSeguro** foi desenvolvida para oferecer aos desenvolvedores uma maneira fácil e eficiente de integrar funcionalidades de segurança e controle remoto de dispositivos em seus aplicativos. O objetivo principal da biblioteca é fornecer métodos para registrar usuários no sistema **Device Seguro**, permitindo que dispositivos móveis possam ser gerenciados remotamente.

A integração da **DeviceSeguro** possibilita o registro de um usuário, que é composto por um número de telefone, uma senha tipo token e um hash aleatório gerado no momento do registro. Este processo é realizado por meio de chamadas de API, o que requer uma conexão ativa com a internet. Uma vez que o usuário esteja registrado no sistema **Device Seguro**, o dispositivo associado estará habilitado para receber e executar comandos remotos de segurança.

Esses comandos remotos incluem ações como bloquear a tela do dispositivo (lock screen) ou até mesmo forçar um wipe (Reset de Fábrica) do dispositivo, proporcionando um controle de segurança adicional para o usuário final.

A biblioteca **DeviceSeguro** é ideal para desenvolvedores que desejam incorporar recursos de segurança avançados em seus aplicativos, facilitando a implementação de controle remoto e gerenciamento seguro de dispositivos.

### 2. Como adicionar a biblioteca ao projeto

#### 2.1 Adicionando o Repositório ao projeto

A biblioteca está estruturada como um módulo Android (Kotlin) e é disponibilizada na forma de um pacote Java e distribuída no repositório Maven do fornecedor.

```
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
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
}
```

O acesso é realizado através de credenciais exclusivas do cliente, que são disponibilizadas mediante solicitação explícita. As informações incluídas com as credenciais são:\


* REPOSITORY\_URL: Url de acesso aos recursos da biblioteca.
* USERNAME: Identificação de acesso do usuário.
* ACESS\_TOKEN: Token de autenticação.
* EXPIRATION\_DATE: Data de expiração do token de acesso.

#### 2.2 Adicionar a dependência ao Gradle

2.2.1 Atualizar o build.gradle

```

dependencies {
    implementation("com.google.android.gms:play-services-auth:21.2.0")
    implementation("androidx.security:security-crypto:1.0.0")
    implementation("br.net.datamob.mobile:dslib:<VERSION>")
}

```

2.2.2 Sincronizar o Projeto

Após adicionar a dependência, clique em "Sync Now" na barra de notificações que aparece no topo da tela do Android Studio ou use o comando "Sync Project with Gradle Files" para sincronizar o projeto.

#### 2.3 Verificar a Configuração

2.3.1 Confirmar Importação Bem-Sucedida

Para confirmar que a biblioteca foi importada corretamente, tente usar uma classe ou método fornecido pela biblioteca em uma das suas classes de código-fonte. Se a importação e a sincronização estiverem corretas, o Android Studio não exibirá erros de compilação.

Exemplo:

```


import br.net.datamob.dslib.DeviceSeguro

fun main() {
    DeviceSeguro.unregisterDeviceAdmin(this)
}

```

#### 2.4 Inicialização

Adicione no ponto de entrada do seu aplicativo a chamada para o método Device Seguro.initializeBroadcastReceiver().

```
class MainActivity : AppCompatActivity() {


   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
	  ...
       DeviceSeguro.initializeBroadcastReceiver(
           context = this,
           commandBroadcastReceiver = DeviceSeguroReceiver()
       )
   }
}

```

Este método recebe um objeto BroadcastReceiver que seu aplicativo pode implementar para receber notificações assíncronas da biblioteca contendo informações de status e de retorno de comandos. Abaixo um exemplo de implementação de BroadcastReceiver:

```
class DeviceSeguroReceiver : BroadcastReceiver() {


   override fun onReceive(context: Context?, intent: Intent?) {
       Toast.makeText(context, intent?.action, Toast.LENGTH_LONG).show()
       Log.d("DeviceSeguroReceiver", intent?.action ?: "")
   }
}

```

Abaixo estão declaradas as ações que são adicionadas ao filtro de Intents do BroadcastReceiver no método DeviceSeguro.initializeBroadcastReceiver():

```


const val ACTION_COMMAND_RECEIVED = "br.net.datamob.dslib.ACTION_COMMAND_RECEIVED"
const val ACTION_COMMAND_FAILED = "br.net.datamob.dslib.ACTION_COMMAND_FAILED"
const val ACTION_REGISTERED = "br.net.datamob.dslib.ACTION_REGISTERED"
const val ACTION_REGISTER_FAILED = "br.net.datamob.dslib.ACTION_REGISTER_FAILED"
const val ACTION_UNREGISTERED = "br.net.datamob.dslib.ACTION_UNREGISTERED"
const val ACTION_UNREGISTER_FAILED = "br.net.datamob.dslib.ACTION_UNREGISTER_FAILED"
const val ACTION_UNREGISTERED_DEVICE_ADMIN = "br.net.datamob.dslib.ACTION_UNREGISTERED_DEVICE_ADMIN"
const val ACTION_GOOGLE_ACCOUNT_LOGGED_OFF = "br.net.datamob.dslib.ACTION_GOOGLE_ACCOUNT_LOGGED_OFF"
const val ACTION_LOCK_PASS_QUALITY_MISSING = "br.net.datamob.dslib.ACTION_LOCK_PASS_QUALITY_MISSING"

```

ACTION\_COMMAND\_RECEIVED: Disparado como callback ao receber um comando.

ACTION\_COMMAND\_FAILED: Disparado em resposta a qualquer falha na execução de um comando.

ACTION\_REGISTERED: Disparado como callback ao realizar o registro no Device Seguro.

ACTION\_REGISTER\_FAILED: Disparado em caso de falha no processo de registro.

ACTION\_UNREGISTERED: Disparado como callback ao remover o registro no Device Seguro.

ACTION\_UNREGISTER\_FAILED: Disparado em caso de falha ao remover o registro.

ACTION\_UNREGISTERED\_DEVICE\_ADMIN: Disparado em resposta à remoção da aplicação como Administrador do Dispositivo

ACTION\_GOOGLE\_ACCOUNT\_LOGGED\_OFF: Disparado em resposta aos eventos de Gestão de Contas do Android.

ACTION\_LOCK\_PASS\_QUALITY\_MISSING: Disparado em resposta à mudança de senha da tela de bloqueio, quando a nova senha não atender os requisitos mínimos

#### 2.5 Pronto para usar!

Agora, sua biblioteca DeviceSeguro V1.3.0 está pronta para ser utilizada no seu projeto. Siga para os próximos passos para aprender como configurar e utilizar suas funcionalidades.

### 3. Pré-requisitos

Para utilizar a biblioteca **DeviceSeguro** e registrar um usuário no sistema, é necessário atender a alguns pré-requisitos fundamentais. Estes requisitos garantem que o aplicativo e o dispositivo estejam corretamente configurados para permitir a execução dos comandos de controle remoto com segurança.

Esses pré-requisitos são validados automaticamente ao chamar o método DeviceSeguro.register(), e caso algum não seja atendido, uma exceção específica que acusa o pré-requisito faltante é levantada.

A biblioteca disponibiliza um helper (DeviceSeguroPreRequisitesHelper) que pode ser utilizado para validar se os pré-requisitos estão configurados corretamente. Isso pode ser feito através do método “validatePrerequisites”, que verificará cada pré-requisito, levantando exceções em caso de requisitos faltantes. Outra possibilidade é utilizar os métodos específicos para cada pré-requisito, conforme descritos abaixo:

| _**Pré-requisito**_                  | _**Método de validação**_                                                      |
| ------------------------------------ | ------------------------------------------------------------------------------ |
| Administrador de Dispositivo         | <pre><code>fun isDeviceAdmin(context: Context): Boolean
</code></pre>          |
| Conta Google vinculada               | <pre><code>fun hasGoogleAccount(context: Context): Boolean
</code></pre>       |
| Segurança mínima na tela de bloqueio | <pre><code>fun hasLockPassword(context: Context): Boolean
</code></pre>        |
| Opções de Acessibilidade             | <pre><code>fun hasAccessibilityOption(context: Context): Boolean
</code></pre> |
| Número de telefone                   | <pre><code>fun validatePhoneNumber(phoneNumber: String): Boolean
</code></pre> |
| Senha                                | <pre><code>
fun validateToken(token: String): Boolean
</code></pre>            |

#### 3.1 Aplicativo como Administrador de Dispositivo

O aplicativo que implementa a biblioteca **DeviceSeguro** deve ser registrado como uma aplicação gerenciadora de sistema (Device Admin). Esta configuração é essencial para permitir que o aplicativo tenha permissões suficientes para executar comandos de segurança, como bloqueio de tela e reset de fábrica.

A biblioteca também disponibiliza um método para auxiliar nesse registro. Para utilizá-lo, basta chamar DeviceSeguro.registerDeviceAdmin() conforme o exemplo abaixo:

```


val REQUEST_CODE_ENABLE_ADMIN = 1
val intent = DeviceSeguro.registerDeviceAdmin(context = context)
if (intent != null) {
    startActivityForResult(intent, REQUEST_CODE_ENABLE_ADMIN)
}

```

Se a aplicação já for Device Admin, esse método retornará NULO. Caso contrário, retorna um Intent que pode ser chamado para abrir um prompt onde o usuário pode permitir o aplicativo como Administrador do Dispositivo.

Caso seja iniciado o processo de registro sem que o app esteja registrado como administrador do dispositivo, uma exceção do tipo “DeviceSeguroMissingDeviceAdminException” é levantada.

Também é possível remover o aplicativo como device admin, através do método

```
DeviceSeguro.unregisterDeviceAdmin(context: Context)
```

#### 3.2 Conta Google vinculada

O dispositivo deve possuir uma conta Google vinculada. A presença de uma conta Google ativa é necessária para garantir a sincronização dos serviços e o gerenciamento do dispositivo.

A biblioteca disponibiliza um método para auxiliar o processo de login com conta Google:

```

val RC_SIGN_IN = 123
val intent = DeviceSeguro.loginGoogleAccount(context)
if (intent != null) {
    startActivityForResult(intent, RC_SIGN_IN)
}

```

Caso seja iniciado o processo de registro sem que haja uma conta Google vinculada ao dispositivo, uma exceção do tipo “DeviceSeguroMissingGoogleAccountException” é levantada.

#### 3.3 Opções de Acessibilidade

Para o funcionamento da funcionalidade de WIPE, as opções de acessibilidade devem estar ativas para a aplicação

Caso seja necessário solicitar ao usuário que habilite as opções de acessibilidade, isso pode ser feito conforme o exemplo a seguir:

```

val intent = DeviceSeguro.getAccessibilityIntent()
startActivity(intent)

```

#### 3.4 Nível mínimo de segurança na tela de bloqueio

O dispositivo deve estar configurado com um nível mínimo de segurança na tela de bloqueio, como PIN, padrão de desbloqueio, ou senha. Isso é importante para garantir que o dispositivo esteja protegido contra acessos não autorizados.

A biblioteca disponibiliza um método para auxiliar a solicitação de alteração de senha para o usuário:

```

val intent = DeviceSeguro.getChangePasswordIntent()
startActivity(intent)

```

Caso seja iniciado o processo de registro sem que o nível de segurança da tela de bloqueio atenda o mínimo, uma exceção do tipo “DeviceSeguroMissingPasswordQualityException” é levantada.

3.4.1 Qualidade de Senha

Qualidade de senha é um pré-requisito opcional, ou seja, seu não cumprimento não impede o registro no Device Seguro. Para que a qualidade de senha possa ser verificada, primeiramente é necessário garantir que os pré-requisitos de Administrador do Dispositivo, Opções de Acessibilidade e Nível mínimo de segurança na tela de bloqueio estejam atendidos. Em seguida, é necessário invocar um método que irá recuperar automaticamente o tipo de senha do usuário e tornar disponível para consulta:

```
fun checkPasswordQuality(context: Context)
```

Após chamar esse método, o tipo de senha do usuário pode ser validado da seguinte forma:

```
DeviceSeguroPreRequisitesHelper.validateLockPasswordQuality(context)
```

Esse método retorna “True” quando o tipo de senha do usuário for PIN ou Padrão, e “False” quando for tipo Password.

{% hint style="info" %}
Recomendação

Por motivos de compatibilidade da ferramenta de Acessibilidade utilizado na funcionalidade de Limpeza (Wipe) é recomendado a utilização específica do tipo de senha PIN e Padrão, em detrimento ao tipo Password. Esse tipo de senha pode apresentar em alguns casos uma discrepância no funcionamento observado em versões do Android e modelos específicos.
{% endhint %}

#### 3.5 Informações do usuário para registro

É necessário fornecer à biblioteca o número de telefone e a senha tipo token do usuário a ser cadastrado. Essas informações são essenciais para o processo de registro e para a geração do hash aleatório necessário no momento do registro.

Esses dados devem ser informados no momento do registro, como parâmetros para o método Register, como no exemplo a seguir:

```

DeviceSeguro.register(context = context, phoneNumber = "41998626807", tokenPassword = "123456", onRegisterCallback = object: OnResultCallbackInterface {
    override fun onSuccess() {
        Toast.makeText(context, "Registrado com sucesso", Toast.LENGTH_SHORT).show()
    }

    override fun onError(ex: Exception) {
        Toast.makeText(context, "Erro: " + ex.message, Toast.LENGTH_SHORT).show()
    }

})

```

### 4 Comandos

Para que a biblioteca possa executar as operações de Lock e Wipe, a aplicação deve realizar uma chamada para o método DeviceSeguro.executeMessageReceived() nos pontos de entrada dos canais de comunicação definidos pelo app. A biblioteca não define nem restringe quais canais podem ser utilizados, ficando a cargo da aplicação defini-los.

No exemplo abaixo, o aplicativo implementa um Receiver responsável pelo recebimento de mensagens via Firebase Cloud Message (PUSH).

```


class LocalFirebaseMessagingService : FirebaseMessagingService() {
   private val TAG = "LocalFirebaseMessagingService"
   override fun onMessageReceived(message: RemoteMessage) {
       super.onMessageReceived(message)
       DeviceSeguro.executeMessageReceived(this, message.data)
   }
}

```

A comunicação é realizada através do BroadcastReceiver configurado na inicialização. São registrados os eventos:

```

const val ACTION_COMMAND_RECEIVED: String = "br.net.datamob.dslib.ACTION_COMMAND_RECEIVED"
const val ACTION_COMMAND_FAILED: String = "br.net.datamob.dslib.ACTION_COMMAND_FAILED"

```

#### 4.1 Comunicação do Status do Comando

É possível&#x20;

```
android {
    defaultConfig {
        ...
        resValue("string", "api_key", "<API_KEY>")
        resValue("string", "api_url", "<API_URL>")
    }
}
```

