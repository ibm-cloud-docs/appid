---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Customizado
{: #custom-identity}

É possível usar seu próprio provedor de identidade customizado ao autenticar. Seu provedor de identidade pode estar em conformidade com qualquer mecanismo de autenticação que não seja especificamente suportado pelo {{site.data.keyword.appid_full}}, incluindo o proprietário.
{: shortdesc}

Quando o {{site.data.keyword.appid_short_notm}} não fornece suporte direto para um provedor de identidade específico, é possível usar o fluxo de identidade customizado para fazer ponte com o protocolo de autenticação para o fluxo de autenticação existente do {{site.data.keyword.appid_short_notm}}. Por exemplo, você deseja usar GitHub ou LinkedIn para permitir que os seus usuários se conectem. É possível usar o SDK existente do provedor de identidade para facilitar as informações sobre autenticação do usuário antes de empacotar e trocando-o pelo {{site.data.keyword.appid_short_notm}}. Em
muitos cenários corporativos, um provedor de identidade anterior pode usar seu próprio protocolo de autenticação
customizado, mas você ainda deseja aproveitar os recursos do {{site.data.keyword.appid_short_notm}}. Para esse tipo de cenário, o fluxo de identidade customizado fornece um meio desacoplado de autenticar de forma segura seus usuários sem expor as credenciais deles.

## Configurando a identidade customizada
{: #custom-configure}

É possível usar as etapas a seguir para configurar o provedor de identidade customizado para trabalhar com o {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Antes de iniciar
{: #custom-identity-before}

Para estabelecer a confiança entre o {{site.data.keyword.appid_short_notm}} e o provedor de identidade customizado, deve-se ter um par de chaves PEM RSA com um comprimento mínimo de 2048. Certifique-se
de fazer backup seguro de quaisquer chaves que usar na produção.

Como as chaves são usadas?

- Sua chave privada é usada em seu aplicativo ou provedor de identidade para assinar JWTs.
- Sua chave pública é usada pelo {{site.data.keyword.appid_short_notm}} para validar o JWT que contém informações sobre o usuário.

Para gerar um par de chaves PEM RSA usando o Open SSL, execute o comando a seguir:

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### Configurando com a GUI
{: #custom-identity-configure-gui}

1. Conecte-se à sua conta do {{site.data.keyword.cloud_notm}} e navegue para a instância do {{site.data.keyword.appid_short_notm}}.

2. Na guia **Gerenciar**, configure **Provedor de identidade customizado** como **Ativado**.

3. Registre sua chave pública com o {{site.data.keyword.appid_short_notm}}.
  1. Navegue para a guia **Provedor de identidade customizado**
  2. Cole a chave pública na caixa **Chave pública** e clique em **Salvar**.



### Configurando com a API
{: #custom-identity-configure-api}

Registre sua chave fazendo uma solicitação PUT para o [Terminal de API de gerenciamento](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp).

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Testando sua configuração
{: #custom-identity-testing}

Depois de configurar sua instância do {{site.data.keyword.appid_short_notm}} com uma chave pública válida, será
possível usar o aplicativo de teste que é fornecido pelo serviço para verificar se sua configuração está corretamente configurada. No
aplicativo de exemplo, é possível ver cargas úteis de token de acesso e de identidade do
{{site.data.keyword.appid_short_notm}} que são retornadas durante um fluxo de conexão padrão.

1. Na guia **Provedor de identidade customizada**, clique em **Testar** para abrir o aplicativo de teste.

2. Crie um exemplo de JWT usando [JWT.io](https://jwt.io/) seguindo a identidade customizada [protocolo](/docs/services/appid?topic=appid-custom-auth#generating-jwts).

3. Cole seu JWT na caixa rotulada **JSON Web Token** e clique em **Testar** para executar uma autenticação de amostra.

Se bem-sucedido, agora será possível ver os tokens de identidade e de acesso decodificados do
{{site.data.keyword.appid_short_notm}} que estariam disponíveis para seu aplicativo em um fluxo de conexão padrão.

## Próximas Etapas
{: #custom-identity-next}

Agora que seu provedor de identidade customizado está configurado, [inclua-o em seu aplicativo](/docs/services/appid?topic=appid-custom-auth#custom-auth).
